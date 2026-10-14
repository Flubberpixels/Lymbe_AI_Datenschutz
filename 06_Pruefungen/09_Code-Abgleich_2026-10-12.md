# Code-Abgleich „Hält die Maschine, was der Vertrag verspricht?" – 12.10.2026

**Geprüft:** Quellcode des Repositorys `26lab/lymbe-ai`, Stand Commit 923f8ee (11.10.2026, 17:04), nur lesend – keine Skripte, keine Datenbank, kein Server, keine Änderung. **Gegen:** Kunden-AVV 1.7, Datenschutzerklärung 1.6, Widget-Texte 1.5 (1.1) und die Einträge im Freigabeprotokoll 5.9. **Prüfer:** Cowork für Dennis mit drei Lese-Agenten. Einzelbelege mit Datei und Zeile: `09a_Code_Fristen.md`, `09b_Code_Zugriff.md`, `09c_Code_Websuche_Widget.md`.

**Was im Code nicht prüfbar ist:** alles, was nur auf dem Server steht – Cron-Zeiten, Umgebungsvariablen (`AI_PROVIDER_WERKSTATT`, Azure-Region), Hetzner-Abbilder, der Ablauf-Kern (eigenes Repository `lymbe-ablaeufe`). Dafür gilt Christians Unterschrift unter 5.9.

## Kurzfazit

Die Kernzusagen halten: Websuche schickt nur den geprüften Suchbegriff an OpenAI, kein Anbieter-Rückfall, Löschläufe mit den Fristen aus § 8, Mandantentrennung per eigener Datenbank, Support-Zugang mit Protokoll, Zugangsdaten verschlüsselt, Widget-Analyse nur mit gehashter IP. Von 35 geprüften Zusagen sind 24 belegt, 8 teilweise, 3 nicht belegt. Die drei nicht belegten und die wichtigsten Teil-Befunde sind unten als Aufgaben gefasst – alle gehören auf Christians Liste, keine erfordert eine Vertragsänderung außer zwei kleinen Sätzen in der Datenschutzerklärung.

## A – Nicht belegt (Vertrag verspricht, Code hält nicht)

| Nr | Zusage | Befund | Folge |
|---|---|---|---|
| K1 | AVV § 8 Abs. 3 / DSE: Zustimmungs- und Weisungsprotokolle 3 Jahre nach Vertragsende | `AvvZustimmung` hängt mit `onDelete: Cascade` am Workspace (`prisma/schema.prisma:2607`); die Workspace-Löschung löscht auch alle Audit-Zeilen des Workspaces (`lib/mandant/loeschung.ts:130`). 30 Tage nach Vertragsende ist der Nachweis, dass der Kunde den AVV bestätigt hat, weg. | **Christian A53:** Zustimmungs- und Weisungsnachweise beim Löschen des Workspaces in eine Nachweistabelle kopieren (ohne Inhalte) und 3 Jahre halten. |
| K2 | AVV § 8 Abs. 4: Export mit Dokumenten, Gedächtnis, Abläufen | `gdpr-actions.ts:63-105` liefert Gespräche, Leads, Termine, Übergaben; Dokumente nur Metadaten, kein Gedächtnis, keine Abläufe. | bekannt = 5.9 A18 / Aufgabe **A44** (bauen oder § 8 Abs. 4 kürzen). |
| K3 | Portal zeigt AVV 1.7 | `AVV_FASSUNG = '1.6'` (`lib/legal/avv.ts:79`), Text in `avv-text.ts` ist der Zwischenstand vom 06.10. | bekannt = Aufgabe **A42**; Altfassung 1.6 unter `/avv/fassung-1-6` ablegen, so wie 1.5 schon liegt. |

## B – Teilweise (Kern stimmt, Rand fehlt)

| Nr | Zusage | Befund | Folge |
|---|---|---|---|
| K4 | § 3 Abs. 1: Einstellungen mit Zeit und Nutzer protokolliert | Websuche abbestellen, Webhooks, API-Schlüssel, Dokumente: Audit-Log ja. Benachrichtigungsziele (`integration-actions.ts:57-125`), Kalender, Shops, WhatsApp, Meta: kein Audit-Eintrag, nur `createdAt` ohne Person. Selbstlernen: Vorgabe DISABLED belegt; Protokoll nur als Sammel-`BOT_UPDATED` ohne Vorher/Nachher. | bekannt = **A43**; dazu: `BOT_UPDATED` mit altem/neuem Wert für `selfLearningMode`. |
| K5 | § 8 Abs. 1: Zugriffsprotokolle 14 Tage | Container-Logs 14 Tage belegt (`scripts/aufbewahrung-server.sh`). Aber: Mail-Versandprotokoll mit Empfängeradressen 30 Tage, IP-Adressen in `AuditLog`/`UserSession` 30 Tage. | **Christian A54:** auf 14 Tage setzen – oder Dennis ändert § 8 und DSE auf „Mail-Versandprotokoll und Anmelde-IPs 30 Tage". Empfehlung: Code auf 14 Tage, Text bleibt. |
| K6 | § 3 Abs. 5: Support-Zugriff nur mit Freigabe und Protokoll, für den Kunden sichtbar | Support-Zugang mit Grund/Umfang/Frist, jede Seite protokolliert, Kundensicht unter Einstellungen → Datenschutz, 365 Tage: belegt. Lücke: `updateTenantBotForAdmin` (`admin-tenant-bot-actions.ts:122-208`) ändert den Systemprompt eines Kunden-Assistenten ohne Support-Zugang; landet nur im zentralen Audit-Log, der Kunde sieht es nicht. Sicherungs-Download (`api/sicherung/download`) ebenso nur zentral. | **Christian A55:** beide Wege hinter den Support-Zugang legen oder als `BetriebsZugriff` mit Workspace protokollieren. |
| K7 | Anlage 1: Zugangsdaten verbundener Dienste verschlüsselt | AES-256-GCM für Kalender, Shops, WhatsApp, Meta, API-Quellen, DB-Passwörter: belegt. Klartext: Webhook-Signaturgeheimnisse (`webhook-actions.ts:53`, in 5.9 A17 schon genannt) **und** Slack-/Teams-Webhook-URLs in `BotIntegration.target` (`tenant/schema.prisma:1094`) – eine Webhook-URL ist ein Geheimnis, wer sie hat, kann in den Kanal des Kunden posten. | **Christian A56:** `BotIntegration.target` und Webhook-Signaturen verschlüsseln. |
| K8 | Anlage 1: Mehr-Faktor für Admin-Zugänge | Nur `app/admin/layout.tsx:30-40` erzwingt 2FA; `requireRole` (`lib/auth.ts:598`) prüft keine 2FA – Admin-Server-Actions und `/api/admin` sind ohne zweiten Faktor erreichbar, wenn die Sitzung besteht; OAuth-Login ohne TOTP-Schritt. | **Christian A57:** 2FA-Prüfung in `requireRole` für Personal-Rollen (gehört zu A41 Portal-TOTP). |
| K9 | Sicherungen „vom Server aus nicht löschbar" | rsync läuft mit `--delete`; der Schutz liegt allein in den Hetzner-Snapshots der Storage Box (7 Tage). Im Code stimmt die Aussage nur zusammen mit der Box-Einstellung. | kein Handlungsbedarf, in 5.9 A14b so vermerken. |
| K10 | § 8 Abs. 3: Löschung nach Vertragsende „einschließlich Cache" | `cacheLeeren` leert nur den prozessinternen Tarif-Cache; Redis-Schlüssel laufen per TTL (≤ 24 h) aus, Inngest nach 30 Tagen – innerhalb der 30-Tage-Frist, aber nicht „gelöscht", sondern „abgelaufen". | kein Handlungsbedarf, Formulierung in 5.9 A19 präzisieren. |
| K11 | Jeder Löschlauf schreibt eine Protokollzeile | Gesprächs-Löschlauf: ja (`LoeschLauf`, Betriebsprüfung meldet Ausbleiben). Vertragsende-, Audit-, Analytics- und Server-Läufe: keine Zeile, keine Überwachung. | **Christian A58:** alle Löschläufe in `LoeschLauf` schreiben (kleiner Aufwand). |

## C – Texte, die der Code anders sagt (Dennis / Christian)

| Nr | Stelle | Befund | Folge |
|---|---|---|---|
| T1 | Widget-Rechtstext (`widget-legal.ts:54`) | Enthält 1.5 Fassung 1.0: ohne Stimmung, ohne Besuchsanalyse-Zusatz, ohne `lymbe_ignore`, ohne Sprach-Hinweis-Marker; Zeile 346 sagt „Alle Empfänger verarbeiten die Daten in Deutschland" – AVV 1.7 sagt für STACKIT EU/EWR. Der Besucher bekommt ein größeres Versprechen als der Vertrag. | **Christian, Teil von A42:** Widget-Texte auf 1.5 Fassung 1.1 heben. |
| T2 | Demo-Text 1.5 L | Nicht umgesetzt; Demo zeigt nur Startdialog A mit „24 Stunden". | **Christian A42:** L einbauen. |
| T3 | DSE 1.6 Abschnitt 6: Session-Cookie „beim Schließen des Browsers gelöscht" | Cookie hat 12 Stunden `maxAge`. | **Dennis:** DSE-Satz auf „12 Stunden bzw. bis zur Abmeldung" (DSE 1.6 wird noch nicht veröffentlicht, Korrektur vor A42 ohne neue Fassung). |
| T4 | DSE 1.6 Abschnitt 2.7: Do-Not-Track/GPC wird beachtet | Stimmt in der Vorgabe, ist aber je Bot abschaltbar. | **Dennis:** Satz „sofern der Website-Betreiber dies nicht abgeschaltet hat" – oder **Christian:** Schalter entfernen. Empfehlung: Schalter entfernen (A59). |
| T5 | Kunde kann Startdialog und Rechtstext per Bot-Schalter ganz abschalten (`legalEnabled`, `legalRequireConsent`) | Dann bleibt nur das KI-Kennzeichen im Kopf; Art. 13-Information liegt beim Kunden, aber AVV § 6 Abs. 2 verspricht die Kennzeichnung „in allen Kanälen". | kein Vertragsbruch; **Dennis:** in 1.3/1.6 bleibt die Pflicht des Kunden; Christian: Schalter nur für Admins (A59). |
| T6 | Intent-Cache in Redis (900 s) hält `reasoning`/`extractedFields` | Nirgends genannt; kurzlebig, mandantenpräfixiert. | kein Handlungsbedarf (unter „Redis-Antwort-Cache" in 5.9 A4 mit abgedeckt). |
| T7 | Latenter OpenAI-Pfad: `lib/ai/openai-dateien.ts` + `rechnen.ts` laden Nutzerdateien zu `api.openai.com/v1/files`, sobald `AI_PROVIDER=openai` | Heute inaktiv (`AI_PROVIDER=stackit`), hängt nur an einer Umgebungsvariable. | **Christian A60:** Pfad entfernen oder hart auf STACKIT/Azure festnageln – sonst reicht ein Tippfehler in der Env, und Kundendateien gehen in die USA. |

## D – Bestätigt (Auswahl, Belege in 09a–09c)

Websuche: Generator mit STACKIT-Modell, Regex-Filter, Sperrliste je Workspace, Zweitprüfung, bei Fehler geschlossen; an OpenAI nur Suchbegriff + Land „DE" + `store:false`; Nachweis 14 Tage; Abbestellen greift bei jedem Zug. Anbieter: nur openai/azure/stackit, kein automatischer Wechsel, Werkstatt fällt bei fehlender Env auf STACKIT. Einordnung gpt-oss-20b, Stimmung nur Summe je Assistent, Mitarbeiter-Chats ohne Stimmung. Azure Speech ohne Logging, Audio nur im Prozess. Gespräche/Leads/Termine/Abläufe 90 Tage mit kürzerer Frist je Workspace; Einwilligungsnachweise 3 Jahre; Demo 24 h stündlich; Redis-Cache 1 h, IP ≤ 24 h. Mandantentrennung: DB je Workspace, Qdrant `tenant_{id}_bot_{id}`, MinIO `tenants/{id}/`, alle 31 Routen mit Mandanten-ID aus der Anfrage haben einen Wächter. Frag-Lymbe-Verläufe nur für die Person. Workspace-Formular mit Pflichtangaben, `AvvZustimmung` mit Fassung/Zeit/Name/E-Mail/IP. Schwärzung in `instrumentation.ts` und `lib/betrieb/fehler.ts`, keine Stelle loggt Besuchernachrichten. Widget-Analyse: IP nur als tagesrotierender Hash, DNT/GPC/Opt-out beachtet. Browserspeicher-Liste vollständig, keine Cookies. Portal: vier Cookies, lokale Schrift, kein Stripe-Skript. Meta-Webhook verwirft ohne Verbindung durch den Kunden. Wächter und „wachhalten" wie beschrieben.

## E – Neue Aufgaben für die To-do-Liste

| Nr | Aufgabe | Quelle | Wer |
|---|---|---|---|
| A53 | Zustimmungs- und Weisungsnachweise überleben die Workspace-Löschung (3 Jahre, ohne Inhalte) | K1, AVV § 8 Abs. 3 | Christian |
| A54 | Mail-Versandprotokoll und Anmelde-IPs auf 14 Tage | K5 | Christian |
| A55 | Admin-Änderung am Kunden-Assistenten und Sicherungs-Download nur über Support-Zugang bzw. als BetriebsZugriff mit Workspace | K6 | Christian |
| A56 | Slack-/Teams-Webhook-URLs und Webhook-Signaturen verschlüsseln | K7 | Christian |
| A57 | 2FA in `requireRole` für Personal-Rollen erzwingen | K8 | Christian |
| A58 | Alle Löschläufe schreiben eine `LoeschLauf`-Zeile | K11 | Christian |
| A59 | Schalter für DNT/GPC-Ignorieren entfernen; Rechtstext-Schalter nur für Admins | T4, T5 | Christian |
| A60 | OpenAI-Datei-Upload-Pfad entfernen oder hart sperren | T7 | Christian |
| D26 | DSE 1.6: Session-Cookie „12 Stunden bzw. bis zur Abmeldung" | T3 | Dennis |
| – | A42 ergänzen: Widget-Texte auf 1.5 Fassung 1.1, Demo-Text L, Altfassung AVV 1.6 ablegen | T1, T2, K3 | Christian |
