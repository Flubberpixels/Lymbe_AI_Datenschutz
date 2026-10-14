# Nachtrag zu AGB 1.4 und Datenschutzerklärung 1.6 (13.10.2026)

Beim Einbau ins Portal ist aufgefallen: In AGB 1.4 und in der DSE 1.6 fehlen drei Stellen, die in den Vorfassungen (AGB 1.3, DSE 1.5) standen. Die Plattform arbeitet genau so, wie diese Stellen es beschreiben. Am Code ändern wir nichts. Die Texte sollen deshalb wieder sagen, was die Plattform tut.

Bitte die drei Ergänzungen in die Dateien im Ordner einsetzen. Die Fassungsnummern bleiben 1.4 und 1.6, denn keine der Fassungen ist bisher live. Danach übernehmen wir die Dateien wortgleich ins Portal.

---

## 1. AGB – Zusatzpakete fehlen

**Datei:** `01_Kunden/1.0_AGB_v1.4.md`, § 5 Preise und Zahlungsbedingungen

**Warum:** Im Portal kann man Zusatzpakete kaufen. FAQ und Kontingent-Anzeige sagen „zwölf Monate gültig, Rest geht mit“. Ohne den Absatz regeln die AGB nicht, wie lange gekaufte Antworten gelten und was bei Vertragsende mit ihnen passiert.

**Einfügen** als neuer Absatz (5) nach „(4) Die erste Abbuchung erfolgt …“. Die bisherigen Absätze (5)–(7) werden zu (6)–(8):

> (5) Zusätzliche KI-Antworten (Zusatzpakete) bucht der Kunde im Portal als Einmalzahlung. Ein Zusatzpaket gilt zwölf Monate ab dem Kauf. Es wird erst verbraucht, wenn das im Tarif enthaltene Kontingent des laufenden Abrechnungszeitraums aufgebraucht ist; bei mehreren Zusatzpaketen zuerst das früher ablaufende. Nicht verbrauchte Antworten gehen in den nächsten Abrechnungszeitraum über und verfallen mit dem ersten Wechsel des Abrechnungszeitraums nach Ablauf der zwölf Monate. Endet der Vertrag, verfallen nicht verbrauchte Antworten; ein Anspruch auf Erstattung besteht insoweit nicht.

---

## 2. Datenschutzerklärung – Speicherdauer des Audit-Protokolls fehlt

**Datei:** `04_Oeffentlich/4.1_Datenschutzerklaerung_v1.6.md`, Abschnitt 11 Speicherdauer

**Warum:** Seit 08.10. protokolliert die Plattform, wer im Konto wann was geändert hat. Dazu gehören auch die Anmeldungen und Zugriffe des Lymbe-Personals (A11). Für dieses Protokoll muss die DSE die Speicherdauer nennen (Art. 13 Abs. 2 lit. a DSGVO). In der DSE 1.5 stand sie, in der 1.6 fehlt sie.

**Einfügen** als neuer Punkt nach „Zugriffs- und Betriebsprotokolle: 14 Tage; Fehlerprotokoll: 30 Tage“:

> - Audit-Protokoll (wer im Konto wann was geändert hat, Anmeldungen des Lymbe-Personals; Name und E-Mail-Adresse, keine IP-Adressen): 2 Jahre, auch über die Löschung eines Kontos hinaus; Nachweise über Löschungen und beendete Verträge: 3 Jahre

Abschnitt 2 erwähnt das Audit-Protokoll bisher gar nicht (siehe auch Prüfprotokoll 02a, Teil B, Zeile „Team-Mitglieder“). Bitte dort einen Satz ergänzen: welche Daten, Zweck Nachweis und Sicherheit, Rechtsgrundlage Art. 6 Abs. 1 lit. f DSGVO.

---

## 3. Datenschutzerklärung – zwei Angaben bei den Gesprächen fehlen

**Datei:** `04_Oeffentlich/4.1_Datenschutzerklaerung_v1.6.md`, Abschnitt 11 Speicherdauer, erster Punkt

**Warum:** Die Plattform hat zwei Ausnahmen von der 90-Tage-Regel. Der Kunde kann die Frist je Workspace kürzer stellen. Und der Verlauf einer aktiven geplanten Aufgabe wird nicht gelöscht, solange die Aufgabe läuft. Der AVV 1.7 nennt beide, die DSE 1.6 keine. Ohne den Hinweis wirkt die DSE so, als würde ein Verlauf nach 90 Tagen gelöscht, der in Wahrheit stehen bleibt.

**Ersetzen:**

> - Gespräche und interne Chats samt Prompt-Inhalten: automatische Löschung spätestens 90 Tage nach der letzten Nachricht

**durch:**

> - Gespräche und interne Chats samt Prompt-Inhalten: automatische Löschung spätestens 90 Tage nach der letzten Nachricht, je Workspace kürzer einstellbar; der Verlauf einer aktiven geplanten Aufgabe bleibt, solange die Aufgabe aktiv ist

In Abschnitt 2 steht derselbe Satz noch einmal: „Gespräche und interne Chats werden automatisch spätestens 90 Tage nach der letzten Nachricht gelöscht.“ Dort kann er so bleiben, Abschnitt 11 ist die vollständige Angabe.

---

Wenn die drei Stellen in den Dateien stehen, bitte kurz Bescheid geben. Wir übernehmen den Text dann ins Portal und schalten AGB 1.4, DSE 1.6 und AVV 1.7 zusammen live.
