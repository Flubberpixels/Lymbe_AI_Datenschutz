# Prüfprotokoll Inhaltsverzeichnis – Zusammenfassung für Dennis

Stand: 02.10.2026 · Geprüft: 01_Inhaltsverzeichnis.md, 00_Projektplan.md, Dienstleisterverzeichnis · Prüfer: unabhängiger Prüf-Agent (hat die Entwürfe nicht geschrieben)
Vollständiges Protokoll mit allen Artikeln: `02a_Pruefprotokoll_Detail.md` (342 Zeilen, für den Anwalt)

Prioritäten: **P1** = vor Livegang zwingend · **P2** = vor breitem Verkauf · **P3** = Anwalt klärt

Gesamturteil des Prüfers: Struktur ungewöhnlich gut für 3 Tage. Die Risiken liegen nicht in fehlenden Kapiteln, sondern in **Rollenfehlern, Zusagen, die die Technik nicht hält, und drei Personengruppen, die niemand informiert.**

---

## 1. Was ich (Cowork) falsch hatte – korrigiert

| Fehler | Richtig |
|---|---|
| Impressum: „OS-Plattform-Link ergänzen" | **Falsch.** Die EU-Streitschlichtungsplattform ist seit 20.07.2025 abgeschaltet (VO (EU) 2024/3228). Ein Link wäre irreführend. Aufgabe D8 gestrichen. |
| Stripe als Unterauftragsverarbeiter im Kunden-AVV | **Rollenfehler.** Stripe verarbeitet eure eigenen Rechnungsdaten der Kunden-Firmen – dafür ist Flubber Verantwortlicher, nicht Auftragsverarbeiter. Stripe gehört in die Datenschutzerklärung, raus aus AVV § 4. |
| Microsoft: „Drittland nicht nötig" | Zu absolut. EU-Datenzone deckt Kundendaten, nicht alle Support-/Telemetriedaten. Formulierung: „EU-Datenzone; Rest-Übermittlungen über SCC/DPF". |
| „Nur der Suchbegriff geht an OpenAI" | Der Suchbegriff wird aus der Nutzerfrage gebildet und kann Namen, Orte, Gesundheitsbezüge enthalten. Der Hinweistext darf nicht behaupten, es gingen keine personenbezogenen Daten. |
| 1.3 behauptet „Browserspeicher technisch erforderlich" | Christian selbst markiert das als offen (0.5). Braucht eine eigene Bewertung (neues Dokument 5.8). |
| Vorfall-Prozess und Betroffenenanfragen „nach Livegang" | Der AVV verspricht 24 h Meldung ab Tag 1 – ohne Prozess unerfüllbar. Beide als Kurzfassung (je 1 Seite) **vor** Livegang. |
| DSB-Begründung „unter 20 Personen" | Unvollständig. § 38 Abs. 1 S. 2 BDSG: Wer DSFA-pflichtige Verarbeitungen hat, braucht einen DSB **unabhängig von der Personenzahl**. Ergibt die DSFA-Vorprüfung „ja", folgt die DSB-Pflicht. Externer DSB ist kurzfristig buchbar. |

## 2. Vertrag sagt A, Maschine macht B (P1)

Das ist das Muster, das ein Prüfer der Behörde zuerst sucht. Christian hat es im Verzeichnis selbst benannt (0.7). Lösung: **ein Freigabeprotokoll „Vertrag = Maschine"** (neues Dokument 5.9), das Christian vor Livegang mit Datum bestätigt – kein Fragenkatalog, eine Abnahmeliste:

| Zusage im Vertrag | Stand laut Verzeichnis | Christian bestätigt |
|---|---|---|
| Werkstatt läuft über Azure | OpenAI geschaltet, Azure aus | ☐ umgestellt |
| Backups 7 Tage | 30 Tage | ☐ umgestellt |
| Gespräche werden nach 90 Tagen gelöscht | **nicht gemessen**, nur Abläufe 30 Tage | ☐ läuft |
| Selbstlernen Standard aus | unbekannt | ☐ |
| Admin-Zugriff 26lab wird protokolliert | unbekannt | ☐ |
| Mistral-Rückfall (G2) aus oder gelistet | im Code vorhanden | ☐ |
| Azure Speech live? | im Verzeichnis **nicht enthalten**, in Datenschutz aber genannt | ☐ |
| Messenger/Instagram über die Meta-App aus oder abgedeckt | „über dieselbe App" (A7) | ☐ |
| „Einordnung jeder Nachricht" (gpt-oss) erkennt keine Emotionen | unbekannt – wäre Art. 5 KI-VO (verboten am Arbeitsplatz) | ☐ |
| Wer ist Vertragsinhaber der Konten Hetzner/STACKIT/Azure/OpenAI: Flubber oder 26lab? | unklar | ☐ |

Der letzte Punkt entscheidet, wie AVV § 4 und der 26lab-AVV gebaut werden (hält 26lab die Konten, sind die Clouds „Sub-Sub-Prozessoren" und laufen über 2.1).

## 3. Drei Gruppen, die niemand informiert (P1)

| Gruppe | Problem | Lösung (neu im Verzeichnis) |
|---|---|---|
| **WhatsApp-Nutzer** | Sehen die Kundenwebsite nie, bekommen keinen KI-Hinweis, keinen Datenschutzlink | 1.5 Widget-/Kanal-Hinweistexte: Erstnachricht-Vorlage für WhatsApp |
| **Beschäftigte der Kunden** (Digitaler Mitarbeiter, Frag Lymbe, Live-Chat) | Ihre Fragen sind Verhaltensdaten, Admins können sie einsehen, Suchbegriffe gehen in die USA – Mitbestimmung beim Kunden | 1.6 Textbaustein „Information der Beschäftigten" |
| **Leads** (Bot fragt nach Name/E-Mail) | Art. 13 verlangt Info **im Moment der Erhebung** | 1.5: Bot-Satz vor der Kontaktabfrage |
| **Demo-Nutzer auf lymbe.ai** | Flubber ist hier selbst Verantwortlicher – nirgends geregelt | Absatz in 4.1 + Regel: Demo-Chats nach 24 h löschen, kein Gedächtnis, keine Leads |

## 4. Produktspezifische Risiken (P1)

- **Selbstlernen:** Inhalte aus Gesprächen (90-Tage-Frist) werden dauerhaft Wissen und können anderen Besuchern ausgespielt werden. Empfehlung: Standard **aus**, Einschalten = dokumentierte Weisung des Kunden; bei Gesundheits-/Rechtskunden zwingend aus.
- **IMAP-Postfächer:** größter Datenumfang (komplette Mails Dritter inkl. Anhänge). AVV § 2 muss das als Datenkategorie nennen, § 6 muss den Kunden verpflichten: nur dienstliche Postfächer, keine Privatnutzung.
- **Art.-9-Daten** (Friseur ist unkritisch, Therapie/Arzt/Anwalt kritisch): schon ein Termin beim Therapeuten ist ein Gesundheitsdatum. Falls die Pilotkundin aus dem Bereich kommt: Zusatzpaket (§ 203 StGB-Verpflichtung für dich und Christian, Websuche/Selbstlernen aus, DSFA der Kundin **vor** Livegang).
- **Admin-Zugriff 26lab auf alle Mandanten:** Kunden müssen im AVV erfahren, dass Support-Zugriff auf Inhalte möglich ist und nur auf Ticket erfolgt; technisches Protokoll nötig, nicht nur Absichtserklärung.
- **Bestandsmandanten:** Das Verzeichnis zeigt 5 Mandanten-Datenbanken in Produktion und 4 Bestandsmandanten ohne AVV-Nachweis, WhatsApp seit 14.09. in Betrieb. Wenn das echte Kunden sind, ist „nach Livegang" nicht haltbar – erneute Checkbox beim nächsten Login (nicht rückdatieren).

## 5. Neue Dokumente (ins Inhaltsverzeichnis aufgenommen)

**Vor Livegang (P1):**
- 1.5 Widget-/Kanal-Hinweistexte (Widget, WhatsApp-Erstnachricht, Lead-Satz, Wechsel Mensch↔KI, Demo)
- 1.6 Textbaustein „Information der Beschäftigten" für Kunden
- 1.7 Zusatzvereinbarung Art. 9 / § 203 StGB (nur falls Pilotkundin Gesundheit/Recht)
- 5.6 Vorfall-Prozess Kurzfassung (vorgezogen)
- 5.7 Betroffenenanfragen Kurzfassung (vorgezogen)
- 5.8 § 25-Bewertung Browserspeicher (1 Seite)
- 5.9 Freigabeprotokoll „Vertrag = Maschine" (Christian bestätigt)
- 5.10 Rollen-Matrix: je Verarbeitung Flubber Verantwortlicher / Auftragsverarbeiter / Dritter
- 5.11 DSB-Entscheidung mit Begründung (gekoppelt an 5.2)

**Vor breitem Verkauf (P2):** Transfer-Folgenabschätzung OpenAI · DSFA-Vorlage für Kunden · KI-VO-Einstufung · KI-Kompetenz-Merkblatt (Art. 4) · Löschkonzept vollständig · AVV-Änderungsverfahren · Anlage Ansprechpartner · Meta-/Shopify-Verträge ablegen · Let's Encrypt in Verzeichnis + Datenschutz · Export-Format · Rollen-/Rechtekonzept Portal · Dienstleisterverzeichnis-Korrektur

**Anwalt (P3):** DSB-Pflicht für Auftragsverarbeiter · Art. 50 Abs. 2 KI-VO bei Chat-Text · Rolle bei Frag Lymbe und Demo · Rechtsgrundlage Websuche (Hinweis oder Einwilligung) · Meta-Rollenkette · § 203 StGB bei zweistufiger Kette · Haftung 50/50 vs. Art. 82 DSGVO · Minderjährige und Leads

## 6. Änderungen an bestehenden Dokumenten (P1)

- **AVV 1.1:** § 2 Datenkategorien vollständig (Mails Dritter, Shop-Kunden, Kalenderteilnehmer, WhatsApp, Sprache, Leads, Art. 9) · § 3 Hinweispflicht bei rechtswidrigen Weisungen · § 4 Stripe raus, Vertragsinhaber-Frage · § 8 Fristen ehrlich (nur was läuft) + „Löschung aus Backups mit Ablauf der Sicherungsfrist" · Support-Zugriff 26lab · Weisungen in Textform = Portal-Einstellungen
- **Datenschutz 4.1:** Rechtsgrundlage je Abschnitt · berechtigte Interessen · Demo · Zertifikate (Let's Encrypt) · Fristen konkret (Rechnungen 10 Jahre) · Stripe mit DPF
- **Nutzungsbedingungen 1.0:** nur B2B · Kunde ist KI-Betreiber · keine Anhang-III-Zwecke (Bewerber-/Mitarbeiterbewertung) · Art.-9 nur mit Zusatz · Beschäftigteninfo und Mitbestimmung Sache des Kunden
- **Textbaustein 1.3:** Referrer + IP bei jedem Seitenaufruf (auch ohne Chat) · Live-Chat · Leads · Benachrichtigungsziele (Slack/Teams USA) · Selbstlernen · Termine · Bewertungen · 90 Tage
- **Impressum 4.2:** nichts ergänzen

## 7. Was Dennis entscheiden muss

1. Branche der Pilotkundin (entscheidet über Art.-9-Paket und DSFA vor Livegang)
2. Die 4 Bestandsmandanten: Testmandanten (dokumentieren, Daten löschen) oder echte Kunden (AVV-Nachweis sofort)?
3. Wer hält die Cloud-Konten (Hetzner, STACKIT, Azure, OpenAI): Flubber oder 26lab?
4. Selbstlernen: Standard aus?
