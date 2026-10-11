# Gegenprüfung (Vier-Augen) – Microsoft/Azure (A6–A9, B1, C3, C4) und Anbieter-Angaben (A12)

**Geprüft am:** 11.10.2026
**Prüfer:** Claude Code (Gegenprüfer für Dennis)
**Grundlage:** Aufgabenliste `06_Pruefungen/08_Gegenpruefung_Dennis_2026-10-08.md`, Textfassungen in `text/`, Azure-Nachweis samt drei Screenshots, 3.1 Checkliste, 5.9 Freigabeprotokoll, Kunden-AVV v1.6, Datenschutzerklärung v1.5, `lib/integrations/anbieter.ts` (Repo lymbe-ai).

Hinweise vorab:
- Die Microsoft-DPA liegt als Textfassung aus der docx vor; Seitenzahlen sind darin nicht enthalten. Ich habe sie über das Inhaltsverzeichnis (S. 2–3 der DPA) abgeglichen – die dort genannten Seiten stimmen mit den Angaben in 3.1/5.9 überein (Anlage 1 = S. 42, Vertraulichkeit = S. 22, Art der Datenverarbeitung = S. 9, Datenübermittlungen = S. 19, Speicherung und Löschung = S. 21).
- Die Nummerierung der Anlage 1 ist in der Textfassung verrutscht (Ziffern „1., 6., 7., 8., 9., 10., 11., 12.“ statt 1–8) – ein Konvertierungsartefakt der docx-Listen. Inhaltlich sind alle acht Ziffern vorhanden; Buchstabe d verweist auf „Ziffern 2 und 4 dieser Anlage“, was zur Originalzählung passt.
- Der Kern-Anbieter-Code (`packages/web/src/app/lymbe/anbieter.ts`, Repo lymbe-ablaeufe) liegt hier nicht vor. Die Kern-Anbieter (DeepL, Mollie, Brevo, Mailjet, Plausible, Teamleader, seven, clockodo, bexio) konnte ich daher nur auf Plausibilität der in 08_Gegenpruefung genannten Sitze prüfen, nicht gegen den tatsächlichen Code.
- dataprivacyframework.gov ist eine JavaScript-Anwendung; der direkte Abruf (curl) ist vom Proxy gesperrt, WebFetch liefert nur „You need to enable JavaScript“. Die DPF-Einträge habe ich deshalb über die offiziellen Eigenangaben der Firmen geprüft (Google, Microsoft, WhatsApp/Meta, Slack/Salesforce, Calendly, Cal.com). Das ist ein Beleg zweiter Ordnung – der Registereintrag selbst sollte von Dennis einmal im Browser nachgesehen werden.

---

## Teil A – Microsoft

### A6 – Microsoft-DPA (22.05.2026, deutsch): Art.-28-Bestimmungen, Löschung 90 + 90, SCC 2021, Vertraulichkeit, keine Profilbildung/Werbung/Marktforschung

**Urteil: bestätigt** (mit zwei Präzisierungen).

| Behauptung (3.1 D / 5.9 B3) | Fundstelle in der DPA | Wörtlich | Urteil |
|---|---|---|---|
| Stand 22.05.2026, deutsch | Kopf, Zeile 1; „Zusammenfassung der Änderungen“ | „Letzte Aktualisierung: 22. Mai 2026“ – „22.05.2026 – Im Abschnitt ‚Hinweise und Kontrollen beim Einsatz von Unterauftragsverarbeitern‘ wurde eine Erläuterung zu Unterauftragsverarbeitern hinzugefügt, die KI-Funktionen unterstützen.“ | bestätigt |
| Anlage 1 „Bestimmungen zur DSGVO“ (S. 42), Art. 5, 28, 32, 33 | Inhaltsverzeichnis: „Anlage 1 – Bestimmungen zur Datenschutz-Grundverordnung der Europäischen Union 42“; Überschrift „Relevante DSGVO-Verpflichtungen: Artikel 5, 28, 32 und 33“ | s. Buchstaben-Tabelle unten | bestätigt |
| Unterauftragnehmer mit Einspruchsrecht | Anlage 1 (Art. 28 Abs. 2); Abschnitt „Hinweise und Kontrollen beim Einsatz von Unterauftragsverarbeitern“ (S. 22) | „Im Fall einer allgemeinen schriftlichen Genehmigung wird Microsoft den Kunden immer über jede beabsichtigte Änderung … informieren, wodurch der Kunde die Möglichkeit erhält, gegen derartige Änderungen Einspruch zu erheben.“ – Frist: „mindestens 6 Monate im Voraus“; für KI-Unterauftragsverarbeiter „30 Tage, wobei die Möglichkeit besteht, die Nutzung … bis mindestens 6 Monate nach dieser Benachrichtigung zu deaktivieren.“ Rechtsfolge: Kündigung „ohne Strafe oder Kündigungsgebühr“. | bestätigt. Präzisierung: Das „Einspruchsrecht“ ist faktisch ein Kündigungsrecht, kein Vetorecht. |
| Löschung 90 + 90 Tage nach Vertragsende („Speicherung und Löschung“, S. 21) | Abschnitt „Speicherung und Löschung von Daten“ | „… wird Microsoft Kundendaten, die in den Onlinediensten gespeichert bleiben, 90 Tage lang nach Ablauf oder Beendigung des Abonnements des Kunden in einem eingeschränkten Funktionskonto aufbewahren … Nach Ablauf der 90-tägigen Aufbewahrungsfrist deaktiviert Microsoft das Konto des Kunden und löscht die in den Onlinediensten gespeicherten Kundendaten und personenbezogenen Daten innerhalb weiterer 90 Tage“ | bestätigt |
| SCC 2021 im DPA („Datenübermittlungen und Speicherort“, S. 19) | Definition „Standardvertragsklauseln von 2021“ (S. 7) und Abschnitt „Datenübermittlungen“ | „Sämtliche Übermittlungen … aus der Europäischen Union, dem Europäischen Wirtschaftsraum, dem Vereinigten Königreich und der Schweiz … unterliegen den Bedingungen der von Microsoft implementierten Standardvertragsklauseln von 2021.“ – Modul: „Auftragsverarbeiter-zu-Auftragsverarbeiter-Modul … zwischen Microsoft Ireland Operations Limited und Microsoft Corporation“. Zusätzlich: „Microsoft [ist] nach den EU-U.S.- und Swiss-U.S. Data Privacy Frameworks … zertifiziert.“ | bestätigt |
| EU-Datengrenze | Abschnitt „Speicherorte von Kundendaten“ | „Für EU-Datengrenzen-Dienste speichert und verarbeitet Microsoft Kundendaten und personenbezogene Daten … innerhalb der Europäischen Union und der Europäischen Freihandelsassoziation (EFTA), wie in den Produktbestimmungen beschrieben.“ | bestätigt – aber: ob Azure OpenAI/Speech „EU-Datengrenzen-Dienste“ sind, steht nicht in der DPA, sondern in den Produktbestimmungen (nicht im Ordner). |
| Vertraulichkeit der Mitarbeiter, auch nach Beschäftigungsende (S. 22) | Abschnitt „Vertraulichkeitsverpflichtung des Auftragsverarbeiters“ | „Microsoft stellt sicher, dass die Mitarbeiter von Microsoft, die mit der Verarbeitung … befasst sind, (i) diese Daten nur auf Weisung des Kunden oder gemäß Beschreibung in diesem DPA verarbeiten und (ii) sich verpflichten, die Vertraulichkeit und Sicherheit dieser Daten auch nach Beendigung des Beschäftigungsverhältnisses aufrechtzuerhalten.“ | bestätigt; **keine § 203-Klausel** (Suche nach „203“, „Berufsgeheimnis“ ohne Treffer) – wie in 3.1 vermerkt |
| Keine Nutzung für Profilbildung, Werbung, Marktforschung (S. 9) | Abschnitt „Art der Datenverarbeitung; Eigentumsverhältnisse“ | „Bei der Bereitstellung von Produkten und Services wird Microsoft Kundendaten, Professional Services-Daten oder personenbezogene Daten nicht verwenden oder anderweitig verarbeiten für: (a) Benutzerprofilerstellung, (b) Werbung oder ähnliche kommerzielle Zwecke oder (c) Marktforschung zur Entwicklung neuer Funktionen, Dienstleistungen oder Produkte oder zu anderen Zwecken; es sei denn, eine solche Verwendung oder Verarbeitung erfolgt in Übereinstimmung mit den dokumentierten Weisungen des Kunden.“ | bestätigt |

**Art. 28 Abs. 3 DSGVO, Buchstaben a–h, einzeln gegen Anlage 1 (S. 42 ff.):**

| Buchstabe | Pflicht | In Anlage 1 | Wörtlich (Anfang) |
|---|---|---|---|
| Satz 1 (Gegenstand, Dauer, Art, Zweck, Datenarten, Betroffene) | Festlegung im Vertrag | ja – Ziffer zu Art. 28 Abs. 3, Einleitungssatz; ausgeführt im Abschnitt „Verarbeitungsdetails“ (S. 13–14) | „Gegenstand und Dauer der Verarbeitung, Art und Zweck der Verarbeitung, Art der personenbezogenen Daten, Kategorien der betroffenen Personen sowie Pflichten und Rechte des Kunden werden im Lizenzvertrag des Kunden festgelegt, der die DSGVO-Bestimmungen einschließt.“ |
| a | nur auf dokumentierte Weisung, auch Drittland | ja, Buchst. a | „personenbezogene Daten nur auf dokumentierte Weisung des Kunden zu verarbeiten, auch in Bezug auf die Übermittlung personenbezogener Daten in ein Drittland …“ |
| b | Vertraulichkeitsverpflichtung der Personen | ja, Buchst. b | „zu gewährleisten, dass sich die zur Verarbeitung der personenbezogenen Daten befugten Personen zur Vertraulichkeit verpflichtet haben oder einer angemessenen gesetzlichen Verschwiegenheitspflicht unterliegen“ |
| c | Maßnahmen nach Art. 32 | ja, Buchst. c; ausgeführt in Ziffern zu Art. 32 Abs. 1, 2, 4 und Anhang A | „alle erforderlichen Maßnahmen gemäß Artikel 32 DSGVO zu ergreifen“ |
| d | Bedingungen für weitere Auftragsverarbeiter (Abs. 2 und 4) | ja, Buchst. d + Ziffern zu Art. 28 Abs. 2 und Abs. 4 | „die Bedingungen einzuhalten, auf die in den Ziffern 2 und 4 dieser Anlage bezüglich der Inanspruchnahme eines weiteren Auftragsverarbeiters verwiesen wird“ |
| e | Unterstützung bei Betroffenenrechten | ja, Buchst. e; ausgeführt in „Rechte der betroffenen Personen; Unterstützung bei Anfragen“ (S. 14) | „… den Kunden nach Möglichkeit mit geeigneten technischen und organisatorischen Maßnahmen dabei zu unterstützen, seiner Pflicht zur Beantwortung von Anträgen … nachzukommen“ |
| f | Unterstützung Art. 32–36 | ja, Buchst. f | „den Kunden … bei der Einhaltung seiner Verpflichtungen gemäß Artikel 32 bis 36 DSGVO zu unterstützen“ |
| g | Löschen/Rückgabe nach Abschluss | ja, Buchst. g; konkretisiert in „Speicherung und Löschung von Daten“ (90 + 90 Tage) | „nach Abschluss der Erbringung der Verarbeitungsleistungen nach Wahl des Kunden alle personenbezogenen Daten entweder zu löschen oder zurückzugeben und die vorhandenen Kopien zu löschen …“ |
| h | Nachweise, Überprüfungen, Inspektionen | ja, Buchst. h; Verfahren in „Prüfung der Einhaltung“ (S. 16–17) | „dem Kunden alle erforderlichen Informationen zum Nachweis der Einhaltung … zur Verfügung zu stellen und Überprüfungen – einschließlich Inspektionen, die vom Kunden oder einem von ihm beauftragten Prüfer durchgeführt werden – zu ermöglichen und dazu beizutragen.“ |
| Abs. 3 Satz 3 (Hinweis bei rechtswidriger Weisung) | ja, Absatz nach Buchst. h | „Microsoft informiert den Kunden unverzüglich, falls Microsoft der Auffassung ist, dass eine Weisung gegen die DSGVO … verstößt (Artikel 28 Absatz 3).“ |

Ergebnis: **Art. 28 Abs. 3 a–h vollständig**, zusätzlich Abs. 2 (Genehmigung weiterer Auftragsverarbeiter) und Abs. 4 (Haftung für Unterauftragsverarbeiter) in Anlage 1 enthalten.

**Behauptet 3.1 / 5.9 B3 mehr, als die DPA hergibt?**
1. 3.1 Nr. 4, Spalte „Besonderheiten“: „‚kein Training‘ (Product Terms)“ – die DPA enthält **kein Wort zu Training** (Suche „Training“, „trainier“: kein Treffer in der DPA). Die Product Terms (Azure-OpenAI-Abschnitt) liegen nicht im Ordner; der eigentliche Beleg ist die Microsoft-Learn-Seite (A7). Das reicht als Nachweis für § 3 Abs. 6 des Kunden-AVV („vertraglich bestätigen lassen“) nur über einen Umweg: Die DPA sagt (S. 12–13), dass „der Kundenvertrag … zusammen mit der Produktdokumentation … die vollständigen und dokumentierten Weisungen des Kunden“ bilden – die Dokumentation ist also Teil der Weisung, die Microsoft bindet. Empfehlung: Product-Terms-Abschnitt „Azure OpenAI Service“ / „Microsoft Foundry“ als PDF zusätzlich ablegen, damit „vertraglich“ auch wörtlich belegt ist.
2. 5.9 B3 verweist für „kein Training“ auf „DPA S. 9“ – diese Stelle belegt nur „keine Profilbildung/Werbung/Marktforschung“, nicht „kein Training“. Nicht falsch, aber die Zuordnung in 5.9 sollte sauber getrennt werden: „kein Training“ = Microsoft Learn (+ Product Terms); „keine Profilbildung/Werbung“ = DPA S. 9.
3. Die DPA-Zusage „keine Profilbildung/Werbung/Marktforschung“ steht unter dem Vorbehalt „es sei denn … in Übereinstimmung mit den dokumentierten Weisungen des Kunden“ – unschädlich, solange Lymbe keine solchen Funktionen aktiviert.

---

### A7 – „kein Training“ für Azure OpenAI

**Urteil: bestätigt.**

Quelle: Microsoft Learn „Data, privacy, and security for Models sold by Azure in Microsoft Foundry“, Fuß: „Last updated on 05/19/2026“ (3.1/5.9 nennen „Stand 18.05.2026“ – Differenz von einem Tag, vermutlich Zeitzone; unerheblich).

Wörtlich (Kasten „Important“, oben):
> „Your prompts (inputs) and completions (outputs), your embeddings, and your training data: are NOT available to other customers. are NOT available to OpenAI or other providers of Models sold by Azure. are NOT used by providers of Models sold by Azure to improve their models or services. are NOT used to train any generative AI foundation models without your permission or instruction. Customer Data, Prompts, and Completions are NOT used to improve Microsoft or third-party products or services without your explicit permission or instruction.“

Abschnitt „Generating completions, images or embeddings through inferencing“:
> „The models are stateless: no prompts or completions are stored in the model. Additionally, prompts and completions are not used to train, retrain, or improve the base models.“

Abschnitt „Preventing harmful content generation“:
> „No prompts or generated content are stored in the content classifier models, and prompts and outputs are not used to train any generative AI foundation models without your permission or instruction.“

Das in 3.1 D / 5.9 B3 verwendete Zitat „prompts and completions are not used to train, retrain, or improve the base models“ steht wörtlich so im Dokument. „nicht für OpenAI zugänglich“ ist gedeckt („are NOT available to OpenAI“; „Models sold by Azure do NOT interact with any services operated by providers … for example, OpenAI“).

Einschränkung, die in 3.1/5.9 fehlt: Die Zusagen gelten mit dem Zusatz „without your permission or instruction“ – Funktionen wie „Stored completions“ oder Fine-Tuning würden Daten speichern bzw. (nach Kundenwunsch) für Training nutzen. Lymbe nutzt laut Nachweis nur Chat Completions / Embeddings mit DataZoneStandard; damit ist die Aussage „kein Training“ für den tatsächlichen Einsatz gedeckt. Hinweis auf dem Azure-Screenshot: die Ressource zeigt „Stored Completions (Deprecated)“ im Menü – das ist nur der Menüpunkt, kein Nachweis, dass die Funktion aus ist. Für die Vollständigkeit wäre ein kurzer Satz in 5.9 B3 sinnvoll: „Stored completions, Fine-Tuning und Assistants/Responses API werden nicht genutzt.“

---

### A8 – Missbrauchsüberwachung: menschliche Prüfung möglich, Speicherung in der Geografie der Ressource, Prüfer im EWR, 30 Tage nicht mehr genannt

**Urteil: bestätigt.**

Quelle: Microsoft Learn „Abuse monitoring“, Fuß „Last updated on 05/19/2026“ (3.1 nennt 13.05.2026 – kleine Abweichung, Inhalt derselbe), ergänzt durch die Datenschutzseite aus A7.

**a) Speicherfrist (30 Tage o. ä.)?** In beiden Dokumenten steht **keine** Frist. Die Wörter „30“, „thirty“, „days“ kommen im Abuse-Monitoring-Text nicht vor; auf der Datenschutzseite nur im Changelog-Datum und bei Speech nicht relevant. Es gibt nur qualitative Aussagen:
> „prompts and completions that undergo such review [automatisierte Prüfung] are not stored by the abuse monitoring system or used to train the AI model or other systems.“
> „The abuse monitoring data store where prompts and completions are stored for human review is logically separated by customer resource …“

Ein Microsoft-Q&A-Thread vom 01./02.10.2026 (learn.microsoft.com, Frage 6022860) bestätigt aus Community-Sicht: „No retention maximum is published as far as I can find“ – die 30 Tage „appear on neither Abuse monitoring nor the data privacy page“. Ältere Q&A-Threads (2024) zitieren die frühere Doku mit „stored for 30 days“. Die Frist stand also früher drin und wurde entfernt; die Behauptung in 3.1 („nennt die aktuelle Doku nicht mehr ausdrücklich“) ist korrekt.

**b) Wo gespeichert, wer sieht es?** Datenschutzseite, Abschnitt „Preventing abuse“:
> „A separate data store is located in each geography in which the model sold by Azure is available, and a customer's prompts and generated content are stored in the Azure geography where the customer's Foundry resource is deployed, within the Models sold by Azure service boundary.“
> „The human reviewers are authorized Microsoft employees who access the data via point wise queries using request IDs, Secure Access Workstations (SAWs), and Just-In-Time (JIT) request approval granted by team managers. For Models sold by Azure deployed in the European Economic Area, the authorized Microsoft employees are located in the European Economic Area.“

Für Datenzonen-Bereitstellungen zusätzlich (Abschnitt „Understanding location of processing“): „… including the abuse monitoring data store created for Global and DataZone deployments, is stored in the customer-designated geography.“

Wann Menschen überhaupt prüfen (Abuse monitoring, „Review and Decision“):
> „By default, if prompts and completions are flagged … they might be sampled for review by using automated means including AI models such as LLMs instead of a human reviewer.“ – „In some cases, when automated review doesn't meet applicable confidence thresholds in complex contexts or if automated review systems aren't available, human eyes-on review might be introduced …“

**c) Modified Abuse Monitoring / Ausnahme-Antrag:** ja, eigener Abschnitt:
> „Microsoft allows customers who meet additional Limited Access eligibility criteria to apply to modify abuse monitoring by completing this form. Some advanced Models sold by Azure may have more stringent criteria for turning off abuse monitoring.“
Laut Q&A-Thread (Oktober 2026) ist das „only to customers and partners managed by a Microsoft account team or under an eligible program“ – Flubber Pixels als Pay-as-you-go-Kunde erfüllt das vermutlich nicht; 3.1 vermerkt zutreffend „nicht beantragt“. Prüfbar ist der Status über das Attribut `ContentLogging=false` (Datenschutzseite, Abschnitt „How can a customer verify…“) – deckt B2.

**d) Deckt die Doku die Formulierung in 3.1 D?** „Gespeichert wird nur für menschliche Prüfung, in der Geografie der Ressource, Prüfer im EWR“ – ja, wörtlich gedeckt. „menschliche Prüfung möglich“ – ja.

---

### A9 – Azure Speech: schnelle Transkription ohne Speicherung, Audio-Logging standardmäßig aus

**Urteil: bestätigt.**

Quelle 1: Microsoft Learn „Data and Privacy for Speech to text“, Fuß „Last updated on 08/27/2026“, Abschnitt „Data storage and retention – No data trace“:
> „When doing real-time speech to text, fast transcription, pronunciation assessment, and speech translation, Microsoft does not retain or store the data provided by customers.“

Abschnitt „Real-time speech to text“:
> „For real-time speech to text, audio input is processed only on the Azure's server memory, and no data is stored at rest. All data in-transit are encrypted for protection.“

Quelle 2: Microsoft Learn „How to log audio and transcriptions for speech recognition“, Fuß „Last updated on 10/31/2025“, Abschnitt „Enable audio and transcription logging“:
> „Logging is disabled by default. Logging can be enabled per recognition session or per custom model endpoint.“
Und für den Fall, dass es eingeschaltet wäre: „The logs are retained for 30 days. After this period, the logs are automatically deleted.“

Code: `lib/sprache/transkription.ts` ruft `…/speechtotext/transcriptions:transcribe` (Fast-Transcription-API) auf; ein Parameter `storeAudio=true` oder `enable_audio_logging` kommt in `lib/sprache/` nicht vor. Die Aussage „im Code nicht eingeschaltet“ ist damit gedeckt.

Präzisierung: Die Logging-Seite beschreibt den Schalter für SDK/REST-Kurzaudio und Custom-Endpunkte; für die Fast-Transcription-API ist dort kein Schalter beschrieben. Die tragende Zusage ist deshalb der Satz „fast transcription … Microsoft does not retain or store the data“ aus Quelle 1 – der ist eindeutig.

Hinweis zu den Daten: Die Speech-Seite stuft Audio als mögliche biometrische Daten ein („may be considered personal data and/or sensitive data … you are responsible for … obtaining consent“). Das betrifft die Kunden-DSE-Formulierung „Spracheingabe“ – die DSE v1.5 Abschnitt 2 informiert bereits, dass die Aufnahme nicht gespeichert wird; eine ausdrückliche Einwilligung ist dort nicht vorgesehen. Das wäre ein Punkt für den Anwalt (Mikrofon-Nutzung ist freiwillig, Verarbeitung nur flüchtig; m. E. keine biometrische Verarbeitung im Sinne Art. 9, weil keine Identifizierung stattfindet – aber bitte rechtlich bestätigen lassen).

---

### A12 – Anbieter-Angaben im Verbinden-Dialog (`lib/integrations/anbieter.ts`)

**Urteil: überwiegend stimmig; ein inhaltlicher Fehler in der Text-Vorlage, eine Abweichung bei Slack, Rest bestätigt oder nicht prüfbar.**

#### Liste im Portal-Code (Stand Repo lymbe-ai, 11.10.2026)

| Schlüssel | Dienst | Rechtsträger im Code | Sitz | Grundlage | Drittland |
|---|---|---|---|---|---|
| google-calendar | Google Calendar | Google Ireland Limited | Irland | dpf | USA |
| outlook | Microsoft Outlook | Microsoft Ireland Operations Limited | Irland | dpf | USA |
| calendly | Calendly | Calendly LLC | USA | pruefen | USA |
| calcom | Cal.com | Cal.com, Inc. | USA | pruefen | USA |
| shopify | Shopify | Shopify International Limited | Irland | angemessen | Kanada |
| shopware | Shopware | der Betreiber Ihres Shop-Servers | – | eigen | – |
| woocommerce | WooCommerce | der Betreiber Ihres Shop-Servers | – | eigen | – |
| whatsapp | WhatsApp | WhatsApp Ireland Limited (Meta) | Irland | dpf | USA |
| meta | Facebook Messenger und Instagram | Meta Platforms Ireland Limited | Irland | dpf | USA |
| slack | Slack | Slack Technologies, LLC (Salesforce) | USA | dpf | USA |
| teams | Microsoft Teams | Microsoft Ireland Operations Limited | Irland | dpf | USA |
| webhook | Webhook | Betreiber der Zieladresse | je nach Anbieter | pruefen | – |
| datenquelle | Datenquelle über Schnittstelle | Betreiber der Schnittstelle | je nach Anbieter | pruefen | – |

Die in 08_Gegenpruefung A12 genannten Kern-Anbieter (DeepL, Mollie, Brevo, Mailjet, Plausible, Teamleader, seven, clockodo, bexio) stehen **nicht** in dieser Datei, sondern im Kern-Repo (nicht vorliegend).

#### Prüfung je Anbieter

| Anbieter | Rechtsträger / Sitz | DPF-Status | Urteil | Beleg |
|---|---|---|---|---|
| Google (Calendar) | Google Ireland Limited, Dublin – für Nutzer im EWR korrekt | Google LLC ist zertifiziert (EU-U.S. DPF, UK Extension, Swiss-U.S. DPF), „along with its wholly-owned US subsidiaries unless explicitly excluded“ | **stimmt** (mit Hinweis unten zur Formulierung) | policies.google.com/privacy/frameworks, „Effective August 23, 2025“; DPF-Eintrag Google LLC = participant/5780 (nur als Link sichtbar, Inhalt nicht abrufbar) |
| Microsoft (Outlook, Teams) | Microsoft Ireland Operations Limited, Dublin – korrekt (auch DPA: „Microsoft Ireland Operations Limited ist der Datenschutzvertreter von Microsoft für den EWR“) | Microsoft Corporation: „Microsoft complies with the EU-U.S., UK Extension to the EU-U.S., and Swiss-U.S. Data Privacy Frameworks“; DPA S. 19 bestätigt die Zertifizierung vertraglich | **stimmt** | microsoft.com/…/microsoft-data-privacy-framework-covered-entities; DPA „Datenübermittlungen“; DPF-Eintrag participant/6474 |
| WhatsApp | WhatsApp Ireland Limited – korrekt (Microsofts Seite nennt „services offered by WhatsApp Ireland Ltd.“) | WhatsApp LLC: „has certified our participation in the EU-U.S. Data Privacy Framework“ (Swiss-U.S. ebenfalls) | **stimmt** | whatsapp.com/legal/data-privacy-framework, „effective December 3, 2025“ |
| Meta (Messenger/Instagram) | Meta Platforms Ireland Limited – korrekt für EU | Meta Platforms, Inc.: Seite facebook.com/privacy/policies/data_privacy_framework (robots-gesperrt, nicht lesbar); DPF-Eintrag participant/4452 taucht in der Suche auf | **sehr wahrscheinlich stimmt, nicht direkt prüfbar** – Dennis bitte im Browser nachsehen | – |
| Slack | Code: „Slack Technologies, LLC (Salesforce), Sitz USA“. Slack Supplemental Terms: für Kunden außerhalb USA/Kanada/Japan ist Vertragspartner **Slack Technologies Limited, Salesforce Tower, 60 R801, North Dock, Dublin, Ireland**; die LLC (415 Mission Street, San Francisco) gilt nur für Kunden in USA/Kanada | Slack: „Through Salesforce, Slack participates in the EU-U.S. Data Privacy Framework (DPF)“; Salesforce: „a certified organization under the EU-US DPF“ seit 17.07.2023; zertifizierter Teilnehmer ist Salesforce, Inc. (participant/5959), Slack als gedeckte Einheit | **abweichend beim Rechtsträger/Sitz**: für deutsche Kunden ist Slack Technologies Limited (Irland) der Vertragspartner, nicht die LLC. DPF-Aussage im Kern richtig, aber zertifiziert ist Salesforce, Inc., nicht „Slack Technologies, LLC“ als eigener Teilnehmer | api.slack.com/slack-supplemental-terms; slack.com/trust/compliance/gdpr; salesforce.com/news/…/salesforce-transatlantic-data-privacy-update |
| Shopify | Shopify International Limited: „Irish-registered entity contracting with merchants in Europe, the Middle East, and Africa (EMEA)“ – korrekt. Shopify Inc. (Kanada) für USA/Kanada | Grundlage „angemessen“ (Angemessenheitsbeschluss Kanada): plausibel; der Beschluss 2002/2/EG für Kanada (PIPEDA, kommerzielle Empfänger) gilt fort und wurde 2024 von der Kommission bestätigt. Shopify-Hilfeseite nennt die Rechtsgrundlage nicht ausdrücklich | **stimmt** (Rechtsträger); Grundlage plausibel, auf der Shopify-Seite nicht wörtlich belegt | help.shopify.com/…/contracting-entities |
| Calendly | Calendly LLC, 115 E Main St, Ste A1B, Buford, GA 30518 (nicht Atlanta) – Rechtsträger stimmt | Calendly-DPA: „Calendly is self-certified under the Data Privacy Frameworks“; SCC Modul 2 als Rückfall. Registereintrag nicht geprüft | **stimmt** (Rechtsträger/Sitz USA); „pruefen“ ist vorsichtig und bleibt richtig, solange der Registereintrag nicht nachgesehen ist – könnte nach Prüfung auf „dpf“ gehen | calendly.com/dpa |
| Cal.com | Cal.com, Inc., 2261 Market Street #4382, San Francisco, CA 94114 – stimmt | Privacy Policy: „Cal.com, Inc. complies with the EU-U.S. Data Privacy Framework (EU-U.S. DPF)“ + SCC. Registereintrag nicht geprüft | **stimmt** (Rechtsträger/Sitz); „pruefen“ wie bei Calendly vertretbar | cal.com/privacy |
| Shopware / WooCommerce / Webhook / Datenquelle | „eigen“ bzw. „pruefen“ – keine feste Firma | – | **stimmt** (keine Firmenangabe nötig) | – |

Kern-Anbieter (nur Plausibilität der Sitz-Angabe, Code nicht vorliegend):

| Anbieter | Erwarteter Rechtsträger / Sitz | Urteil |
|---|---|---|
| DeepL | DeepL SE, Köln (DE) | plausibel (aus Kenntnis) – nicht prüfbar gegen Code |
| Mollie | Mollie B.V., Amsterdam (NL) | plausibel – nicht prüfbar |
| Brevo | Sendinblue SAS (Marke Brevo), Paris (FR) | plausibel – nicht prüfbar |
| Mailjet | Impressum mailjet.com: **Mailjet GmbH, Alt Moabit 2, 10557 Berlin**; Vertragspartner laut AGB i. d. R. Mailjet SAS, Paris (Sinch-Gruppe) – beides EU | EU-Sitz bestätigt; welcher Rechtsträger im Kern steht, nicht prüfbar |
| Plausible | Plausible Insights OÜ, Tallinn (EE) | plausibel – nicht prüfbar |
| Teamleader | Teamleader NV, Gent (BE) | plausibel – nicht prüfbar |
| seven.io | seven communications GmbH & Co. KG, Kiel (DE), früher sms77 e.K. | plausibel – nicht prüfbar |
| clockodo | **Clockodo GmbH, Unna** (zweiter Standort Fürth), früher clickbits GmbH | EU-Sitz bestätigt (clockodo.com/about-us) |
| bexio | bexio AG, Rapperswil-Jona (CH) – Angemessenheitsbeschluss Schweiz | plausibel – nicht prüfbar |

#### Befund zur Text-Vorlage (wichtig)

`verbindenText()` erzeugt bei `grundlage: 'dpf'` den Satz:
> „Daten können in die USA gehen. ${a.anbieter} ist nach dem EU-US Data Privacy Framework zertifiziert.“

Mit den aktuellen Einträgen liest der Kunde also: „Google Ireland Limited ist nach dem EU-US Data Privacy Framework zertifiziert“ bzw. „Microsoft Ireland Operations Limited …“, „WhatsApp Ireland Limited (Meta) …“, „Meta Platforms Ireland Limited …“. **Das ist sachlich falsch**: Das DPF ist ein Selbstzertifizierungsprogramm für **US-Organisationen**; eine irische Gesellschaft kann nicht zertifiziert sein. Zertifiziert sind Google LLC, Microsoft Corporation, WhatsApp LLC, Meta Platforms, Inc., Salesforce, Inc. Die EU-Gesellschaft ist Vertragspartner; die Übermittlung an die US-Mutter stützt sich auf deren Zertifizierung (bei Google/Meta/Microsoft zusätzlich auf SCC in den jeweiligen Data-Transfer-Addenda).

Empfehlung (kleine Code-Änderung, kein Umbau): ein optionales Feld `dpfTraeger` je Anbieter (z. B. `'Google LLC'`, `'Microsoft Corporation'`, `'WhatsApp LLC'`, `'Meta Platforms, Inc.'`, `'Salesforce, Inc. (für Slack)'`) und den Satz ändern in:
> „Daten können in die USA gehen; Empfänger dort ist ${a.dpfTraeger}, zertifiziert nach dem EU-US Data Privacy Framework.“

Für Slack zusätzlich Rechtsträger auf „Slack Technologies Limited (Salesforce), Sitz: Irland“ ändern, `drittland: 'die USA'` bleibt.

---

## Teil B1 – Azure-Nachweis (Screenshots)

**Urteil: Screenshots decken die Aussage „Germany West Central, Datenzonenstandard (EUR)“ für die Azure-OpenAI-Ressource `lymbe-ai`.**

| Screenshot | Was zu sehen ist |
|---|---|
| `Azure_Ressource_lymbe-ai_Germany-West-Central_2026-10-08.jpg` | Azure-Portal, Ressource **lymbe-ai** (Typ „Azure OpenAI“), Ressourcengruppe lymbe-ai, Status Aktiv, **Standort: Germany West Central**, Abonnement „Azure subscription 1“ (6a340424-5602-4b7c-8497-b954cf8c61e3), API-Art OpenAI, Tarif Standard. Angemeldet: info@flubber-pixels.de. Im Menü sichtbar: „Stored Completions (Deprecated)“ (nur Menüpunkt). |
| `Azure_Bereitstellungen_lymbe-ai_DataZone-EUR_2026-10-08.jpg` | Microsoft Foundry, lymbe-ai (germanywestcentral, S0), „Modellimplementierungen“: drei Bereitstellungen **gpt-6.1-sol** (Version 2026-09-29), **model-router** (2025-11-18), **text-embedding-3-small** (1), alle Zustand „Erfolgreich“, Inhaltsfilter DefaultV2, **Bereitstellungstyp „Datenzonenstandard (EUR)“** bei allen dreien. Modelleinstellungsdaten (Retirement): 11.03.2028, 20.05.2027, 09.02.2028. |
| `Azure_Alle_Ressourcen_nur-lymbe-ai_2026-10-08.jpg` | Foundry „Alle Ressourcen (1)“: nur **lymbe-ai**, Typ Azure OpenAI, Abonnement „Azure subscription 1“, Region **Germany West Central**, erstellt von info@flubber-pixels.de. Die alte Sweden-Central-Ressource erscheint nicht mehr. |

Abgleich mit `Azure_Regionen_Nachweis_2026-10-08.md`: Ressourcenname, Region, Abonnement-ID, die drei Bereitstellungen samt Versionen und der SKU „DataZoneStandard / EUR“ stimmen 1:1 überein. Die Löschung der Ressourcengruppe `rg-info-8226` ist durch Screenshot 3 plausibel belegt (nur eine Ressource).

Lücke: Die Speech-Ressource **`lymbe-ai-sprache`** ist auf keinem Screenshot zu sehen (Foundry-„Alle Ressourcen“ listet offenbar nur Azure-OpenAI-Ressourcen). Ihre Region „Germany West Central“ steht nur in der MD-Tabelle (Abfrage per Azure MCP). Für die DSE-Aussage „Spracheingabe in Deutschland (Frankfurt)“ fehlt also der Screenshot-Beleg – empfohlen: Übersichtsseite der Ressource `lymbe-ai-sprache` im Azure-Portal ebenfalls als JPG ablegen.

Hinweis zur Formulierung im Nachweis („Speicherung in der Region Germany West Central, Verarbeitung nur in Rechenzentren innerhalb der EU-Datenzone“): Microsoft sagt „stored in the customer-designated **geography**“ – Geografie Deutschland (Germany West Central + Germany North), nicht nur die eine Region. Praktisch gleichbedeutend mit „Deutschland“, aber „Frankfurt“ ist enger als Microsofts Zusage (s. C3).

Teil B2 (Missbrauchsüberwachung aktiv, kein `ContentLogging=false`) kann ich nicht nachmessen; die Methode entspricht der Microsoft-Doku: „The value of ‚false‘ for the ‚ContentLogging‘ attribute appears only if data storage for abuse monitoring is turned off.“ Plausibel.

---

## Teil C Nr. 3 – „EU-Datenzone“: Speicherung vs. Verarbeitung

**Was Microsoft sagt** (Datenschutzseite, Abschnitt „Understanding location of processing for ‚Global‘ and ‚Data zone‘ deployment types“):
> „For any deployment type labeled as 'DataZone,' prompts and responses may be processed in any geography within the specified data zone, as defined by Microsoft. … If you create a DataZone deployment in a Foundry resource located in a European Union Member Nation, prompts and responses may be processed in that or any other European Union Member Nation. For both Global and DataZone deployment types, any data stored at rest, such as uploaded data, and including the abuse monitoring data store created for Global and DataZone deployments, is stored in the customer-designated geography. Only the location of processing is affected when a customer uses a Global deployment type or DataZone deployment type …; Azure data processing and compliance commitments remain applicable.“

Für Standard-Bereitstellungen ohne Datenzone zusätzlich: „Prompts and responses are processed within the customer-specified geography … but may be processed between regions within the geography for operational purposes.“

Die DPA (S. 20) sagt für EU-Datengrenzen-Dienste „innerhalb der Europäischen Union und der EFTA“; die Datenzone „EUR“ ist enger (nur EU-Mitgliedstaaten). Das Wort „Datenzone“ kommt in der DPA nicht vor – es ist ein Produktbegriff aus den Produktbestimmungen/Doku.

Also: **Speicherung (at rest, inkl. Abuse-Monitoring-Speicher) = Geografie Deutschland; Verarbeitung (Inferenz) = jeder EU-Mitgliedstaat.**

**Sätze in AVV und DSE:**

- AVV v1.6, Anlage 2 Nr. 4, Spalte Ort: „**Spracheingabe: Frankfurt; Werkstatt: EU-Datenzone**“
- AVV § 3 Abs. 10: „Lymbe verarbeitet die Daten in Deutschland und in der EU. Übermittlungen in Länder außerhalb der EU/des EWR finden nur in den in Anlage 2 beschriebenen Fällen und auf der dort genannten Grundlage statt.“
- DSE v1.5, Abschnitt 4 (Tabelle Microsoft): „Irland; **Spracheingabe in Deutschland (Frankfurt), Werkstatt in der EU-Datenzone**; Rest-Übermittlungen für Support und Telemetrie über Standardvertragsklauseln und EU-US Data Privacy Framework“
- DSE v1.5, Abschnitt Drittland: „Die Werkstatt zum Erstellen von Abläufen läuft bei der Microsoft Ireland Operations Ltd. (Azure) **in der EU-Datenzone und damit innerhalb der EU**.“
- DSE v1.5, Abschnitt 2 (Spracheingabe): „… dessen Aufnahme wird **in einem Rechenzentrum in Frankfurt** in Text umgewandelt … Die Aufnahme speichern weder wir noch Microsoft.“ und Abschnitt 5: „seit dem 30.09.2026 bei der Microsoft Ireland Operations Ltd. (Azure) in einem Rechenzentrum in Frankfurt“.

**Bewertung:**
- „Werkstatt: EU-Datenzone“ / „in der EU-Datenzone und damit innerhalb der EU“ – **gedeckt**. Die Formulierung verspricht nicht „Deutschland“, sondern EU; genau das sagt Microsoft („that or any other European Union Member Nation“). § 3 Abs. 10 („in Deutschland und in der EU“) passt ebenfalls.
- „Spracheingabe: Frankfurt“ / „in einem Rechenzentrum in Frankfurt“ – **im Kern gedeckt, aber etwas enger als Microsofts Zusage**. Die Speech-Ressource steht laut Nachweis in Germany West Central (= Frankfurt). Microsoft sichert für regionale Ressourcen die Geografie zu, mit möglicher Verarbeitung „between regions within the geography“ – für Deutschland wäre das auch Germany North (Berlin). Das Speech-Dokument selbst nennt keinen Ort. Vorschlag: „in Deutschland (Region Frankfurt)“ oder schlicht „in Deutschland“ – dann ist der Satz auf jeden Fall gedeckt. Kein Fehler, nur Vorsicht; zudem fehlt der Screenshot für die Speech-Ressource (siehe B1).
- Kleiner Begriffs-Hinweis für den Kunden-Text: „EU-Datenzone“ ist ein Microsoft-Produktbegriff. Die DSE erklärt ihn mit „und damit innerhalb der EU“ – gut; im AVV Anlage 2 steht nur „EU-Datenzone“ ohne Erklärung. Optional: „EU-Datenzone (Verarbeitung nur in EU-Mitgliedstaaten, Speicherung in Deutschland)“.

**Für den Anwalt:** nichts Zwingendes; die Aussagen sind durch die Microsoft-Doku gedeckt. Offen bleibt nur die Frage, ob eine reine Doku-Zusage (Microsoft Learn) als „vertraglich“ gilt – die DPA bindet Microsoft an die Produktdokumentation als Teil der Weisung (S. 12–13), das trägt m. E.

---

## Teil C Nr. 4 – „bis zu 30 Tage“ Missbrauchsüberwachung

**Wörtliche Stellen:**
- AVV v1.6, Anlage 2 Nr. 4, Spalte Daten: „Beschreibungstexte; Sprachaufnahmen. **Microsoft kann Ein- und Ausgaben der Werkstatt bis zu 30 Tage zur Missbrauchsüberwachung speichern; kein Training**“
- AVV v1.6, Anlage 2 Historie: „Fassung 1.6 (05.10.2026): … Speicherung zur Missbrauchsüberwachung bei Microsoft und OpenAI ergänzt“
- DSE v1.5, Abschnitt 4 (Tabelle Microsoft): „(ohne Kundengespräche, Zugangsschlüssel werden vorher maskiert; **Microsoft kann die Texte bis zu 30 Tage zur Missbrauchsüberwachung speichern, kein Training**)“
- 3.1 Nr. 4 (alte Zeile): „Abuse Monitoring: 30 Tage Speicherung, in AVV Anlage 2 und 4.1 genannt“ – diese Zeile ist durch 3.1 D (Zeile Microsoft, 08.10.2026) überholt, steht aber noch so da.

**Stützt die Microsoft-Doku die 30 Tage noch?** **Nein.** Weder „Abuse monitoring“ (Stand 19.05.2026) noch „Data, privacy, and security“ (Stand 19.05.2026) nennen eine Frist. Belegt ist nur: automatisierte Prüfung speichert nichts; für die menschliche Prüfung gibt es einen Datenspeicher je Geografie; keine Höchstdauer. Microsoft-Q&A vom 02.10.2026: „No retention maximum is published“. Frühere Fassungen der Doku (bis ca. 2024) nannten „up to 30 days“; die Zahl stammt von dort.

**Rechtliche Einordnung:** Der Satz „bis zu 30 Tage“ ist eine Zusage von Lymbe gegenüber dem Kunden (Art. 28 Abs. 3 lit. a/g – Lymbe muss wissen, was der Unterauftragsverarbeiter tut) und zugleich eine Information nach Art. 13/14 in der DSE. Eine Frist, die die Quelle nicht mehr hergibt, ist eine unbelegte Behauptung – nach dem Grundsatz aus 5.9 („Was nicht bestätigt werden kann, wird im Vertrag geändert“) sollte sie raus. Da die Änderung für den Kunden keine Verschlechterung der Leistung ist, sondern eine Berichtigung, dürfte § 4 (Änderungsmitteilung mit 30 Tagen Frist) greifen; ob die Pilotkundin aktiv informiert werden muss, bitte der Anwalt bewerten (derselbe Fall wie A37).

**Empfehlung: umformulieren, nicht nur kürzen.** Ein bloßes „zur Missbrauchsüberwachung“ lässt offen, wie lange und wer – das ist für eine Praxis/Kanzlei als Kunde wenig hilfreich. Vorschlag:

*AVV Anlage 2 Nr. 4, Spalte Daten:*
> „Beschreibungstexte; Sprachaufnahmen. Microsoft prüft Ein- und Ausgaben der Werkstatt automatisiert auf Missbrauch; nur auffällige Inhalte kann Microsoft vorübergehend für eine Prüfung durch eigene, im EWR tätige Mitarbeiter speichern – getrennt je Kunde, in der Geografie der Ressource (Deutschland). Kein Training.“

*DSE v1.5, Abschnitt 4, Tabelle Microsoft:*
> „… (ohne Kundengespräche, Zugangsschlüssel werden vorher maskiert; Microsoft prüft die Texte automatisiert auf Missbrauch und kann auffällige Inhalte vorübergehend zur Prüfung durch Mitarbeiter im EWR speichern; kein Training)“

Wer die Zahl behalten will, müsste sie bei Microsoft schriftlich bestätigen lassen (Support-Ticket) und die Antwort im Ordner ablegen – dann wäre „bis zu 30 Tage“ wieder belegt. Ohne das: ändern.

Nebenbefund: Für **OpenAI** (Anlage 2 Nr. 5, DSE Abschnitt 4 und 5) steht ebenfalls „bis zu 30 Tage“ – das ist dort durch die OpenAI-API-Bedingungen („retained for up to 30 days“) gestützt und nicht Gegenstand dieser Prüfung; die beiden Aussagen bitte nicht versehentlich gemeinsam ändern.

---

## Kurzfazit

- A6 bestätigt; Art. 28 Abs. 3 a–h vollständig in Anlage 1. Zwei Präzisierungen: „kein Training“ steht nicht in der DPA (nur Learn/Product Terms); 5.9 B3 ordnet „DPA S. 9“ dem Training zu, dort steht aber nur Profilbildung/Werbung.
- A7 bestätigt (wörtliches Zitat vorhanden), mit Vorbehalt „without your permission or instruction“ – für den tatsächlichen Einsatz unschädlich.
- A8 bestätigt: keine Frist mehr in der Doku; Speicher je Geografie; Prüfer im EWR; Modified Abuse Monitoring nur auf Antrag für „managed customers“.
- A9 bestätigt: „fast transcription … does not retain or store“; „Logging is disabled by default“; Code nutzt Fast-Transcription ohne Logging-Parameter.
- B1: Screenshots decken Germany West Central + Datenzonenstandard (EUR) für `lymbe-ai`; Speech-Ressource ohne Screenshot.
- C3: „Werkstatt in der EU-Datenzone“ gedeckt; „Frankfurt“ bei Speech lieber „Deutschland“.
- C4: „bis zu 30 Tage“ nicht mehr belegt – umformulieren (Vorschlagstext oben).
- A12: Rechtsträger/Sitze stimmen bis auf Slack (EU-Vertragspartner ist Slack Technologies Limited, Dublin). DPF-Zertifizierungen von Google LLC, Microsoft Corporation, WhatsApp LLC, Salesforce über Firmenangaben bestätigt, Meta Platforms, Inc. nicht direkt lesbar; Registereinträge auf dataprivacyframework.gov nicht abrufbar. **Fehler in der Text-Vorlage:** Der Dialog schreibt die DPF-Zertifizierung der irischen Gesellschaft zu („Google Ireland Limited ist … zertifiziert“) – zertifiziert ist immer die US-Gesellschaft; Satz anpassen.
