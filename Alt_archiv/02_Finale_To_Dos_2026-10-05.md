# Finale To-dos – Lymbe AI Datenschutz

**Flubber Pixels UG · Stand 05.10.2026 (abends, nach Prüfung der Liste) · Livegang 08.10.2026 · Ein Dokument für Status, Aufgaben (Dennis, Christian, Kundin, Anwalt), Zugangsliste und Sicherheits-Checkliste · Erledigtes wird abgehakt, nicht gelöscht · Verweise auf „04" in Prüfberichten meinen diese Datei**

## 1. Stand

Alle 26 Dokumente sind final formuliert, zweimal unabhängig geprüft (06_Pruefungen) und untereinander konsistent; keine Platzhalter außer Kundenfeldern in Mustern und Unterschriftszeilen. Der Anwalt kommt später, wenn Budget da ist; bis dahin gelten die Verträge wie sie sind, die Fragen J1–J43 bleiben gesammelt.

Livegang Mittwoch mit: Website-Bot, WhatsApp (Kundin verbindet ihr Meta-Konto), Digitaler Mitarbeiter, Frag Lymbe mit Websuche. Anrede Sie. Abläufe/Werkstatt für die Pilotkundin erst, wenn die Werkstatt auf Azure läuft (A1).

Der AVV geht an die Kundin, sobald Christian die Zeilen mit Frist Mittwoch im Freigabeprotokoll 5.9 mit Datum und Beleg bestätigt hat; Zeilen mit Frist Sonntag oder später trägt er dort mit ⏳ und Datum ein – das genügt für die Freigabe am Mittwoch. Die drei harten Punkte: Suchbegriff-Generator mit Testprotokoll 30/30 (A22, nach Prüfung A32), Sicherungen weg von der einen Maschine (A28), Netzgrenze der internen Dienste nachgemessen (A29). Alles andere im Mittwoch-Block ist Konfiguration, Antworten oder Papier.

| Ordner | Inhalt |
|---|---|
| 00_Steuerung | Projektplan, Inhaltsverzeichnis, diese To-do-Liste |
| 01_Kunden | 1.0 AGB 1.3 · 1.1 AVV 1.6 mit § 12, Unterschriftsseite, Anlagen 1–5 · 1.3 Textbaustein Datenschutzerklärung · 1.4 Änderungsmitteilung · 1.5 Widget-/Kanal-Texte · 1.6 Beschäftigteninformation · 1.7 Plattformbeschreibung + Kurz-DSFA |
| 02_26lab | 2.1 Partnerschaftsvertrag Flubber Pixels UG ↔ 26lab.io |
| 03_Dienstleister | 3.1 Checkliste; Unterordner Hetzner, STACKIT, Microsoft_Azure, OpenAI für die PDFs |
| 04_Oeffentlich | 4.1 Datenschutzerklärung 1.5 |
| 05_Intern | 5.1 Verarbeitungsverzeichnis · 5.2 DSFA-Vorprüfung · 5.3 Vertraulichkeit · 5.6 Vorfall · 5.7 Betroffene · 5.8 TDDDG · 5.9 Freigabeprotokoll · 5.10 Rollen · 5.11 DSB · 5.12–5.17 Register und Testprotokoll |
| 06_Pruefungen | 07 Gesamtprüfung 2 + 07a Recht + 07b Technik (Beilage für den Anwalt); ältere 02/02a/05 |

---

## 2. Dennis

| Nr | Aufgabe / Entscheidung | Dokument | Frist | Status |
|---|---|---|---|---|
| D1 | Bestandsmandanten: alle 4 sind Testmandanten ohne Kundendaten, werden nach dem Livegang gelöscht | 00 O2 | – | ✅ 05.10.2026 |
| D2 | DSB: kein DSB, Zwei-Personen-Betrieb; jährliche Neuprüfung, Auslöser in 5.11 Abschnitt 2 | 5.11 | – | ✅ 05.10.2026 |
| D3 | Partnerschaftsvertrag – Zahlen bestätigen oder ändern: Rücklage 3 Monatskosten; Nachschuss höchstens 500 € je Partner und Monat; Tätigkeitsvergütung erst ab 4.000 € Gewinn in 3 Folgemonaten | 2.1 §§ 3–5 | – | ✅ 05.10.2026 bestätigt |
| D4 | Partnerschaftsvertrag – Abfindung bei Tod/dauerhaftem Ausfall (26lab → Flubber, Flubber → 26lab): Gewinnanteil der letzten 12 Monate, mindestens 5.000 €, höchstens 50.000 €, 12 Raten, plus Hälfte des Erlösanteils bei Verkauf binnen 24 Monaten | 2.1 § 8 | – | ✅ 05.10.2026 bestätigt |
| D5 | Pilotkundin bucht ihren Tarif selbst im Portal über Stripe – wie jeder Kunde, nichts zu tun | – | – | ✅ 05.10.2026 |
| D6 | Anrede im Chat der Pilotkundin: Sie (Fassung A aus 1.5) | 1.5 | – | ✅ 05.10.2026 |
| D7 | Partnerschaftsvertrag – Gründung der eigenen Gesellschaft: Auslöser 3.000 € Netto-Erlös in 3 Folgemonaten, spätestens 31.12.2027 – bestätigt 05.10.2026. Offen: Vertrauensperson für Anlage 2 eintragen, vollständiger Name laut Ausweis prüfen | 2.1 § 10, Anlage 2 | Di 07.10. | ☐ (nur Anlage 2) |
| D8 | Anwalt beauftragen – verschoben, bis Budget da ist; bis dahin gelten die Verträge so, wie sie sind; Fragen J1–J43 bleiben gesammelt | – | später | ☐ |
| D9 | STACKIT: beide Konten (chris@26lab.io, info@flubber-pixels.de) als Owner in Organisation LYMBE AI hinterlegt | 3.1 Nr. 3 | – | ✅ 05.10.2026 |
| D10 | Vier PDFs in die Unterordner von 03_Dienstleister legen: OpenAI-DPA (gegengezeichnet, Mail von DocuSign) → OpenAI; STACKIT-AVV + TOMs (Links in 3.1) → STACKIT; Microsoft-DPA (aka.ms/dpa, Deutsch) → Microsoft_Azure; Stripe-DPA (stripe.com/legal/dpa) → Ordner Stripe anlegen | 3.1 | So 12.10. | ☐ |
| D11 | AVV-Unterschriftsseite gegenzeichnen (Kundin füllt aus, K6) und Original ablegen | 1.1 | Mi 08.10. | ☐ |
| D12 | Prüfberichte vom 05.10. (06_Pruefungen/07, 07a, 07b) mit dem Partnerschaftsvertrag an den Anwalt geben | 06 | mit D8, später | ☐ |
| D13 | Christian (chris@26lab.io) als zweiten Administrator eintragen: OpenAI (platform.openai.com → Organisation → Mitglieder, Rolle Owner), Azure (Abonnement → Zugriffssteuerung, Rolle Besitzer) – Azure vor A26, damit Christian die Region prüfen kann; Einladungen von Christian für Hetzner und GitHub annehmen; 2FA überall | 2.1 § 7 Abs. 2, Abschnitt 6 dieser Datei | Mi 08.10. | ☐ |
| D15 | Unterschreiben bis Mittwoch: 5.3 (dein Exemplar), AVV Anlage 5 (Belehrung durch Marion) und Partnerschaftsvertrag 2.1 – Marion für Flubber, Christian für 26lab, du die Vollmachtszeile; vorher D3, D4, D7 entschieden und Vertrauensperson in Anlage 2 eingetragen; Anwalt prüft später nach (J29–J32) | 5.3, 1.1 Anlage 5, 2.1 | Mi 08.10. | ☐ |
| D16 | Antwort von Christian zur Websuche (A32) an Cowork melden. Bei „nur Suchbegriff" ändert sich nichts; bei „ganze Frage" baut Christian vor dem Livegang um (A32) – kein Vertragstext wird angepasst | 1.1 § 3 Abs. 10 | Mi 08.10. | ☐ |
| D17 | Christian im Stripe-Konto als Teammitglied mit Administrator-Rolle eintragen (Dashboard → Einstellungen → Team), 2FA | 2.1 § 7 Abs. 2, Abschnitt 6 dieser Datei | Mi 08.10. | ☐ |
| D18 | Übergabepaket an die Kundin: AVV 1.6 als Ausdruck mit Unterschriftsseite, Textbaustein 1.3 (Varianten D und B), 1.6, 1.7; Termin für die 15-Minuten-Einweisung; prüfen, dass ihre Datenschutzerklärung (K2) vor dem ersten Widget-Aufruf ergänzt ist | 1.1, 1.3, 1.6, 1.7 | Mo 06.10. | ☐ |
| D19 | Workspace der Pilotkundin einrichten (mit Christian): Systemprompt-Regeln nach AVV § 12 Abs. 5 (KI zu erkennen geben, keine Diagnosen, keine Behandlungsempfehlungen, keine Notfälle, Gesundheitsdetails nicht abfragen, Minderjährige an Sorgeberechtigte verweisen), Benachrichtigungsziel dienstlich/EU, Selbstlernen aus, Admin-Einsicht aus (A40), Datenschutz-Link, Anrede Sie; Widget-Skript auf ihrer Website einbauen | 1.1 § 12 Abs. 5, 1.5 | Mi 08.10., vor Freischaltung | ☐ |
| D20 | STACKIT: Kontakt-E-Mail im Kundenkonto von chris@26lab.io auf info@flubber-pixels.de ändern | 3.1 Nr. 3 | So 12.10. | ☐ |

**Von Cowork entschieden, bitte absegnen:** AGB als vollständige Fassung 1.3 aus 1.2 fortgeschrieben · Haftung intern 50/50 als Kosten von Lymbe, allein nur bei Vorsatz/grober Fahrlässigkeit · Lymbe als Innengesellschaft 50/50 zwischen Flubber Pixels UG und 26lab.io, Dennis als Bevollmächtigter von Flubber · Selbstlernen Standard aus · § 7 Regelfrist 24 h · Gerichtsstand Düsseldorf (wie AGB) · 1.7 in AVV § 12 aufgegangen, keine Branchenabfrage · Websuche als Teil von Frag Lymbe mit Suchbegriff-Generator, kein Schalter · Fristen 30/14/30 Tage als Vorschlag · Demo-Chats 24 h

---

## 3. Christian (26lab.io)

Hauptdokument: `05_Intern/5.9_Freigabeprotokoll_Vertrag_gleich_Maschine.md` – dort jede Zeile bestätigen; Zeilen mit späterer Frist mit ⏳ und Datum. Ohne den Mittwoch-Block kein Livegang, auch nicht als Beta.

### Bis Mittwoch 08.10. – Voraussetzung für den Start

| Nr | Aufgabe | Quelle | Status |
|---|---|---|---|
| A32 | **Zuerst:** `web-suche.ts` prüfen – wird der Suchbegriff zweistufig gebildet (STACKIT formuliert, nur der Begriff geht an OpenAI) oder geht die Nutzerfrage selbst an OpenAI? Wenn Letzteres: vor A22 umbauen. Ergebnis an Dennis | 5.9 B1, AVV § 3 Abs. 10 | ☐ |
| A22 | **Suchbegriff-Generator live:** feste Anweisung (STACKIT formuliert, nur der Begriff geht an OpenAI, `store: false`), Regex-Filter, Mandanten-Sperrliste aus Kontakten/Teamnamen, Blockiermeldung aus 1.5 G, Nachweis-Log 14 Tage; Testprotokoll 5.16 mit 30/30 ausgefüllt und unterschrieben – **ohne 30/30 kein Livegang mit Websuche**. Abbestellen je Workspace als Konfiguration vorsehen | 5.9 A10/B1, 5.16, 07b Abschnitt 2 | ☐ |
| A28 | Datensicherungen: 7 Tage (statt heute 30), verschlüsselt an einen zweiten Ort (Hetzner Storage Box oder Object Storage, anderer Standort, nur anfügbar); Hetzner-Backups einschalten (7 Rotationen), alte Snapshots löschen; wöchentliche Wiederherstellungsprobe mit Zeilenzählung | 5.9 A2/A2b/A14b, AVV § 8, Anlage 1 | ☐ |
| A29 | Netzgrenze nachmessen: `docker ps` – keine veröffentlichten Ports außer Caddy 80/443 und Postfix; Hetzner Cloud Firewall; von außen prüfen; Inngest-Oberfläche und MinIO-Konsole hinter Anmeldung | 07b Abschnitt 9 Nr. 1 | ☐ |
| A7 | Mistral-Rückfall deaktivieren (Schlüssel entfernen, Verhalten bei fehlendem Schlüssel prüfen) | 5.9 A11 | ☐ |
| A9 | Messenger/Instagram über die Meta-App für die Pilotkundin aus; WhatsApp-Erstantwort aus 1.5 J einbauen – einmal je Nummer, erneut nach 90 Tagen ohne Kontakt; für § 12-Kunden mit dem Zusatzsatz aus 1.5 J | 5.9 A13, 1.5 J | ☐ |
| A14 | Widget-Texte aus 1.5, Mittwoch-Teil: A Startdialog (Kundenname, Datenschutz-Link, Checkbox „Ich habe die rechtlichen Hinweise gelesen", Bestätigung mit Fassung und Zeitpunkt im Browser), B Rechtliches 1:1, D Lead-Satz mit Minderjährigen-Regel, E Übergabe-Meldungen, G Websuche-Hinweis einmal je Nutzer + Blockiermeldung + Chat-Badge, J WhatsApp-Erstantwort, K Sprach-Hinweis falls A33 = ja, KI-Badge; Anrede-Einstellung je Assistent (A = Sie, P = Du), Pilotkundin Sie | 1.5 | ☐ |
| A12 | Dennis (info@flubber-pixels.de) bei Hetzner und in der GitHub-Organisation (lymbe-ai, lymbe-ablaeufe) als Owner eintragen; 2FA bei Hetzner und GitHub; SSH nur mit Schlüssel, Passwort-Login aus | 5.9 A14/A23, 2.1 § 7 Abs. 2 | ☐ |
| A19 | Unterschreiben: 5.3 (dein Exemplar), AVV Anlage 5 (Belehrung durch Marion) und Partnerschaftsvertrag 2.1; Vertrauensperson für Anlage 2 nennen | 5.9 E, 2.1 | ☐ |
| A8 | Antwort: Azure Speech live oder nicht? Audio-Logging aus? Region? | 5.9 A12 | ☐ |
| A10 | Antwort: Nachrichten-Einordnung ohne Emotionserkennung (kein Feld für Stimmung/Emotion im Ausgabeschema)? | 5.9 B4 | ☐ |
| A33 | Antwort: Gibt es ein Mikrofon im Website-Chat? Wenn ja, ergänzt Cowork Microsoft in 1.5 B und 1.3 D; wenn nein, streicht Cowork die Sprach-Zeile aus 1.5 B | 1.5, 5.9 A12 | ☐ |
| A40 | Antwort: Gibt es die Einstellung „Admin-Einsicht in Frag-Lymbe-Verläufe aus", was ist Standard? Für die Pilotkundin aus. Und: sehen alle Workspace-Mitglieder alle Dokumente? | 5.9 B6/B8, 1.7 Abschnitt 5, AVV § 12 Abs. 5 | ☐ |
| A11 | Antwort: Gibt es ein technisches Support-Zugriffsprotokoll (Zeit, Person, Grund, Umfang, Mandant)? Bis dahin führt Dennis das Zugriffsregister 5.15; jeder Zugriff vorher mit Zeile und Freigabe des anderen | 5.9 A9/B5, 5.15 | ☐ |
| A21 | Mobilnummer von Dennis in den Passwort-Tresor / Kontaktliste (5.6 Abschnitt 7) | 5.6 | ☐ |

### Bis Sonntag 12.10.

| Nr | Aufgabe | Quelle | Status |
|---|---|---|---|
| A1 | Werkstatt auf Azure OpenAI umstellen (`AI_PROVIDER_WERKSTATT=azure`); bis dahin keine Abläufe für die Pilotkundin | 5.9 A1 | ☐ |
| A26 | Azure OpenAI: Regionsname des Modells prüfen (nach D13) und als Screenshot in 03_Dienstleister/Microsoft_Azure ablegen – muss EU sein (Germany West Central, Sweden Central, West Europe, France Central, North Europe); sonst umstellen | 3.1 Nr. 4, 5.9 A1 | ☐ |
| A3 | 90-Tage-Löschung der Gespräche (Kundenservice, Live-Chat, Digitaler Mitarbeiter, Frag Lymbe): Job bauen oder belegen (Name, letzter Lauf, Protokollzeile je Lauf); Demo-Gespräche 24 h | 5.9 A3, C1 | ☐ |
| A4 | Fristen umsetzen und bestätigen: Zugriffsprotokolle 14 Tage, Fehlerprotokoll 30 Tage, Messenger-Ereignisdaten 30 Tage, Server-Abbilder 7 Tage; Redis-Antwort-Cache mit Ablauf | 5.9 A2b/A5/A6, AVV § 8, 4.1 | ☐ |
| A6 | Kein-Training-Belege: STACKIT-Bedingungen, Microsoft-Produktbedingungen (inkl. Abuse-Monitoring-Status Azure OpenAI) – Fundstellen in 3.1 D eintragen | 5.9 B2/B3, 3.1 D | ☐ |
| A13 | Hetzner-AVV (Kundenkonto → Vereinbarung zur Auftragsverarbeitung) und ISO-27001-Zertifikat in 03_Dienstleister/Hetzner ablegen | 3.1 Nr. 2 | ☐ |
| A14b | Widget-Texte aus 1.5, Rest: H Selbstlernen-Dialog, I Dienst-verbinden-Dialog aus Baustein-Metadaten, L Demo-Text, M Portal-Hinweis einmal pro Nutzer, N Mail-Fußzeile, O AVV-Seite mit Checkbox-Text | 1.5 | ☐ |
| A15 | Workspace-Formular: Firma, Anschrift, vertretungsberechtigte Person, Telefon abfragen; Checkbox-Text aus 1.5 O; Fassungskonstante 1.6; Protokoll Fassung/Zeit/Name/E-Mail/IP | 5.9 A20/B7 | ☐ |
| A16 | Demo-Widget: 24-h-Löschung, kein Gedächtnis, keine Leads | 5.9 C1 | ☐ |
| A17 | Browserspeicher-Liste des Widgets vollständig nennen, inkl. Sitzungskennung: wo gespeichert, gibt es den 12-Stunden-Ablauf? Wenn nicht: einbauen oder Cowork passt 1.3/1.5/4.1/5.8 an | 5.9 C3, 5.8 W3 | ☐ |
| A18 | Wächter-Meldeweg benennen (welcher Dienst); monatlichen Leer-Commit einrichten, weil GitHub geplante Workflows nach 60 Tagen ohne Commit abschaltet | 5.9 C4, 4.1 Abschn. 2.6 | ☐ |
| A20 | Die 4 Testmandanten vollständig löschen (Datenbank, Suchindex, Dateiablage, Ereignisspeicher, Cache) mit Skript „Mandant löschen" und Löschung in 5.9 A20b bestätigen; vorher klären, welche der fünf Mandanten-Datenbanken bleibt (Demo? Lymbe selbst?) | 00 O2, 5.9 A19/A20b | ☐ |
| A24 | Werkstatt: bis A1 erledigt ist, läuft sie laut Verzeichnis über OpenAI – für die Pilotkundin bleiben Abläufe bis dahin aus | 5.9 A1 | ☐ |
| A30 | Mandantentrennung nachmessen: Qdrant (Collection je Mandant oder Filter?), MinIO-Pfade, Redis-Schlüssel mit Mandanten-Präfix; Test „Mandant B sieht nichts von A"; Befunde beheben | 5.9 A16, 07b Abschnitt 3 | ☐ |
| A31 | Keine Inhalte in Protokollen: App-Logs und Fehlerprotokoll (Stapel) auf Gesprächs-/Dokumentinhalte prüfen, Fehlermeldungen kürzen, Docker-Log-Rotation 14 Tage | 5.9 A6b, AVV § 8 | ☐ |
| A37 | Verschlüsselung ruhender Daten: belegen (LUKS/Hetzner-Nachweis) oder sagen – dann passt Cowork Anlage 1 auf das Belegbare an („Übertragung TLS; Zugangsdaten, Sicherungen und Passwörter verschlüsselt; Rechenzentrum ISO 27001") | 5.9 A14b, AVV Anlage 1 | ☐ |
| A39 | Zugangsliste (Abschnitt 6) vervollständigen: Kontoinhaber und Rollen für Domain/DNS, Meta Business, Mailserver, Portal-Admin melden; alle Zugänge im Tresor mit Präfix „Lymbe – " | 2.1 § 7 Abs. 2, Anlage 1 | ☐ |

### Nach dem Livegang

| Nr | Aufgabe | Quelle | Status |
|---|---|---|---|
| A38 | Drei Downloads im Portal unter „Datenschutz" für jeden Kunden: 1.3 Textbaustein Datenschutzerklärung, 1.6 Information der Beschäftigten, 1.7 Plattformbeschreibung und Kurz-DSFA (Art. 28 Abs. 3 lit. f); dazu ein Satz in der Willkommens-Mail | 1.3, 1.6, 1.7 | ☐ |
| A41 | Technisches Support-Zugriffsprotokoll und Audit-Tabelle (Checkliste Nr. 5), Export im Portal, Portal-TOTP, Dienst-Hinweis für alle Bausteine | 07b Abschnitt 5, 8 | ☐ |

**Später (P2):** Lead-Benachrichtigung nur an dienstliche Postfächer prüfbar machen · sessionStorage-Marker erst nach Nutzerhandlung setzen (5.8 W2) · Hilfeseiten-Logo serverseitig spiegeln · Dienstleisterverzeichnis korrigieren (Azure Speech, Wächter, Stripe-Cookies, Kontoinhaber) · Export-Funktion für Art.-30-Angaben je Kunde · Rollen-/Rechtekonzept Portal · Löschung einer Person über alle Speicher als Ablauf · Zertifikate der Cloud-Anbieter ablegen

Entfallen: A2, A23 (in A28/A4), A5 (in A22), A25 (in A14), A27 (jetzt D20), A34 (in A17), A35 (in A18), A36 (in A20).

---

## 4. Pilotkundin (Übergabe durch Dennis, D18)

| Nr | Was | Dokument |
|---|---|---|
| K1 | AGB 1.3 und AVV 1.6 im Portal bestätigen | 1.0, 1.1 |
| K2 | Textbaustein Varianten D und B in ihre Datenschutzerklärung – vor dem ersten Widget-Aufruf; Klammern ersetzen (Kontaktadresse, Benachrichtigungsziel, Kalenderanbieter, Frist), nicht genutzte Abschnitte weglassen; ihrem Datenschutzbeauftragten oder Anwalt zeigen; Link zur Datenschutzerklärung an Dennis für das Portal | 1.3 |
| K3 | Information der Beschäftigten aushändigen (Art. 13), bevor das Team eingeladen wird; Variante A/B bei „Wer kann was sehen" passend zur Portal-Einstellung (Admin-Einsicht aus); Websuche-Absatz enthalten; Betriebsrat einbeziehen, falls vorhanden (§ 87 Abs. 1 Nr. 6 BetrVG); 15-Minuten-Einweisung; Datum notieren | 1.6 |
| K4 | Kurz-DSFA ausfüllen und unterschreiben – ihre Pflicht vor Beginn der Verarbeitung (AVV § 12 Abs. 5, Technik-Teil in 1.7 vorausgefüllt); Lymbe macht den Start nicht davon abhängig, Dennis erinnert einmal schriftlich | 1.7 Abschnitt 4/5 |
| K6 | Unterschriftsseite des AVV ausfüllen (Firma, Anschrift, Vertretung, E-Mail, Telefon für Vorfälle) und unterschreiben | 1.1 |
| K7 | Telefonnummer für Vorfälle steht auf der Unterschriftsseite (K6); ins Portal nachtragen, sobald das Feld da ist (A15) | AVV § 12 Abs. 6 |
| K8 | WhatsApp: eigenes WhatsApp-Business-Konto bei Meta verbinden, WhatsApp Business Data Processing Terms von Meta akzeptieren (sie ist Auftraggeberin von Meta, AVV § 5 Abs. 5); Team-Regel: über WhatsApp nur Termine und Organisatorisches, keine Therapie- oder Diagnoseinhalte | 1.1 § 5, 1.3 B |

Entfallen: K5 (in K2 und D19).

---

## 5. Anwalt

| Nr | Frage | Dokument |
|---|---|---|
| J1 | Trägt Art. 9 Abs. 2 lit. h i. V. m. § 22 BDSG auch Erstanfragen Interessierter über den Website-Chat (Anbahnung)? | AVV § 12 Abs. 1 |
| J2 | § 203-Kette bei Cloud-Anbietern (Hetzner, STACKIT, Microsoft): reicht vertragliche Geheimhaltung oder ausdrückliche Verpflichtung nach § 203 Abs. 4 S. 2 Nr. 2? | AVV § 12 Abs. 3, 2.1 § 16 Abs. 2 |
| J3 | DSB-Pflicht für Flubber als Auftragsverarbeiter (§ 38 Abs. 1 S. 2 BDSG) und Schwelle „umfangreich" bei Art. 37 Abs. 1 lit. c | 5.11 |
| J4 | Heilpädagogen als Berufsgeheimnisträger (umstritten) – relevant für die Pilotkundin | AVV § 12 |
| J5 | Rolle von Lymbe bei Frag Lymbe: reine Auftragsverarbeitung oder gemeinsame Verantwortlichkeit (Art. 26)? Ebenso Demo-Widget | 5.10 |
| J6 | Meta-Rollenkette (Lymbe als Business Solution Provider) | AVV § 5 Abs. 5 |
| J7 | Haftung im Innenverhältnis (2.1 § 14) vs. Art. 82 Abs. 4/5; Haftungsgrenze AGB (3 Monatsentgelte) bei Gesundheitsdaten; Versicherung | 2.1, 1.0 |
| J8 | Freistellungsklauseln (AVV § 10 Abs. 3, § 12 Abs. 7; AGB § 8 Abs. 6) gegenüber Kleinunternehmern | AVV, 1.0 |
| J9 | Gerichtsstand Düsseldorf vs. Wuppertal (Sitz Mettmann) | AVV § 11, 2.1, AGB |
| J10 | Art. 50 Abs. 2 KI-VO (maschinenlesbare Kennzeichnung) für Chat-Text | 1.5 |
| J11 | Widerspruchsrecht gegen neue Unterauftragsverarbeiter: Kündigungslösung genügt Art. 28 Abs. 2 S. 2? | AVV § 4 Abs. 2 |
| J12 | OpenAI: DPF-Status prüfen; Transfer-Folgenabschätzung nötig trotz Suchbegriff ohne Personenbezug? | AVV Anlage 2 Nr. 5 |
| J13 | Nutzungsrechte am Code (ausschließlich, zur Hälfte „Lymbe", Urheberpersönlichkeitsrecht) | 2.1 § 2 Abs. 4 |
| J14 | § 53a / § 97 StPO für Lymbe und 26lab als mitwirkende Personen | AVV § 12 Abs. 3 |
| J15 | § 25 TDDDG: sessionStorage-Marker für proaktive Ansprache als „erforderlich"? | 5.8 W2 |
| J16 | Minderjährige und Lead-Erfassung; Art. 8 DSGVO bei lit. h als Grundlage | AVV § 12 Abs. 5 |
| J17 | Form der Belehrung nach § 203 Abs. 4 (Geschäftsführung belehrt Dennis) | AVV Anlage 5 |
| J18 | AGB § 13 „Schweigen gilt als Akzeptanz" im B2B | 1.0 AGB v1.3 |
| J19 | DSFA-Vorprüfung Teil 1 (keine DSFA für Flubbers eigene Verarbeitungen) bestätigen | 5.2 |
| J20 | Team-Verwaltung und Weisungsprotokoll: in 1.1 § 1 Abs. 2 / 4.1 / 5.10 als eigene Verantwortlichkeit von Flubber, in 1.1 Anlage 3 letzte Zeile / 5.1 A7 als Auftragsverarbeitung – eine Rolle wählen | 1.1, 5.1 |
| J21 | ✅ erledigt 05.10.2026 (§ 22 Abs. 2 Satz 2 BDSG – Verweise vereinheitlicht), keine Frage mehr | 1.1 § 12 Abs. 5 |
| J22 | 1.1 § 6 Abs. 7 / AGB § 2 Abs. 2: „gilt mit der ersten Nutzung als genehmigt" bei nicht vertretungsberechtigter Person (§ 177 BGB) | 1.1, 1.0 |
| J23 | Websuche-Zusage „nach fester Anweisung ohne personenbezogene Angaben, regelmäßig getestet": reicht das als Maßnahme, oder TIA? | 1.1 § 3 Abs. 10 |
| J24 | Partnerschaftsvertrag: Lymbe als Innengesellschaft (GbR ohne Außenauftritt) zwischen einer UG und 26lab.io (Rechtsform von 26lab.io klären: Einzelunternehmen = Christian haftet persönlich) – richtige Rechtsform, steuerliche Folgen (Feststellungserklärung, Gewerbesteuer, Bilanzierung bei Flubber) | 2.1 Teil A, Vertragsparteien |
| J25 | Flubber hält Lymbe-Werte für die Partnerschaft: Schutz der 26lab-Hälfte bei Insolvenz oder Gesellschafterwechsel von Flubber; Vollmacht von Dennis als Projektleiter (Umfang, Form); Zustimmung der Gesellschafterin von Flubber zum Vertrag | 2.1 § 3, Vertragsparteien |
| J26 | Übergang bei Tod/dauerhaftem Ausfall: 26lab-Anteil → Flubber, wenn Christian ausfällt (Erben, Pflichtteil, Testament nötig?); Flubber-Anteil → 26lab, wenn Dennis ausfällt, obwohl Flubber fortbesteht – zulässig und steuerlich sauber (verdeckte Gewinnausschüttung?); Definition dauerhafter Ausfall (12 Monate) und Nachweis | 2.1 § 8 |
| J27 | Wettbewerbsverbot 12 Monate nach Ausscheiden ohne Karenzentschädigung – wirksam? Kündigungsfrist 6 Monate, Ausschluss aus wichtigem Grund | 2.1 § 9 |
| J28 | Gründung UG/GmbH aus der Innengesellschaft: Gesellschafter Flubber/26lab oder je eine benannte Person (Dennis, Christian), Einbringung zu Buchwerten, Übertragung der Flubber-Verträge (Kunden-AVV, Anbieter) auf die neue Gesellschaft, Zustimmung der Kunden nötig? | 2.1 § 10 |
| J29 | Gerichtsstandsvereinbarung 2.1 § 21 Abs. 4 nur zwischen Kaufleuten wirksam (§ 38 ZPO) – ist 26lab.io eingetragener Kaufmann? Sonst streichen | 2.1 § 21 |
| J30 | 2.1 § 10 (Gründung UG/GmbH spätestens 31.12.2027, feste Beteiligung, Geschäftsführer): Vorvertrag zur GmbH-Gründung, der nach § 2 GmbHG analog notariell beurkundet werden muss? | 2.1 § 10 |
| J31 | Innengesellschaft trotz Außenauftritt von 26lab (Hetzner-Vertrag, öffentliche Nennung, Administrator in allen Konten): nach MoPeG (§ 705 Abs. 2 BGB) noch Innengesellschaft oder rechtsfähige Außen-GbR mit gesamtschuldnerischer Haftung (§ 721 BGB)? Folge für § 14 Abs. 4 | 2.1 § 1 Abs. 3, § 14 |
| J32 | Rechteinhaberschaft § 2 Abs. 4: Innengesellschaft hat kein Vermögen – Flubber als Treuhänderin oder Bruchteilsgemeinschaft? Dennis als Nicht-Partei: reicht seine Unterschriftszeile für Rechteeinräumung und § 13? Falls Arbeitnehmer von Flubber: § 43 UrhG | 2.1 § 2 Abs. 4, § 13 |
| J33 | AGB § 3 Abs. 4 / § 12 Abs. 5: Haftungsausschluss für Drittanbieter als Erfüllungsgehilfen (§ 278, § 307, § 309 Nr. 7 BGB) – reicht der ergänzte Vorbehalt? | 1.0 |
| J34 | Art. 50 Abs. 1 KI-VO als Anbieterpflicht: genügt die Formulierung „kennzeichnet in allen von ihm betriebenen Kanälen" plus Hinweistexte für kundeneigene Ausgaben? | 1.0 § 9 Abs. 3, 1.1 § 6 Abs. 2 |
| J35 | AGB-Vertrag bei Registrierung, AVV erst beim Anlegen des Workspace – Lücke beim Benutzerkonto unproblematisch? Testphase mit Echtbetrieb von Gesundheitsdaten ohne Entgelt: Auftragsverarbeitung ohne Vergütung, Haftungsgrenze „3 Monatsentgelte" = 0 €? | 1.0 § 2, § 4, § 12 |
| J36 | Rolle von Stripe: Auftragsverarbeiter für Rechnungs-/Abodaten, eigener Verantwortlicher für die Zahlungsabwicklung – Formulierung in 4.1 Abschnitt 4 und 5.1 V3 bestätigen | 4.1, 5.1 |
| J37 | Rechtsgrundlage der Nachweisprotokolle (3 Jahre): Art. 6 Abs. 1 lit. f (so jetzt in 4.1/5.1) oder lit. c i. V. m. Art. 28 Abs. 9? | 4.1 Abschn. 2.2, 3 |
| J38 | Freiwillig eingegebene Gesundheitsdaten bei Kunden ohne § 12: genügt Eingabe nach Hinweis als ausdrückliche Einwilligung (Art. 9 Abs. 2 lit. a) oder braucht das Widget eine Einwilligungshandlung? | 1.5 B, 1.1 § 3 |
| J39 | § 53a StPO: Formulierung in AVV § 12 Abs. 3 und Anlage 5 („abgeleitetes Zeugnisverweigerungsrecht, Entscheidung beim Berufsgeheimnisträger") und Prozess bei Behördenanfragen | 1.1 § 12 Abs. 3, Anlage 5 |
| J40 | Widerspruch gegen neue Unterauftragsverarbeiter bei § 203-Daten: darf die Kündigungslösung (§ 4 Abs. 2) greifen, wenn der neue Anbieter Zugriff auf Berufsgeheimnisse hätte? Reicht der Zusatz „§ 12 Abs. 3 bleibt unberührt"? | 1.1 § 4 Abs. 2 |
| J41 | Hetzner-Kette: Flubber hat keinen eigenen Vertrag mit Hetzner (Konto 26lab). Genügt 2.1 § 17 Abs. 1 („Flubber genehmigt Hetzner") für Art. 28 Abs. 4 gegenüber den Kunden, bei denen Hetzner als Unterauftragsverarbeiter von Lymbe gelistet ist? | 2.1 § 17, 1.1 Anlage 2 |
| J42 | Websuche-Zusage in AVV § 3 Abs. 10 ist als Maßnahme mit Restrisiko formuliert (Technik: nicht garantierbar, realistisch unter 1 % Fehlerrate mit Sperrliste und Zweitprüfung). Reicht das, oder TIA / zusätzliche Einwilligung je Nutzer? (ergänzt J23) | 1.1 § 3 Abs. 10, 5.16 |
| J43 | Partnerschaftsvertrag wurde am 08.10.2026 ohne anwaltliche Vorprüfung unterschrieben – nachträglich prüfen, ob Änderungen nötig sind (J29–J32); Änderungen dann als Nachtrag in Textform (§ 21 Abs. 2) | 2.1 |


---

## 6. Zugänge – wo beide drin sein müssen

Grundlage: Partnerschaftsvertrag § 7 Abs. 2 (Vertretung bei Krankheit) und Anlage 1. Ziel: Bei jedem Dienst sind Dennis und Christian als Administrator eingetragen, beide mit zweitem Faktor; alle Zugänge liegen im gemeinsamen Passwort-Tresor mit Präfix „Lymbe – ".

| Dienst | Kontoinhaber | Dennis | Christian | Wer trägt ein | Status |
|---|---|---|---|---|---|
| STACKIT (Organisation LYMBE AI) | Flubber Pixels UG | Owner | Owner | – | ✅ 05.10.2026 |
| Hetzner Cloud | 26lab.io | fehlt | Owner | Christian (A12) | ☐ |
| GitHub-Organisation (lymbe-ai, lymbe-ablaeufe) | 26lab.io | prüfen | Owner | Christian (A12) | ☐ |
| OpenAI (platform.openai.com) | Flubber Pixels UG | Owner | fehlt | Dennis (D13) | ☐ |
| Microsoft Azure | Flubber Pixels UG | Owner | fehlt | Dennis (D13) | ☐ |
| Stripe | Flubber Pixels UG | Owner | fehlt | Dennis (D17) | ☐ |
| Domain lymbe.ai und DNS | prüfen | prüfen | prüfen | Christian meldet Stand (A39) | ☐ |
| Meta Business (WhatsApp-App von Lymbe) | prüfen | prüfen | prüfen | Christian meldet Stand (A39) | ☐ |
| Mailserver / Admin-Postfach | 26lab.io (Server) | prüfen | Admin | Christian meldet Stand (A39) | ☐ |
| Portal-Admin (lymbe-prod) | Flubber Pixels UG | Admin | Admin | Christian bestätigt (A39) | ☐ |
| Passwort-Tresor (Bitwarden) | gemeinsam | Zugang | Zugang | beide; Mobilnummer von Dennis dort (A21) | ☐ |

---

## 7. Sicherheits-Checkliste – die 10 wichtigsten Punkte (Christian)

Maßstab: Multi-Mandanten-Portal mit Gesundheitsdaten, ein Entwickler, Start-up-Budget. Reihenfolge nach Risiko geteilt durch Aufwand. Ausführlich mit Belegen in 06_Pruefungen/07b Abschnitt 9. Abgehakt wird nur in Abschnitt 3 – die Spalte „Aufgabe" zeigt, wo.

| Nr | Maßnahme | Warum zuerst | Aufwand | Aufgabe |
|---|---|---|---|---|
| 1 | **Interne Dienste vom Internet trennen.** Keine veröffentlichten Docker-Ports außer Caddy (80/443) und Mailserver; Hetzner Cloud Firewall mit genau diesen Ports; Inngest-Oberfläche und MinIO-Konsole hinter Anmeldung; von außen nachmessen. | Das Verzeichnis sagt selbst: Qdrant, MinIO und Inngest „verlassen sich darauf, dass ihr Port nicht nach außen zeigt". Docker-Ports umgehen die Server-Firewall. Ein offener Port = alle Mandantendaten im Klartext. | 2 h | A29 |
| 2 | **Mandant nur aus der Anmeldung, nie aus der Anfrage.** Jeder Datenbank-, Suchindex-, Datei- und Cache-Zugriff holt die Mandanten-ID aus der Sitzung; ein zentraler Wrapper erzeugt Verbindung, Filter und Pfad-Präfix; ein Test „Mandant B sieht nichts von A" läuft bei jedem Release. | Die Datenbank-Trennung ist echt. Suchindex, Dateiablage und Cache hängen an Filtern im Code – ein vergessener Filter liefert fremde Patientendokumente. | 1–2 Tage, schrittweise | A30 |
| 3 | **Sicherungen außer Haus, verschlüsselt, vom Server aus nicht löschbar.** Nächtliche Dumps plus Dateiablage plus Suchindex mit eigenem Schlüssel auf eine Hetzner Storage Box oder Object Storage an einem anderen Standort, nur anfügbar; 7 Tage; wöchentliche Wiederherstellungsprobe mit Zeilenzählung und Alarm. | Heute liegt alles auf einer Maschine. Erpressungssoftware oder ein falscher Befehl löschen Daten und Sicherungen zusammen. | 3 h | A28 |
| 4 | **Zweiter Faktor überall, SSH nur mit Schlüssel.** Hetzner, GitHub, STACKIT, Azure, OpenAI, Stripe, Meta mit Authenticator-App; Passwort-Anmeldung per SSH aus; SSH nur von bekannten Adressen oder über ein privates Netz (Tailscale); Portal-Admins nur über 2FA-gesicherten Google/GitHub-Login, bis das Portal eigenes TOTP hat. | Ein gestohlenes Passwort ist heute Vollzugriff auf Server, Code und alle Anbieterkonten. | 2 h | A12, D13, D17 |
| 5 | **Ein Protokoll für alles, was ein Mensch mit Rechten tut.** Eine Tabelle, in die nur geschrieben wird: Einstellungen je Workspace, Support-Zugriffe, Mitgliederänderungen, Löschläufe, Exporte – mit Zeit, Person, Mandant, Grund. | Drei Vertragszusagen hängen daran, und es ist die einzige Möglichkeit, nach einem Vorfall zu wissen, wer was wann gesehen hat. Bis dahin: Zugriffsregister 5.15 auf Papier. | 1 Tag | A11, A41 |
| 6 | **Löschen als Beweis.** Automatische Läufe für 90 Tage (Gespräche), 24 h (Demo), 30 Tage (Laufdaten, Fehlerprotokoll), 14 Tage (Zugriffsprotokolle), jeder Lauf schreibt eine Zeile ins Protokoll; ein Skript „Mandant löschen" räumt Datenbank, Suchindex, Dateiablage, Ereignisspeicher und Cache ab und gibt Zähler aus; beim Löschen im Portal sofort auch Suchindex und Ereignisse. | Bei Gesundheitsdaten von Kindern ist „wir glauben, es ist weg" keine Antwort auf eine Löschanfrage oder eine Behördenfrage. | 1 Tag | A3, A4, A20 |
| 7 | **Keine Inhalte in Protokollen und Fehlermeldungen.** Logger mit Schwärzung für Nachrichten, Dokumente, E-Mails, Telefonnummern; Fehlermeldungen vor dem Speichern kürzen; Datenbankfehler ohne Parameter; Docker-Logs nach 14 Tagen weg. | Fehlerprotokolle sind der häufigste Ort, an dem Gesundheitsdaten unbemerkt mandantenübergreifend und ohne Frist landen. | 0,5 Tag | A31 |
| 8 | **Verschlüsselung ehrlich machen.** Entweder Datenträgerverschlüsselung belegen oder den Satz in AVV Anlage 1 auf das Belegbare ändern: Übertragung TLS; Zugangsdaten, Sicherungen und Passwörter verschlüsselt; Rechenzentrum ISO 27001. | Ein Versprechen, das die Maschine nicht hält, ist bei einer Prüfung schlimmer als ein ehrlich kleineres Versprechen. Pflicht bleibt: Sicherungen und Zugangsdaten verschlüsselt. | 10 min Text oder 0,5 Tag Technik | A37 |
| 9 | **Aktuell halten, Lieferkette klein.** Automatische Sicherheitsupdates auf dem Server; wöchentlicher Sammel-PR für Abhängigkeiten; Container-Images monatlich neu bauen; Prüfung im Build blockiert bei schweren Lücken; Bausteine des Ablauf-Kerns, die kein Kunde nutzt, aus dem Katalog nehmen und den Katalog-Sync im Build gegen versehentliches Einschalten absichern. | Der Ablauf-Kern mit über 700 Bausteinen ist die größte Angriffsfläche im System. | 2 h Einrichtung, dann laufend | nach Livegang |
| 10 | **Sicherheitsereignisse sehen, nicht nur Ausfälle.** Alarm bei gehäuften Anmeldefehlern, Rate-Limit-Sperren über Schwelle, jedem Support-Zugriff, jedem neuen Admin-Konto, jedem Lauf des Löschskripts, fehlgeschlagener Wiederherstellungsprobe; Meldeweg unabhängig vom eigenen Mailserver. Dazu ein Skript für den Vorfall: Server-Abbild ziehen, Logs sichern, alle API-Schlüssel tauschen. | Der Wächter sieht heute nur „Portal antwortet". Eindämmung um 3 Uhr nachts darf nicht aus dem Kopf passieren (Vorfall-Prozess 5.6). | 0,5 Tag | A18, nach Livegang |

Reihenfolge für die ersten zwei Wochen: 1, 3, 4 (ein Tag), dann 7 und 10 (ein Tag), dann 2, 5, 6 (vier Tage), 8 und 9 nebenher.
