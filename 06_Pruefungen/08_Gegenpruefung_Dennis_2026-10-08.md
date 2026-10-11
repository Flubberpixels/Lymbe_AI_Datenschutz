# Gegenprüfung für Dennis – Stand 08.10.2026

**Zweck:** Christian hat am 06.–08.10.2026 mit Claude Code Punkte aus „Finale To-dos“ (Notion, Abschnitt 3) erledigt und in diesem Ordner eingetragen. Wo dabei Vertragstexte gelesen oder Systemwerte gemessen wurden, steht als Prüfer „Claude Code für Chris (Dennis prüft)“. Diese Datei sammelt alles, was eine zweite Person (Vier-Augen) gegenlesen soll, und die offenen Rechtsfragen.

---

## Auftrag an Claude (zum Kopieren)

> Lies in diesem Ordner zuerst `06_Pruefungen/08_Gegenpruefung_Dennis_2026-10-08.md`. Prüfe jeden Punkt in Teil A gegen die genannten Dateien: Steht die zitierte Stelle wirklich so im Dokument (Abschnitt/Seite)? Ist die Schlussfolgerung („kein Training“, „Standort“, „Art. 28 vollständig“) davon gedeckt? Melde je Punkt: bestätigt / abweichend (mit Zitat) / nicht prüfbar. Teil B sind Messungen am laufenden System – die kannst du nur auf Plausibilität und Widersprüche zwischen den Dokumenten prüfen, nicht nachmessen. Zu Teil C gib eine kurze rechtliche Einschätzung mit Empfehlung und kennzeichne, was ein Anwalt klären sollte. Ändere keine Dateien, schreib das Ergebnis als neue Datei `06_Pruefungen/08a_Ergebnis_Gegenpruefung.md`.

---

## A – Abgleich mit Vertragstexten (gegenlesen)

| Nr | Aussage | Wo eingetragen | Quelle zum Prüfen |
|---|---|---|---|
| A1 | STACKIT-AVV (v2.4.2) erfüllt Art. 28 Abs. 3 vollständig (Ziff. 2.2/Anlage 1, 2.4, 3, 5, 6, 7, 8, 9, 10, 11) | 3.1 D, Zeile STACKIT | `03_Dienstleister/STACKIT/STACKIT_Auftragsverarbeitungsvertrag.pdf` |
| A2 | STACKIT-AVV erwähnt Training nicht; „kein Training“ ist über den Leistungsschein belegt: „does not collect or evaluate any customer data other than billing-relevant data“, Kundendaten „not stored permanently“ | 3.1 D, 5.9 B2, Notion A6 | `03_Dienstleister/STACKIT/STACKIT_Leistungsschein_AI_Model_Serving_v1.3_2025-09-18.pdf` (und v1.4 ab 06.11.2026) |
| A3 | STACKIT AVV Ziff. 2.3 erlaubt „anonymisierte Nutzungsdaten für eigene Zwecke“ – betrifft Nutzungs-, nicht Inhaltsdaten | 3.1 D | STACKIT-AVV Ziff. 2.2, 2.3, Anlage 1 |
| A4 | STACKIT-Standort laut AVV nur EU/EWR (Ziff. 2.5), Deutschland nur über Leistungsschein/Region eu01 | 3.1 D | STACKIT-AVV Ziff. 2.5, Anlage 2; Leistungsschein |
| A5 | STACKIT-Zertifikate: TOMs nur „angelehnt an ISO/IEC 27001“, BSI C5 nicht genannt | 3.1 D | `STACKIT_TOMs.pdf` Kap. 6.1.1 |
| A6 | Microsoft-DPA (22.05.2026, deutsch) enthält Art.-28-Bestimmungen (Anlage 1, S. 42), Löschung 90 + 90 Tage, SCC 2021, Vertraulichkeit der Mitarbeiter (S. 22), keine Nutzung für Profilbildung/Werbung/Marktforschung (S. 9) | 3.1 D, 5.9 B3 | `03_Dienstleister/Microsoft_Azure/MicrosoftProductandServicesDPA(WW)(German)(May2026)(CR).docx` |
| A7 | Microsoft „kein Training“ für Azure OpenAI | 3.1 D, 5.9 B3 | `03_Dienstleister/Microsoft_Azure/Microsoft_Learn_Azure_OpenAI_Datenschutz_kein_Training_2026-10-08.pdf` (learn.microsoft.com/en-us/azure/foundry/responsible-ai/openai/data-privacy, Stand 18.05.2026) |
| A8 | Microsoft-Missbrauchsüberwachung: menschliche Prüfung möglich, Speicherung in der Geografie der Ressource, Prüfer im EWR; die 30 Tage nennt die aktuelle Doku nicht mehr ausdrücklich | 3.1 D | `03_Dienstleister/Microsoft_Azure/Microsoft_Learn_Azure_OpenAI_Abuse_Monitoring_2026-10-08.pdf` (learn.microsoft.com/en-us/azure/foundry/openai/concepts/abuse-monitoring, Stand 13.05.2026) |
| A9 | Azure Speech: schnelle Transkription ohne Speicherung, Audio-Logging standardmäßig aus | 3.1 D, 5.9 B3 | `03_Dienstleister/Microsoft_Azure/Microsoft_Learn_Speech_to_Text_Datenschutz_2026-10-08.pdf` und `…/Microsoft_Learn_Speech_Audio_Logging_2026-10-08.pdf` |
| A10 | Hetzner-AV-Vertrag v1.2 (16.02.2026) mit 26Lab.io erfüllt Art. 28 Abs. 3 vollständig (bisher nur Kopf und § 1 gelesen); Vertraulichkeit/Geheimhaltung der Mitarbeiter (§ 203?) | 3.1 A Nr. 2, 3.1 D | `03_Dienstleister/Hetzner/Hetzner_AVV_v1.2_26Lab_2026-10-05.pdf` |
| A12 | Anbieter-Angaben im Verbinden-Dialog (1.5 I, seit 08.10.2026): Rechtsträger, Sitz und Übermittlungsgrundlage stimmen – v. a. „DPF-zertifiziert“ bei Google Ireland/LLC, Microsoft, Meta/WhatsApp, Slack (Salesforce); Shopify Irland/Kanada (Angemessenheit); EU-Sitz bei DeepL, Mollie, Brevo, Mailjet, Plausible, Teamleader, seven, clockodo; bexio Schweiz. Calendly und Cal.com stehen bewusst auf „Grundlage prüfen“ | 5.9 A21 | Portal `lib/integrations/anbieter.ts`, Kern `packages/web/src/app/lymbe/anbieter.ts` (Repo lymbe-ablaeufe); Prüfung gegen dataprivacyframework.gov |
| A11 | Hetzner ISO/IEC 27001:2022 (SOCOTEC, ZN-2025-35 V 1.1, gültig bis 26.09.2028) deckt Nürnberg und Falkenstein ab | 3.1 A Nr. 2, 3.1 D | `03_Dienstleister/Hetzner/Hetzner_ISO27001_Zertifikat_2026-10-08.pdf` |

## B – Messungen am System (nur Plausibilität prüfen)

Alle Messungen liefen über `scripts/zugriff.sh` und stehen im Zugriffsprotokoll `BetriebsZugriff` (zentrale DB); was einen Workspace betrifft, sieht der Kunde unter Einstellungen → Datenschutz.

| Nr | Aussage | Wo eingetragen | Beleg |
|---|---|---|---|
| B1 | Azure: Ressource `lymbe-ai` in Germany West Central, alle Bereitstellungen „Datenzonenstandard (EUR)“; alte Ressource in Sweden (Global Standard) gelöscht | Notion A26, 3.1 D | `03_Dienstleister/Microsoft_Azure/Azure_Regionen_Nachweis_2026-10-08.md` + 3 Screenshots |
| B2 | Azure: Missbrauchsüberwachung aktiv (kein `ContentLogging=false`) | 3.1 D, 5.9 B3 | Abfrage Azure Resource Graph 08.10.2026 |
| B3 | Nachtlauf der 90-Tage-Löschung scheiterte 05.–08.10. am Protokollschritt (gelöscht war alles), seit 08.10. behoben, Protokoll je Lauf | Notion A3, 5.9 A3 | Commit 40421ff; Tabelle `LoeschLauf` |
| B4 | Demo-Workspace löscht Gespräche nach 24 Stunden; Widget auf lymbe.ai umgestellt | Notion A3, 5.9 C1 | Commits 40421ff, 3f58b31 |
| B5 | Alte Testmandanten vollständig entfernt (DB, Qdrant, MinIO, Cache); Inngest läuft bis 05.11. aus | Notion A20, 5.9 A20b | Nachmessung 08.10.2026 |
| B6 | Support-Zugang mit Grund/Frist/Protokoll; Betriebszugriffe (psql, docker, Live-Log, Admin-Einsicht) protokolliert; SSH nur mit Schlüssel | Notion A11, 5.9 A9/A14 | Commits 79f8f55, 2c788d5, 6084f33, 89e4b3d |

## C – Offene Rechtsfragen (Einschätzung, ggf. Anwalt)

1. **§ 203 StGB bei STACKIT und Microsoft:** Keiner der beiden Verträge enthält eine § 203-Klausel; beide verpflichten Mitarbeiter nur allgemein zur Vertraulichkeit bzw. aufs Datengeheimnis (STACKIT AVV Ziff. 5, TOMs 1.2.4/7.1.1; Microsoft DPA S. 22). Reicht das für Kunden nach AVV § 12 (Praxen, Therapieeinrichtungen, Kanzleien – die Pilotkundin ist ein Autismustherapiezentrum)? § 203 Abs. 3 und 4 StGB verlangen, dass „mitwirkende Personen“ zur Geheimhaltung verpflichtet werden. Wie steht es um 26lab.io (AVV Anlage 5) als nächstem Glied?
2. **STACKIT-Standort EU/EWR statt Deutschland:** AVV und Datenschutzerklärung sagen „Deutschland“; der STACKIT-AVV sagt nur EU/EWR. Formulierung anpassen oder schriftliche Zusage zu Deutschland einholen?
3. **Microsoft Datenzone EU:** Speicherung in Frankfurt, Verarbeitung in jedem EU-Staat möglich – passt das zu „Werkstatt in der EU-Datenzone“ in AVV/DSE? (Vermutlich ja, gegenlesen.)
4. **30 Tage Missbrauchsüberwachung:** AVV Anlage 2 und 4.1 nennen „bis zu 30 Tage“; die aktuelle Microsoft-Doku nennt keine Frist mehr. Satz lassen oder auf „zur Missbrauchsüberwachung“ kürzen?
5. **Stimmung aus Text (Notion A10, 5.9 B4):** bewusst beibehalten, weil Text keine biometrischen Daten sind (Art. 3 Nr. 39 KI-VO, ErwG 18) und Mitarbeiter-Chats nie ausgewertet werden. Bitte bestätigen und 5.9 B4 umformulieren; klären, ob die Stimmungsauswertung in die Textbausteine der Kunden-DSE gehört.

## D – Was in 5.9 noch ❌ ist (zur Kenntnis)

- **A8:** Benachrichtigungsziele und das Verbinden von Diensten werden nicht mit Zeit und Nutzer protokolliert (AVV § 3 Abs. 1 sagt es zu).
- **A18:** Export enthält Dokumente nur als Metadaten, kein Gedächtnis, keine Abläufe (AVV § 8 Abs. 4).
- ~~**A21:** Kein Hinweis auf Anbieter und Standort beim Verbinden eines Dienstes~~ – seit 08.10.2026 gebaut (siehe A12 oben).
- **C2:** Das Widget sendet ohne Chat mehr als Referrer und IP (Analyse ist an); DSE-Satz anpassen oder Analyse-Vorgabe ändern.

- **A37 – Verschlüsselung ruhender Daten (Text anpassen, Entscheidung Christian 08.10.2026):** Der Server hat keine Datenträgerverschlüsselung (gemessen: ext4 ohne LUKS); nachgerüstet wird sie nicht, den Schutz der Platte übernimmt Hetzner (ISO/IEC 27001). Drei Stellen versprechen mehr:
  - `01_Kunden/1.1_AVV_Kunden_v1.6.md`, Anlage 1, Vertraulichkeit – bisher „Verschlüsselung: TLS 1.2+ bei der Übertragung, verschlüsselte Datenträger (AES-256), Zugangsdaten verbundener Dienste zusätzlich verschlüsselt“ → neu: „Verschlüsselung: TLS 1.2+ bei der Übertragung; Datensicherungen, Passwörter und Zugangsdaten verbundener Dienste verschlüsselt (AES-256 bzw. Hash); Rechenzentrum nach ISO/IEC 27001 zertifiziert“
  - `01_Kunden/1.7_Plattformbeschreibung_und_Kurz-DSFA.md`, Risiko R1 – „verschlüsselte Datenträger“ streichen, ersetzen durch „verschlüsselte Sicherungen und Zugangsdaten, Rechenzentrum ISO 27001“
  - `04_Oeffentlich/4.1_Datenschutzerklaerung_v1.5.md`, Abschnitt Sicherheit – „Verschlüsselte Speicherung sensibler Daten (AES-256)“ → „Verschlüsselte Speicherung von Passwörtern, Zugangsdaten und Datensicherungen (AES-256)“
  Ändert AVV Anlage 1 den Text nach Versand an Kunden, gilt § 4 bzw. die Änderungsmitteilung (1.4) nur, wenn es eine Verschlechterung ist – hier wird ein unzutreffender Satz berichtigt; bitte bewerten, ob Bestandskunden (Pilotkundin) informiert werden müssen.

Entweder System nachbauen oder Vertrag/DSE anpassen – Grundsatz aus 5.9: „Was nicht bestätigt werden kann, wird im Vertrag geändert, nicht umgekehrt.“
