# Ergebnis Gegenprüfung Teil A – STACKIT und Hetzner (A1–A5, A10, A11)

**Prüfer:** Claude (Vier-Augen für Dennis) · **Datum:** 11.10.2026
**Geprüft gegen:** Textfassungen in `gegenpruefung/text/` (aus den PDFs extrahiert). Seitenangaben nach den Fußzeilen der PDFs. Unterschriften, Stempel oder Grafiken sind in den Textfassungen nicht sichtbar – dazu kann ich nichts sagen.
**Nicht vorliegend:** STACKIT-Produktseite, STACKIT-Zertifikate (ISO/C5), Hetzner-C5-Testat, Hetzner-Kontoansicht (Serverstandort). Aussagen, die sich darauf stützen, sind „nicht prüfbar“.

---

## 1. Übersichtstabelle

| Nr | Aussage (Kurzform) | Fundstelle im Vertrag | Wörtlich dort (gekürzt) | Urteil | Von 3.1 / 5.9 gedeckt? |
|---|---|---|---|---|---|
| A1 | STACKIT-AVV v2.4.2 erfüllt Art. 28 Abs. 3 vollständig (Ziff. 2.2/Anlage 1, 2.4, 3, 5, 6, 7, 8, 9, 10, 11) | AVV S. 1–7, Anlage 1 S. 9, Anlage 2 S. 10–11 – Einzelnachweis je Buchstabe in Abschnitt 2 | Ziff. 2.1: „Der Auftragnehmer verarbeitet die Auftraggeber-Daten im Auftrag (bzw., soweit der Auftraggeber selbst Auftragsverarbeiter ist, im Unterauftrag) und nach Weisung des Auftraggebers i.S.v. Art. 28 DSGVO“ | **bestätigt mit einer Einschränkung** (lit. g: nur Löschung, keine Rückgabe-Option nach Wahl des Auftraggebers; Ziff. 10.1) | 3.1 D: Ziffern stimmen alle. „vollständig“ ist leicht überzeichnet wegen lit. g (siehe unten); praktisch unerheblich, weil AI Model Serving nichts dauerhaft speichert |
| A2 | „does not collect or evaluate any customer data other than billing-relevant data“; Kundendaten „not stored permanently“ – damit „kein Training“ belegt | Leistungsschein v1.3, „High level service description“ S. 2; Annex Exportability S. 4, Zeile „Customer data (database content)“ | „When using the AI Model Serving Service, STACKIT does not collect or evaluate any customer data other than billing-relevant data.“ / „Customer data is not stored permanently. The e-mail and subject ID are stored temporarily (30 days) in the logs of the service“ | **Zitate bestätigt** (v1.3 und v1.4 wortgleich). **„kein Training“ ist Ableitung:** das Wort Training/Modelltraining kommt weder im AVV noch in den Leistungsscheinen noch in den TOMs vor | 3.1 D und 5.9 B2 sagen selbst „AVV nennt Training nicht“ und „über den Leistungsschein“ – das ist ehrlich. Unerwähnt bleibt: E-Mail und Subject-ID werden 30 Tage in Service-Logs gehalten. Die Produktseite („weder gespeichert noch zum Training“) liegt nicht vor → nicht prüfbar |
| A3 | AVV Ziff. 2.3 erlaubt „anonymisierte Nutzungsdaten für eigene Zwecke“ – betrifft Nutzungs-, nicht Inhaltsdaten | AVV Ziff. 2.3, S. 1–2 | siehe Volltext in Abschnitt 4 | **bestätigt**, mit Zusatz: 2.3 erlaubt auch **nicht anonymisierte** Nutzungsdaten für eigene Zwecke „im Rahmen des datenschutzrechtlich Zulässigen (insbesondere etwa zur Erfüllung von gesetzlichen Pflichten)“ – 3.1 nennt das nicht | Die Lesart „Nutzungs-, nicht Inhaltsdaten“ stützt sich auf die Definition „erfasst … die Nutzung der STACKIT Services durch den Auftraggeber“. Eine ausdrückliche Abgrenzung zu Prompt-Inhalten steht nicht im AVV; sie ergibt sich erst zusammen mit dem Leistungsschein („does not collect or evaluate any customer data other than billing-relevant data“) |
| A4 | Standort laut AVV nur EU/EWR (Ziff. 2.5); Deutschland nur über Leistungsschein/Region eu01 | AVV Ziff. 2.5 S. 2; Anlage 2 S. 10–11; Leistungsschein S. 4 | 2.5: „Die Verarbeitung der Auftraggeber-Daten durch den Auftragnehmer findet innerhalb der Europäischen Union oder in einem anderen Vertragsstaat des Abkommens über den Europäischen Wirtschaftsraum (EWR) statt.“ | **EU/EWR bestätigt. „Deutschland über Leistungsschein“ abweichend:** „eu01“ steht im Leistungsschein nur als Teil einer Dokumentations-URL (`docs.api.eu01.stackit.cloud`), ohne Aussage zu Land oder Rechenzentrum. „Deutschland“ kommt im AVV nur in Anschriften vor (Auftragnehmer Bad Friedrichshall; Anlage 2) | 3.1 D „Rechenzentrum der Region eu01 laut Leistungsschein/Produktseite in Deutschland“: der Leistungsschein gibt das **nicht** her, die Produktseite liegt nicht vor. Richtig ist in 3.1: „nicht ausdrücklich Deutschland“ und „Unterauftragnehmer (Anlage 2) alle in der EU“ (DE, NL, BG, RO, ES) |
| A5 | Zertifikate: TOMs nur „angelehnt an ISO/IEC 27001“, BSI C5 nicht genannt | TOMs Kap. 2 Nr. 6.1.1 (S. 11); AVV Ziff. 11.7 (S. 7) | 6.1.1: „Die Prozesse und Prozeduren der Informationssicherheit sind als Teil des Informationssicherheitsmanagementsystems (ISMS) definiert, angelehnt an ISO/IEC 27001 ff.“ | **bestätigt.** „C5“ kommt in AVV und TOMs nicht vor. AVV 11.7 nennt ISO 27001 / BSI-Grundschutz nur als mögliche Nachweisform, nicht als vorhandenes Zertifikat | Gedeckt. Zusatz: Die TOMs sind die „Standard-TOMs“ der **Schwarz Gruppe, Version 1.0** – kein STACKIT-spezifisches Dokument; projektspezifische Abweichungen sollen laut Einleitung in gesonderten Dokumenten stehen, die nicht vorliegen. Zeile 3.1 A Nr. 3 „Zertifikate (ISO 27001, C5)“ bleibt damit offen |
| A10 | Hetzner-AVV v1.2 (16.02.2026) mit 26Lab.io erfüllt Art. 28 Abs. 3 vollständig; Vertraulichkeit/§ 203 | AV-Vertrag S. 1–11, Anlagen 1–3 S. 12–27 – Einzelnachweis in Abschnitt 3 | § 5 Nr. 2: „Der Auftragnehmer setzt bei der Durchführung der Arbeiten nur Beschäftigte ein, die auf die Vertraulichkeit verpflichtet und zuvor mit den für sie relevanten Bestimmungen zum Datenschutz vertraut gemacht wurden. Diese Vertraulichkeitsverpflichtung besteht auch nach Beendigung des Auftrags fort.“ | **Art. 28 Abs. 3 bestätigt** (alle acht Buchstaben belegt). **§ 203 StGB: nicht enthalten.** Vertragspartner 26Lab.io bestätigt – aber als **„Verantwortlicher im Sinne der DSGVO“** (Kopf S. 1, § 1 Abs. 3), nicht als Auftragsverarbeiter | 3.1 D sagt „bitte gegenlesen“ – gedeckt. **Nicht gedeckt:** die Bemerkung „passt zur Kette Flubber → 26lab → Hetzner“ – der Vertrag kennt diese Kette nicht, er behandelt 26Lab als Verantwortlichen (Details Abschnitt 5) |
| A11 | ISO/IEC 27001:2022, SOCOTEC, ZN-2025-35 V 1.1, gültig bis 26.09.2028, deckt Nürnberg und Falkenstein ab | Zertifikat S. 1 und Zertifikatsanhang | „Gültigkeit Zertifikat: 27.09.2025 - 26.09.2028“, „Zertifikatsnummer: ZN-2025-35 V 1.1“, Geltungsbereich: „Der Anwendungsbereich des lnformationssicherheitsmanagementsystems umfasst alle Hosting-Dienstleistungen und die Rechenzentren.“ Standorte: Nürnberg, Falkenstein/Vogtland, Tuusula (Finnland) | **bestätigt** (plus Standort 3 Tuusula, das 3.1 D bereits nennt) | Gedeckt. Hinweis: Hetzner Anlage 2 (S. 25) behauptet zusätzlich „§ 8a BSI-KritisV und BSI C5 Typ 2 Testat“ – dafür liegt kein Nachweis vor |

---

## 2. A1 – Art. 28 Abs. 3 DSGVO Buchstabe für Buchstabe gegen den STACKIT-AVV v2.4.2

| Art. 28 Abs. 3 | Anforderung | STACKIT-AVV | Wörtlich (gekürzt) | Urteil |
|---|---|---|---|---|
| Satz 1 | Gegenstand, Dauer, Art, Zweck, Datenarten, Kategorien Betroffener | Ziff. 1 (Gegenstand), 2.2 + Anlage 1 (Art, Zweck, Datenarten, Betroffene), 2.4 (Dauer) | 2.4: „Die Dauer der Verarbeitung entspricht der Laufzeit des Hauptvertrages“; Anlage 1: „Bestimmungsgemäß ist die Art der Daten nicht beschränkt“ | ✅ |
| lit. a | Nur auf dokumentierte Weisung; Mitteilung bei gesetzlicher Pflicht | Ziff. 2.1, 3.1, 3.2 | 3.1: „Der Auftragnehmer verarbeitet die Auftraggeber-Daten gemäß den Weisungen des Auftraggebers, sofern der Auftragnehmer nicht gesetzlich zu einer anderweitigen Verarbeitung verpflichtet ist. In letzterem Fall teilt der Auftragnehmer dem Auftraggeber diese rechtlichen Anforderungen vor der Verarbeitung mit“ | ✅ (Hinweis: 3.2 – Weisungen sind „grundsätzlich abschließend“ im Vertrag und in der Dienstkonfiguration festgelegt; Einzelweisungen nur über den Hauptvertrag) |
| lit. b | Vertraulichkeitsverpflichtung der Personen | Ziff. 5 | „Der Auftragnehmer hat alle Personen, die Auftraggeber-Daten verarbeiten, bezüglich der Verarbeitung von Auftraggeber-Daten zur Vertraulichkeit zu verpflichten.“ | ✅ (ein Satz; keine Nachwirkung, keine Form genannt) |
| lit. c | Maßnahmen nach Art. 32 | Ziff. 6.1, 6.2 | „Der Auftragnehmer wird gemäß Art. 32 DSGVO erforderliche, geeignete technische und organisatorische Maßnahmen ergreifen … verpflichtet sich, die unter https://stackit.com/de/agb/cloud-services … abrufbaren technischen und organisatorischen Maßnahmen umzusetzen“ | ✅ (TOMs nur per Link, änderbar nach 6.2) |
| lit. d | Bedingungen für weitere Auftragsverarbeiter (Abs. 2 und 4) | Ziff. 7.1–7.5, Anlage 2 | 7.1: „allgemeine Genehmigung“; 7.2: Information per E-Mail, Einspruch „nur aus wichtigem … Grund“ innerhalb 14 Tagen; 7.4: „Der Vertrag zwischen dem Auftragnehmer und dem weiteren Auftragsverarbeiter muss letzterem dieselben Pflichten auferlegen“ | ✅ |
| lit. e | Unterstützung bei Betroffenenrechten | Ziff. 8.1–8.4 | 8.1: „… im Rahmen des Zumutbaren dabei unterstützen, seiner Pflicht zur Beantwortung von Anträgen auf Wahrnehmung der ihnen zustehenden Rechte betroffener Personen nachzukommen.“ | ✅ (8.3/8.4 gegen Kostenerstattung) |
| lit. f | Unterstützung Art. 32–36 | Ziff. 6 (Art. 32), 9.1 (Art. 33, 34), 9.2 (Art. 35, 36) | 9.1: „… wird der Auftragnehmer den Auftraggeber unverzüglich über etwaige meldepflichtige Ereignisse in seinem Verantwortungsbereich informieren“; 9.2: „… bei … Datenschutz-Folgenabschätzungen und … Konsultationen der Aufsichtsbehörden nach Art. 35, 36 DSGVO unterstützen“ | ✅ (gegen Kostenerstattung; keine Frist für die Meldung außer „unverzüglich“) |
| lit. g | Nach Abschluss nach Wahl des Verantwortlichen löschen **oder zurückgeben** | Ziff. 10.1, 10.2 | „Der Auftragnehmer wird die Auftraggeber-Daten nach Beendigung dieses Vertrages löschen, sofern nicht gesetzlich eine Verpflichtung … zur weiteren Speicherung … besteht. … erstellt über die Löschung … ein Löschprotokoll“ | ⚠ **nur Löschung**, kein Wahlrecht Rückgabe. Für AI Model Serving praktisch ohne Folge (nichts wird dauerhaft gespeichert, Leistungsschein), formal aber keine vollständige Abbildung von lit. g |
| lit. h | Informationen zum Nachweis, Überprüfungen/Inspektionen; Hinweis auf rechtswidrige Weisung | Ziff. 11.1–11.7; Ziff. 3.3 | 11.1: „… alle erforderlichen und beim Auftragnehmer vorhandenen Informationen zum Nachweis der Einhaltung seiner Pflichten … zur Verfügung stellen“; 11.2: „… zu überprüfen; einschließlich durch Inspektionen“; 3.3: „Ist der Auftragnehmer der Ansicht, dass eine Weisung … verstößt, ist er nach einer entsprechenden Mitteilung an den Auftraggeber berechtigt aber nicht verpflichtet, die Ausführung … auszusetzen“ | ✅ (Inspektion: eine pro Jahr, zwei Wochen Vorlauf, Mo–Fr 10–18 Uhr, Ersatz durch Prüfbericht/Zertifikat nach 11.7 möglich) |

**Fazit A1:** Die in 3.1 D genannten Ziffern stimmen alle. „Vollständig“ trifft mit der Einschränkung bei lit. g zu (Löschung ohne Rückgabe-Option). Positiv: Ziff. 2.1 sieht ausdrücklich den Fall vor, dass der Auftraggeber (Flubber) selbst Auftragsverarbeiter ist – das deckt die Kette Kunde → Flubber → STACKIT ab.

---

## 3. A10 – Art. 28 Abs. 3 DSGVO Buchstabe für Buchstabe gegen den Hetzner-AV-Vertrag v1.2

| Art. 28 Abs. 3 | Anforderung | Hetzner-AVV | Wörtlich (gekürzt) | Urteil |
|---|---|---|---|---|
| Satz 1 | Gegenstand, Dauer, Art, Zweck, Datenarten, Kategorien | § 1 Abs. 1 und 4 (Gegenstand/Dauer über Hauptvertrag), § 2 + Anlage 1 (S. 12) | Anlage 1: „Umfang, Art und Zweck … Ergeben sich direkt aus dem Hauptvertrag.“ Art der Daten: „Personenstammdaten, Kommunikationsdaten (z.B. Telefon, E-Mail), Vertragsstammdaten, Protokolldaten, Vertragsabrechnungs- und Zahlungsdaten“; Betroffene: „Kunden und Interessenten … Mitarbeiter und Lieferanten des Auftraggebers“ | ✅ formal. ⚠ Anlage 1 ist die Hetzner-Vorlage, nicht „vom Auftraggeber ausgefüllt“ (so verlangt es § 2). **Besondere Kategorien (Gesundheitsdaten, Pilotkundin Therapiezentrum) stehen nicht drin**; Betroffene „Kunden des Auftraggebers“ erfasst Endkunden von Flubber nur mittelbar |
| lit. a | Nur auf dokumentierte Weisung | § 10 Abs. 1–2 | „Der Auftragnehmer und jede ihm unterstellte Person, die Zugang zu personenbezogenen Daten hat, dürfen die Daten … ausschließlich im Rahmen des Auftrags und gemäß den Weisungen des Auftraggebers verarbeiten, es sei denn, dass sie gesetzlich zur Verarbeitung verpflichtet sind“ | ✅ |
| lit. b | Vertraulichkeit | § 5 Nr. 2; Anlage 2 Kap. 7 (S. 20) | § 5 Nr. 2 (Zitat oben, Tabelle 1); Anlage 2: „Verpflichtungserklärung der Hetzner-Mitarbeitenden vor Tätigkeitsbeginn zur datenschutzkonformen Verarbeitung personenbezogener Daten“ | ✅ |
| lit. c | Art. 32 | § 4 Abs. 1–4, § 5 Nr. 3, Anlage 2 | § 4 Abs. 1: „… technische und organisatorische Maßnahmen, die einen angemessenen Schutz der Daten des Auftraggebers gewährleisten und den Anforderungen der Datenschutz-Grundverordnung (Art. 32 DSGVO) entsprechen“ | ✅ (Anlage 2 enthalten, 13 Seiten; Hinweis S. 14: bei Cloud/Dedicated Servern liegt „die Verantwortung für die Verwaltung, Wartung und Sicherheit der Serverinfrastruktur vollständig beim Auftraggeber“) |
| lit. d | Unterauftragsverarbeiter | § 7 Abs. 1–5, Anlage 3 (S. 26) | § 7 Abs. 2: „… obliegt es dem Auftragnehmer, seine datenschutzrechtlichen Pflichten aus diesem Vertrag dem Subunternehmer zu übertragen“; Abs. 3: Information vorab, Widerspruch 14 Tage „aus wichtigem datenschutzrechtlichem Grund“, Sonderkündigungsrecht | ✅ |
| lit. e | Unterstützung Betroffenenrechte | § 5 Nr. 7, § 9 Abs. 1 c | „Der Auftragnehmer unterstützt den Auftraggeber angemessen bei der Erfüllung von Anfragen und Ansprüche betroffener Personen gemäß Kapitel III der DSGVO.“ | ✅ |
| lit. f | Unterstützung Art. 32–36 | § 9 Abs. 1 a–e, § 5 Nr. 8 (Meldung mit Mindestinhalt) | „Der Auftragnehmer unterstützt den Auftraggeber bei der Einhaltung der in den Artikeln 32 bis 36 der DSGVO genannten Pflichten.“ | ✅ (vergütungspflichtig nach § 9 Abs. 2 / § 12, außer bei eigenem Verstoß) |
| lit. g | Löschung oder Rückgabe nach Wahl | § 11 Abs. 2–4 | „Daten, Datenträger sowie sämtliche Dokumente sind nach Auftragsende auf Verlangen (schriftlich oder in Textform) des Auftraggebers entweder herauszugeben, sofern sie im Eigentum des Auftraggebers sind, oder zu löschen.“ | ✅ (Wahlrecht vorhanden; Hinweis: „auf Verlangen“ – ohne Verlangen keine automatische Pflicht aus § 11; Löschverfahren für Festplatten in Anlage 2 Kap. 4) |
| lit. h | Nachweise, Audits, Remonstration | § 8 Abs. 1–4; § 10 Abs. 3 | § 8 Abs. 3: „… lässt die technischen und organisatorischen Maßnahmen (TOMs) … mindestens einmal jährlich, durch eine unabhängige, fachlich qualifizierte Stelle überprüfen … gemäß Art. 28 Abs. 3 Satz 2 lit. h DSGVO“; § 10 Abs. 3: „… unverzüglich zu informieren, wenn er der Meinung ist, eine Weisung verstoße gegen die DSGVO … [Remonstrationspflicht]“ | ✅ |
| Drittland | (Art. 28 Abs. 3 lit. a, Kap. V) | § 3 Abs. 1–4; Anlage 3 Hinweis | § 3 Abs. 1: „… findet ausschließlich in einem Mitgliedstaat der Europäischen Union oder in einem anderen Vertragsstaat des … EWR statt.“ Anlage 3: „Soweit Sie sich für einen Serverstandort in der EU entschieden haben, werden Ihre Serverdaten ausschließlich innerhalb der EU verarbeitet. Supportdienstleistungen erfolgen für alle Serverstandorte innerhalb der EU.“ | ✅ (Anlage 3 listet Subunternehmer in USA/Singapur nur für die dortigen Serverstandorte; Hetzner Finland Oy für Finnland) |

**Fazit A10:** Art. 28 Abs. 3 ist im Hetzner-AVV vollständig abgebildet – bestätigt. Was 3.1 D bisher offen lässt („bitte gegenlesen“), kann auf „ja“ gesetzt werden, mit den drei Hinweisen aus Abschnitt 5 (Rolle 26Lab, Anlage 1 ohne besondere Kategorien, Unterschrift).

---

## 4. Zusatzfragen

### 4.1 § 203 StGB / Berufsgeheimnis / Geheimhaltung der Mitarbeiter

**STACKIT – nicht enthalten.** Weder „203“, „Berufsgeheimnis“ noch „Geheimhaltung“ (bezogen auf Mitarbeiter) kommen in AVV oder TOMs vor. Vorhanden ist nur:
- AVV Ziff. 5 (S. 3): „Der Auftragnehmer hat alle Personen, die Auftraggeber-Daten verarbeiten, bezüglich der Verarbeitung von Auftraggeber-Daten zur Vertraulichkeit zu verpflichten.“
- TOMs 1.2.4 (S. 5): „Mitarbeiter der IT sind gemäß Anstellungsvertrag auf das Fernmeldegeheimnis und das Datengeheimnis verpflichtet.“
- TOMs 7.1.1 (S. 12): „Mitarbeiter sind auf das Datengeheimnis verpflichtet und werden angemessen, z.B. durch Schulungs- und Sensibilisierungsmaßnahmen, zu den Themen Datenschutz und Informationssicherheit informiert.“
- „Geheimhaltung“ taucht nur in Ziff. 11.3/11.6 auf – dort geht es um Betriebsgeheimnisse von STACKIT bei Inspektionen und um die Verschwiegenheit eines vom Auftraggeber beauftragten Prüfers („es sei denn, dass der Dritte einer beruflichen Verschwiegenheitsverpflichtung unterliegt“). Das ist keine Mitarbeiter-Verpflichtung.

**Hetzner – nicht enthalten.** Keine Fundstelle zu „203“ oder „Berufsgeheimnis“. Vorhanden:
- § 5 Nr. 2 (S. 4): Beschäftigte „auf die Vertraulichkeit verpflichtet … Diese Vertraulichkeitsverpflichtung besteht auch nach Beendigung des Auftrags fort.“
- Anlage 2 Kap. 7 (S. 20): „Verpflichtungserklärung der Hetzner-Mitarbeitenden vor Tätigkeitsbeginn zur datenschutzkonformen Verarbeitung personenbezogener Daten“; „Verpflichtungserklärung externer Personen vor Tätigkeitsbeginn zu Verschwiegenheit und Umsetzung von TOMs (bei Bedarf)“.
- § 8 Abs. 4 (S. 7) nennt „berufsrechtliche oder gesetzliche Verschwiegenheitspflichten“ – aber nur als Grund, von einem vom Auftraggeber beauftragten Prüfer eine Verschwiegenheitserklärung zu verlangen.

Die Aussage in Teil C Nr. 1 („Keiner der beiden Verträge enthält eine § 203-Klausel“) ist damit für STACKIT und Hetzner bestätigt. Ob die allgemeine Vertraulichkeit für § 203 Abs. 4 StGB („mitwirkende Personen“) reicht, ist eine Anwaltsfrage – hier nur die Feststellung: eine ausdrückliche Verpflichtung nach § 203 StGB fehlt in beiden Verträgen.

### 4.2 STACKIT – Wo steht Land/Region?

- **AVV Ziff. 2.5 (S. 2):** nur „innerhalb der Europäischen Union oder in einem anderen Vertragsstaat des … EWR“. Absatz 2 erlaubt Verarbeitung außerhalb des EWR, „wenn die Parteien eine dahingehend ausdrückliche Vereinbarung treffen (z.B. bei Abschluss eines Abonnements, in der … Servicebeschreibung oder in dem zugehörigen Leistungsschein)“ – in den Leistungsscheinen v1.3/v1.4 steht keine solche Vereinbarung.
- **Anlage 2 (S. 10–11):** 14 weitere Auftragsverarbeiter mit Anschriften in Deutschland (10), Niederlande (1), Bulgarien (1), Rumänien (1), Spanien (2 Einträge, Barcelona). Alle EU. Keine Aussage zum Rechenzentrum.
- **Leistungsschein v1.3/v1.4:** „eu01“ nur in der URL `https://docs.api.eu01.stackit.cloud/documentation/model-serving/version/v1#tag/Models` (Annex, Zeile „System properties“). Keine Region, kein Land, kein Rechenzentrum genannt.
- **„Deutschland“** steht im AVV ausschließlich in Anschriften (Auftragnehmer: Schwarz Digits Cloud GmbH & Co. KG, Bad Friedrichshall; Anlage 2). In den Leistungsscheinen und TOMs gar nicht.

**Folge:** Die Aussage „Deutschland“ ist in keinem der vorliegenden STACKIT-Dokumente vertraglich belegt. Offener Punkt C 2 aus der Aufgabenliste bleibt bestehen; eine Produktseite wäre Marketing, kein Vertrag.

### 4.3 STACKIT Leistungsschein v1.3 vs. v1.4 (gültig ab 06.11.2026)

Vollständiger Textvergleich (diff). Änderungen:

| Thema | v1.3 | v1.4 | Datenschutzrelevant? |
|---|---|---|---|
| Speicherung / „does not collect or evaluate“ / „not stored permanently“ / 30-Tage-Log von E-Mail und Subject-ID | vorhanden | **wortgleich** | nein (unverändert) |
| Training | nicht erwähnt | nicht erwähnt | – |
| Region / Standort | nicht erwähnt (nur URL eu01) | identisch | – |
| Backup | „Customer requests are not backed up.“ | „A backup of Customer requests does not take place.“ | nein (nur Umformulierung) |
| SLA | 99,5 % | 99,5 %; **neu:** „Private Preview and Public Preview models are excluded from any SLA and availability agreements.“ | nur mittelbar (Verfügbarkeit) |
| Laufzeiten / Deprecation | 6 Monate Ankündigung, 3 Monate bei Nachfolgemodell | gleich; **neu:** „Private Preview and Public Preview models may be discontinued, modified, or changed at any time without prior notice.“ „best effort“ | nur falls Preview-Modelle genutzt würden – dann wäre ein Modellwechsel ohne Ankündigung möglich (Prüfen: gpt-oss-20b ist kein Preview-Modell?) |
| Zusatzbedingungen | Link zum Leistungsschein Compute Engine GPU (stackit.de/en/…) | Verweis auf Leistungsschein Compute Engine GPU unter stackit.com/en/gtc/cloud-services | nein (Link geändert; der GPU-Leistungsschein selbst liegt nicht vor) |
| Logging | Annex „Log data“ identisch | identisch | – |

**Fazit:** Die in 3.1 D behauptete Gleichlautung („v1.4 ab 06.11.2026 gleichlautend“) stimmt für alle datenschutzrelevanten Passagen. Neu sind nur die Preview-Regelungen und ein geänderter Link.

### 4.4 STACKIT AVV Ziff. 2.3 – Volltext

> „2.3. Außerdem erfasst der Auftragnehmer die Nutzung der STACKIT Services durch den Auftraggeber (nachfolgend „Nutzungsdaten“ genannt, die ebenfalls Auftraggeber-Daten im Sinne dieses Vertrages darstellen) und verarbeitet diese Nutzungsdaten im Auftrag des Auftraggebers zum Zwecke der Erfüllung des Vertrags, der bedarfsgerechten Gestaltung der STACKIT Services, der Bereitstellung von Nutzungsübersichten und -analysen, der Gewährleistung von IT- und Datensicherheit, der Fehlerdiagnose und -behebung sowie der Optimierung und Weiterentwicklung der STACKIT Services. Zu diesem Zweck wird der Auftragnehmer die Nutzungsdaten ebenfalls anonymisieren und in dieser Form verarbeiten. Dem Auftragnehmer bleibt es vorbehalten, anonymisierte Nutzungsdaten für eigene Zwecke zu verarbeiten. Die Parteien stimmen darin überein, dass dieser Vertrag nicht auf die Verarbeitung von anonymisierten Nutzungsdaten Anwendung findet.
> Eine Verarbeitung von Nutzungsdaten in nicht anonymisierter Form für eigene Zwecke des Auftragnehmers bleibt im Rahmen des datenschutzrechtlich Zulässigen (insbesondere etwa zur Erfüllung von gesetzlichen Pflichten) hiervon unberührt.“

(AVV v2.4.2, S. 1–2)

Hinweise:
1. „Nutzungsdaten“ ist definiert als Erfassung „der Nutzung der STACKIT Services durch den Auftraggeber“ – also Nutzungsvorgänge, nicht Inhalte. Eine ausdrückliche Aussage, dass Prompts/Antworten **keine** Nutzungsdaten sind, fehlt. Die Lesart in 3.1 („Nutzungs-, nicht Inhaltsdaten“) ist vertretbar, wird aber erst durch den Leistungsschein („does not collect or evaluate any customer data other than billing-relevant data“) gestützt.
2. Der zweite Absatz (nicht anonymisierte Nutzungsdaten für eigene Zwecke im gesetzlich zulässigen Rahmen) fehlt in 3.1 und 5.9 B2.
3. Zweck „Optimierung und Weiterentwicklung der STACKIT Services“ auf Basis anonymisierter Nutzungsdaten – das ist kein Modelltraining mit Inhalten, sollte aber bekannt sein, wenn Kunden „keine Nutzung für Produktverbesserung“ zugesagt wird.

### 4.5 Hetzner – Vertragspartner und Kette Flubber → 26Lab → Hetzner

- **Vertragspartner bestätigt:** Kopf S. 1: „26Lab.io, Hasselbeckstr. 37, 40822 Mettmann, DEUTSCHLAND, K0391344926 – Verantwortlicher im Sinne der DSGVO, im Folgenden Auftraggeber –“ und „Hetzner Online GmbH … – Auftragsverarbeiter im Sinne der DSGVO, im Folgenden Auftragnehmer –“. Flubber Pixels kommt im Vertrag nicht vor.
- **Rolle von 26Lab laut Vertrag:** „Verantwortlicher“. § 1 Abs. 3: „Der Auftraggeber gilt als „Verantwortlicher“ im Sinne des Art. 4 Abs. 7 DSGVO.“ Anders als STACKIT (Ziff. 2.1 „soweit der Auftraggeber selbst Auftragsverarbeiter ist, im Unterauftrag“) sieht der Hetzner-Vertrag **keinen** Fall vor, in dem der Auftraggeber selbst Auftragsverarbeiter eines Dritten ist.
- **Regelung zur Unterbeauftragung:** § 7 regelt nur Hetzners eigene Subunternehmer (Anlage 3). Es gibt keine Klausel, die Hetzner ausdrücklich als Unter-Unterauftragsverarbeiter von Flubber zulässt – aber auch keine, die es verbietet. Die Kette Flubber → 26Lab → Hetzner ist damit vertraglich **nicht abgebildet**, nur nicht ausgeschlossen. Sie muss über den Partnerschaftsvertrag 2.1 / AVV Anlage 5 (Flubber ↔ 26Lab) und Art. 28 Abs. 4 DSGVO getragen werden; dort müsste 26Lab verpflichtet sein, Hetzner dieselben Pflichten aufzuerlegen – was durch den vorliegenden Hetzner-AVV materiell der Fall ist.
- **Unterschrift:** S. 11 zeigt im Text nur „Gunzenhausen, den 05.10.2026“ auf Hetzner-Seite; das Feld des Auftraggebers ist leer („, den“). Ob 26Lab den Vertrag im Kundenkonto per Klick angenommen hat, ist aus dem PDF-Text nicht erkennbar → nicht prüfbar; 3.1 A Nr. 2 nennt den Weg „Klick, PDF-Download“.
- **Serverstandort Nürnberg / Storage Box Falkenstein:** steht nicht im AVV (nur „Serverstandort in der EU“ als Bedingung in Anlage 3). Belegbar nur über Kontoansicht/Produktbeschreibung → nicht prüfbar. Das ISO-Zertifikat deckt beide Standorte ab.
- **3.1 D, Spalte Bemerkung** („passt zur Kette Flubber → 26lab → Hetzner, AVV Anlage 2 Nr. 2“): die Feststellung des Vertragspartners stimmt; die Formulierung „passt zur Kette“ ist aus dem Hetzner-Vertrag nicht herleitbar (siehe oben). Empfehlung: Bemerkung ergänzen um „Hetzner-AVV behandelt 26Lab als Verantwortlichen; Kette nur über 2.1/Anlage 5 abgebildet“.

### 4.6 Hetzner ISO-Zertifikat – wörtlich

- Aussteller: „SOCOTEC Certification Deutschland GmbH, Graf-Dürkheim-Straße 3, 87642 Halblech“
- Antragsteller: „Hetzner Online GmbH, Industriestraße 25, D-91710 Gunzenhausen“
- Geltungsbereich: „Der Anwendungsbereich des lnformationssicherheitsmanagementsystems umfasst alle Hosting-Dienstleistungen und die Rechenzentren.“
- Regelwerk: „ISO/IEC 27001:2022“
- „Statement of Applicability(SoA): Version 4.1 datiert 09.07.2025“ · „Zertifizierungsentscheidung: 18.09.2025“ · „Ausgestellt am: 18.09.2025“
- „Gültigkeit Zertifikat: 27.09.2025 - 26.09.2028“ · „Zertifikatsnummer: ZN-2025-35 V 1.1“
- Zertifikatsanhang Standorte: „Standort 1: Hetzner Online GmbH, Sigmundstraße 135, 90431 Nürnberg, Deutschland“ · „Standort 2: Hetzner Online GmbH, Am Datacenter-Park 1, 08223 Falkenstein/Vogtland, Deutschland“ · „Standort 3: Hetzner Online GmbH, Huurrekuja 10, 04360 Tuusula, Finnland“

Alle Angaben in A11 und 3.1 D stimmen mit dem Zertifikat überein.

---

## 5. Was 3.1 bzw. 5.9 mehr behaupten als die Verträge hergeben

1. **3.1 D STACKIT, Standort:** „Rechenzentrum der Region eu01 laut Leistungsschein/Produktseite in Deutschland“ – der Leistungsschein sagt das nicht (eu01 nur in einer URL); die Produktseite liegt nicht vor. Vertraglich belegt ist nur EU/EWR.
2. **3.1 D STACKIT, Art. 28 „vollständig“:** lit. g nur Löschung, keine Rückgabe-Option (Ziff. 10.1). Kleine Einschränkung.
3. **3.1 D / 5.9 B2 „kein Training“:** korrekt als Ableitung gekennzeichnet; das Wort Training steht in keinem STACKIT-Dokument. Unerwähnt: E-Mail und Subject-ID 30 Tage in Service-Logs (Leistungsschein Annex); zweiter Absatz von Ziff. 2.3 (nicht anonymisierte Nutzungsdaten im gesetzlich zulässigen Rahmen).
4. **3.1 D Hetzner, Bemerkung „passt zur Kette Flubber → 26lab → Hetzner“:** der Hetzner-AVV kennt 26Lab nur als Verantwortlichen; die Kette ist dort nicht abgebildet.
5. **3.1 D Hetzner, Standort „Server Nürnberg, Storage Box Falkenstein“:** nicht aus dem AVV, nur aus dem Konto belegbar (nicht prüfbar); das Zertifikat deckt beide Orte ab.
6. **Hetzner Anlage 1:** keine besonderen Kategorien (Gesundheitsdaten) genannt, obwohl Flubber-Kunden solche Daten einbringen können; Anlage 1 ist nicht „vom Auftraggeber ausgefüllt“, wie § 2 vorsieht. Betrifft 3.1 nicht direkt, gehört aber zur Vollständigkeitsfrage A10.

## 6. Fehlende Belege

- STACKIT: Zertifikat ISO 27001 / BSI C5 (3.1 A Nr. 3 „zu prüfen“) – kein Dokument vorhanden; TOMs belegen nur „angelehnt an“.
- STACKIT: Produktseite „weder gespeichert noch zum Training“ – nicht abgelegt (wäre ohnehin kein Vertrag).
- STACKIT: Leistungsschein Compute Engine GPU (in beiden AI-Leistungsscheinen als zusätzlich geltend genannt) – liegt nicht vor; könnte weitere Regelungen enthalten.
- STACKIT: Nachweis Rechenzentrum/Region (Deutschland) – kein Vertragsdokument vorhanden.
- Hetzner: Nachweis Annahme des AVV durch 26Lab (Klick/Signatur) – aus PDF-Text nicht erkennbar.
- Hetzner: Serverstandort Nürnberg / Storage Box Falkenstein – Kontoauszug/Screenshot fehlt.
- Hetzner: C5-Typ-2-Testat und § 8a BSI-KritisV (in Anlage 2 behauptet) – kein Nachweis abgelegt; nur das ISO-Zertifikat.
- Flubber ↔ 26Lab: Partnerschaftsvertrag 2.1 / AVV Anlage 5 unterschrieben (3.1 A Nr. 1 ❌) – ohne ihn hängt die Hetzner-Kette in der Luft.
