# Gesamtprüfung 2 – Stand 05.10.2026

**Lymbe AI Datenschutz · zwei unabhängige Prüfer (Recht: 07a, Technik: 07b) · Livegang 08.10.2026 · Was daraus sofort umgesetzt wurde und was offen bleibt**

## 1. Ergebnis in drei Sätzen

Die Dokumente sind rechtlich vollständig (Art. 28 Abs. 3 a–h, Art. 13/14, Art. 33/34, § 203-Kette, Art. 28 Abs. 9) und untereinander konsistent; 44 kleinere Widersprüche und 12 Verstöße gegen die Finalitätsregel wurden heute behoben. Die Lücke liegt zwischen Vertrag und Maschine: Das Dienstleisterverzeichnis vom 17.09. belegt 10 von 38 technischen Zusagen, 13 sind Konfiguration, 13 sind Bauaufgaben (9–14 Entwicklertage), 5 sind unklar. Entscheidung nach der Prüfung (16:45): Start mit Website-Bot, WhatsApp (Kundin verbindet ihr Meta-Konto) und Frag Lymbe mit Websuche; es gibt keinen Websuche-Schalter, Absicherung ist der Suchbegriff-Generator mit Testprotokoll 5.16. Der Mittwoch-Block in 02_Finale_To_Dos Abschnitt 3 ist darauf zugeschnitten; alles andere ist bis Sonntag bzw. mit ⏳ und Datum im Freigabeprotokoll zu führen.

## 2. Heute umgesetzt (aus 07a)

| Bereich | Änderung |
|---|---|
| 1.1 AVV | Vertragsparteien ohne Formular-Behauptung; § 3 Abs. 5 Vier-Augen-Prinzip; § 4 Abs. 2 „§ 12 Abs. 3 bleibt unberührt"; § 8 Digitaler Mitarbeiter in 90-Tage-Zeile, Testphase-Sperre; § 12 Abs. 0 Anwendungsbereich statt Kursivvermerk, § 22 BDSG korrekt wiedergegeben, staatlich anerkannte Sozialpädagogen, § 53a StPO (Entscheidung beim Berufsgeheimnisträger), Kopie der Verpflichtungserklärung auf Anfrage, Satz-2-Verweis; § 11 Abs. 5 Abschluss als Klausel; **neue Unterschriftsseite** vor den Anlagen; Anlage 2 Nr. 4 Standort präzisiert; Anlage 5 ohne Vermerk |
| 1.0 AGB | AVV beim Anlegen des Workspace; Erfüllungsgehilfen-Vorbehalt in § 3 Abs. 4 / § 12 Abs. 5; Art. 50 KI-VO als eigene Kennzeichnung in allen Lymbe-Kanälen; Änderungsliste entfernt |
| 1.3 / 1.6 | Hinweise und Checklisten entfernt (Inhalt jetzt in 04 K2/K3); Browserspeicher-Liste einheitlich W1–W4 |
| 1.5 | Minderjährige unter 18; Verweis Abschnitt 5; sessionStorage-Marker ergänzt; Art. 9 lit. a als ausdrückliche Einwilligung; Kopfzeile ohne Erklärung |
| 4.1 | IP-Adresse 14 Tage statt „anonymisiert"; Nachweis-Rechtsgrundlage lit. f; Browserspeicher W1–W4; Stripe-Rolle |
| 2.1 | § 1 Abs. 3 Außenauftritt 26lab (Hetzner); § 2 Abs. 4 Flubber hält für die Partnerschaft; § 8 Regel für freiwilliges Ausscheiden von Dennis aus Flubber; § 12 Abs. 6 Flubber schließt Versicherung; § 17 Kontoinhaber schließt AVV; keine internen Dokumentnummern/Ordner; Dennis-Unterschriftszeile mit Rechteeinräumung und § 13 |
| 5.3 / 5.14 | § 42 BDSG korrekt; Vier-Augen; Register in eigene Datei 5.14 |
| 5.9 | Datum 08.10.; A3 Digitaler Mitarbeiter; A14 konkretisiert; A14b Sicherungen außer Haus/Verschlüsselung; B5 Zugriffsregister |
| neu | 5.15 Zugriffsregister, 5.16 Testprotokoll Suchbegriff-Generator (30 Fälle), 5.17 Änderungsmitteilungen-Register; 3.1 D Spalte „Geheimhaltung § 203" |
| Verweise | 1.4, 5.7, 5.8, 00, 01, 03, 04 (P2-Dokumente jetzt 5.18/5.19; J8, J9, J21, J22) |

## 3. Offen und für den Livegang entscheidend (aus 07a A und 07b 8; Aufgabennummern aus 00_Steuerung/02_Finale_To_Dos.md, früher 04)

| Nr | Punkt | Wer | Frist |
|---|---|---|---|
| 1 | Websuche: Suchbegriff-Generator mit Filter, Sperrliste, Blockiermeldung und Testprotokoll 5.16 (30/30) vor Livegang; vorher prüfen, ob heute die Nutzerfrage selbst an OpenAI geht (A32) | Christian | Mi 08.10. |
| 2 | Datensicherungen: 7 Tage (heute 30) und verschlüsselt an einen zweiten Ort (A2, A23, A28) | Christian | Mi 08.10. |
| 3 | Mistral-Rückfall aus (A7) | Christian | Mi 08.10. |
| 4 | Widget-Minimum: Startdialog, Rechtliches, Übergabe, KI-Badge, Sie (A14) | Christian | Mi 08.10. |
| 5 | Unterschriften 5.3, Anlage 5, 2.1; AVV-Unterschriftsseite mit der Kundin (A19, D11, K6) | Dennis, Christian, Marion | Mi 08.10. |
| 6 | Netzgrenze und Mandantentrennung nachmessen (A29, A30) | Christian | Mi 08.10. |
| 7 | 2FA auf allen Konten, SSH nur mit Schlüssel (A12) | Christian | Mi 08.10. |
| 8 | Vier Antworten: Azure Speech live, Einordnung ohne Emotion, Admin-Einsicht, Mikrofon im Widget (A8, A10, B8, A33) | Christian | Mi 08.10. |
| 9 | Testmandanten löschen (A20), fünfte Datenbank klären (A36) | Christian | Mi 08.10. |
| 10 | Werkstatt Azure + Region, 90-Tage-Job, Log-Fristen, Mandantentrennung messen, Audit-Tabelle, Workspace-Felder | Christian | So 12.10. |

## 4. Was nicht geändert wurde und warum

- „Frag Lymbe → OpenAI direkt" (Unterauftragsverarbeiter-Stand Z. 11) widerspricht dem Verzeichnis (nur Suchbegriff). Alle Dokumente bleiben beim Suchbegriff-Modell; A32 klärt es am Code. Falls die Frage selbst an OpenAI geht, ändern sich AVV § 3 Abs. 10, Anlage 2 Nr. 5, 4.1 Abschnitt 5 und 1.7.
- Azure Speech „seit 30.09.2026" (4.1) bleibt, bis A8 beantwortet ist; wenn nicht live, wird der Satz entfernt.
- Messenger/Instagram werden für die Pilotkundin abgeschaltet, WhatsApp läuft über ihr eigenes Meta-Konto (A9, K8); Hilfeseiten-Logo (P2) bleibt offen.
- Verschlüsselung ruhender Daten (Anlage 1 „AES-256") bleibt stehen, bis A37 beantwortet ist; Empfehlung der Technikprüfung: Satz auf das Belegbare anpassen.

## 5. Für den Anwalt

Neue Fragen J29–J42 in 04 Abschnitt C (Gerichtsstand nur unter Kaufleuten, § 10 als beurkundungspflichtiger Vorvertrag, Innengesellschaft nach MoPeG, Rechteinhaberschaft, Erfüllungsgehilfen, Art. 50 KI-VO, Testphase mit Gesundheitsdaten, Stripe, Rechtsgrundlage Nachweise, Art. 9 lit. a, § 53a StPO, Widerspruch bei § 203-Daten, Hetzner-Kette, Websuche-Restrisiko). Vollständige Begründungen in 07a Abschnitt D.
