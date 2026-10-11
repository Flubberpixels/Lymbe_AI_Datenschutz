# Gesamtprüfung Lymbe AI – Datenschutz-Dokumentenset vor Livegang

**Unabhängige Prüfung · Stand 02.10.2026 · Grundlage: alle 21 P1-Dokumente, 00/01/04, Dienstleisterverzeichnis vom 17.09.2026 (17 Seiten)**

Nicht infrage gestellt (Entscheidungen des Anbieters): ein AVV mit § 12, keine Branchenabfrage, keine Abschaltungen durch Lymbe, Suchbegriff-Generator, Haftung nach Verursachung, Gerichtsstand Düsseldorf, Meldefrist „in der Regel 24 h", Selbstlernen Standard aus, Patientendaten im Digitalen Mitarbeiter.

Priorität: **P1** vor Auslieferung · **P2** vor breitem Verkauf · **P3** Anwalt.

---

## 1. Blocker (müssen vor Auslieferung behoben werden)

**B1 · P1 · 1.6 Zeile 17 – falsche Anschrift im Kundentext.**
„Verantwortlich sind wir, [Firma], Hasselbeckstr. 37, 40822 Mettmann" – das ist die Anschrift von 26lab/Christian, eingetragen in die Vorlage, die die Kundin an ihr Team gibt. Korrektur: „Verantwortlich sind wir, [Firma], [Anschrift], [Datenschutz-Kontakt]."

**B2 · P1 · 4.1 Abschnitt 2 (Zeile 23) und Überschrift Abschnitt 12 (Zeile 113) – falsche Tatsachenbehauptung in der öffentlichen Datenschutzerklärung.**
„Nur eine Funktion schickt Daten in die USA: die Websuche" / „die einzige Übermittlung in die USA". Dieselbe Erklärung nennt Übermittlungen in die USA in Abschnitt 6 (GitHub-Login), 7 (Stripe Inc.), 9 (GitHub Actions), 10 (Let's Encrypt), 13 (Slack/Teams), 14 (Meta) und Anlage-2-Rest-Übermittlungen bei Microsoft. Korrektur Abschnitt 2: „Deine Inhalte im Portal und in den Chats bleiben in Deutschland und der EU. Nur die Websuche in ‚Frag Lymbe' (standardmäßig aus) sendet einen Suchbegriff ohne personenbezogene Angaben an OpenAI. Wofür wir selbst verantwortlich sind (Konto, Zahlung, Anmeldung), gibt es einzelne weitere US-Empfänger – siehe Abschnitt 16." Überschrift 12: „Websuche in ‚Frag Lymbe' – Übermittlung an OpenAI".

**B3 · P1 · 1.1 Anlage 2 Nr. 4, 4.1 Abschnitt 11/16, 5.1 A5/A6, 2.1 Anlage 1 – Vertrag beschreibt einen Zustand, den das Verzeichnis widerlegt.**
Dienstleisterverzeichnis 0.4/A4/G1: Werkstatt läuft über OpenAI (`AI_PROVIDER_WERKSTATT=openai`, Verarbeitung Schweden), Azure OpenAI ist „kein Empfänger"; Azure Speech kommt im Verzeichnis gar nicht vor. Die Umstellung ist Aufgabe 5.9 A1/A12, aber unbestätigt. Vor Freischaltung des AVV: entweder A1 und A12 mit Datum bestätigt – oder Anlage 2 anpassen: Nr. 4 streichen bzw. „nur wenn genutzt" durch „derzeit nicht aktiv" ersetzen; Nr. 5 OpenAI ergänzen um „Werkstatt für Abläufe: Beschreibungstexte und Ablaufdefinitionen (Zugangsdaten maskiert), Verarbeitung im EU-Rechenzentrum (Schweden)". Gleiches in 4.1 Abschnitt 11 (Zeile 107, 109), 16 und 5.1 A5/A6.

**B4 · P1 · 1.1 § 3 Abs. 10, Anlage 2 Nr. 5, 4.1 Abschnitt 2/12, 5.9 A10 – Websuche-Schalter je Workspace existiert laut Verzeichnis nicht.**
Verzeichnis 0.4: „Abschaltbar: `OPENAI_API_KEY` leeren" – ein globaler Schalter, kein Mandanten-Schalter, kein Einschalt-Dialog (1.5 Nr. 6). Der AVV macht das Einschalten zur Weisung („das Einschalten ist die Weisung zur Übermittlung"). Ohne Schalter ist die Websuche für alle an (dann Übermittlung ohne Weisung, auch für die Pilotkundin) oder für alle aus. Vor Livegang: Mandanten-Schalter mit Protokoll bauen (A8/A10) – oder `OPENAI_API_KEY` leeren und in Anlage 2 Nr. 5 „derzeit nicht aktiv; Einschalten je Workspace wird mit Ankündigung nach § 4 Abs. 2 freigeschaltet" eintragen.

**B5 · P1 · 1.1 § 3 Abs. 10 / Anlage 2 Nr. 5 / 4.1 Abschnitt 12 / 1.5 Nr. 6 – absolute Garantie, die ein Sprachmodell nicht halten kann.**
„Der Suchbegriff wird ... so gebildet, dass er keine Namen, Kontaktdaten oder sonstigen personenbezogenen Angaben enthält." 1.6 Zeile 25 sagt ehrlicher: „der Suchbegriff kann Inhalte eurer Frage enthalten", und das Inhaltsverzeichnis (1.5, Zeile 73) verlangt den Hinweis „ohne die Behauptung, es gingen keine personenbezogenen Daten". Ein Prompt-Filter ist eine Maßnahme, keine Garantie; die Zusage im AVV begründet Haftung bei jedem Fehlgriff. Korrektur (behält den Suchbegriff-Generator und die Kundenpflichten): „Der Suchbegriff wird vom KI-Modell nach fester Anweisung ohne Namen, Kontaktdaten und sonstige personenbezogene Angaben gebildet; Lymbe prüft das regelmäßig mit Testfragen (Anlage 1). Gesprächsverlauf, Dokumente und Nutzeridentität werden nicht übermittelt. Der Kunde weist sein Team an, in Fragen, die eine Websuche auslösen, keine Personen zu nennen." Gleich in 4.1 Abs. 12, 1.5 Nr. 6 („Suchbegriff wird ohne Personenbezug gebildet" statt „ohne Personenbezug" als Eigenschaft) und 1.3/1.6 angleichen.

**B6 · P1 · 1.1 § 8 Abs. 1/3, 5.1 V9, 5.9 – Hetzner-Server-Snapshots haben nirgends eine Frist.**
Verzeichnis A2/B9: Snapshots existieren; Mailvolume und DKIM-Schlüssel liegen nur dort. AVV verspricht „Datensicherungen 7 Tage" und „spätestens 37 Tage nach Vertragsende überschrieben". 5.1 V9 verweist auf „Snapshot-Frist (5.9)" – in 5.9 gibt es keine solche Zeile. Korrektur: 5.9 neue Zeile „A2b Hetzner-Snapshots: Aufbewahrung ___ Tage, Beleg Cloud-Konsole" und in AVV § 8 Abs. 1 „Datensicherungen (Datenbank-Sicherung und Server-Snapshot): 7 Tage" – oder, falls Snapshots länger laufen, die Frist dort nennen.

**B7 · P1 · 5.9 A6 (Zeile 20) und 5.1 V7 (Zeile 74) – falsche Fristen in der Abnahmeliste und im Verzeichnis.**
AVV § 8 Abs. 1 und 4.1 Abschnitt 9: Zugriffs-/Betriebsprotokolle 14 Tage, Fehlerprotokoll 30 Tage. 5.9 A6 fasst beides unter „30" zusammen – Christian würde die falsche Zahl bestätigen. 5.1 V7 nennt „Fehlerprotokoll 14 Tage". Korrektur: 5.9 A6 aufteilen: „A6a Zugriffs-/Betriebsprotokolle (Caddy, Redis-Zähler): 14 Tage · A6b Fehlerprotokoll: 30 Tage"; 5.1 V7 „Fehlerprotokoll 30 Tage"; 5.1 V6 „Mail-Logs 14 Tage".

**B8 · P1 · 2.1 § 1 Abs. 4 (Zeile 25) und § 3 Abs. 10 (Zeile 55) – falsche Paragrafenverweise im Vertrag, der morgen unterschrieben wird.**
§ 1 Abs. 4: „§ 3 Abs. 3, § 8 und § 9 gelten über das Vertragsende hinaus" – in 2.1 ist § 7 Löschung, § 8 Kontrolle, § 9 Haftung (Nummerierung weicht vom Kunden-AVV ab). Korrektur: „§ 3 Abs. 3 und 4, § 7 und § 8 gelten über das Vertragsende hinaus." § 3 Abs. 10: „ermöglicht Kontrollen (§ 9)" → „(§ 8)".

**B9 · P1 · 5.3 Nr. 2 (Zeile 14) – Freigabepflicht fehlt; Zeile 23 falsches Strafmaß.**
AVV § 3 Abs. 5, Anlage 5 Nr. 2 und 2.1 § 3 Abs. 6 verlangen vorherige Freigabe durch den Datenschutz-Ansprechpartner; 5.3 verlangt nur Protokoll. Korrektur Nr. 2: „... nur zuzugreifen, wenn es zur Störungsbeseitigung oder auf Anfrage des Kunden erforderlich ist, nur nach vorheriger Freigabe durch den Datenschutz-Ansprechpartner (bei Gefahr im Verzug mit unverzüglicher nachträglicher Information) und jeden Zugriff mit Zeitpunkt, Person, Grund und Umfang zu protokollieren". Zeile 23: § 42 Abs. 2 BDSG (gegen Entgelt/Bereicherungsabsicht) droht bis zu **zwei** Jahre; drei Jahre gelten für § 42 Abs. 1 (gewerbsmäßige Übermittlung großer Datenmengen). Korrektur: „nach § 42 BDSG strafbar sein können (Freiheitsstrafe bis zu zwei, in schweren Fällen bis zu drei Jahren)".

**B10 · P1 · 1.2 § 1 (Zeile 17) – Verweis auf AGB „Fassung [1.3]", die es nicht gibt.**
1.0 ist nur eine Änderungsliste; der AGB-Text v1.3 muss von Christian/Dennis erst eingepflegt und veröffentlicht werden. Entweder v1.3 vor dem 05.10. live, oder in 1.2: „Nutzungsbedingungen (AGB, Fassung 1.2) in Verbindung mit den in Anlage A dieser Vereinbarung aufgeführten Ergänzungen" und 1.0 als Anlage beifügen.

**B11 · P1 · 1.5 – Sie-Fassung fehlt.**
04_Offene_Punkte D6 sagt „beide Fassungen in 1.5 Anlage" – 1.5 enthält nur die Du-Fassung. Eltern eines Therapiezentrums erwarten „Sie". Korrektur: Anlage zu 1.5 mit Sie-Fassung von Nr. 1, 2, 3, 4, 5, 9, 11 ergänzen oder Christian die Anrede als Einstellung je Assistent bauen lassen.

**B12 · P1 · 1.1 § 12 Abs. 3 (Zeile 185) – Behauptung „von deren Vorliegen Lymbe sich vergewissert hat" ohne Nachweis.**
3.1 Tabelle A: alle fünf Nachweise ❌. Bis C3 erledigt ist, stimmt der Satz nicht. Korrektur, falls C3 bis 05.10. nicht geschafft wird: „... die Cloud-Anbieter durch die Geheimhaltungspflichten in deren Verträgen, deren Vorliegen Lymbe vor dem Einsatz für Daten nach diesem Paragrafen prüft und dokumentiert."

**B13 · P1 · 5.6 Zeile 12 und Zeile 86 – Telefonnummer im Klartext, aber Abschnitt 7 verweist auf den Tresor; Christians E-Mail als Platzhalter.**
Zeile 12 nennt „0177 2262453"; Abschnitt 7 sagt für alle „siehe Kontaktliste Passwort-Tresor"; Offene Punkte A21 will die Nummern erst in den Tresor. Entscheiden: Nummer entweder in beiden Stellen (dann auch Christians Nummer) oder nur im Tresor. Zeile 86: „[E-Mail]" → „hello@26lab.io" (so in AVV Anlage 4 und 2.1 § 3 Abs. 1).

**B14 · P1 · 5.2 Abschnitt 2.5 (Zeile 109 vs. 112) – Widerspruch in der Vorlage für die Kundin.**
„Frag Lymbe (ohne Websuche)" und zwei Zeilen später „Datenminimierung: Websuche nur mit Suchbegriffen ohne Personenbezug". Korrektur Zeile 112: „Websuche für diesen Workspace aus (Weisung: nicht einschalten)".

**B15 · P1 · 4.1 Zeile 5 (Vermerk) und Zeile 18 (DSB-Platzhalter) – vor Veröffentlichung entfernen.**
Beide Zeilen dürfen nicht auf lymbe.ai/datenschutz erscheinen. Zeile 18 ersetzen durch nichts (5.11: kein DSB) oder „Datenschutz-Ansprechpartner: Dennis [Nachname], datenschutz@lymbe.ai".

**B16 · P1 · 1.1 Anlage 2 Nr. 3 – Sitz von STACKIT abgleichen.**
AVV: „Stiftsbergstraße 1, 74172 Neckarsulm". Verzeichnis A3: „Bad Friedrichshall, HRA 741347 (AG Stuttgart)". Eine der beiden Angaben ist falsch; vor Vertragsschluss gegen das STACKIT-Impressum prüfen und Verzeichnis oder AVV korrigieren.

**B17 · P1 · 1.1 Vertragsparteien / Abschluss, 5.9 A15/A20 – ohne Formularfelder gibt es keinen Auftraggeber.**
Der AVV identifiziert den Kunden über „Firma, Anschrift, vertretungsberechtigte Person beim Anlegen des Workspace". Verzeichnis 0.7: Die Checkbox protokolliert „Fassung, Zeitpunkt, Person, Adresse" – Firma/Anschrift/Vertretung werden bislang nicht abgefragt. Für die Pilotkundin reicht K1 (Ausdruck unterschreiben); für jeden weiteren Neukunden ist A15/A20 Voraussetzung. In 1.2 Checkliste ergänzen: „☐ AVV als Ausdruck mit Firma/Anschrift/Vertretung unterschrieben, solange das Portal die Felder nicht hat".

---

## 2. Widersprüche zwischen Dokumenten

| # | Dokument A sagt | Dokument B sagt | Korrektur | Prio |
|---|---|---|---|---|
| W1 | 1.1 § 8 Abs. 1: Zugriffsprotokolle 14 Tage, Fehlerprotokoll 30 Tage; 4.1 Abschnitt 9 gleich | 5.9 A6: beide „30"; 5.1 V7: Fehlerprotokoll 14 Tage | 5.9 A6 aufteilen (14/30); 5.1 V7 „30 Tage" (B7) | P1 |
| W2 | 1.1 § 8 Abs. 1: Datensicherungen 7 Tage; § 8 Abs. 3: 37 Tage nach Vertragsende | Verzeichnis E4: Datenbanksicherungen 30 Tage; Snapshots ohne Frist; 5.1 V9 verweist auf nicht existierende 5.9-Zeile | 5.9 A2 bestätigen + Snapshot-Zeile (B6) | P1 |
| W3 | 1.1 Anlage 2 Nr. 4 / 4.1 Abschnitt 11, 16 / 5.1 A5, A6 / 2.1 Anlage 1: Werkstatt = Azure OpenAI, Spracheingabe = Azure Speech | Verzeichnis 0.4, A4, G1: Werkstatt = OpenAI (Schweden), Azure kein Empfänger; Azure Speech nicht erfasst | A1/A12 bestätigen oder Anlage 2 ändern (B3) | P1 |
| W4 | 1.1 § 3 Abs. 10 / 4.1 Abs. 2: Websuche „nur wenn der Kunde sie eingeschaltet hat", Standard aus | Verzeichnis 0.4: nur globaler Schalter (API-Key) | Mandanten-Schalter bauen oder Key leeren (B4) | P1 |
| W5 | 1.1 § 3 Abs. 10, Anlage 2 Nr. 5, 4.1 Abs. 12, 1.5 Nr. 6: Suchbegriff „enthält keine personenbezogenen Angaben" | 1.6 Zeile 25: „kann Inhalte eurer Frage enthalten"; 01_Inhaltsverzeichnis 1.5: „ohne die Behauptung, es gingen keine personenbezogenen Daten" | Formulierung als Maßnahme + Testpflicht (B5) | P1 |
| W6 | 4.1 Abschnitt 2/12: Websuche einzige US-Übermittlung | 4.1 Abschnitte 6, 7, 9, 10, 13, 14, 16: weitere US-Empfänger | Abschnitt 2/12 umformulieren (B2) | P1 |
| W7 | 1.1 § 3 Abs. 5, Anlage 5 Nr. 2, 2.1 § 3 Abs. 6, 2.2 § 3 Abs. 4: Zugriff nur nach vorheriger Freigabe | 5.3 Nr. 2: nur Protokoll, keine Freigabe; 5.9 A9: Protokoll ohne „Umfang" | 5.3 ergänzen (B9); 5.9 A9 „Zeitpunkt, Person, Grund, Umfang, Mandant" | P1 |
| W8 | 2.2 § 3 Abs. 4: „Flubbers eigene Zugriffe unterliegen demselben Protokoll" (Freigabe durch Flubber) | 5.2 R2: „Vier-Augen bei sensiblen Mandanten" – nirgends definiert; Dennis gibt sich selbst frei | 2.2 § 3 Abs. 4 ergänzen: „Zugriffe von Flubber gibt 26lab frei (Vier-Augen-Prinzip)" oder 5.2 R2 streichen | P2 |
| W9 | 1.1 § 1 Abs. 2, 4.1 Abschnitt 5, 5.10 Zeile 1/8, 5.1 V1: Team-Verwaltung und Weisungsprotokoll = Flubber Verantwortlicher | 1.1 Anlage 3 letzte Zeile, 5.1 A7: dieselben Daten als Auftragsverarbeitung | Eine Rolle wählen (Empfehlung: Konto/Team = Flubber; Weisungsprotokoll je Workspace = Auftrag) und Anlage 3/5.1 bereinigen | P3 |
| W10 | 1.1 § 12 Abs. 5, 1.5 Nr. 3: „Minderjährige" (unter 18) an Sorgeberechtigte verweisen, keine Kontaktdaten | 1.3 Variante D: „Kinder und Jugendliche unter 16 Jahren" | 1.3 D auf „Minderjährige" angleichen | P2 |
| W11 | 1.3 Variante A: IP dient auch „einer Auswertung der Nutzung"; 4.1 Abs. 13: „Auswertung für den Kunden"; Verzeichnis D1: „Ratenbegrenzung und Auswertung" | 1.3 Variante D: nur „Bereitstellung und Schutz" | Variante D ergänzen oder – wenn für § 12-Kunden keine Auswertung – technisch abschaltbar machen und in 5.9 aufnehmen | P2 |
| W12 | 1.3 Variante A (Selbstlernen): „Personenbezogene Angaben werden dabei nicht übernommen" | 1.1 § 6 Abs. 4, 5.2 R6: Kunde muss Einträge prüfen und löschen (also können welche enthalten sein); kein 5.9-Beleg | Satz streichen oder 5.9-Zeile „Selbstlernen filtert Personenbezug" mit Testbeleg ergänzen | P2 |
| W13 | 1.1 Vorspann Satz 3: „Außer dir und deinem Team sieht niemand deine Inhalte" | 1.1 Anlage 2: STACKIT, Microsoft, OpenAI verarbeiten Inhalte | „Außer dir, deinem Team und den in Anlage 2 genannten KI-Anbietern sieht niemand ..." | P2 |
| W14 | 1.1 Vorspann Satz 4: „nach Vertragsende ist innerhalb von 30 Tagen alles weg" | 1.1 § 8 Abs. 3: Sicherungen bis 37 Tage, Vertragsprotokolle 3 Jahre | „... innerhalb von 30 Tagen gelöscht, Sicherungen spätestens nach 37 Tagen überschrieben" | P2 |
| W15 | 1.1 § 4 Abs. 2 / 1.4 Vorlage: Widerspruch bis Tag 14 möglich; Lymbe antwortet innerhalb 5 Werktagen; Kündigung „bis zum Zeitpunkt des Einsatzes" | Bei Widerspruch an Tag 13 kommt die Antwort nach dem Einsatz – das Kündigungsrecht läuft leer | „Der Kunde kann innerhalb von 14 Tagen nach Zugang der Antwort außerordentlich kündigen; bis dahin setzt Lymbe den Unterauftragsverarbeiter für den Workspace des Kunden nicht ein, soweit möglich" | P3 |
| W16 | 1.1 § 5 Abs. 1 / 4.1 Abschnitt 14: verbundene Dienste = Messenger, Kalender, Shops, Postfächer, Benachrichtigungsziele, Abrufadressen | Verzeichnis C9/E3: 718 Bausteine mit Kontoanbindung im Ablauf-Kern (beliebige Drittdienste) | § 5 Abs. 1 „zum Beispiel ... sowie alle weiteren Dienste, die der Kunde über Bausteine der Abläufe verbindet"; 4.1 Abschnitt 14 gleich | P2 |
| W17 | 1.1 § 5 Abs. 5 Überschrift „Messenger (WhatsApp)"; 4.1, 1.3 B, 1.5 Nr. 8/9: nur WhatsApp | Verzeichnis A7: Messenger und Instagram über dieselbe Meta-App in Betrieb | 5.9 A13 bestätigen; falls aktiv: § 5 Abs. 5 „WhatsApp, Facebook Messenger, Instagram" | P1 (Bestätigung), P2 (Text) |
| W18 | 4.1 Abschnitt 9: GitHub Actions (USA) als Wächter | 4.1 Abschnitt 16: „Keine weiteren Empfänger" – GitHub Actions fehlt in der Tabelle | Zeile „GitHub Inc. – Verfügbarkeitsprüfung (ohne personenbezogene Daten) – USA" ergänzen | P2 |
| W19 | 3.1 B7: GitHub mit DPA (Login, Code-Hosting, Wächter) | 4.1 Abschnitt 6/16, 5.10, 5.1 V2: GitHub beim Login = eigener Verantwortlicher | 3.1 B7 aufteilen: Login = eigener Verantwortlicher (wie Google), Code-Hosting/Actions = DPA | P3 |
| W20 | 2.2 § 1 Abs. 2: „26lab ist Unterauftragsverarbeiter nach dem AVV" | 2.1 § 1 Abs. 2: 26lab auch direkter Auftragsverarbeiter für Flubbers eigene Daten | 2.2: „Auftragsverarbeiter bzw. Unterauftragsverarbeiter nach dem AVV (2.1)" | P2 |
| W21 | 5.6 Zeile 12: Mobilnummer im Text | 5.6 Abschnitt 7, 04 A21: Nummern nur im Tresor | vereinheitlichen (B13) | P1 |
| W22 | 1.6 Zeile 25: „an OpenAI (USA)" | 1.1 Anlage 2 Nr. 5, 4.1 Abs. 12: OpenAI Ireland Ltd., Verarbeitung ggf. USA | „an OpenAI Ireland Ltd. (Verarbeitung ggf. in den USA)" | P2 |
| W23 | 1.6 Zeile 56: Beschwerde bei LDI NRW | Zuständig ist die Behörde am Sitz des Kunden, nicht Flubbers | „bei der für uns zuständigen Aufsichtsbehörde (in NRW: LDI NRW, ldi.nrw.de)" | P2 |
| W24 | 5.9 A10: Fundstelle „§ 3 Abs. 9" | 1.1: Websuche steht in § 3 Abs. 10 | Fundstelle korrigieren | P2 |
| W25 | 2.1 Offene Punkte Nr. 4, 2.2 Offene Punkte Nr. 6: „Gerichtsstand einheitlich mit 2.2/2.1" | Beide sagen bereits Düsseldorf | Beide Punkte streichen | P2 |
| W26 | 03_Status_fuer_Dennis.md: nennt 1.7, „Anlage A", „Anlage B", „AVV + 1.7 bestätigen lassen" | 00/01/04: 1.7 entfallen, Anlagen A/B existieren nicht mehr | 03_Status aktualisieren oder ins Archiv | P2 |
| W27 | 00_Projektplan: 1.1 „Entwurf 2, geprüft", alle anderen „Entwurf 1"; E-Nummern E9, E10, E8 in dieser Reihenfolge | 00 Protokoll „Finale Fassung" | Statusspalte auf Fassungsstand setzen; Nummern ordnen | P2 |

Geprüft und **ohne** Widerspruch: Meldefristen 12 h (2.1 § 6, 5.6) / 24 h (AVV § 7, 2.1 § 6 Abs. 2, 5.6, 5.2 R10) / 72 h / 4 h Telefon (AVV § 12 Abs. 6, 5.6 Schritt 5); 90/30/30/7 Tage in AVV § 8, 4.1 Abschnitt 11, 5.2, 2.1 § 7, 1.2 § 5; 3 Werktage Weiterleitung (AVV § 3 Abs. 7, 4.1 Teil B/19, 5.7); 5/10 Werktage Löschung (5.7, 2.1 § 3 Abs. 7, AVV § 3 Abs. 7); 14/30 Tage Ankündigung (AVV § 4, 1.4, 2.1 § 4 Abs. 3, 1.2 § 3); Gerichtsstand Düsseldorf in 1.1, 2.1, 2.2, 1.0; Rollen Stripe/Google/GitHub/Meta in 1.1, 4.1, 5.10, 5.1 (bis auf W9, W19); Flubber-Anschrift, Telefon, datenschutz@lymbe.ai, 26lab-Anschrift, LDI-NRW-Kontakt überall gleich.

Hinweis zur Erreichbarkeit (kein Widerspruch, aber eng): 2.2 § 3 Abs. 5 erlaubt Dennis nachts 6 h Reaktionszeit; AVV § 12 Abs. 6 verlangt Telefonanruf, wenn die Kundin die Mail nicht in 4 h bestätigt. 12 h + 6 h + Kundenmeldung muss in 24 h passen.

---

## 3. Verbliebene Platzhalter

Kundenfelder in Mustern ([Kunde], [Name], [Datenschutz-Link], Unterschriftszeilen, Mail-Vorlagenfelder in 1.4/5.6/5.7) sind beabsichtigt und nicht gelistet.

| Datei | Zeile | Platzhalter | Wer füllt | Prio |
|---|---|---|---|---|
| 01_Kunden/1.6 | 17 | „[Firma], Hasselbeckstr. 37, 40822 Mettmann" – falsche echte Daten statt Platzhalter | Cowork | P1 |
| 04_Oeffentlich/4.1 | 5 | „Vermerk (nicht Teil der Erklärung)" – vor Veröffentlichung entfernen | Dennis | P1 |
| 04_Oeffentlich/4.1 | 18 | „[Datenschutzbeauftragter: [Name, Kontakt] – nur, falls benannt]" | Dennis (5.11) | P1 |
| 01_Kunden/1.2 | 12, 17, 21, 25, 29, 37, 53 | [den Pilotpreis / Konditionen], [1.3], [05.10.2026], [3], [14 Tage], [Pilotpreis …], [Angebot vom …], [3 Werktage], [alle zwei Wochen], [14 Tagen] – Anbieter-Entscheidungen (04 D5), keine Kundenfelder | Dennis | P1 |
| 01_Kunden/1.2 | 5 | „Vermerk (nicht Vertragsbestandteil)" und Abschnitt „Checkliste (intern)" – vor Übergabe an die Kundin trennen | Dennis | P1 |
| 05_Intern/5.6 | 86 | „[E-Mail]" für Christian | Cowork | P1 |
| 05_Intern/5.6 | 89 | „Anwalt [Name]" | Dennis (04 D8) | P2 |
| 05_Intern/5.1 | 5 | „DSB: [keiner benannt / Name]" | Dennis | P1 |
| 03_Dienstleister/3.1 | 14–17 | „[5.9 A23]" Kontoinhaber ×4 | Christian | P1 |
| 05_Intern/5.9 | 19, 20 | „___ Tage" A5/A6 – A6 zusätzlich falsch (B7) | Christian | P1 |
| 05_Intern/5.9 | 37 | A23 Kontoinhaber ☐-Felder – 2.1 § 4 Abs. 1 verweist darauf | Christian | P1 |
| 05_Intern/5.8 | 13 | „[laut C3]" | Christian | P1 |
| 01_Kunden/1.5 | 73 | „[Mehr]" – Linkziel nicht definiert | Christian | P2 |
| 02_26lab/2.1 | 145–152 | „Offene Punkte für den Anwalt (nicht Vertragsbestandteil)" – vor Unterschrift abtrennen | Dennis | P1 |
| 02_26lab/2.2 | 5, 119–126 | Vermerk + Offene Punkte – vor Unterschrift abtrennen | Dennis | P1 |
| 01_Kunden/1.0 | 25–30 | „Offene Punkte für den Anwalt" – nur Anwalt | – | – |
| 05_Intern/5.11 | 37 | „Entscheidung Dennis: ☐ … Datum: ___" | Dennis | P1 |
| 05_Intern/5.3 | 35–39 | Register ohne Daten – nach Unterschrift füllen | Dennis | P1 |

Keine Treffer für „Entwurf", „Interner Vermerk", „[…]" in den 21 Dokumenten selbst (nur im Projektplan/Status).

---

## 4. Gesetzliche Vollständigkeit (Kurzcheck)

**AVV 1.1 – Art. 28 DSGVO**

| Pflicht | Status | Fundstelle |
|---|---|---|
| Abs. 3 S. 1: Gegenstand, Dauer, Art, Zweck, Datenart, Betroffene | ✅ | § 1, § 2, Anlage 3 |
| lit. a Weisung, auch für Drittland | ✅ | § 3 Abs. 1, Abs. 10 |
| lit. b Vertraulichkeit | ✅ | § 3 Abs. 3, Anlage 5 |
| lit. c Art. 32 | ✅ | § 3 Abs. 4, Anlage 1 |
| lit. d Bedingungen Abs. 2/4 | ✅ | § 4 |
| lit. e Unterstützung Betroffenenrechte | ✅ | § 3 Abs. 7 |
| lit. f Unterstützung Art. 32–36 | ✅ | § 3 Abs. 8, § 7 |
| lit. g Löschung/Rückgabe nach Wahl | ✅ (Wahl nur implizit: Export 14 Tage, dann Löschung) | § 8 Abs. 3, 4 |
| lit. h Nachweise, Überprüfungen, Hinweis bei rechtswidriger Weisung | ✅ | § 3 Abs. 2, 9; § 9 |
| Abs. 2 allgemeine Genehmigung + Information + Widerspruch | ✅ (W15: Kündigungslösung – Anwalt J11) | § 4 Abs. 1, 2 |
| Abs. 4 Durchreichen der Pflichten | ✅ | § 4 Abs. 1; 2.1 § 1 Abs. 3 |
| Abs. 9 Schriftform/elektronisch | ✅ Checkbox + Protokoll; ❌ für die 4 Bestandsmandanten (04 D1) und ⚠️ Formularfelder (B17) | Abschluss |

**Datenschutzerklärung 4.1 – Art. 13**

| Pflicht | Status |
|---|---|
| Abs. 1 a Identität, Kontakt | ✅ Abschnitt 1 |
| b DSB | ⚠️ Platzhalter (B15); nach 5.11 keiner → Zeile streichen |
| c Zwecke, Rechtsgrundlage | ✅ je Abschnitt |
| d berechtigte Interessen | ✅ je lit.-f-Abschnitt |
| e Empfänger | ✅ Abschnitt 16 (W18: GitHub Actions fehlt) |
| f Drittland, Garantien, wo erhältlich | ⚠️ Garantien genannt, aber kein Hinweis, wo Kopie der SCC/DPF-Nachweis erhältlich („auf Anfrage an datenschutz@lymbe.ai") |
| Abs. 2 a Speicherdauer | ✅ |
| b Betroffenenrechte | ✅ Abschnitt 19 |
| c Widerruf | ✅ |
| d Beschwerderecht | ✅ |
| e Pflicht zur Bereitstellung | ✅ Abschnitt 5; ⚠️ bei Zahlung (Abschnitt 7) fehlt der Satz |
| f automatisierte Entscheidungen | ✅ Abschnitt 15 |
| Richtigkeit | ❌ Abschnitt 2/12 (B2), Abschnitt 11 Azure (B3) |

**Weitere**

| Thema | Status | Bemerkung |
|---|---|---|
| KI-VO Art. 50 Abs. 1 (Kennzeichnung) | ⚠️ | Texte in 1.5 vollständig; Einbau (5.9 A22, 04 A14) unbestätigt. Art. 50 gilt seit 02.08.2026 – ohne Einbau am 05.10. Verstoß ab Tag 1 |
| KI-VO Art. 50 Abs. 2 (maschinenlesbar) | ⚠️ | P3 (J10) – vertretbar offen |
| KI-VO Art. 4 (KI-Kompetenz) | ⚠️ | 1.6 nennt Einweisung; 5.14 P2 |
| § 25 TDDDG | ⚠️ | 5.8 schlüssig; W2 Grenzfall; Liste C3 unbestätigt (W3/P4 offen) |
| Art. 30 | ⚠️ | 5.1 vorhanden; Abs. 2 lit. a (Name/Anschrift je Auftraggeber) nur „ableitbar"; Fristfehler V6/V7 (B7); Snapshot-Frist (B6) |
| Art. 33/34 | ✅ | 5.6 vollständig inkl. Art. 33 Abs. 5; Register noch anzulegen |
| Art. 35 | ⚠️ | 5.2 Teil 1 plausibel (Anwalt J19); Teil 2 für Kundin brauchbar, B14 beheben |
| Art. 37/§ 38 BDSG | ⚠️ | 5.11 sauber hergeleitet; Entscheidung offen (D2) |
| § 203 StGB-Kette | ⚠️ | Kunde → Lymbe (§ 12 Abs. 3) → 26lab (2.1 § 3 Abs. 4, Anlage 5) → Cloud (Vertragsgeheimhaltung) schlüssig aufgebaut; **Nachweise fehlen (B12)**, Unterschriften fehlen (5.9 E), Belehrungsform offen (J17), Cloud-Stufe rechtlich offen (J2) |

---

## 5. Abgleich mit dem Dienstleisterverzeichnis

| Datenweg | Abgedeckt in | Lücke |
|---|---|---|
| A1 26lab | 1.1 Anl. 2, 2.1, 4.1, 5.1 | – |
| A2 Hetzner | 1.1, 4.1, 5.1, 3.1 | **Snapshot-Frist** nirgends (B6) |
| A3 STACKIT | überall | Sitz-Angabe abweichend (B16) |
| A4 OpenAI – Websuche | überall | Mandanten-Schalter (B4) |
| A4 OpenAI – **Werkstatt** | **nirgends** – alle Dokumente sagen Azure | B3 |
| A5 Stripe | 4.1, 5.1, 5.10, 3.1 | – (Verzeichnis A5 selbst veraltet: nennt noch js.stripe.com, obwohl 0.3 behoben – Korrektur P2) |
| A6 Cloudflare (Abgang) | 1.1 Anl. 2 Historie, 4.1 Abschnitt 20 | – |
| A7 Meta WhatsApp | 1.1 § 5 Abs. 5, 4.1, 1.3 B, 1.5, 5.1, 3.1 | **Messenger/Instagram** nur in 5.9 A13 (W17) |
| A8 GitHub – Login | 4.1 Abschnitt 6, 5.1 V2 | – |
| A8 GitHub – Wächter | 4.1 Abschnitt 9, 5.1 V7 | fehlt in 4.1 Abschnitt 16 (W18); Meldeweg offen (5.9 C4) |
| A8 GitHub – Release-Abfrage Desktop-App | **nirgends** | Server-zu-Server, ohne Personenbezug – in 5.1 V7 oder 5.4 nennen (P2) |
| A9 Let's Encrypt/ZeroSSL | 4.1 Abschnitt 10, 5.1 V8, 3.1 | – |
| A10 Spamhaus | 4.1 Abschnitt 8, 5.1 V6, 3.1 | – |
| B1–B8, B10 (eigene Container) | 5.1, 2.1 Anl. 1, AVV Anl. 1 | – |
| B9 Mailserver, Mailvolume + DKIM nur im Snapshot | 5.1 V6/V9 | Snapshot-Frist (B6) |
| C1–C8 verbundene Dienste | 1.1 § 5, 4.1 Abschnitt 14, 1.5 Nr. 8, 5.1 A5 | – |
| C9/E3 **718 Bausteine** mit Kontoanbindung | **nicht ausdrücklich** | W16; 1.5 Nr. 8 „Dialog je Dienst" braucht Metadaten für alle Bausteine – realistisch? (P2, Christian) |
| C10 Benachrichtigungsziele | 1.1 § 5, 4.1 Abschnitt 13/14, 1.3, 1.5 Nr. 3 | – |
| C11 Website-Crawl, API-Import | 1.1 § 5 Abs. 1, Anl. 1 | – |
| C11 **Logo der Hilfeseite** (fremder Server sieht IP jedes Besuchers) | nur 5.1 V4 als Hinweis | 4.1 Abschnitt 3 „Alles liegt auf unserem Server" stimmt für Hilfeseiten nicht – Satz einschränken oder P2-Spiegelung vorziehen |
| D1, D6 Widget/Demo-Speicher | 5.8, 4.1 Abschnitt 13/17, 1.3 | Liste C3 unbestätigt |
| D2–D5, D8, D9 (behoben) | 4.1 Abschnitt 20 (Cloudflare) | – |
| D7 Schriften | 4.1 Abschnitt 3 | – |
| E1 Telemetrie aus, E2 Katalog aus | 2.1 § 3 Abs. 9 (Schalter) | – |
| E4 Laufdaten 30 Tage, Sandbox | 1.1 § 8, Anl. 1 | – |
| G1 Azure (nicht geschaltet) | 5.9 A1 | Dokumente behandeln es als live (B3) |
| G2 Mistral | 5.9 A11, 3.1 C13 | – |
| G3 ee-Module (PostHog, Cloudflare-SaaS, AppSumo) | 2.1 § 3 Abs. 9 (`AP_EDITION`) | – |
| F1–F4 Bezugsquellen | – | ohne Personenbezug; 5.4 (P2) |
| H bewusst nicht eingesetzt | 4.1 Abschnitt 2, 16, 17 | – |

Zusätzlich aus dem Verzeichnis, in keinem Dokument aufgegriffen: 0.6 (ob die Nachtragung der Unterauftragsverarbeiter am 17.09. die 14-Tage-Frist ausgelöst hat – betrifft die 4 Bestandsmandanten, gehört zu 04 D1); 0.7 „Offen bleibt: die vier Bestandsmandanten haben keinen Nachweis" (= 04 D1).

---

## 6. Sprachliche und sachliche Fehler

| Datei | Stelle | Fehler | Korrektur | Prio |
|---|---|---|---|---|
| 1.1 § 12 Abs. 5, 4. Spiegelstrich | „§ 22 Abs. 2 Nr. 2 BDSG" für Sensibilisierung | § 22 Abs. 2 S. 2 Nr. 2 ist Protokollierung; Sensibilisierung ist Nr. 3 (Nr. 6 Pseudonymisierung stimmt) | „§ 22 Abs. 2 Satz 2 Nr. 3 BDSG" – Anwalt gegenprüfen | P2 |
| 1.1 § 12 Abs. 1 | „Anbahnung" als Zweck des § 22 Abs. 1 Nr. 1 lit. b BDSG | steht nicht im Gesetzeswortlaut (J1 bereits offen) | so lassen, J1 | P3 |
| 1.1 Anlage 2 Nr. 1, Anlage 4, Anlage 5 | „26LAB.IO" | sonst überall „26lab.io"; Verzeichnis „26.lab.io" | einheitlich „26lab.io" (Impressum maßgeblich) | P2 |
| 1.1 Vorspann Satz 3 | „sieht niemand deine Inhalte" | sachlich falsch (W13) | s. W13 | P2 |
| 1.1 § 6 Abs. 7 / 1.0 Nr. 1 | „Bestätigt eine nicht berechtigte Person, gilt der Vertrag mit der ersten Nutzung als genehmigt" | Genehmigung durch Nutzung eines Nichtberechtigten bindet das Unternehmen nicht automatisch (§ 177 BGB) | Anwalt | P3 |
| 1.3 Variante A, Abs. 2 | „einer Auswertung der Nutzung" | unklar, klingt nach Analytics; bei Therapiezentrum heikel | „einer Statistik, wie oft der Chat genutzt wird (ohne Profilbildung)" | P2 |
| 1.3 Variante D | „nach § 203 Abs. 4 StGB zur Geheimhaltung verpflichtet" | Abs. 4 ist die Strafnorm; Verpflichtung folgt aus Abs. 3 S. 2 i. V. m. Abs. 4 | „sind als mitwirkende Personen nach § 203 StGB zur Geheimhaltung verpflichtet" | P2 |
| 1.4 Vorlage, Grußzeile | „Dennis (Flubber Pixels UG) · Flubber Pixels UG · datenschutz@lymbe.ai" | doppelt | „Dennis [Nachname] · Flubber Pixels UG · datenschutz@lymbe.ai" | P2 |
| 1.5 Nr. 1 | „Was du hier schreibst, wird in Deutschland verarbeitet" | bei Benachrichtigungsziel Slack/Teams oder WhatsApp nicht nur Deutschland | „wird auf Servern in Deutschland verarbeitet" (das ist korrekt) | P2 |
| 1.6 Zeile 17 | Anschrift | B1 | – | P1 |
| 1.6 Zeile 56 | „Landesbeauftragten für Datenschutz NRW" | Titel: „Landesbeauftragte für Datenschutz und Informationsfreiheit NRW"; Zuständigkeit W23 | – | P2 |
| 2.1 § 1 Abs. 4, § 3 Abs. 10 | Paragrafenverweise | B8 | – | P1 |
| 2.2 § 2 Tabelle | „Flubber (Dennis)" | Dennis ist nicht Vertretungsorgan; für Zuständigkeiten ok, aber Unterschrift Marion Schagen | Zusatz „(Dennis als Datenschutz-Ansprechpartner)" | P3 |
| 4.1 Abschnitt 17 | Sitzungs-Cookie „Art. 6 Abs. 1 lit. f" | Anmeldung ist Vertragserfüllung | „lit. b (Anmeldung) bzw. lit. f (CSRF-Schutz)" | P2 |
| 4.1 Abschnitt 1 | „Verantwortlich ... auf lymbe.ai und im Lymbe-Portal" | Teil B sagt: im Portal sind Kunden verantwortlich | „... soweit Teil A dieser Erklärung" | P2 |
| 4.1 Abschnitt 13 | „Auswertung für den Kunden" | unverständlich für Besucher (W11) | konkret benennen | P2 |
| 5.1 V6 | „Mail-Logs 14" | Einheit fehlt | „14 Tage" | P1 (mit B7) |
| 5.3 Zeile 23 | § 42 BDSG „bis zu drei Jahren" | B9 | – | P1 |
| 5.9 Kopf | „in der § 12 des Kunden-AVV" | Grammatik | „im § 12" | P2 |
| 5.9 A10 | „§ 3 Abs. 9" | § 3 Abs. 10 | – | P2 |
| 00_Projektplan Zeile 42–44 | E9, E10, E8 | Reihenfolge | – | P2 |
| 3.1 B7 | GitHub „Login" unter DPA | W19 | – | P3 |

Kundengerichtete Texte (1.1 Vorspann, 1.3, 1.5, 1.6, 4.1) sind sonst verständlich und im Ton passend. Zwei Stellen, die Leser stolpern lassen: 1.1 Vorspann „Mitwirkende Person – so nennt § 203 StGB Dienstleister, denen ein Therapeut oder Anwalt Geheimnisse anvertrauen darf" (gut); 1.3 D „Lymbe AI und der technische Betreiber" – der „technische Betreiber" ist für Patienten unerklärt → „und ihr technischer Dienstleister 26lab.io, Mettmann".

---

## 7. Urteil

**An den Anwalt: ja, mit dieser Prüfung als Beilage.** Das Set ist strukturell vollständig (Art. 28, Art. 13, Art. 30, Art. 33/34, § 203-Kette, § 25 TDDDG sind alle adressiert), die Rollenlogik ist konsistent und die offenen Rechtsfragen sind sauber in 04 Abschnitt C gesammelt. Der Anwalt sollte B5, W9, W15 und die § 203-Cloud-Stufe zuerst ansehen.

**An die Kundin: noch nicht.** Zwei Dokumente enthalten echte Fehler (1.6 falsche Anschrift, 5.2 Widerspruch), die Datenschutzerklärung enthält eine falsche Tatsachenbehauptung, und der AVV beschreibt für Werkstatt, Spracheingabe, Websuche-Schalter und Sicherungen einen Zustand, den das Verzeichnis vom 17.09. nicht bestätigt. Der eigene Grundsatz „Vertrag = Maschine" ist für diese vier Punkte noch nicht erfüllt.

**Vor Übergabe an die Kundin, nach Wichtigkeit:**

1. **Christian: 5.9 Block A/B bestätigen** – mindestens A1 (Azure), A2 (7 Tage) + Snapshot-Frist, A3 (90-Tage-Lauf), A7/A10 (Schalter Selbstlernen/Websuche je Mandant mit Protokoll), A12 (Speech), A22 (KI-Kennzeichnung), B1 (Suchbegriff-Test), B5 (Zugriffsprotokoll). Was nicht bestätigt wird, wird im AVV geändert (B3, B4, B6).
2. **1.6 Zeile 17 korrigieren** (B1) und 1.3 D / 1.6 nochmal gegen 1.1 § 12 lesen.
3. **4.1 Abschnitt 2/12 umformulieren**, Vermerk und DSB-Platzhalter entfernen (B2, B15).
4. **AVV § 3 Abs. 10 / Anlage 2 Nr. 5 / 4.1 / 1.5 Nr. 6** als Maßnahme statt Garantie formulieren (B5) – eine Textänderung, vier Dateien.
5. **Fristen bereinigen**: 5.9 A6 teilen, 5.1 V6/V7 (B7); Snapshot-Zeile (B6).
6. **2.1 Verweise** (B8) und **5.3 Freigabe + Strafmaß** (B9) korrigieren, dann unterschreiben: 5.3, Anlage 5, 2.1, 2.2 – A23 vorher ausfüllen, sonst verweist 2.1 § 4 auf ein leeres Feld.
7. **1.2 fertigstellen**: AGB-Fassung klären (B10), D5-Werte eintragen, Vermerk/Checkliste abtrennen; Sie-Fassung für 1.5 (B11).
8. **AVV-Abschluss mit der Kundin auf Papier** (K1), solange das Workspace-Formular Firma/Anschrift/Vertretung nicht abfragt (B17); § 12-Telefonnummer der Kundin aufnehmen (B7 in 5.9).
9. **5.2 Abschnitt 2.5** bereinigen (B14), dann DSFA-Vorlage und 1.3 D / 1.6 übergeben; Rückmeldung „eingesetzt" vor Freischaltung des Widgets abwarten (1.2 § 5 Abs. 3).
10. **03_Status_fuer_Dennis.md** archivieren oder aktualisieren – es widerspricht dem aktuellen Stand (1.7, Anlage A/B) und würde beim Anwalt Verwirrung stiften.

P2 vor breitem Verkauf (zusätzlich zu 00): W8, W10–W14, W16–W18, W20, W22, W23; 718-Bausteine-Dialog; Hilfeseiten-Logo; Verzeichnis A5/Azure Speech/Snapshots korrigieren; Bestandsmandanten (D1).
