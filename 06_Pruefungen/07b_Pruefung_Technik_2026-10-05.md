# Technische Prüfung: Was die Datenschutz-Dokumente versprechen vs. was das Dienstleisterverzeichnis belegt

**Lymbe AI · Prüfung aus Plattform-/Security-Sicht · 05.10.2026 · Grundlage: Dienstleisterverzeichnis Stand 17.09.2026 (im Folgenden „V", Zeilenangaben = Zeilen der Textfassung `Dienstleisterverzeichnis.txt`), Unterauftragsverarbeiter-Stand 05.10.2026, AVV v1.6, Datenschutzerklärung v1.5, 1.5, 1.7, 5.6, 5.8, 5.9, 04 Abschnitt A**

Lesehilfe: ✅ laut V bereits so · ⚙️ Konfiguration (Minuten/Stunden) · 🔨 Bauaufgabe (Schätzung für einen Entwickler) · ❌ unrealistisch oder unklar · „nicht dokumentiert" = V sagt dazu nichts. Zeitrahmen: Mittwoch 08.10. sind ab heute rund 2,5 Arbeitstage (ca. 20 h), Sonntag 12.10. rund 4 weitere Tage. Alle Schätzungen setzen voraus, dass Christian den Code kennt und keine Überraschungen findet; bei Fremdcode (Activepieces-Fork) Faktor 2 einplanen.

Zwei Vorbemerkungen, die alles andere einfärben:

1. **V ist 18 Tage alt und war am 17.09. schon in Bewegung.** 4.1 behauptet Azure Speech „seit 30.09.2026" – das liegt nach V, V kennt keinen Microsoft-Empfänger (G1: „kein Empfänger", V-L682). Alles, was nach dem 17.09. gebaut wurde, ist hier als „nicht dokumentiert" markiert, auch wenn es inzwischen existieren mag. Die Abnahme in 5.9 muss deshalb am laufenden System gemessen werden, nicht aus V abgeschrieben.
2. **V ist ein Datenfluss-Verzeichnis, kein Sicherheitskonzept.** Es sagt, wohin Daten fließen, und nennt Fundstellen im Code. Es sagt fast nichts über Löschläufe, Protokolle, MFA, Verschlüsselung ruhender Daten oder Backup-Ablageort. Dass etwas in V fehlt, heißt also nicht, dass es fehlt – aber es heißt, dass die Dokumente es behaupten, ohne dass es jemand belegt hat.

---

## 1. Zusagen aus 5.9 – Stand laut Verzeichnis und Aufwand

### Block A – Kunden-AVV v1.6

| Nr | Zusage (Kurz) | Stand laut V | Einstufung | Aufwand / Begründung |
|---|---|---|---|---|
| A1 | Werkstatt über Azure OpenAI | **Nein.** `AI_PROVIDER_WERKSTATT=openai`, gemessen 17.09. (V-L103–105). Azure-Zugangsdaten sind hinterlegt, aber `AI_PROVIDER=stackit` (V-L682). Bei leerem `OPENAI_API_KEY` fällt die Werkstatt auf STACKIT zurück, nicht auf Azure (V-L322). | ⚙️ | 1–2 h: Umgebungsvariable setzen, Container neu starten, einen Ablauf in der Werkstatt erzeugen und im Azure-Portal nachsehen, ob die Anfrage ankommt. Vorher A26 (Region des Deployments = EU) prüfen – das ist ein Klick im Azure-Portal. Offen: ob der Werkstatt-Code den Provider `azure` wirklich unterstützt oder nur `openai`/`stackit`; V-L322 nennt nur den STACKIT-Rückfall. Wenn nicht: 🔨 0,5 Tag. |
| A2 | DB-Sicherungen 7 Tage | **Nein: 30 Tage** (V-L633–638, „nächtliche Datenbanksicherungen", „spätestens nach 30 Tagen"). Ablageort und Verschlüsselung: nicht dokumentiert. | ⚙️ | 15 min, wenn es ein eigenes Dump-Skript mit Retention-Variable ist (wahrscheinlich, da „nächtlich" und „wöchentliche Probe"). Wichtig: V sagt nicht, **wo** die Sicherungen liegen. Liegen sie auf derselben Maschine (V-L284: „Der gesamte Stack läuft auf einem Server"), sind sie kein Schutz gegen Serververlust oder Ransomware – siehe Abschnitt 7 und 9. |
| A2b | Hetzner-Server-Abbilder 7 Tage (inkl. Mailvolume, DKIM) | Mailvolume und DKIM-Schlüssel liegen „nur im Server-Snapshot" (V-L466–467). Häufigkeit und Aufbewahrung der Snapshots: nicht dokumentiert. | ⚙️ | 30 min. Hetzner Cloud hat zwei Dinge: „Backups" (automatisch, täglich, es werden die letzten 7 behalten, 20 % Aufpreis) und „Snapshots" (manuell, bleiben, bis man sie löscht). Die Zusage „7 Tage" passt exakt auf Hetzner-Backups. Also: Backups im Hetzner-Konto einschalten, alle manuellen Snapshots älter als 7 Tage löschen und in V nachtragen. Falls Christian Snapshots per Skript über die Cloud-API zieht (V-L285 nennt die API nur für Zertifikate/DNS): Retention im Skript. Hinweis: Hetzner-Backups sind nicht kundenseitig verschlüsselt. |
| A3 | Gespräche nach 90 Tagen automatisch gelöscht, Löschlauf existiert | **Nicht dokumentiert.** V nennt als einzige Fristen: Laufdaten Abläufe 30 Tage (V-L628) und DB-Sicherungen 30 Tage (V-L633). Kein Wort zu einem Gesprächs-Löschlauf. | 🔨 | 0,5–1 Tag. Inngest-Cron (B6 läuft schon, V-L433) täglich: für jede Mandanten-DB `DELETE` Gespräche + Nachrichten mit `last_message_at < now() - 90 d`; Kontakte/Leads bleiben (AVV § 8 Abs. 1 Tabelle), also Fremdschlüssel vorher lösen. Lauf protokollieren (Mandant, Anzahl, Zeitpunkt) – das ist der Beleg für 5.9. Dazu Test mit künstlich alt datierten Gesprächen. Für die Pilotkundin entsteht das erste 90-Tage-alte Gespräch erst Anfang Januar – der Job muss bis dahin laufen, nicht bis Mittwoch. |
| A4 | Laufdaten Abläufe 30 Tage | **Ja** (V-L628: „Laufdaten 30 Tage"). | ✅ | Beleg: Umgebungsvariable des Abläufe-Kerns, am 17.09. gemessen. |
| A5 | Inngest-Ereignisdaten 30 Tage | **Nicht dokumentiert.** B6 nennt „Ereignisdaten inkl. WhatsApp-Nachrichten" (V-L433–434), keine Frist. | ⚙️ oder 🔨 | 1–4 h. Selbst gehostetes Inngest speichert Events in seiner eigenen Datenbank (Postgres oder SQLite). Ob die OSS-Fassung eine Retention-Einstellung hat, muss Christian in der Inngest-Konfiguration nachsehen; wenn nein: SQL-Job gegen Inngests Tabellen (🔨 2–4 h) oder Frist im Vertrag auf das setzen, was wirklich gilt. Für die Pilotkundin ohne WhatsApp enthalten die Events nur interne Ereignisse (z. B. Löschläufe, Dokument-Import) – trotzdem Mandantendaten. |
| A6a | Zugriffs-/Betriebsprotokolle 14 Tage (Caddy, Mail) | **Nicht dokumentiert.** B7: „Zugriffsprotokolle mit IP-Adressen" (V-L437), keine Frist. Mail-Logs: nicht erwähnt. | ⚙️ | 1 h. Caddy: `log { output file ... { roll_keep_for 336h } }`. Docker-Container-Logs (Postfix, rspamd): `logging: driver json-file, max-size, max-file` im Compose oder journald `MaxRetentionSec=14d`. rspamd-History liegt in Redis (B5) – dort `history_rows`/TTL prüfen. |
| A6b | Fehlerprotokoll 30 Tage | **Nicht dokumentiert.** B10: „in der eigenen Datenbank, je Fehlerart eine Zeile" (V-L450–451, V-L707), keine Frist. | 🔨 | 1 h: täglicher Cron `DELETE ... WHERE last_seen < now() - 30 d`. Wichtiger als die Frist: **was** in „Fehlermeldung, Ort, Stapel" steht – siehe Abschnitt 3 (Payloads in Stacktraces). |
| A7 | Selbstlernen Standard aus; Einschalten protokolliert | **Nicht dokumentiert.** V erwähnt Selbstlernen nirgends. | ❌ unklar → ⚙️/🔨 | Erst klären, ob die Funktion existiert und wie der Default heißt (15 min). Protokollierung: Teil des Einstellungs-Audit-Logs aus A8. |
| A8 | Portal-Einstellungen mit Zeitpunkt und Nutzer protokolliert | **Nicht dokumentiert.** Einzige belegte Protokollzeile ist die AVV-Zustimmung (V-L143–145: Fassung, Zeitpunkt, Person, Adresse, in derselben Transaktion). | 🔨 | 0,5–1 Tag. Eine Tabelle in der zentralen DB (B1): `workspace_audit(id, workspace_id, user_id, action, key, old_value, new_value, ip, created_at)`, append-only (kein UPDATE/DELETE-Recht für den App-Benutzer, oder Trigger, der beides verbietet). Schreiben in den Server-Actions für: Websuche, Selbstlernen, Benachrichtigungsziel, Dienst verbinden/trennen, Mitglied einladen/entfernen, Rolle ändern. Ansicht im Portal kann später kommen; Export per SQL reicht für „Kunde erhält Protokoll auf Anfrage". Dieselbe Tabelle trägt A7, A9/B5 und A10. |
| A9 | Support-Zugriff protokolliert (Zeit, Person, Grund, Umfang, Mandant), nur mit Freigabe | **Nicht dokumentiert.** V belegt ein Admin-Postfach (0.2, V-L59) und Datenbankzugriffe durch Christian („in der Produktionsdatenbank nachgezählt", V-L42; „Die beiden gemessenen Zeilen … sind geleert", V-L52–53) – also direkten DB-Zugriff ohne jedes technische Protokoll. | 🔨 (technisch) / ⚙️ (organisatorisch) | Minimal technisch: 1–2 Tage (Abschnitt 5). Bis Mittwoch realistisch nur organisatorisch: ein Zugriffsregister (Markdown/Tabelle) mit den fünf Pflichtfeldern, das Christian vor jedem Zugriff ausfüllt und Dennis per Mail freigibt. Das erfüllt den Vertragstext („protokolliert") – aber nicht „technisch vorhanden", wie 04 A11 fragt. |
| A10 | Mandanten-Schalter Websuche, Standard aus, Einschalten protokolliert | **Nein.** Websuche ist „fest auf den OpenAI-Zugang verdrahtet" (V-L100), abschaltbar nur global über `OPENAI_API_KEY` (V-L322). Kein Workspace-Schalter erwähnt. | 🔨 | 0,5–1 Tag: Spalte `web_search_enabled boolean default false` am Workspace; in `lib/ai/web-suche.ts` vor dem Aufruf prüfen; Dialog aus 1.5 G beim Einschalten; Audit-Zeile (A8). Dazu Chat-Badge „🔍 Websuche" bei jeder Suche (1.5 G). Bis der Schalter existiert, ist die einzige Möglichkeit, die Zusage für die Pilotkundin einzuhalten: Key leer – siehe Abschnitt 8. |
| A11 | Mistral-Rückfall deaktiviert | **Unklar.** G2: „Zugangsdaten gesetzt, Rückfallebene" (V-L685). Ob der Rückfall automatisch greift (z. B. bei STACKIT-Timeout) oder nur per Konfigurationswechsel, sagt V nicht. | ⚙️ | 15 min: Key aus `docker/.env` entfernen, im Code nachsehen, was bei fehlendem Key passiert (Fehler statt stillem Rückfall). Wenn der Rückfall automatisch war, ist das außerdem ein Verfügbarkeits-Thema: ohne Rückfall steht der Chat, wenn STACKIT steht. Das ist die richtige Entscheidung bei Gesundheitsdaten, aber Christian muss es wissen. |
| A12 | Azure Speech live? Aufnahmen nicht gespeichert | **Nicht in V** – V kennt keinen Microsoft-Empfänger (G1 V-L682, Abschnitt A ohne Microsoft). 4.1 sagt „seit 30.09.2026", 1.5 K hat den Dialog. Also entweder nach dem 17.09. gebaut oder nicht live. | ❌ unklar → ⚙️ | 30 min: Christian bestätigt live/nicht live. Wenn live: Azure Speech speichert Audio standardmäßig nicht; Audio-Logging ist eine explizite Option (Custom Speech / „Log audio") – Screenshot der Ressourceneinstellung als Beleg, Region (Frankfurt = Germany West Central) im Portal ablesen. Wenn nicht live: aus 4.1, 1.5 K und AVV Anlage 2 Nr. 4 streichen, bis es kommt. |
| A13 | Messenger/Instagram aus oder wie WhatsApp | **Live:** „Messenger und Instagram über dieselbe App" (V-L359). | ⚙️ | 1–2 h: Entweder die Kanäle im Code/der Meta-App-Konfiguration für Kunden ausblenden, oder die Erstantwort aus 1.5 J für alle drei Kanäle einbauen. Für die Pilotkundin irrelevant (kein Messenger). |
| A14 | Admin-Zugänge mit MFA | **Nicht dokumentiert.** Portal-Login: Passwort oder Google/GitHub (C7, V-L504), Ratenbremse am Login (V-L258–259). Kein MFA erwähnt – weder Portal noch SSH noch Hetzner-Konto. | ⚙️ (Konten) / 🔨 (Portal) | ⚙️ 1–2 h: 2FA bei Hetzner, GitHub, STACKIT (TOTP laut Unterauftragsverarbeiter-Stand Z. 29), Azure, OpenAI, Stripe, Meta erzwingen; SSH nur mit Schlüssel, Passwort-Login aus; Portal-Admin-Konten nur über Google/GitHub-Login mit dort erzwungener 2FA anmelden lassen (Passwort-Login für Admin-Rolle sperren). 🔨 Portal-eigenes TOTP: 1–2 Tage – später. |
| A15 | Wöchentliche Wiederherstellungsprobe | **Ja** (V-L638: „Eine wöchentliche Probe spielt eine Sicherung wirklich zurück"). | ✅ | Beleg: letzter Lauf mit Datum. Offen: ob die Probe auf der Produktionsmaschine oder getrennt läuft; und ob sie prüft, dass die Daten lesbar sind (Zeilen zählen) oder nur, dass `pg_restore` durchläuft. |
| A16 | Mandantentrennung: DB je Kunde; Qdrant und MinIO mandantengetrennt | **DB: ja** (B2 V-L418; „fünf Mandanten-Datenbanken der Produktion", V-L162). **Qdrant, MinIO: nicht dokumentiert** – B3/B4 nennen nur Inhalt, nicht Struktur. | ✅ (DB) / ❌ unklar (Qdrant, MinIO) | 1 h Nachmessen: `GET /collections` in Qdrant (eine Collection je Mandant oder eine mit `tenant_id`-Payload-Filter?), `mc ls` in MinIO (Bucket oder Präfix je Mandant?). Beides kann „mandantengetrennt" sein, wenn jeder Lese- und Schreibpfad den Mandanten aus der Session zieht. Wenn Filter statt Collection: Tests schreiben (Abschnitt 3). Umbau auf Collection je Mandant: 🔨 0,5–1 Tag plus Neuindexierung. |
| A17 | Zugangsdaten verbundener Dienste verschlüsselt | **Ja** (V-L475: „Die Zugangsdaten lagern bei uns verschlüsselt"; V-L217, L544 „entschlüsselte Zugangsdaten"). | ✅ | Beleg: Modul und Algorithmus benennen, Ablageort des Schlüssels (Umgebungsvariable? dann liegt er in `docker/.env` auf derselben Maschine wie die Daten – legitim für diese Größe, aber in V nachtragen). |
| A18 | Export im Portal (JSON/CSV, Dokumente original) | **Nicht dokumentiert.** | 🔨 | 1–2 Tage für sauberen Export aller vier Datentypen je Workspace. Für Mittwoch nicht nötig: § 8 Abs. 4 greift bei Vertragsende; bis dahin reicht „Gesamtexport auf Verlangen" per Skript (pg_dump der Mandanten-DB → JSON, MinIO-Präfix als ZIP: 2–3 h, einmal geschrieben, manuell ausgeführt). Empfehlung: AVV-Text vorerst auf „auf Verlangen" belassen, Portal-Funktion P2. |
| A19 | Löschung nach Vertragsende: DB, Qdrant, MinIO, Inngest | **Nicht dokumentiert.** Belegt ist nur die Einzel-Löschung von Widget-Dokumenten aus MinIO (0.8, V-L159–162). | 🔨 | 0,5–1 Tag: ein Skript `mandant-loeschen <workspace_id>`: Mandanten-DB droppen, Qdrant-Collection löschen (oder Punkte nach Filter), MinIO-Präfix löschen, Inngest-Events mit diesem Mandanten löschen, Redis-Keys mit Präfix löschen, Zeile in zentraler DB auf „gelöscht am" setzen (Vertragsnachweis bleibt 3 Jahre, § 8 Abs. 3). Dasselbe Skript erledigt A20b. Beweis: Ausgabe des Skripts mit Zählern. |
| A20 | Workspace-Formular: Firma, Anschrift, Vertreter; Checkbox-Protokoll | **Teilweise.** Checkbox beim Anlegen des Workspace, nicht vorausgewählt, serverseitig geprüft, Protokoll mit Fassung, Zeitpunkt, Person, Adresse (V-L141–145). Felder Firma, Anschrift, Vertreter, Telefon: nicht dokumentiert. Fassung steht „an genau einer Stelle im Code" (V-L144) – muss auf 1.6 gesetzt werden. | ✅ (Checkbox) / 🔨 (Felder) | 2–4 h: vier Felder im Formular und in der Zustimmungszeile, Fassungskonstante auf „1.6", Checkbox-Text aus 1.5 O. Bis dahin gilt K1 (Papier-AVV). |
| A20b | 4 Testmandanten vollständig gelöscht | **Nicht erledigt** (V-L146–147: „die vier Bestandsmandanten haben keinen solchen Nachweis"). Hinweis: V zählt **fünf** Mandanten-DBs (V-L162) – die fünfte ist vermutlich Demo oder Lymbe selbst; klären, welche bleibt. | 🔨 | Mit A19-Skript: 2–4 h inkl. Skript. Ohne Skript manuell 1 h, aber dann ohne Nachweis und ohne Qdrant/MinIO-Reste. |
| A21 | Hinweis beim Verbinden zeigt Anbieter und Standort | **Nicht dokumentiert.** | 🔨 | Für die 8 festen Konnektoren (C1–C8): 0,5 Tag (Metadaten-Tabelle + Dialog aus 1.5 I). Für die 718 Bausteine des Abläufe-Kerns (V-L510): Tage – die Activepieces-Metadaten enthalten keinen Firmensitz. Für Mittwoch nicht nötig (Pilotkundin ohne Abläufe); vor dem ersten Abläufe-Kunden. |
| A22 | KI-Kennzeichnung Widget + Portal; Wechsel Mensch/KI sichtbar | **Nicht dokumentiert.** | 🔨 | Teil von A14 in 04 (Widget-Texte). Minimum für Mittwoch: Startdialog A + Rechtliches-Accordion B + Übergabe-Meldungen E + „Powered by"/KI-Badge: 0,5–1 Tag, wenn das Widget bereits einen Vorab-Dialog oder ein Menü hat; sonst 1–2 Tage. Portal-Hinweis M: 1 h. |
| A23 | Kontoinhaber der Verträge | V sagt dazu nichts (V-L728–729: Vertragsstand nicht geprüft). Unterauftragsverarbeiter-Stand 05.10.: STACKIT, Azure, OpenAI = Flubber (Z. 13, 27, 37); Hetzner: nicht dokumentiert. | ⚙️ organisatorisch | 1 h: Hetzner-Konto prüfen, Dennis als zweiten Nutzer mit Admin-Rolle einladen (Hetzner Cloud Console kann das), 2FA für beide. |

### Block B – AVV § 12 und Websuche

| Nr | Zusage | Stand laut V | Einstufung | Aufwand / Begründung |
|---|---|---|---|---|
| B1 | Suchbegriff ohne Personenbezug, feste Anweisung, 10 Testfragen | **Teilweise.** A4: „Hinaus geht ausschließlich der Suchbegriff, den das Modell formuliert hat – nicht das Gespräch, nicht die Dokumente, nicht wer gefragt hat", dazu „Land DE" fest (V-L316–317). Also gibt es schon einen Schritt, der aus der Frage einen Suchbegriff macht. **Nicht dokumentiert:** welches Modell ihn bildet (STACKIT oder OpenAI selbst?), ob die Nutzerfrage im Input an OpenAI steht, welche Anweisung gilt, ob `store: false` gesetzt ist. Keine Filterregel, kein Test. | 🔨 | 0,5–1 Tag für Prompt + Filter + Testskript + Protokoll (Abschnitt 2). **Kritischer Punkt:** Wenn der Suchbegriff heute vom OpenAI-Modell mit Web-Search-Tool aus der Nutzerfrage gebildet wird, dann geht die Nutzerfrage selbst an OpenAI – dann wäre V-L316 falsch. Das muss Christian in `lib/ai/web-suche.ts` als Erstes prüfen (15 min). |
| B2 | STACKIT: kein Training (Vertragsbeleg) | Dokument, keine Technik. STACKIT-AVV/TOMs verlinkt (Unterauftragsverarbeiter-Stand Z. 31–32). | ⚙️ | 30 min: Abschnitt im STACKIT-AVV/AGB finden und zitieren. |
| B3 | Microsoft: kein Training, Abuse-Monitoring-Status, Speech-Logging aus | Dokument + 1 Screenshot. Abuse-Monitoring: standardmäßig 30 Tage Speicherung, Abschaltung nur auf Antrag (Unterauftragsverarbeiter-Stand Z. 23). | ⚙️ | 1 h: Product Terms ablegen, Azure-Portal-Screenshot „Content filtering / abuse monitoring", Speech-Ressource „Audio logging: off". Die 30-Tage-Speicherung steht bereits korrekt in AVV Anlage 2 Nr. 4. |
| B4 | Einordnung (gpt-oss-120b) nur Absicht/Thema, keine Emotion | V: „gpt-oss-120b für die Einordnung jeder Nachricht" (V-L301–302). Was eingeordnet wird: nicht dokumentiert. | ⚙️ | 15 min: System-Prompt lesen, Ausgabeschema prüfen (kein Feld `sentiment`, `emotion`, `mood`). Wenn doch ein solches Feld existiert: 1 h entfernen. |
| B5 | Support-Zugriff nur nach Freigabe, protokolliert, alle Mandanten | wie A9 | 🔨 / ⚙️ | siehe A9 und Abschnitt 5. |
| B6 | Sehen alle Mitglieder alle Dokumente? | **Nicht dokumentiert.** V nennt Rollen nur als Inhalt der zentralen DB (B1, V-L415). | ⚙️ | 15 min nachsehen. Wahrscheinlich ja (Wissensbasis je Workspace, nicht je Nutzer) – dann stimmt AVV § 12 Abs. 5 und die Kundin muss es wissen. |
| B7 | Telefonfeld im Workspace-Formular | wie A20: nicht dokumentiert. | 🔨 | in A20 enthalten. Bis dahin K7/K1 (Papier). |
| B8 | Admin-Einsicht in Frag-Lymbe-Verläufe: Einstellung? Standard? | **Nicht dokumentiert.** | ❌ unklar | 15 min klären. Wenn Admins alles sehen und es keinen Schalter gibt: 1.5 M-Zusatz immer anzeigen und 1.6 entsprechend formulieren; Schalter 🔨 0,5 Tag später. 1.7 Abschnitt 5 behauptet „Admin-Einsicht aus" für die Pilotkundin – das ist nur haltbar, wenn der Schalter existiert. |

### Block C – Datenschutzerklärung v1.5

| Nr | Zusage | Stand laut V | Einstufung | Aufwand / Begründung |
|---|---|---|---|---|
| C1 | Demo-Widget: 24 h Löschung, kein Gedächtnis, keine Leads | D6: „Eigene Domain, gleiche Speichervorgänge wie D1" (V-L581). 24-h-Löschung, Gedächtnis und Lead-Erfassung: nicht dokumentiert. | 🔨 | 2–4 h: Demo-Assistent im eigenen Mandanten ohne Lead-Fähigkeit und ohne Selbstlernen (⚙️), Cron „Demo-Gespräche älter 24 h löschen" (Variante des 90-Tage-Jobs mit anderem Parameter). |
| C2 | Widget überträgt nur Referrer und IP | **Ja** (D1 V-L601–603: Referrer beim ersten Seitenaufruf, IP aus X-Forwarded-For für Ratenbegrenzung „und Auswertung"). | ✅ | „Auswertung" = die eigene Statistik in der Mandanten-DB (V-L699–700) – in 4.1 Abschnitt 2.7 als „Statistik ohne Profilbildung" benannt. Beleg: Netzwerkmitschnitt eines Seitenaufrufs ohne Chat. |
| C3 | Browserspeicher-Liste des Widgets | **Teilweise.** V belegt genau zwei Einträge: `lymbe_ignore` (localStorage) und Marker für proaktive Ansprache (sessionStorage) (V-L111, L601–602, Fundstellen widget.js:507, :728, :783). Sitzungskennung (12 h) und Bestätigung der Hinweise (180 Tage) stehen **nicht** in V. | ❌ Widerspruch, siehe Abschnitt 6 | 30 min Nachmessen in der Browser-Konsole, nach A14/A22-Umbau erneut. |
| C4 | Wächter: Meldeweg benennen | Wächter existiert (0.11, V-L199–202): GitHub Actions alle 30 min, `/api/puls`, Marketing-Seite, Zertifikat; „Gemeldet wird über einen Weg, der mit unserem Mailserver nichts zu tun hat" – der Weg ist nicht benannt. | ⚙️ | 5 min: Workflow-Datei lesen und den Dienst nennen (Push-Dienst, Telegram, zweites Postfach?). Falls ein Dritter: in 4.1 Abschnitt 2.6 ergänzen (er bekommt nur „Lymbe antwortet nicht" – kein Personenbezug). |
| C5 | Kein Stripe-Skript, Checkout nur per Weiterleitung | **Ja** (0.3 V-L89–94; D4 V-L575). | ✅ | Beleg: Netzwerk-Tab auf der Abrechnungsseite. **Achtung:** V-A5 (V-L331) enthält noch den alten Satz „js.stripe.com lädt beim Rendern" – veraltet, bei nächster V-Fassung streichen. |
| C6 | Profilbild einmal geholt, lokal gespeichert | **Ja** (0.1 V-L50–53, `lib/profile/anmeldefoto.ts`). | ✅ | |
| C7 | Keine Analyse-/Tracking-Tools, keine fremden Schriften, nur Session + CSRF | **Ja** (H V-L699–712, D7 V-L584). | ✅ | OAuth-State-Cookie (5.8 P3) ist in V nicht erwähnt, aber unvermeidbar bei Google/GitHub-Login – kein Widerspruch, nur in 5.8 schon richtig eingeordnet. |

**Zählung:** ✅ 10 (A4, A15, A17, A20-Checkbox, C2, C5, C6, C7, DB-Teil von A16, Werkstatt-Schalter existiert) · ⚙️ 13 · 🔨 13 · ❌ unklar 5 (A7, A12, A16-Qdrant/MinIO, B8, C3). Die Summe aller 🔨-Posten liegt bei rund **9–14 Entwicklertagen** – das passt nicht bis Sonntag, deshalb Abschnitt 8.

---

## 2. Der Suchbegriff-Generator

### 2.1 Was heute (laut V) passiert und was zuerst zu prüfen ist

V-A4 (V-L316–317) behauptet: nur der vom Modell formulierte Suchbegriff plus „Land DE" verlassen das Haus. V-0.4 (V-L100–101) sagt: das Websuch-Werkzeug gibt es nur in OpenAIs Responses-API. Beides zusammen passt nur, wenn die Architektur zweistufig ist:

1. Ein Modell (idealerweise STACKIT, bleibt in DE) macht aus Frage + Kontext einen Suchbegriff.
2. Nur dieser Suchbegriff geht als `input` an die Responses-API mit dem Tool `web_search`.

Wenn stattdessen die Nutzerfrage direkt als `input` an die Responses-API geht und OpenAIs Modell daraus intern seine Suchanfragen bildet, dann **geht die Frage mit allem, was darin steht, an OpenAI** – und V-L316 ist falsch. Das ist in 15 Minuten in `lib/ai/web-suche.ts` nachgelesen und muss als Erstes passieren, bevor irgendein Dokument „Suchbegriff ohne Personenbezug" sagt.

### 2.2 Bauplan (0,5–1 Tag)

**Schritt 1 – Generator (STACKIT, Qwen-Modell aus V-L301):**
System-Prompt, fest im Code, Hash des Prompts wird im Testprotokoll vermerkt:

```
Du erzeugst aus einer Nutzerfrage genau einen Suchbegriff für eine Internetsuche.
Regeln, ohne Ausnahme:
1. Übernimm nur das Sachthema. Niemals: Vor- oder Nachnamen, Initialen, Firmennamen von
   Privatpersonen, E-Mail-Adressen, Telefonnummern, Postadressen, Geburtsdaten, Alter in
   Verbindung mit Namen, Kennnummern (Versicherung, IBAN, Akten), Benutzernamen.
2. Niemals Angaben, die eine Person in Verbindung mit Gesundheit, Diagnose, Behandlung,
   Religion, Herkunft, Sexualität, Straftaten beschreiben. Das Thema selbst darf bleiben
   („Therapieansätze bei Autismus"), die Person nicht („Autismus bei Leon Müller, 7").
3. Keine Ortsangabe kleiner als Bundesland, außer der Ort ist selbst das Thema
   („Öffnungszeiten Stadtbibliothek Mettmann").
4. Höchstens 12 Wörter. Kein Satz, keine Frage, keine Anführungszeichen.
5. Lässt sich das Thema ohne Personenangabe nicht formulieren, antworte mit
   {"query": null, "reason": "personenbezogen"}.
Antworte ausschließlich als JSON: {"query": "...", "contains_person": false}
```

Input an den Generator: nur die aktuelle Nutzerfrage, nicht der Gesprächsverlauf. (Wenn Folgefragen Kontext brauchen: den Verlauf vorher durch dasselbe Modell zu einem Thema in drei Wörtern zusammenfassen und nur das mitgeben – nie den Verlauf.)

**Schritt 2 – deterministische Filter (TypeScript, kein Modell):**
- Regex-Sperre: E-Mail, Telefonnummern (international + deutsch), IBAN, Datumsformate, PLZ+Ort-Muster, `@`-Handles, Zahlenfolgen ≥ 6 Stellen.
- **Mandanten-Sperrliste:** alle Vor-/Nachnamen aus der Mandanten-DB (Kontakte/Leads, Team-Mitglieder, Namen in Gedächtnis-Einträgen) als normalisierte Wortmenge laden (gecacht, Redis, 10 min TTL); jedes Token des Suchbegriffs dagegen prüfen. Das ist der stärkste Filter, weil er genau die Personen kennt, die in diesem Workspace vorkommen.
- Großgeschriebene Wortpaare („Vorname Nachname"-Muster) gegen eine Vornamenliste (Open-Source-Liste, ~20 k Einträge, liegt im Repo) prüfen; Treffer → blockieren.
- Längenlimit 12 Wörter, Zeichen-Whitelist.

**Schritt 3 – zweite Meinung (optional, STACKIT, billig):** „Enthält dieser Suchbegriff Angaben zu einer bestimmten Person? ja/nein." Bei „ja" → blockieren. Zwei Modelle mit unterschiedlicher Aufgabe fangen mehr als eines.

**Schritt 4 – Versand an OpenAI:** `input` = nur der Suchbegriff, `tools: [{type: "web_search", user_location: {country: "DE"}}]`, **`store: false`** (sonst bleibt das Response-Objekt bei OpenAI abrufbar – unabhängig von der 30-Tage-Missbrauchsspeicherung), kein `user`/`safety_identifier`-Feld, keine Metadaten. Instruktion an OpenAI: nur Treffer (Titel, URL, Snippet) zurückgeben, keine Antwort formulieren. Die eigentliche Antwort baut dann das STACKIT-Modell aus Frage + Treffern – so bleibt der Gesprächsverlauf in Deutschland.

**Schritt 5 – Nachweis-Log:** jeder gesendete Suchbegriff wird in der Mandanten-DB gespeichert (Workspace, Zeitpunkt, Suchbegriff, Generator-Hash), 14 Tage, dann gelöscht. Das ist die Grundlage für die „regelmäßige Prüfung" aus AVV § 3 Abs. 10 und für die Auskunft an den Kunden, was wann an OpenAI ging. (Ja: wenn der Filter versagt, steht hier ein Name – deshalb 14 Tage und Mandanten-DB, nicht zentral.)

**Schritt 6 – Blockierfall im Chat:** „Für diese Frage kann ich keine Websuche ausführen, weil sie Angaben zu einer Person enthält. Formulieren Sie die Frage ohne Namen oder Kontaktdaten." Nicht still weglassen – der Nutzer soll lernen, was 1.5 G verlangt.

### 2.3 Garantierbar?

**Nein – nur als Maßnahme mit Restrisiko.** Ehrlich benannt:
- Ein Sprachmodell ist nicht deterministisch; Prompt-Regeln werden in Einzelfällen gebrochen, besonders bei Namen, die auch Wörter sind (Lang, Berg, Fuchs), bei ausländischen Namen ohne deutsche Großschreibungs-Signale und bei Namen, die nicht in der Mandanten-Sperrliste stehen (ein Kind, dessen Eltern erst heute angefragt haben).
- „Personenbezug" durch Kombination: „Autismustherapie Mettmann Zwillinge 2019 geboren" enthält keinen Namen und ist trotzdem für ein kleines Therapiezentrum quasi-identifizierend. Regel 3 im Prompt dämpft das, verhindert es nicht.
- Der Suchbegriff bleibt bei OpenAI bis zu 30 Tage (Missbrauchsüberwachung) – das ist vertraglich korrekt benannt, aber der Grund, warum die Kundin die Websuche aus lässt.

Das ist exakt die Frage J23 (TIA nötig?). Technische Antwort: Die Maßnahme reduziert die Wahrscheinlichkeit eines Personenbezugs im Suchbegriff deutlich (mit Sperrliste und zweiter Prüfung realistisch unter 1 % der Fälle mit Namen in der Frage), hebt sie nicht auf null. Der Vertragstext „nach fester Anweisung … ohne personenbezogene Angaben gebildet" ist als Beschreibung der Maßnahme richtig, als Garantie wäre er falsch. 1.5 G sagt deshalb zu Recht zusätzlich „Patienten- oder Mandantennamen gehören trotzdem nicht in Fragen".

### 2.4 Testprotokoll

Datei `05_Intern/5.14_Testprotokoll_Suchbegriff_JJJJ-MM-TT.md`, automatisch erzeugt von `pnpm test:suchbegriff` (ein Skript, das die echte Pipeline bis vor den OpenAI-Versand ausführt):

| Spalte | Inhalt |
|---|---|
| Kopf | Datum, Modell und Version (STACKIT), SHA-256 des System-Prompts, Git-Commit, wer ausgeführt hat |
| Je Fall | Nr, Testfrage, erwartete Sperr-Tokens (die Namen/Nummern/Diagnose-Person-Kombinationen aus der Frage), erzeugter Suchbegriff, Filterstufe (Generator / Regex / Sperrliste / Zweitprüfung / blockiert), **bestanden ja/nein** (= kein Sperr-Token im Suchbegriff, zusätzlich manuelle Sichtprüfung auf Kombinationen) |
| Fuß | Anzahl bestanden/gesamt; 100 % ist Freigabekriterium; ein Fehlschlag = Prompt nachbessern, erneut laufen |

Mindestens 30 statt 10 Fälle, in sechs Gruppen: (1) Klarname + Thema, (2) Telefon/E-Mail/Adresse, (3) Diagnose + Name + Alter, (4) Name als Wort („Herr Lang fragt nach langen Wartezeiten"), (5) indirekte Identifikation (Ort + seltenes Merkmal + Jahr), (6) harmlose Kontrollfragen, die **nicht** blockiert werden dürfen (sonst ist die Suche nutzlos). Lauf: vor jedem Release, das `web-suche.ts` oder den Prompt berührt, und vierteljährlich mit dem Dienstleisterverzeichnis (AVV Anlage 1: „vierteljährlich nachgemessen"). Jedes Protokoll wird abgelegt – das ist der Beleg für „regelmäßig getestet".

---

## 3. Mandantentrennung – wo es typischerweise leckt

Was V belegt: eine PostgreSQL-Datenbank je Mandant (B2, V-L418–419; „fünf Mandanten-Datenbanken", V-L162), eine zentrale DB für Konten/Mandanten/Abrechnung (B1), ein Qdrant, ein MinIO, zwei Redis-Instanzen (B5), ein Inngest, ein Abläufe-Kern mit eigener DB und „eigenem Redis-Bereich" (V-L611). Die DB-Trennung ist die stärkste Form, die es gibt – ein SQL-Fehler kann keine fremden Zeilen liefern. Alles andere ist in V nicht beschrieben.

| Leckstelle | Was V sagt | Risiko / Prüfung |
|---|---|---|
| **Qdrant-Collections** | B3: „Textabschnitte aus Dokumenten" (V-L422). Struktur: nicht dokumentiert. | Typisches Muster: eine Collection `documents`, Trennung nur über `filter: {must: [{key: "tenant_id", match: ...}]}`. Ein vergessener Filter in einem Suchpfad (z. B. Selbstlernen, Gedächtnis-Suche, Debug-Endpoint) liefert fremde Patientendokumente. **Prüfen:** `GET /collections`; jeden `search`/`scroll`-Aufruf im Code nach dem Filter durchsuchen; Test: Dokument in Mandant A hochladen, in Mandant B danach fragen. Empfehlung bei Filter-Modell: Filter zentral in einem Qdrant-Wrapper erzwingen, der ohne `tenant_id` nicht aufrufbar ist (Typsystem). |
| **MinIO-Pfade** | B4 (V-L425). 0.8: „Objektschlüssel aus der gespeicherten Adresse … beide gewachsenen Schreibweisen" (V-L159–160) → Pfadkonvention hat sich geändert. | Wenn Objekte unter `uploads/<uuid>.pdf` ohne Mandantenpräfix liegen, ist Trennung nur so gut wie die DB-Referenz. Risiko: vorhersagbare oder enumerierbare Schlüssel, Download-Route, die den Schlüssel aus dem Request nimmt statt aus der DB des Session-Mandanten. **Prüfen:** Download-Route lesen; signierte URLs mit kurzer Laufzeit? Bucket je Mandant oder Präfix `<workspace_id>/…` – letzteres reicht, wenn jede Route das Präfix aus der Session baut. Mandanten-Löschung (A19) braucht das Präfix ohnehin. |
| **Redis-Keys** | B5: „IP-Zähler, zwischengespeicherte Antworten" (V-L429–430). | „Zwischengespeicherte Antworten" ist der heikle Teil: Wenn ein Cache-Key aus dem Frage-Hash ohne Mandanten-ID gebildet wird, bekommt Mandant B die Antwort von Mandant A (inkl. Wissen aus dessen Dokumenten). **Prüfen:** alle `redis.set`-Aufrufe, Key-Schema muss `ws:<id>:` enthalten. Keine Trennung zwischen Mandanten ist bei Rate-Limits (IP-Zähler) in Ordnung. |
| **Logs mit Inhalten** | B7 Caddy: nur IP/Zugriff (V-L437). App-Logs (stdout der Next.js-Container): **nicht dokumentiert**. | Ein `console.log(messages)` beim Debuggen reicht, damit Chatinhalte aller Mandanten in einem gemeinsamen Docker-Log liegen – ohne Frist, ohne Trennung, im Server-Snapshot. **Prüfen:** `grep -rn "console.log\|logger\." lib/ server/ app/` nach Stellen, die Nachrichten, Prompts oder Dokumente loggen; Logger mit Redaction für Felder `content`, `message`, `text`. |
| **Fehlerprotokoll mit Payloads** | B10: „Fehlermeldung, Ort, Stapel – je Fehlerart eine Zeile" (V-L450–451), in der eigenen DB (V-L707), „ohne Sitzungsaufzeichnung". | Stacktraces von Zod/Prisma-Fehlern enthalten oft den fehlerhaften Input („Invalid value at messages[0].content: 'Mein Sohn Leon…'"). Das Fehlerprotokoll ist mandantenübergreifend und laut A6b 30 Tage. **Prüfen:** 5 echte Einträge ansehen; Fehlermeldungen vor dem Speichern auf 500 Zeichen kürzen und bekannte Payload-Muster entfernen; Mandanten-ID als eigenes Feld mitführen, Inhalt nie. |
| **Backups ohne Mandanten-Trennung** | V-L633: nächtliche Datenbanksicherung (vermutlich alle DBs in einem Lauf); Server-Snapshot enthält alles (V-L466–467). | Das ist bei einem Server normal und vertraglich abgedeckt (§ 8 Abs. 2: keine Einzel-Löschung aus Sicherungen). Problem ist nicht Trennung, sondern: Wiederherstellung eines Mandanten erfordert Zugriff auf das Gesamt-Dump; die Restore-Probe (A15) spielt alles zurück – wohin? Wenn auf die Produktionsmaschine in eine Test-DB: dann liegen alle Mandanten dort doppelt. **Prüfen:** Restore-Ziel und Aufräumen nach der Probe. |
| **Inngest-Events** | B6: Ereignisdaten inkl. WhatsApp-Nachrichten (V-L433–434); Inngest „läuft ohne Anmeldung" (V-L210). | Inngest-UI zeigt alle Events aller Mandanten im Klartext. Zugriff nur, wenn der Port nach außen zeigt (V-L210–211: „verlassen sich darauf, dass ihr Port nicht nach außen zeigt"). **Prüfen:** `docker ps` – kein `0.0.0.0:8288`; Hetzner Cloud Firewall; zusätzlich Basic-Auth vor Inngest-UI über Caddy (10 min). |
| **Abläufe-Kern** | eigene DB, eigener Redis-Bereich (V-L611); AP-Projekte je Mandant? nicht dokumentiert. | Activepieces trennt nach „Projekt"; wenn alle Lymbe-Mandanten in einem AP-Projekt laufen, sehen sie gegenseitige Verbindungen. Für die Pilotkundin ohne Abläufe irrelevant, vor Abläufe-Kunde Nr. 2 prüfen. |
| **Admin-Postfach** | 0.2: Admin-Oberfläche rendert eingehende Mails (V-L59). | Support-Mails aller Kunden an einem Ort, für 26lab lesbar – legitim, aber ein Zugriff auf Kundeninhalte im Sinne von AVV § 3 Abs. 5 und § 203. Gehört ins Zugriffskonzept (Abschnitt 5). |

Fazit: Die DB-Trennung ist echt und gut. Für die Zusage „Suchindex und Dateiablage mandantengetrennt" (AVV Anlage 1, 4.1 Abschnitt 10) gibt es **keinen Beleg** – sie ist plausibel, aber ungeprüft. Mit einer einzigen echten Kundin ist das Risiko bis zum zweiten Kunden gering (die 4 Testkonten werden gelöscht); bis dahin muss es gemessen sein.

---

## 4. Löschkonzept – was läuft, was fehlt

| Datenart | Frist (AVV § 8) | Job laut V | Stand | Was zu tun ist |
|---|---|---|---|---|
| Gespräche (Kundenservice, Live-Chat, Frag Lymbe) | 90 Tage nach letzter Nachricht | **keiner dokumentiert** | 🔨 | Inngest-Cron über alle Mandanten-DBs (A3). Erster Ernstfall für die Pilotkundin: Januar 2027. |
| Demo-Gespräche | 24 h | keiner dokumentiert | 🔨 | derselbe Job, anderer Parameter für den Demo-Mandanten (C1). |
| Laufdaten Abläufe | 30 Tage | **ja**, AP-Retention (V-L628) | ✅ | Beleg: Umgebungsvariable. Prüfen, ob Dateien ≤ 25 MB in AP-Storage dieselbe Frist haben. |
| Ereignisdaten Inngest | 30 Tage | keiner dokumentiert | ⚙️/🔨 | Inngest-Konfiguration prüfen, sonst SQL-Job (A5). |
| Zugriffsprotokolle Caddy, Mail | 14 Tage | keiner dokumentiert | ⚙️ | Log-Rotation (A6a). |
| Fehlerprotokoll | 30 Tage | keiner dokumentiert | 🔨 | 1 h Cron (A6b). |
| Sprachaufnahmen | keine Speicherung | Funktion nicht in V | ❌ unklar | A12 klären. Auch lokal: wird das Audio-Blob irgendwo zwischengespeichert (MinIO, tmp)? |
| Kontakte, Dokumente, Gedächtnis | bis Kunde löscht | Portal-Löschung; MinIO-Datei wird seit 0.8 mitgelöscht (V-L159–162) | ✅ teilweise | Nicht dokumentiert: Wird beim Löschen eines Dokuments auch sein Qdrant-Eintrag gelöscht? Wird beim Löschen eines Kontakts das Benachrichtigungs-Event (Inngest) gelöscht? Beides prüfen; AVV § 3 Abs. 7 verspricht „Reste in Suchindex, Dateiablage, Ereignisspeicher löscht Lymbe auf Weisung in 10 Werktagen" – das deckt eine Lücke organisatorisch ab, aber es sollte keine Lücke sein. |
| Zustimmungs-/Weisungsprotokoll | 3 Jahre nach Vertragsende | Zustimmungszeile existiert (V-L143) | ✅/🔨 | Beim Mandanten-Löschen (A19) ausnehmen. |
| Nach Vertragsende: DB, Qdrant, MinIO, Inngest | 30 Tage | keiner dokumentiert | 🔨 | Skript A19; manuell gestartet reicht, wenn der Lauf protokolliert wird. |
| DB-Sicherungen | 7 Tage | **30 Tage** (V-L633) | ⚙️ | Retention ändern (A2). |
| Server-Abbilder | 7 Tage | keine Frist dokumentiert | ⚙️ | Hetzner-Backups 7 Rotationen (A2b). |
| Redis-Cache | – (im AVV nicht genannt) | nicht dokumentiert | ⚙️ | TTL auf allen Antwort-Caches setzen (≤ 24 h), sonst ist der Cache ein unbefristeter Speicher von Chatantworten. |

**Backups „7 Tage" realistisch?** Drei Schichten, alle verschieden:
1. **Eigene Dumps (nächtlich):** 7 Tage sind eine Zeile im Skript. Risiko: Ein Fehler, der erst nach 8 Tagen bemerkt wird (schleichende Datenkorruption, versehentliche Löschung durch den Kunden, die erst nach dem Urlaub auffällt), ist nicht mehr rückholbar. Bei 30 Tagen wäre das abgedeckt. Die Entscheidung steht; Christian sollte wissen, was sie kostet. Milderung: zusätzlich ein wöchentlicher Dump, der 4 Wochen bleibt, wäre vertraglich nicht gedeckt – also nein. Dann wenigstens: Restore-Probe wöchentlich mit Zeilenzählung, damit kaputte Dumps nach spätestens 7 Tagen auffallen.
2. **Hetzner-Backups:** genau 7 tägliche Rotationen – passt. Hetzner-Snapshots (manuell) müssen diszipliniert gelöscht werden; ein vergessener Snapshot vom Debugging ist ein Verstoß. Empfehlung: Snapshots nur über ein Skript mit Ablaufdatum im Namen und wöchentlicher Aufräumlauf (hcloud CLI, 20 Zeilen).
3. **Ablageort:** V sagt nicht, wo die Dumps liegen. Liegen sie auf der Maschine selbst, löscht ein Angreifer mit Root-Zugang Daten und Sicherungen zusammen, und ein Hardware-Ausfall nimmt beides mit. Mindeststandard: Dumps verschlüsselt (age oder restic mit eigenem Schlüssel) auf eine Hetzner Storage Box oder Object Storage in einem anderen Hetzner-Standort, mit Zugangsdaten, die nur schreiben dürfen (Append-only / Objekt-Lock) – dann kann Ransomware auf dem Server die Sicherungen nicht löschen. 2–3 h. Das ist Punkt 4 in Abschnitt 9.

---

## 5. Support-Zugriff und Protokoll

**Gibt es das laut V?** Nein. V belegt das Gegenteil: Christian hat die Produktionsdatenbank direkt abgefragt und Zeilen geändert (V-L42, L52–53, L162) – aus gutem Grund, aber ohne Freigabe und ohne Protokoll außer dem Verzeichnis selbst. Ein Admin-Postfach (V-L59) und Admin-Oberflächen existieren; eine Impersonation-Funktion oder ein Audit-Log werden nicht erwähnt.

**Was der Vertrag verlangt (AVV § 3 Abs. 5, Anlage 1, Anlage 5 Nr. 2):** Zugriff nur bei Störung oder Kundenanfrage, vorherige Freigabe durch Dennis (bei Gefahr im Verzug nachträglich), Protokoll mit Zeitpunkt, Person, Grund, Umfang; der Kunde erhält es auf Anfrage.

**Minimale technische Umsetzung (1–2 Tage):**

1. **Tabelle** `support_access` in der zentralen DB: `id, admin_user_id, workspace_id, reason (Pflicht, min. 20 Zeichen), scope (enum: conversations | documents | contacts | settings | database), approved_by, approved_at, approval_ref (Ticket/Mail-Betreff), started_at, ended_at, ip`. Append-only.
2. **Impersonation im Portal:** Admin-Rolle bekommt „Workspace öffnen als Support" → Formular mit Grund, Umfang, Freigabe-Referenz → erzeugt die Zeile → setzt eine zeitlich begrenzte Support-Session (z. B. 60 min, Cookie-Claim `support_access_id`) → im Portal ein roter Balken „Support-Zugriff aktiv, Grund: …". Jede Server-Action prüft bei Support-Session: nur Lesen, außer `scope` erlaubt mehr. Beim Ende `ended_at` setzen.
3. **Freigabe:** Für Mittwoch reicht „Freigabe per Mail von datenschutz@lymbe.ai, Betreff im Feld `approval_ref`". Später: Dennis bekommt im Portal einen Knopf „Freigeben", ohne den die Session nicht startet (Vier-Augen-Prinzip, 1.7 R2 verspricht genau das: „Freigabe durch die jeweils andere Partei").
4. **Direkter DB-Zugriff** (psql, Prisma Studio) lässt sich nicht im Portal protokollieren. Zwei Dinge dagegen: (a) Postgres-Logging `log_connections=on`, `log_statement='mod'` für die Admin-Rolle, Logs 30 Tage; (b) Regel in 5.3/Anlage 5: jeder direkte DB-Zugriff bekommt vorher eine Zeile in `support_access` mit `scope=database`, eingetragen über ein kleines CLI (`pnpm support:begin --workspace … --reason …`). Das ist Disziplin, kein Zwang – ehrlich so benennen.
5. **Kundenansicht:** Inhaber sieht im Portal unter Einstellungen → Datenschutz die Zugriffe auf seinen Workspace (Liste aus derselben Tabelle). 2 h, kann nach Sonntag kommen; bis dahin „auf Anfrage" per SQL.

**Bis Mittwoch** (organisatorisch, 30 min): Datei `05_Intern/5.15_Zugriffsregister.md` mit den fünf Spalten; Regel: kein Zugriff ohne Zeile und Freigabe-Mail. Das erfüllt den Vertragstext. Die technische Variante folgt in der ersten Woche nach Livegang.

---

## 6. Widget und Browserspeicher – stimmen 5.8, 4.1, 1.5 mit V überein?

| Eintrag (5.8) | V | Bewertung |
|---|---|---|
| W1 `lymbe_ignore`, localStorage, nach „Schließen" | ✅ V-L111, L601 (widget.js:507) | stimmt |
| W2 Marker proaktive Ansprache, sessionStorage | ✅ V-L111, L602 (widget.js:728, :783 ff.) | stimmt. V-L112: „Der Code argumentiert selbst, dass es um technisch Erforderliches geht" – deckt sich mit 5.8-Bewertung. Umbau auf „erst nach Nutzerhandlung" ist P2, 1–2 h. |
| W3 Sitzungskennung, localStorage, 12 h | **nicht in V.** V-L720 sagt ausdrücklich, „die Speichervorgänge in widget.js" seien ausgewertet, und nennt nur W1 und W2. | ❌ Widerspruch. Entweder das Widget hält die Gesprächs-ID nur im Speicher der Seite (dann geht das Gespräch bei Seitenwechsel verloren – und 1.5 B „damit ein Verlauf beim Zurückkommen erhalten bleibt" ist falsch), oder sie liegt im sessionStorage (dann Dauer = Tab, nicht 12 h), oder sie liegt in localStorage und V hat sie übersehen. 10 min in der Browser-Konsole. Die „12 Stunden" sind in keinem Dokument belegt – wenn es keinen Ablauf gibt, muss das Widget einen bekommen (Zeitstempel neben der ID, beim Laden prüfen: 30 min). |
| W4 Bestätigung der Hinweise, 180 Tage | **nicht in V** – kann nicht existieren, weil der Startdialog mit Checkbox erst gebaut wird (04 A14, Punkt A). | ⏳ entsteht mit A14. Dabei festlegen: Key `lymbe_consent_<assistant_id>` = `{version: "1.0", at: ISO}`; beim Laden prüfen `at > now − 180 d`, sonst Dialog erneut. |
| 4.1 Abschnitt 2.7 / 1.5 B listen W1, W3, W4 | | Nach A14 stimmt die Liste, wenn W3 geklärt ist. **W2 fehlt in 4.1 und 1.5** – der sessionStorage-Marker wird dort nicht genannt, obwohl er laut V existiert. Entweder ergänzen („ein Merker, dass die automatische Ansprache in dieser Sitzung schon gezeigt wurde") oder W2 umbauen, sodass er mit W1 zusammenfällt. |
| C2 „nur Referrer und IP ohne Chat" | ✅ V-L601–603 | stimmt; zusätzlich Browser-Typ/Gerätetyp aus dem User-Agent (1.5 B nennt es korrekt). |
| Portal P4 UI-Einstellungen in localStorage | nicht in V | 5 min Konsole; harmlos. |

Außerdem: 5.8 Kopf verweist auf „4.1 Abschnitt 13/17" und „4.1 Abschnitt 7 und 17" – 4.1 v1.5 hat 13 Abschnitte; gemeint sind 2.7 und 6. Dokumentfehler, nicht Technik.

---

## 7. Was V wirklich sagt – Backups, Verschlüsselung, Mail, Wächter, Mistral, Rate-Limiting, Bot-Prüfung

| Thema | V belegt | Dokumente behaupten darüber hinaus | Lücke |
|---|---|---|---|
| **Backups** | nächtliche DB-Sicherung, 30 Tage; wöchentliche Restore-Probe (V-L633–638). Mailvolume + DKIM nur im Server-Snapshot (V-L466–467). | AVV Anlage 1 / 4.1 Abschn. 10: „tägliche **verschlüsselte** Datensicherung, 7 Tage". AVV § 8: „Server-Abbilder 7 Tage". | Verschlüsselung: nicht dokumentiert. Ablageort: nicht dokumentiert. 7 Tage: nicht so. Snapshot-Frist: nicht dokumentiert. |
| **Verschlüsselung** | TLS über Caddy (B7, V-L437; ACME V-L382). Zugangsdaten verbundener Dienste verschlüsselt (V-L475). Passwort-Hash (B1, V-L415; ~100 ms Hashing V-L254). | AVV Anlage 1: „verschlüsselte Datenträger (AES-256)"; 4.1 Abschn. 10: „Verschlüsselte Speicherung sensibler Daten (AES-256)". | **Nicht dokumentiert und zweifelhaft.** Hetzner Cloud CPX-Server haben lokale NVMe ohne kundenseitig steuerbare Verschlüsselung; LUKS auf dem Root-Volume ist auf einer Cloud-VM ohne Konsole beim Neustart unpraktisch. Entweder Christian belegt es (z. B. `lsblk -f` zeigt `crypto_LUKS`, oder Hetzner-Zusage zur Verschlüsselung ruhender Daten im Rechenzentrum), oder der TOM-Satz wird auf das Belegbare geändert: „TLS bei der Übertragung; Zugangsdaten verbundener Dienste und Datensicherungen verschlüsselt (AES-256); physische Sicherheit des Rechenzentrums nach Hetzner-Zertifizierung (ISO 27001)". Die zweite Fassung ist ehrlich und reicht. |
| **Mailserver** | eigener Container, eigene IP, Postfix/rspamd/ClamAV/Unbound, DKIM, Spamhaus-Abfragen (B9, V-L444–467; A10 V-L394–399); ClamAV-Signaturen täglich (F3). | 4.1 Abschn. 2.4 beschreibt es korrekt inkl. Spamhaus. | Mail-Log-Frist (A6a) nicht dokumentiert. Nicht in den Dokumenten: ClamAV-Signaturabruf (ohne Personenbezug, in Ordnung). |
| **Wächter** | GitHub Actions alle 30 min, `/api/puls` nach DB-Abfrage, Marketing-Seite, Zertifikat; Meldeweg unabhängig vom Mailserver, nicht benannt; GitHub schaltet nach 60 Tagen Inaktivität ab (V-L199–202, L370–372). | 4.1 Abschn. 2.6: „keine personenbezogenen Daten". | Meldeweg benennen (C4). 60-Tage-Abschaltung: Workflow mit `schedule` braucht einen Commit alle 60 Tage – Kalendereintrag oder ein zweiter Workflow, der monatlich einen leeren Commit macht. |
| **Mistral** | G2: Zugangsdaten gesetzt, „Rückfallebene" (V-L685). | 5.9 A11: „deaktiviert". Anlage 2: nicht gelistet. | Ob automatisch: nicht dokumentiert. Key entfernen (A11). |
| **Rate-Limiting** | Widget: Cooldown, Duplikat-, Burst-, Fünfminuten-, Tageslimit; bestandene Bot-Prüfung zählt jetzt (0.13, V-L247–250). Registrierung: 5/h/IP, Rätsel, gleiche Antwort bei bekannter Adresse (V-L253–257). Login: Obergrenze je IP über alle Konten (V-L258–259). Redis für IP-Zähler (B5). | AVV Anlage 1: „Ratenbegrenzung". 4.1 Abschn. 2.6: „Drosselung, dauerhafte Sperren entscheidet ein Mensch". | ✅ Belegt. Nicht dokumentiert: Limits für Portal-APIs (Chat im Portal, Dokument-Upload, Export), die eingeloggte Nutzer treffen. |
| **Eigene Bot-Prüfung** | ALTCHA-Format, eigener Server stellt Prüfsumme, 696 ms in Chrome, letzte Stufe hinter den Ratenbremsen; keine Verhaltensprüfung (0.13, V-L241–244). | AVV Anlage 1: „Eigene Missbrauchsprüfung im Chat-Widget ohne Einbindung Dritter". 4.1 Abschn. 5. | ✅ Belegt. V-L243–244 sagt ehrlich, dass ein Rechenrätsel native Angreifer nicht stoppt – die Dokumente versprechen auch nicht mehr. |
| **SSRF / Abrufadressen** | behoben in `lib/abruf/` (0.12, V-L215–230) für API-Import, Dokument-Neuaufbau, Crawler; Konnektoren zitieren keine Antwortkörper mehr. | AVV Anlage 1: „Abrufadressen geprüft". | ✅. Aber: C11-Tabelle in V (V-L544–549) enthält noch den alten Text „ohne Schranke gegen Anfragen ins interne Netz" – veraltet. Hilfeseiten-Logo als `<img src>` fremder Adresse ist **nicht** behoben (V-L547–549; 04 P2). |
| **Sandbox** | Pyodide im Container ohne Netz (B8, V-L440). Abläufe-Kern: `SANDBOX_CODE_ONLY`, `AP_NETWORK_MODE=STRICT` (V-L628–629). | AVV Anlage 1: „abgeschotteter Bereich ohne Netzzugang". | ✅. |
| **Interne Dienste ohne Auth** | Inngest ohne Anmeldung, Qdrant und MinIO über HTTP, „verlassen sich darauf, dass ihr Port nicht nach außen zeigt" (V-L210–211). | – (in keinem Dokument) | Das ist der wichtigste Satz in V für die Sicherheit: Die gesamte Trennung hängt an der Docker-Netzkonfiguration. Siehe Abschnitt 9, Punkt 1. |
| **MFA, Zugriffsprotokoll, Einstellungs-Protokoll, Löschläufe, Export** | nichts | AVV, 4.1, 1.7 R1/R2/R5 behaupten alle fünf. | Abschnitte 1, 4, 5. |

---

## 8. Realistische Priorisierung (04 Abschnitt A)

Rahmen: eine Kundin, Website-Bot + Digitaler Mitarbeiter + Frag Lymbe **ohne** Websuche, ohne WhatsApp, ohne Abläufe; Gesundheitsdaten von Kindern; 4 Testkonten. Ein Entwickler, ~20 h bis Mittwoch, ~30 h mehr bis Sonntag (wenn das Wochenende durchgearbeitet wird – das sollte Dennis nicht als Normalfall einplanen).

### Bis Mittwoch 08.10. – ohne das sollte die Kundin nicht starten (ca. 14–18 h)

| 04-Nr | Aufgabe | Aufwand | Warum jetzt |
|---|---|---|---|
| A22 (interim) | `OPENAI_API_KEY` leeren, bis Schalter + Generator stehen (Werkstatt fällt auf STACKIT, V-L322 – trifft nur Testkonten) | 10 min | Einzige Möglichkeit, AVV § 3 Abs. 10 („nur wenn eingeschaltet") und 1.7 Abschn. 5 („nicht eingeschaltet") für die Kundin technisch wahr zu machen. Kein Widerspruch zur Entscheidung „nichts abschalten": Es ist ein Zwischenstand von vier Tagen. |
| A7 | Mistral-Key entfernen | 15 min | Nicht gelisteter Empfänger. |
| A2, A23 | Dump-Retention 7 Tage; Hetzner-Backups einschalten, alte Snapshots löschen | 1 h | Vertragswerte. |
| – | Dumps verschlüsselt an einen zweiten Ort (Storage Box, append-only) | 2–3 h | Nicht im Vertrag gefordert, aber: ohne das ist „tägliche verschlüsselte Datensicherung" (Anlage 1) unbelegt und ein Serververlust = Datenverlust. Bei Gesundheitsdaten von Kindern nicht verhandelbar. |
| – | Nachmessen: `docker ps`-Ports, Hetzner Firewall, Qdrant-Collections, MinIO-Layout, Redis-Key-Schema, 5 Fehlerprotokoll-Einträge, App-Logs auf Inhalte | 2 h | Abschnitt 3 – nur messen, Fixes nach Befund. |
| A14 (minimal) + A22 in 5.9 | Widget: Startdialog A + Rechtliches B + Übergabe-Meldungen E + KI-Badge; Datenschutz-Link und Anrede „Sie" als Assistenten-Einstellung; Bestätigung mit Fassung/Zeit in localStorage (W4) | 6–8 h | Art. 50 KI-VO und Art. 13-Information der Eltern beim ersten Kontakt. Rest von 1.5 (D, G, H, I, J, K, N) ist für diese Kundin nicht sichtbar oder nicht aktiv. |
| A12 (MFA, Konten) | 2FA bei Hetzner, GitHub, STACKIT, Azure, OpenAI, Stripe; SSH-Passwort-Login aus; Admin-Konten im Portal nur über 2FA-gesicherten Google/GitHub-Login | 1–2 h | Anlage 1 verspricht MFA; ohne Portal-TOTP ist das die ehrliche Annäherung. |
| A8, A10, B6, B8 | Klären (je 15 min): Azure Speech live? Einordnungs-Prompt ohne Emotion? Rollen/Dokumentsicht? Admin-Einsicht? | 1 h | Vertragstexte hängen daran; keine Bauarbeit, nur Antworten. Wenn Speech nicht live: 4.1/1.5 K/Anlage 2 anpassen (Cowork, 10 min). |
| A11 (interim) | Zugriffsregister als Datei anlegen, Regel vereinbaren | 30 min | Abschnitt 5. |
| A20 | Testmandanten löschen (mit Skript A19 – 3 h; oder manuell 1 h ohne Qdrant/MinIO-Nachweis) | 1–3 h | Kann auf Sonntag, wenn die Zeit fehlt – die Testkonten enthalten laut D1 keine Kundendaten. Besser Mittwoch, weil das Skript ohnehin gebraucht wird. |
| A19, A21, A13, A27 | Unterschriften, Mobilnummer, Dokumente ablegen, STACKIT-Kontakt | 1 h | Organisatorisch, nebenher. |

Nicht bis Mittwoch nötig, obwohl in 5.9 „Pflicht vor Freischaltung": A18 (Export – greift bei Vertragsende), A3 (90-Tage-Job – greift im Januar), A21 (Dienst-verbinden-Hinweis – keine Dienste), A1 (Werkstatt – keine Abläufe; mit leerem OpenAI-Key läuft sie ohnehin über STACKIT). Das ist kein Freibrief, sondern Reihenfolge: Das Freigabeprotokoll kann diese Zeilen mit „⏳ bis 12.10." bzw. „⏳ bis 31.10." tragen, ohne dass eine Zusage gegenüber der Kundin bis dahin gebrochen wird.

### Bis Sonntag 12.10. (ca. 20–28 h)

| 04-Nr | Aufgabe | Aufwand |
|---|---|---|
| A3 + A16-Demo | Lösch-Cron 90 Tage / 24 h Demo, mit Protokollzeile je Lauf | 4–8 h |
| A4 (Fristen) | Caddy/Mail-Log-Rotation 14 Tage; Fehlerprotokoll-Cron 30 Tage; Inngest-Retention prüfen/bauen; Redis-TTLs | 3–5 h |
| A22 + A5 | Mandanten-Schalter Websuche (Standard aus) + Suchbegriff-Generator + Filter + Testskript + erstes Protokoll; dann Key wieder setzen | 8–12 h |
| A8 (Audit-Tabelle) | `workspace_audit` + Hooks für Websuche/Selbstlernen/Benachrichtigung/Dienst/Mitglieder | 4–6 h |
| A1 + A26 | Werkstatt auf Azure, Region prüfen | 1–2 h (oder 🔨 0,5 Tag, wenn der Provider nicht unterstützt wird) |
| A15 | Workspace-Formular: Firma, Anschrift, Vertreter, Telefon; Fassung „1.6" | 2–4 h |
| A17 | Browserspeicher nachmessen nach Widget-Umbau, Liste an 5.8 | 30 min |
| Befunde aus der Mittwoch-Messung | Qdrant-Filter-Wrapper, Redis-Keys, Log-Redaction, Fehlerprotokoll-Kürzung – je nach Befund | 0–8 h |

### Später (Oktober/November, vor Kunde Nr. 2 bzw. erstem Abläufe-/WhatsApp-Kunden)

A11 technisch (Support-Impersonation + Audit, 1–2 Tage) · A18 Export im Portal (1–2 Tage) · Portal-TOTP (1–2 Tage) · A21 für 718 Bausteine · A9 Messenger/Instagram · B8-Schalter · W2-Umbau · Hilfeseiten-Logo spiegeln · Qdrant Collection je Mandant, falls Filter-Modell · Kundenansicht Zugriffsprotokoll · Postgres-Statement-Logging für Admin-Rolle · Export Art.-30-Angaben je Kunde.

**Ehrliche Gesamtsumme:** Die 🔨-Posten aus 5.9 sind 9–14 Entwicklertage. Bis Sonntag sind davon realistisch 4–5 Tage zu schaffen, wenn Christian nichts anderes tut. Was bis Sonntag nicht fertig ist, muss im Freigabeprotokoll mit Datum stehen und – wo es eine Zusage gegenüber der Kundin ist, die vor dem Datum greifen könnte – im AVV-Text zeitlich bedingt formuliert werden. Das betrifft nach dieser Liste nur: Support-Protokoll (organisatorisch gelöst) und Export (auf Verlangen). Alles andere greift erst nach Sonntag oder betrifft Funktionen, die die Kundin nicht nutzt.

---

## 9. Die 10 wichtigsten Sicherheitsmaßnahmen für dieses Portal

Reihenfolge nach Risiko × Umsetzbarkeit für einen Entwickler mit diesem Stack (Next.js, Prisma, Postgres je Mandant, Qdrant, MinIO, Redis, Inngest, Caddy, Docker Compose auf einem Hetzner CPX32).

1. **Netzgrenze der internen Dienste messen und hart machen (2 h).** V-L210–211 sagt es selbst: Inngest ohne Anmeldung, Qdrant und MinIO über HTTP, alle drei „verlassen sich darauf, dass ihr Port nicht nach außen zeigt". Docker-`ports:`-Einträge umgehen `ufw` (Docker schreibt eigene iptables-Regeln) – ein `8288:8288` im Compose ist öffentlich, auch wenn ufw „deny" sagt. Umsetzung: `docker ps` prüfen, jedes `ports:` außer Caddy 80/443 und Postfix 25/587/993 entfernen (interne Dienste brauchen nur `expose`), Hetzner Cloud Firewall mit genau diesen Ports anlegen, von außen mit `nmap` nachmessen. Zusätzlich Basic-Auth vor Inngest-UI und MinIO-Console über Caddy. Das ist die Maßnahme mit dem besten Verhältnis von Risiko zu Aufwand im ganzen System.

2. **Mandanten-ID nur aus der Session, nie aus der Anfrage (1–2 Tage, inkrementell).** Jede Server-Action, Route und jeder Qdrant/MinIO/Redis-Zugriff bekommt den Mandanten aus `session.workspaceId`, nicht aus Body, Query oder Pfad. Umsetzung: ein `withTenant(fn)`-Wrapper, der die Mandanten-DB-Verbindung, den Qdrant-Filter/die Collection, das MinIO-Präfix und den Redis-Key-Präfix erzeugt und als einziges Objekt an den Code gibt – wer direkt `qdrant.search` aufruft, fällt im Code-Review auf (ESLint-Regel `no-restricted-imports` für die Roh-Clients außerhalb des Wrappers). Dazu ein Integrationstest „Mandant B sieht nichts von A" für Dokumente, Gespräche, Kontakte, Dateien.

3. **Sicherungen außer Haus, verschlüsselt, unlöschbar vom Server aus (3 h).** `pg_dumpall` + MinIO-Spiegel + Qdrant-Snapshot → restic mit eigenem Schlüssel → Hetzner Storage Box (anderer Standort) per SFTP oder Object Storage mit Append-only-Schlüssel; 7 Tage Retention per `restic forget`. Restore-Probe wöchentlich gegen einen Wegwerf-Container mit Zeilenzählung und Mail/Push bei Abweichung. Begründung: Heute liegt laut V alles auf einer Maschine; Ransomware oder ein `rm -rf` löschen Daten und Sicherungen zusammen.

4. **Alle Admin-Zugänge mit zweitem Faktor, SSH nur mit Schlüssel (2 h, Portal-TOTP später 1–2 Tage).** Hetzner-, GitHub-, STACKIT-, Azure-, OpenAI-, Stripe-, Meta-Konten mit TOTP; `PasswordAuthentication no`, `PermitRootLogin prohibit-password`; fail2ban oder Hetzner-Firewall auf SSH nur von bekannten IPs (Christian hat eine feste Adresse oder nutzt Tailscale – 30 min, dann ist SSH gar nicht öffentlich). Portal-Admin-Konten bis zum eigenen TOTP nur über Google/GitHub-Login mit dort erzwungener 2FA.

5. **Ein Audit-Log für alles, was ein Mensch mit Rechten tut (1 Tag).** Eine append-only-Tabelle für Workspace-Einstellungen (A8), Support-Zugriffe (A9/B5), Mitgliederänderungen, Löschläufe, Exporte. Postgres-Rolle der App ohne DELETE/UPDATE auf dieser Tabelle. Begründung: Drei Vertragszusagen und 1.7 R2/R8 hängen daran, und es ist die einzige Möglichkeit, nach einem Vorfall zu wissen, wer was wann sah.

6. **Löschen als Beweis, nicht als Versprechen (1 Tag).** Inngest-Crons für 90/24 h/30/14/30 Tage, jeder Lauf schreibt eine Zeile ins Audit-Log (Mandant, Art, Anzahl). Ein `mandant-loeschen`-Skript, das DB, Qdrant, MinIO, Inngest, Redis abräumt und Zähler ausgibt. Beim Löschen eines Dokuments/Kontakts im Portal sofort Qdrant-Punkte und Inngest-Events mitnehmen, nicht „auf Weisung in 10 Werktagen". Begründung: Bei Gesundheitsdaten von Kindern ist „wir glauben, es ist weg" keine Antwort auf eine Betroffenenanfrage.

7. **Keine Inhalte in Logs und Fehlerprotokollen (0,5 Tag).** Logger mit Redaction-Liste (`content`, `message`, `text`, `messages`, `prompt`, `document`, `email`, `phone`), Fehlermeldungen vor dem Speichern auf 500 Zeichen kürzen, Prisma-Fehler ohne Query-Parameter, Next.js `serverActions`-Fehler nicht mit Body. Docker-Log-Rotation 14 Tage. Begründung: B10 speichert „Stapel" (V-L450), und Stacktraces sind der häufigste Ort, an dem Gesundheitsdaten unbemerkt mandantenübergreifend und ohne Frist landen.

8. **Verschlüsselung ehrlich machen (0,5 Tag oder 10 min Textänderung).** Entweder belegen (LUKS auf einem Hetzner-Volume für `/var/lib/docker/volumes` mit Schlüssel aus einer Datei, die beim Boot per Hand oder per Hetzner-Metadaten geladen wird – machbar, aber ein Neustart um 3 Uhr nachts bleibt dann hängen, bis jemand den Schlüssel eingibt) oder den TOM-Satz auf „Übertragung TLS; Zugangsdaten, Sicherungen und Passwörter verschlüsselt; Rechenzentrum ISO 27001" ändern. Für ein Zwei-Personen-Team ist die zweite Variante die sicherere, weil sie keinen Verfügbarkeitsvorfall einbaut. Was auf jeden Fall verschlüsselt sein muss: die Sicherungen (Punkt 3) und die Zugangsdaten verbundener Dienste (ist so, V-L475).

9. **Abhängigkeiten und Host aktuell halten, Lieferkette klein (2 h Einrichtung, dann laufend).** `unattended-upgrades` auf dem Host; Dependabot/Renovate für beide Repos mit wöchentlichem Sammel-PR; Container-Images monatlich neu bauen; `npm audit` im CI blockierend bei „high". Der Activepieces-Fork mit 765 Bausteinen (V-L624) ist die größte Angriffsfläche im System – der Sync ist zu Recht aus (0.10); zusätzlich: `AP_PIECES_SYNC_MODE=NONE` als Test im CI absichern, damit niemand es versehentlich zurückdreht, und Bausteine, die kein Kunde nutzt, aus dem Katalog nehmen.

10. **Sicherheits-Ereignisse sehen, nicht nur Ausfälle (0,5 Tag).** Der Wächter (0.11) sieht nur „Portal antwortet". Dazu: Alarm bei gehäuften Login-Fehlschlägen über alle Konten, bei Rate-Limit-Sperren im Widget über Schwelle, bei jedem Support-Zugriff (Mail an datenschutz@), bei jedem neuen Admin-Konto, bei jedem Lauf des Mandanten-Löschskripts, bei fehlgeschlagener Restore-Probe, bei ablaufendem Zertifikat (gibt es). Meldeweg: derselbe wie der Wächter (unabhängig vom eigenen Mailserver). Plus der Runbook-Schritt aus 5.6 Nr. 3 als Skript: `vorfall-snapshot.sh` erzeugt Hetzner-Snapshot, sichert Docker-Logs, rotiert alle API-Schlüssel – damit Eindämmung um 3 Uhr nachts nicht aus dem Kopf passieren muss.

Nicht in den Top 10, aber kurz: CSP- und Security-Header im Portal (1 h, `next.config` headers); Widget-Skript mit `Subresource Integrity`-Hinweis für Kunden, die es wollen; Secrets aus `docker/.env` in eine Datei mit `chmod 600` und nicht im Repo (prüfen); OpenAI-`store: false` (Abschnitt 2); Prompt-Injection-Schutz für Dokumente, die der Bot liest (markdown-safety existiert für Ausgabe, V-L63 – für die Eingabe aus Webseiten-Crawls gibt es in V keinen Hinweis).

---

*Stand 05.10.2026. Alle Zeilenangaben beziehen sich auf die Textfassung des Dienstleisterverzeichnisses vom 17.09.2026. Was dort nicht steht, ist hier als „nicht dokumentiert" markiert und muss am laufenden System nachgemessen werden, bevor es im Freigabeprotokoll 5.9 ein ✅ bekommt.*
