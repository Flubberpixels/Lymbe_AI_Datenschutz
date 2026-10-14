# Sicherheitsprüfung des Quellcodes – 12.10.2026

**Geprüft:** Repository `26lab/lymbe-ai`, Stand Commit 923f8ee (11.10.2026), nur lesend – keine Skripte, kein Server, kein Netzwerk, keine Änderung. Drei Lese-Agenten: (A) Web-App – Anmeldung, Rechte, Eingaben; (B) Infrastruktur – Docker, Geheimnisse, Lieferkette, Betrieb; (C) KI-Angriffe – Prompt-Injection, Widget-Missbrauch, Webhooks. Jeder Befund mit Datei und Zeile in `10a_Sicherheit_WebApp.md`, `10b_Sicherheit_Infrastruktur.md`, `10c_Sicherheit_KI_Widget.md`. Christians eigene Prüfung `SECURITY_AUDIT_V2.md` wurde gelesen; dort erledigte Punkte sind nicht wiederholt.

**Nicht prüfbar:** der Ablauf-Kern (eigenes Repository `lymbe-ablaeufe`), Server-Einstellungen (Firewall, Cron, Umgebungsvariablen), Git-Historie auf alte Geheimnisse.

## Kurzfazit

Das Fundament ist solide: Passwörter mit bcrypt, Login-Bremse, Cookie-Flags, einmalige Reset-Tokens, zentrale Rechteprüfung, alle 136 API-Routen haben eine Auth-Prüfung oder sind bewusst öffentlich, kein unsicheres Raw-SQL, SSRF-Schutz mit DNS-Rebinding-Abwehr, Markdown ohne HTML, Mailserver kein offenes Relay, Backups verschlüsselt mit Probe, Webhook-Signaturen bei Meta, Stripe, Shopify, Cal.com, Calendly geprüft, RAG-Isolation je Mandant und Assistent. Christians Audit V2 ist zu großen Teilen umgesetzt.

51 Befunde insgesamt: **0 kritisch, 8 hoch, 19 mittel, 24 niedrig.** Keiner erlaubt einem Fremden ohne Konto direkt Zugriff auf Kundendaten. Die hohen Befunde sind von zwei Sorten: Wege, auf denen ein Angreifer *mit* einem Fuß in der Tür (gestohlene Admin-Sitzung, Code im Container, böswilliger Kunde) sehr weit kommt – und Kosten-/Lärm-Angriffe über öffentliche Widget-Endpunkte.

## Die 10 wichtigsten Punkte – in dieser Reihenfolge abarbeiten

| Nr | Schwere | Was | Warum es zählt (einfach) | Aufwand | Aufgabe |
|---|---|---|---|---|---|
| S1 | hoch | **Hetzner-Cloud-API-Token liegt in Caddy und App** (`docker-compose.prod.yml:15`, `Caddyfile:31`) – projektweit Lesen und Schreiben | Wer in den Container kommt, kann den Server, die Firewall und alle sieben Hetzner-Abbilder löschen oder die Mail-Domain umbiegen. Der Token wird nur fürs TLS-Zertifikat per DNS gebraucht. | 1 h | S1: DNS-Zone in eigenes Hetzner-Projekt mit eigenem, nur dafür berechtigtem Token (wie bei der Storage Box schon gemacht) |
| S2 | hoch | **Sicherungs-Download liefert alles auf einen Klick** (`api/sicherung/download`): alle Mandanten-Dumps, `.env`-Dateien, MinIO-Objekte und den Backup-Schlüssel in einer Datei; 2FA optional, Audit nur best-effort | Ein gestohlenes Superadmin-Cookie oder Codeausführung im App-Container = komplette Datenbank aller Kunden samt Schlüssel. | 3 h | S2: TOTP-Pflicht plus erneute Eingabe, serverseitig befristete Freigabe, Mail an die Systemadresse bei jedem Abruf, Protokoll als BetriebsZugriff |
| S3 | hoch | **2FA nur auf der Admin-Oberfläche** (`app/admin/layout.tsx`), nicht in `requireRole` | Admin-Funktionen, `/api/internal/*` und der Sicherungs-Download sind mit Passwort allein erreichbar. Deckt sich mit Code-Abgleich A57. | 2 h | A57 |
| S4 | hoch | **SVG-Logos der Hilfeseite nur per Regex gesäubert** und unter `app.lymbe.ai` als `image/svg+xml` ausgeliefert | Ein Kunde lädt ein präpariertes Logo hoch, ein anderer Kunde oder ein Admin öffnet es – Skript läuft mit dessen Sitzung (Stored XSS über Mandantengrenzen). | 2 h | S4: SVG serverseitig rastern oder mit echtem Sanitizer (DOMPurify) säubern, `Content-Disposition: attachment`, CSP `sandbox` |
| S5 | hoch | **Proaktiv-Endpunkt des Widgets ohne Rate-Limit, `?debug=1` umgeht Cache und Sperre** (`widget/[botId]/proactive/route.ts`) | Jeder Aufruf kostet einen Modellaufruf plus Qdrant und DB; mit dem öffentlichen Widget-Key kann ein Fremder das Monatskontingent eines Kunden leeren und bekommt interne Trace-Daten zurück. | 1 h | S5: Debug nur für Personal, Rate-Limit je IP und Bot, Trace nie an Besucher |
| S6 | hoch | **Werkstatt maskiert Zugangsdaten nur in Trigger-Eingaben**; der Entwurf geht mit echten Schlüsseln an den Browser und beim nächsten Zug unmaskiert an Azure (`werkstatt-domain.ts:951,967`) | Der AVV verspricht „Zugangsdaten vorher maskiert" – das stimmt nur zur Hälfte. Schlüssel landen bei Microsoft. | 1 Tag | S6: Maskierung auf den gesamten Verlauf und Nutzertext anwenden, Geheimnisse serverseitig halten, nicht an den Browser |
| S7 | hoch | **`restore-from-prod.ps1` zieht alle Mandanten als Klartext-Dump auf einen Entwicklerrechner**, ohne `zugriff.sh`-Protokoll | Verstößt gegen AVV § 3 Abs. 5 und eure eigene Regel aus CLAUDE.md; Kundendaten liegen dann auf einem Laptop. | 30 min | S7: Skript entfernen; lokal nur mit Demo-Daten arbeiten |
| S8 | mittel, bei Gesundheitsdaten hoch | **App verbindet alle Mandanten-Datenbanken als Superuser `lymbe_admin`**; die je Mandant angelegten DB-Konten werden nie benutzt (`lib/db/tenant.ts:80-87`) | Die „eigene Datenbank je Kunde" trennt nur, solange der App-Code keinen Fehler macht – die Datenbank selbst hält niemanden auf. | 1 Tag | S8: Mandanten-Konten tatsächlich benutzen (Pool je Mandant), Superuser nur für Provisionierung |
| S9 | mittel | **Qdrant ohne API-Key, Inngest-Oberfläche ohne Anmeldung, inngest-redis ohne Passwort – im selben Docker-Netz wie der Ablauf-Kern**, der Code-Schritte von Kunden ausführt | Ein Kunde mit einem HTTP- oder Code-Baustein kann `http://qdrant:6333` aller Mandanten lesen und löschen, wenn der Kern das nicht abfängt (nicht prüfbar). | 3 h | S9: Qdrant-API-Key, Inngest-Auth, Redis-Passwort; Ablauf-Kern in eigenes Netz ohne Sicht auf Qdrant/DB/Redis |
| S10 | mittel | **Termin-, Lead- und WhatsApp-Eingänge ohne Sitzungsgrenze** (nur 60/min je IP); Intent-Klassifikator mischt Besuchertext und Anweisung | Kalender-Flutung, Einladungs-Spam über die Mail des Kunden, ein WhatsApp-Absender leert das Monatskontingent; ein Besucher kann Abläufe des Kunden mit erfundenen Angaben auslösen. | 1 Tag | S10: Limits je Sitzung/Absender/Bot, Adressprüfung bei Leads, Besuchertext im Klassifikator als Daten rahmen |

## Weitere Befunde (mittel) – nach dem Livegang

- TOTP-Secret und Backup-Codes im Klartext, kein Replay-Schutz, kein Rate-Limit auf Code-Versuche (A5)
- Kalender-OAuth-State ohne Nutzerbindung → fremdes Konto kann untergeschoben werden (A6)
- Support-Zugang erteilt sich das Personal selbst, endlos verlängerbar; Seitenprotokoll kommt aus dem Browser (A7, passt zu Code-Abgleich A55)
- Webhook-Zustellung ohne IP-Festnagelung → DNS-Rebinding in Docker-Dienste (A8)
- `allowDangerousEmailAccountLinking` bei GitHub-Login ohne E-Mail-Prüfung (A9); keine CSP, `allowedOrigins: *.lymbe.ai` (A10/B7)
- `:latest`-Images für Inngest, Qdrant, MinIO; `postinstall` lädt Python-Pakete ohne Hash; Deploy holt Prisma zur Laufzeit (B5, B6)
- `.env.vor-*`-Dateien nicht in `.gitignore` → ein `git add -A` auf dem Server schreibt Geheimnisse in die Historie (B8)
- UFW schützt Docker-Ports nicht; Dev-Compose veröffentlicht Postgres/Redis/MinIO/Qdrant auf allen Adressen (B9)
- `ENCRYPTION_KEY` nicht rotierbar (keine Schlüssel-ID, kein Zweitschlüssel); `NEXTAUTH_SECRET` mehrfach verwendet (B10)
- Mail-Brücke läuft als root mit Zugriff auf die TLS-Schlüssel von Caddy (B11)
- Selbstlernen `AUTO_ACCEPT` nur mit KI-Prüfung → Besucher A kann Wissen einpflanzen, das Besucher B sieht (C7)
- KI-Felder in Abläufen steuern Folgeschritte ohne harte Schranke – eingeschleuster Text in einer E-Mail kann einen Ablauf lenken (C8)

Die 24 niedrigen Befunde (u. a. `error.message` an Clients, kein Virenscan bei Uploads, möglicher echter Google-API-Key in einer Testdatei `tests/ablaeufe-werkstatt-offen.test.mts:33` – sofort prüfen und sperren, Workflow ohne `permissions:`, kein Dependabot, `speakeasy` seit 2017 ungepflegt, Sitzungen 12 h gleitend ohne absolute Grenze) stehen in 10a–10c.

## Einordnung für den Betrieb mit der Pilotkundin

Nichts davon ist ein Grund, die Übergabe zu stoppen – aber S1, S2, S5 und S7 sind jeweils unter einer Stunde und schließen die größten Türen; S4 und S6 betreffen direkt Zusagen aus AVV Anlage 1 und Anlage 2. Empfohlene Reihenfolge: S7 (Skript löschen, 10 Minuten) → S1 → S5 → S2 → S3/A57 → S4 → S6 → S9 → S8 → S10. Danach die Sicherheits-Checkliste in 02_Finale_To_Dos Abschnitt 7 um diese Punkte fortschreiben.
