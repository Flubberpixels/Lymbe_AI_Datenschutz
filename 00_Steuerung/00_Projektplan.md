# Lymbe AI – DSGVO-Projektplan

Stand: 11.10.2026, Fassung 4 (Protokoll fortgeschrieben; Tabellen zeigen den Planungsstand vom 02.10., aktueller Stand der Dokumente in 02_Finale_To_Dos Abschnitt 1) · Ziel: Livegang mit erster Pilotkundin am 08.10.2026 (kein Betatest – echter Betrieb mit eingeschränktem Kundenkreis) · Verantwortlich: Dennis (Projektleitung Datenschutz)

Pilotkundin: Autismustherapiezentrum · nutzt Website-Bot, Digitaler Mitarbeiter, Frag Lymbe mit Websuche, WhatsApp (seit 08.10.2026 live) · nicht: Abläufe, Kalender

## Rollen

| Rolle | Wer |
|---|---|
| Anbieter / Auftragsverarbeiter gegenüber Kunden | Flubber Pixels UG, Florastraße 56, 40822 Mettmann |
| Technischer Betrieb / Unterauftragsverarbeiter | Christian Gudermann, 26lab.io |
| Rechtliche Prüfung (nach Livegang) | Anwalt (noch zu beauftragen) |

Grundsatz: Kunden sind Verantwortliche, Flubber ist Auftragsverarbeiter, 26lab ist Unterauftragsverarbeiter. Beteiligung 50/50 (Flubber, 26lab) und interne Haftung im Partnerschaftsvertrag (2.1).

## Was schon da ist

| Dokument | Fundort | Stand | Bewertung |
|---|---|---|---|
| AVV für Kunden | lymbe.ai/avv | v1.5, Sept. 2026 | Gut, wird v1.6 (1.1); seit 11.10.2026 Fassung 1.7 |
| Datenschutzerklärung | lymbe.ai/datenschutz | v1.4, Sept. 2026 | Gut, wird v1.5 (4.1); seit 11.10.2026 Fassung 1.6 |
| Impressum | lymbe.ai/impressum | Sept. 2026 | OK, keine Änderung |
| Zustimmungs-Nachweis AVV | Portal (Checkbox beim Workspace-Anlegen) | seit 17.09.2026 | Erledigt – die 4 Bestandsmandanten sind Testmandanten und werden beim Livegang gelöscht |
| Dienstleisterverzeichnis | Briefing/Lymbe Dienstleisterverzeichnis.pdf | 17.09.2026 | Sehr gut, Basis; Korrekturen P2 |
| Inhaltsverzeichnis | 01_Inhaltsverzeichnis.md | Fassung 2 | abgenommen |
| Prüfprotokoll | 02_Pruefprotokoll.md + 02a Detail | 02.10.2026 | Grundlage für Fassung 2 |

---

## Entscheidungen (Dennis, 02.10.2026)

| Nr | Entscheidung | Folge |
|---|---|---|
| E1 | Werkstatt läuft nur über Azure (EU-Datenzone) | AVV/Datenschutz bleiben bei Microsoft; Technik stellt Christian um (5.9) |
| E2 | Backups 7 Tage | AVV bleibt; Technik stellt Christian um (5.9) |
| E3 | Vom Kunden verbundene Dienste sind keine Unterauftragsverarbeiter | AVV § 5 + Portal-Hinweis beim Verbinden. Ausnahme Meta/WhatsApp: Anwalt klärt Rollenkette (P3) |
| E4 | Websuche in Frag Lymbe bleibt, OpenAI bleibt Empfänger | SCC + Suchbegriff-Generator (05.10.: kein Schalter, Websuche ist Teil des Leistungsumfangs, auch für die Pilotkundin an) |
| E5 | Verarbeitungsverzeichnis + DSFA-Vorprüfung vor Livegang, TOMs ausführlich danach | – |
| E6 | Kein Betatest, sondern Livegang mit Pilotkundin – Verträge gelten ab Tag 1; keine Einzelverträge, Pilotkundin akzeptiert AGB + AVV wie alle | – |
| E8 | Keine Fragen an Christian, nur Aufgaben | Freigabeprotokoll 5.9 als Abnahmeliste |
| E7 | Pilotkundin ist Therapiezentrum → Art.-9-Regeln gelten | AVV § 12 + Anlage 5 (§ 203), DSFA-Plattformseite vor Livegang |
| E9 | Ein AVV für alle, eine Checkbox, keine Branchenabfrage; 1.7 geht in AVV § 12 auf | 1.1 |
| E10 | Keine Abschaltungen durch Lymbe – stattdessen Suchbegriff-Generator ohne Personenbezug (Christian) und Kundenpflichten | 5.9 B1, AVV § 3 Abs. 10 |

## Offene Entscheidungen (Dennis)

| Nr | Frage | Warum |
|---|---|---|
| O1 | ~~Digitaler Mitarbeiter: Patientendaten?~~ Entschieden: ja, erlaubt (AVV § 12 Abs. 2: kein Primärsystem) | – |
| O2 | Bestandsmandanten – entschieden 05.10.2026: alle 4 sind interne Testmandanten ohne Kundendaten, Löschung beim Livegang | Art. 28 Abs. 9 |
| O3 | Cloud-Konten – entschieden 05.10.2026: Hetzner = 26lab, STACKIT/Azure/OpenAI = Flubber (5.9 A23, 2.1 § 17) | AVV § 4, 2.1 § 17 |
| O4 | Selbstlernen: Standard aus für alle Mandanten? | In allen Dokumenten so vorausgesetzt – bitte bestätigen |
| O5 | DSB – entschieden 05.10.2026: kein DSB (5.11) | § 38 Abs. 1 S. 2 BDSG |

---

## VOR DEM LIVEGANG (bis 05.10.) – P1

### Aufgaben für Christian (Anweisungen)

| Nr | Aufgabe | Status |
|---|---|---|
| C1 | Freigabeprotokoll 5.9 abarbeiten und mit Datum bestätigen (Werkstatt Azure, Backups 7 Tage, Gesprächslöschung 90 Tage, Selbstlernen-Default, Admin-Protokoll, Mistral aus, Azure Speech, Messenger/Instagram, Einordnung ohne Emotionserkennung, Kontoinhaber, Wächter-Meldeweg) | offen |
| C2 | Suchbegriff-Generator der Websuche: feste Regel „kein Personenbezug", mit Testfragen belegt | offen |
| C3 | Fünf Nachweise in 03_Dienstleister ablegen: Hetzner-AVV, STACKIT-AVV, Microsoft-DPA, OpenAI-DPA (unterschrieben), Stripe-DPA | offen |
| C4 | KI-Kennzeichnung im Widget und Portal-Chat; sichtbarer Wechsel Mensch ↔ KI im Live-Chat | offen |
| C5 | Hinweis vor der Websuche in Frag Lymbe (Text aus 1.5) | offen |
| C6 | Hinweis im Portal beim Verbinden eines Kontos mit Anbieter und Standort (Text aus 1.5) | offen |
| C7 | Bot-Satz vor Kontaktabfrage (Leads/Termine) einbauen (Text aus 1.5) | offen |
| C8 | Demo-Widget: Chats, Leads und Termine nach 24 h löschen, kein Gedächtnis | erledigt 08.10.2026 (5.9 C1) |
| C9 | Vertraulichkeitsverpflichtung 5.3 und § 203-Erklärung (AVV Anlage 5) unterschreiben | offen |
| C10 | Testmandanten beim Livegang löschen und Löschung bestätigen | offen |

### Dokumente (Reihenfolge = Schreibreihenfolge)

| Nr | Was | Zuständig | Status |
|---|---|---|---|
| 5.10 | Rollen-Matrix | Cowork | final (Gesamtprüfung) |
| 5.9 | Freigabeprotokoll „Vertrag = Maschine" | Cowork → Christian | Entwurf 1 → an Christian |
| 1.1 | AVV Kunden v1.7 inkl. § 12 + Anlage 5 (1.6 vom 05.10., 1.7 vom 11.10.) | Cowork → Dennis | final, 2× geprüft + Gegenprüfung 08a |
| 1.7 | Plattformbeschreibung + Kurz-DSFA für Kunden (aus 5.2 Teil 2) | Cowork → Kundin | final |
| 2.1 | Partnerschaftsvertrag Lymbe (Flubber Pixels UG ↔ 26lab.io) – Beteiligung 50/50, Zusammenarbeit, Auftragsverarbeitung | Cowork → Dennis, Christian, Anwalt | final, Anwalt prüft |
| 2.2 | – entfallen, in 2.1 aufgegangen | – | erledigt |
| 4.1 | Datenschutzerklärung v1.6 (1.5 vom 05.10., 1.6 vom 11.10.) | Cowork → Dennis | final (Gesamtprüfung) |
| 1.0 | AGB Fassung 1.4 (vollständig; 1.3 vom 05.10., 1.4 vom 11.10.) | Cowork → lymbe.ai/agb | final |
| 1.2 | – entfallen (keine Einzelverträge) | – | erledigt |
| 1.3 | Textbaustein Datenschutzerklärung Kunden | Cowork → Kundin | final (Gesamtprüfung) |
| 1.5 | Widget-/Kanal-Hinweistexte | Cowork → Christian | final (Gesamtprüfung) |
| 1.6 | Textbaustein Information der Beschäftigten | Cowork → Kundin | final (Gesamtprüfung) |
| 5.3 | Vertraulichkeitsverpflichtung | Cowork → Dennis, Christian | final (Gesamtprüfung) |
| 5.6 | Vorfall-Prozess Kurzfassung | Cowork → Dennis | final (Gesamtprüfung) |
| 5.7 | Betroffenenanfragen Kurzfassung | Cowork → Dennis | final (Gesamtprüfung) |
| 5.8 | § 25-Bewertung Browserspeicher | Cowork | final (Gesamtprüfung) |
| 5.1 | Verarbeitungsverzeichnis (Abs. 1 + Abs. 2) | Cowork | final (Gesamtprüfung) |
| 5.2 | DSFA-Vorprüfung Flubber | intern | final |
| 5.11 | DSB-Entscheidung | Cowork → Dennis | final – Entscheidung Dennis (D2) |
| 3.1 | Checkliste Dienstleister-AVVs | Cowork → Christian (C3) | final (Gesamtprüfung) |
| 1.4 | Vorlage Änderungsmitteilung | Cowork | final (Gesamtprüfung) |

### Prüfung je Dokument (Pflicht vor Übergabe an Dennis)
1. Gegen die gesetzliche Pflichtliste (Art. 28 / Art. 13 / Art. 50 KI-VO / § 25 TDDDG) – Prüfprotokoll als Anhang
2. Gegen das Dienstleisterverzeichnis (jeder Datenweg einem Dokument zugeordnet)
3. Gegen das Portal (jede Funktion hat eine Grundlage)
4. Unabhängiger Prüf-Agent liest gegen, Ergebnis fließt ein

---

## NACH DEM LIVEGANG – P2 (vor breitem Verkauf)

| Nr | Was | Zuständig |
|---|---|---|
| 5.4 | TOMs ausführlich | Christian + Cowork |
| 5.5 | Löschkonzept vollständig | Christian + Cowork |
| 5.18 | Transfer-Folgenabschätzung OpenAI/Microsoft | Cowork → Anwalt |
| 5.19 | KI-VO-Einstufung | Cowork → Anwalt |
| 5.14 | KI-Kompetenz-Nachweis + Kunden-Merkblatt | Cowork |
| 5.15 | Rollen-/Rechtekonzept Portal | Christian + Cowork |
| 1.8 | AVV-Änderungsverfahren Textfassungen | Cowork |
| 1.9 | Anlage Ansprechpartner | Cowork |
| 1.10 | Export-/Rückgabeformat | Christian + Cowork |
| 3.3 | Meta-/Shopify-Verträge und Rollendoku | Dennis + Cowork |
| – | Dienstleisterverzeichnis korrigieren (Azure Speech, Wächter, Stripe-Cookies, Kontoinhaber) | Christian |
| – | Zertifikate der Cloud-Anbieter ablegen | Christian |
| – | Volle DSFA, falls 5.2 ergibt | Cowork → Anwalt |
| – | Anwaltliche Prüfung aller Dokumente | Anwalt |

## P3 – Anwalt klärt
DSB-Pflicht für Auftragsverarbeiter · Art. 50 Abs. 2 KI-VO · Rolle bei Frag Lymbe/Demo · Rechtsgrundlage Websuche · Meta-Rollenkette · § 203 StGB zweistufig · Haftung 2.1 § 14 vs. Art. 82 · Innengesellschaft 2.1 · Minderjährige und Leads

---

## Ordnerstruktur

```
Lymbe DSGVO/
  00_Projektplan.md
  01_Inhaltsverzeichnis.md
  02_Pruefprotokoll.md · 02a_Pruefprotokoll_Detail.md
  01_Kunden/
  02_26lab/
  03_Dienstleister/
  04_Oeffentlich/
  05_Intern/
  Briefing/
```

## Protokoll

- 02.10.2026 (Abschluss): Gesamtprüfung durch unabhängigen Prüf-Agenten (05_Gesamtpruefung.md) – 17 Blocker, 27 Widersprüche. Alle von Cowork behebbaren Punkte eingearbeitet (u. a. Websuche als Maßnahme statt Garantie, Fristen vereinheitlicht, 1.6-Anschrift, 4.1 USA-Aussage, 2.1-Verweise, 5.3 Freigabe/Strafmaß, Sie-Fassungen in 1.5, Vermerke und Anwaltslisten aus den Verträgen in 04 verschoben). Verbleibend: technische Bestätigungen durch Christian (04 A), Entscheidungen Dennis (04 B), Anwalt (04 C). Urteil des Prüfers: an den Anwalt ja; an die Kundin erst nach Freigabeprotokoll.

- 02.10.2026 (spät): Finale Fassung. 1.7 in AVV § 12 + Anlage 5 aufgegangen; alle Abschaltungs-Regeln entfernt, ersetzt durch Suchbegriff-Filter (5.9 B1) und Kundenpflichten; Platzhalter mit echten Daten gefüllt (26lab-Anschrift aus Impressum, Flubber-Telefon); Fristen 30/14/30 Tage gesetzt (Bestätigung durch Christian in 5.9 offen); 04_Offene_Punkte.md angelegt; alte Dateien in Alt_archiv/. Gesamtprüfung durch Prüf-Agent folgt.

- 02.10.2026 (abends, Dennis beim Sport): Alle 21 P1-Dokumente als Entwurf 1 geschrieben und in die Unterordner gelegt. 1.1 und 1.7 mit unabhängiger Prüfung (Entwurf 2). Entscheidungen von Cowork ohne Rückfrage: AGB v1.2 wird nicht neu geschrieben, sondern per Änderungsliste (1.0) ergänzt; Haftung im Kooperationsvertrag nach Verursachung, im Zweifel hälftig (statt starr 50/50); DSB-Empfehlung: beim zweiten Gesundheits-/Rechtskunden oder nach Anwaltsvotum; Selbstlernen Standard aus in allen Dokumenten vorausgesetzt. Status-Übersicht: 03_Status_fuer_Dennis.md.
- 02.10.2026 (spät): Auf Entscheidung von Dennis AVV Flubber↔26lab (2.1) und Kooperationsvertrag (2.2) ins Archiv; ersetzt durch einen Partnerschaftsvertrag Lymbe (2.1) zwischen Flubber Pixels UG (Marion Schagen, Dennis als Bevollmächtigter) und 26lab.io (Christian Gudermann): Beteiligung je 50 %, Zusammenarbeit, Auftragsverarbeitung in Teil C, gegenseitige Übernahme bei Krankheit/Tod, Weg zur eigenen UG. Neue Anwaltsfragen J24–J28, Entscheidungen D3/D4/D7 neu gefasst.
- 05.10.2026: Ordnerstruktur bereinigt (00_Steuerung, 06_Pruefungen, Anbieter-Unterordner in 03). Kein DSB (5.11). 5.3 als fertige Exemplare. Register 5.12/5.13 angelegt. 5.2 geteilt: Kundenteil jetzt 1.7. Kontoinhaber festgelegt: Hetzner = 26lab, STACKIT/Azure/OpenAI = Flubber. OpenAI-DPA abgeschlossen (Dennis); 30-Tage-Speicherung zur Missbrauchsüberwachung bei Microsoft und OpenAI in AVV Anlage 2, 4.1 und 1.7 ergänzt. Neue Aufgaben A26/A27, D9/D10.
- 05.10.2026 (nachmittags): Zweite Gesamtprüfung durch zwei unabhängige Prüfer (Recht 07a, Technik 07b, Zusammenfassung 07 in 06_Pruefungen). 44 Widersprüche und 12 Finalitätsverstöße behoben; AVV-Unterschriftsseite, Register 5.14/5.15/5.17 und Testprotokoll 5.16 angelegt; Sicherheits-Checkliste 05 in 00_Steuerung; Fristen Mi 08.10./So 12.10. in 04; Anwaltsfragen J29–J42. Livegang-Datum auf 08.10.2026 korrigiert.
- 05.10.2026 (abends): 03_Status, 04_Offene_Punkte und 05_Sicherheits-Checkliste zu 02_Finale_To_Dos.md zusammengeführt (alte Dateien in Alt_archiv). Konten: STACKIT beide Owner (erledigt), Hetzner trägt Christian Dennis ein (A12), OpenAI/Azure trägt Dennis Christian ein (D13). Neue Aufgabe A38: Downloads 1.3/1.6/1.7 im Portal.
- 05.10.2026 (18:30): Liste 02 nach Prüfung bereinigt (30 Funde). Entscheidung Dennis: Anwalt verschoben (Budget); Partnerschaftsvertrag 2.1 wird am Mittwoch ohne Vorprüfung unterschrieben, D3/D4/D7 bis Dienstag entscheiden; 2.1 § 21 Abs. 4 Gerichtsstand (soweit gesetzlich zulässig) ergänzt (J29). Verweise auf „04“ in Prüfberichten und älteren Protokollzeilen meinen jetzt 02_Finale_To_Dos, Nummern (A/D/K/J) unverändert.
- 05.10.2026: Entscheidung Dennis: Livegang Mittwoch mit Website-Bot UND WhatsApp (Kundin verbindet ihr Meta-Konto selbst, AVV § 5); Frag Lymbe MIT Websuche ab Mittwoch. Entscheidung Dennis 16:45: Es gibt keinen Mandanten-Schalter und es wird keiner gebaut – Websuche ist Teil des Leistungsumfangs (AVV § 3 Abs. 10 neu: Weisung durch Vertragsabschluss, abbestellbar in Textform); Absicherung ausschließlich Suchbegriff-Generator + Filter + Testprotokoll 5.16 (30/30 als Freigabekriterium). Texte angepasst: AVV § 3 Abs. 1/10, Anlage 2 Nr. 5, Anlage 3; 1.5 G (Hinweis statt Einschalt-Dialog, Blockiermeldung); 1.6; 1.7; 4.1 Abschn. 5; 5.1 A4; 5.9 A10; 04 A22/A5/A32. A9/A14 J in den Mittwoch-Block, K8 für die Kundin.
- 11.10.2026: Finaler Ordner „Lymbe DSGVO Final" aus Dennis' Stand 05.10., Christians Stand 08.10. (Belege, 5.9-Messungen, 3.1 D, 08_Gegenprüfung) und der Notion-Liste zusammengeführt; Notion abgeschafft. Gegenprüfung von Christians Einträgen durch Cowork (06_Pruefungen/08a mit Belegen 08b/08c): 10 von 12 Aussagen bestätigt, abweichend STACKIT-Standort (vertraglich nur EU/EWR) und Rolle von 26lab im Hetzner-Vertrag. Entscheidungen Dennis: STACKIT ehrlich als „EU/EWR (vertraglich); Rechenzentrum in Deutschland nach Angabe des Anbieters" bis zur schriftlichen Zusage (D20); alle Textpunkte aus 08a umgesetzt. Neue Fassungen: AVV 1.7 (Fristen wie im Betrieb – Kontakte/Termine 90 Tage, ausgeführte Abläufe 90, Schrittprotokolle 30, Sicherungen bis 14, nach Vertragsende 44 Tage; Verschlüsselung ohne Datenträger, dafür ISO-27001-Rechenzentrum; Microsoft ohne „30 Tage"; Spracheingabe Deutschland; § 11 Abs. 5 an richtiger Stelle), AGB 1.4 (AVV in jeweils veröffentlichter Fassung), DSE 1.6, 1.3/1.5/1.6 je 1.1 (Stimmungs-Einordnung, Besuchsanalyse, Browserspeicher nach Messung, Microsoft bei Spracheingabe, Demo-Leads 24 h, Frag-Lymbe-Verläufe ohne Admin-Einsicht), 1.7, 5.1 1.1, 5.8, 5.9 (B4/C2 ✅, A4/A14b/A23 aktualisiert, 2.1 unterschrieben 08.10.), 5.12 (Eintrag 2026-01 Löschlauf-Störung), 5.14 (Dienstleister-Geheimhaltung). Fund: AVV im Portal war seit 06.10. ein anderer Text als 1.6 in der Datei – daher 1.7 und Aufgabe A42 (Christian übernimmt 1.7/1.6 ins Portal, bevor die Kundin bestätigt). Neue Aufgaben D20–D25, A42–A52, J44–J46. Christian ändert im Code; Cowork arbeitet nur im Ordner.
- 11.10.2026 (abends): Entscheidung Dennis: Thema bis Dienstag 14.10. komplett abschließen. Partnerschaftsvertrag als Fassung 2 (AVV in jeweils veröffentlichter Fassung, ersetzt Unterschrift vom 08.10.) zur Neuunterzeichnung; Ordner 07_Unterschreiben_Final mit allen Unterschriftsdokumenten angelegt; D24 entfällt.

- 02.10.2026: Pilotkundin benannt (Autismustherapiezentrum, Umfang Website-Bot + Digitaler Mitarbeiter + Frag Lymbe). Art.-9-Paket (1.7) als P1 aufgenommen. Inhaltsverzeichnis und Projektplan auf Fassung 2.
- 02.10.2026: Unabhängige Prüfung des Inhaltsverzeichnisses (02_Pruefprotokoll). 9 neue P1-Dokumente, 7 Fehler korrigiert (u. a. OS-Plattform-Link, Stripe-Rolle, Vorfall-Prozess vorgezogen).
- 02.10.2026: Inhaltsverzeichnis Fassung 1 abgenommen. Klarstellung: Livegang mit Pilotkundin, kein Betatest.
- 02.10.2026: Entscheidungen E1–E5, Fragen an Christian in Aufgaben umgewandelt.
- 02.10.2026: Projektstart. Rollenmodell festgelegt. Bestandsaufnahme AVV v1.5, Datenschutz v1.4, Impressum, Dienstleisterverzeichnis.
