# Prüfprotokoll Datenschutz – Lymbe AI (Dokumenten-Set, Stand 02.10.2026)

Prüfer: unabhängige Prüfung (DSGVO, KI-VO, TDDDG), ohne Beteiligung an den Entwürfen
Geprüft: 01_Inhaltsverzeichnis.md, 00_Projektplan.md, Lymbe Dienstleisterverzeichnis (17 Seiten, Stand 17.09.2026)
Livegang: 05.10.2026 mit erster Pilotkundin, kein Beta

Prioritäten: **P1** = vor Livegang zwingend · **P2** = vor breitem Verkauf · **P3** = Anwalt klärt

Vorbemerkung zur Methode: Das Inhaltsverzeichnis beschreibt Gliederungen, keine Texte. Ich prüfe daher, ob ein Pflichtinhalt überhaupt vorgesehen ist und ob die Gliederung ihn tragen kann. Wo das Dienstleisterverzeichnis zeigt, dass die Technik etwas anderes tut als der Vertrag verspricht, werte ich das als Lücke – das Muster „Zusage im Vertrag, im Code nicht belegbar" (Verzeichnis 0.7) ist genau das, was ein Prüfer der Aufsichtsbehörde zuerst sucht.

Leitbefund vorab: Das Set ist für ein 3-Tage-Fenster ungewöhnlich gut strukturiert. Die größten Risiken liegen nicht in fehlenden Kapiteln, sondern in **vier Rollen- und Tatsachenfehlern** (Stripe als Unterauftragsverarbeiter, Vertragsinhaber der Cloud-Konten unklar, Backup-Frist und Werkstatt-Standort im Vertrag anders als auf der Maschine, Azure Speech im Verzeichnis nicht vorhanden) und in **drei Betroffenengruppen ohne Information** (WhatsApp-Nutzer, Beschäftigte der Kunden, Demo-Nutzer auf lymbe.ai).

---

## A. Pflichtinhalte Art. 28 Abs. 3 DSGVO (AVV 1.1)

| Pflichtinhalt | Status | Befund | Prio |
|---|---|---|---|
| Gegenstand und Dauer (Art. 28 Abs. 3 S. 1) | ✅ | § 1 vorgesehen. | – |
| Art und Zweck der Verarbeitung | ✅ | § 2 plus Anlage 3 „Verarbeitungsübersicht je Bereich". | – |
| Art der personenbezogenen Daten (Datenkategorien) | ⚠️ unklar | § 2 nennt „Art, Zweck, Umfang, betroffene Personen" – Datenkategorien tauchen in der Gliederung nicht auf. Zwingend zu nennen laut Verzeichnis: vollständige E-Mails und Anhänge Dritter (C8), Bestell- und Kundendaten aus Shops (C5/C6), Termine mit Teilnehmern (C1–C4), Telefonnummer/Profilname/Nachrichtentext aus WhatsApp (A7), Sprachaufnahmen/Transkripte, Kontaktdaten aus Lead-Erfassung, Inhalte aus Dokument-Uploads, ggf. besondere Kategorien (Art. 9) bei Gesundheits-/Rechtsberufen. | P1 |
| Kategorien betroffener Personen | ⚠️ unklar | Website-Besucher, Endkunden, Mitarbeiter der Kunden sind neu drin. Es fehlen: Kommunikationspartner der Kunden (IMAP, Kalender, Shop-Kunden), WhatsApp-Nutzer, Personen, die in hochgeladenen Dokumenten vorkommen, Personen in Mails, die Abläufe lesen. | P1 |
| (a) Verarbeitung nur auf dokumentierte Weisung, einschließlich Drittlandübermittlung | ⚠️ unklar | § 3 vermutlich. Die Websuche (OpenAI USA) ist eine Drittlandübermittlung **durch den Auftragsverarbeiter** – sie braucht eine dokumentierte Weisung des Kunden. Das Set sieht nur einen „Hinweis vor der Suche" an den Nutzer vor (C5), nicht eine Entscheidung des Kunden als Verantwortlichem. Nötig: Mandantenschalter „Websuche an/aus" oder ausdrückliche Weisung im AVV/Portal. Außerdem: Portal-Einstellungen (Selbstlernen, Benachrichtigungsziele, verbundene Konten) sollten im AVV als Weisungen in Textform definiert werden, sonst ist Art. 28 Abs. 3 lit. a nicht belegbar. | P1 |
| Hinweispflicht bei rechtswidrigen Weisungen (Art. 28 Abs. 3 UAbs. 2) | ❌ fehlt | In keiner Gliederungszeile erkennbar. Ein Satz in § 3 genügt. | P1 |
| (b) Vertraulichkeitsverpflichtung der Personen | ✅ | § 3 plus 5.3 (Christian, Dennis). | – |
| (c) Maßnahmen nach Art. 32 | ⚠️ unklar | Anlage 1 „Kurzfassung" – Projektplan selbst nennt sie „sehr knapp" (E10). Vor Livegang muss die Kurzfassung mindestens enthalten: Mandantentrennung (eigene DB je Kunde, B2), Verschlüsselung Zugangsdaten (C), Zugriffsbeschränkung und Protokollierung des 26lab-Adminzugriffs, Backup/Restore-Probe (E4), Ratenbegrenzung, Sandbox (B8). Alles ist im Verzeichnis belegt – nur noch nicht aufgeschrieben. | P1 (Kurzfassung), P2 (ausführlich) |
| (d) Unterauftragsverarbeiter, Genehmigung, Information, Pflichtenweitergabe (Art. 28 Abs. 2, 4) | ⚠️ unklar | § 4 und Anlage 2 vorhanden, Ankündigung 14 Tage, 1.4 Prozess – gut. **Aber:** Die Liste „26lab, Hetzner, STACKIT, Microsoft, OpenAI, Stripe" enthält mit **Stripe einen Rollenfehler**: Stripe verarbeitet Abrechnungsdaten der Kunden-Firmen, für die Flubber selbst Verantwortlicher ist, keine Kundendaten im Auftrag. Stripe gehört in die Datenschutzerklärung, nicht in § 4. Außerdem ungeklärt, **wer Vertragspartner von Hetzner/STACKIT/Microsoft/OpenAI ist** (Flubber oder 26lab, siehe J.5) – davon hängt ab, ob diese in § 4 des Kunden-AVV oder als Sub-Sub-Prozessoren in 2.1 stehen. Mistral AI ist als „Rückfallebene" im Code hinterlegt (Verzeichnis G2) und fehlt in Anlage 2 – entweder ausbauen oder listen. | P1 |
| (e) Unterstützung bei Betroffenenrechten | ⚠️ unklar | Vermutlich § 3. Ohne Prozess (5.7 erst nach Livegang) ist die Zusage leer. Minimum vor Livegang: Postfach, Zuständiger, Weiterleitung an Kunden binnen 3 Werktagen, Hinweis welche Portal-Funktionen (Löschen eines Gesprächs, eines Leads, Export) der Kunde selbst hat. | P1 (eine Seite) |
| (f) Unterstützung bei Art. 32–36 (Sicherheit, Meldung, DSFA) | ⚠️ unklar | Meldung an Kunden 24 h in § 7 ✅. DSFA-Unterstützung nicht erkennbar – die Kunden werden sie brauchen (siehe F, Art. 35). | P1 (Satz), P2 (DSFA-Vorlage) |
| (g) Löschung/Rückgabe nach Abschluss | ⚠️ unklar | § 8 mit Fristen vorhanden. Drei Probleme: (1) „Backups 7 Tage" ist auf der Maschine nicht umgesetzt (30 Tage, C2 offen); (2) „Gespräche 90 Tage" – im Verzeichnis ist **keine automatische Löschung von Gesprächen gemessen** worden, nur Abläufe 30 Tage; (3) Rückgabeformat (Export der Gespräche, Leads, Dokumente, Gedächtnis) nicht benannt. Fristen für Leads, Termine, Bewertungen, Dokumente, Gedächtnis, Inngest-Ereignisdaten (B6), Caddy-Logs (B7) fehlen – dann muss es heißen „bis zur Löschung durch den Kunden". | P1 |
| (h) Nachweise und Audits | ✅ | § 9 Kontrollrechte. | – |
| Form (Art. 28 Abs. 9) und Nachweis der Fassung | ⚠️ unklar | Checkbox beim Workspace-Anlegen mit Fassungsnummer ✅ (0.7). Vier Bestandsmandanten ohne Nachweis – Projektplan verschiebt das auf „nach Livegang", obwohl diese Mandanten jetzt schon Daten verarbeiten. | P1 (siehe J.7) |
| Änderung des AVV-Texts (v1.5 → v1.6) | ❌ fehlt | 1.4 regelt nur neue Unterauftragsverarbeiter. Wie werden Bestandskunden an v1.6 gebunden (erneute Checkbox, Änderungsmitteilung mit Widerspruchsfrist)? | P2 |
| Weisungsberechtigte/Ansprechpartner beider Seiten | ❌ fehlt | Übliche Anlage; ohne sie ist „dokumentierte Weisung" praktisch nicht zuordenbar. | P2 |

---

## B. Pflichtangaben Art. 13/14 DSGVO (Datenschutzerklärung 4.1)

### B.1 Pflichtangaben

| Angabe | Status | Befund | Prio |
|---|---|---|---|
| Identität/Kontakt Verantwortlicher (13 Abs. 1 lit. a) | ✅ | vorgesehen. | – |
| Kontakt DSB (lit. b) | ⚠️ | Kein DSB benannt – zulässig nur, wenn die Prüfung in F ergibt, dass keiner nötig ist. Bis dahin: Datenschutz-Kontaktadresse angeben. | P1 |
| Zwecke **und Rechtsgrundlage je Zweck** (lit. c) | ⚠️ | Gliederung nennt Verarbeitungen, nicht Rechtsgrundlagen. Die Erklärung muss je Abschnitt Art. 6 Abs. 1 lit. a/b/f nennen. Kritisch: Websuche (Hinweis ≠ Einwilligung – wenn lit. a, dann Widerruf; wenn lit. f, dann Interessenabwägung dokumentieren), Spracheingabe, Demo-Widget, Spamhaus-Abfrage, Login-Anbieter. | P1 |
| Berechtigte Interessen (lit. d) | ⚠️ | Nirgends erkennbar; nötig für Betriebsprotokolle, IP-Ratenbegrenzung (B5/B7), Spamhaus, Wächter, Fehlerprotokoll. | P1 |
| Empfänger/Kategorien (lit. e) | ✅ | „Empfänger / Auftragsverarbeiter" vorgesehen. Fehlt: Let's Encrypt (Domains, Kontaktadresse), Meta als Empfänger im WhatsApp-Fall, Benachrichtigungsziele (Slack/Teams), Mistral falls aktiv. | P1 |
| Drittlandübermittlung + Garantien (lit. f) | ⚠️ | OpenAI mit SCC vorgesehen ✅. Fehlt für: Stripe (SCC/DPF), Meta (DPF), Google/GitHub-Login (DPF), Let's Encrypt (keine Garantie – Art. 49 oder Interessenabwägung mit Minimaldaten), Microsoft Rest-Übermittlungen. Siehe E. | P1 |
| Speicherdauer (Abs. 2 lit. a) | ✅ | vorgesehen; muss konkret werden: Rechnungsdaten 10 Jahre (§ 147 AO, § 257 HGB), Gespräche 90 Tage, Logs X Tage, Demo-Chats, Konto nach Kündigung + 30 Tage. | P1 |
| Betroffenenrechte (lit. b), Widerruf (lit. c), Beschwerde LDI NRW (lit. d) | ✅ / ⚠️ | Rechte und Aufsicht ✅. Widerrufsrecht nur relevant, wenn Einwilligungen eingesetzt werden – dann nennen. | P2 |
| Pflicht zur Bereitstellung / Folgen (lit. e) | ❌ | Für Registrierung und Zahlung notwendig („ohne diese Daten kein Vertrag"). | P2 |
| Automatisierte Entscheidungen (lit. f) | ✅ | „keine Art. 22" vorgesehen. Prüfen: Ratenbegrenzung/Sperre bei Missbrauch ist eine automatisierte Entscheidung mit Wirkung – entweder nennen oder als unerheblich begründen. | P2 |
| Zweckänderung (Abs. 3) | ❌ | Relevant für Selbstlernen und Übernahme von Frag-Lymbe-Antworten ins Gedächtnis (Zweckänderung beim Kunden – Hinweis in 1.3). | P2 |
| Art. 14 (Quelle der Daten) | ❌ | Für Flubber als Verantwortlichem kaum relevant; für Kunden hochrelevant (IMAP-Dritte, Kalenderteilnehmer, Shop-Kunden) – gehört als Pflicht in AVV § 6 und als Hinweis in 1.3. | P2 |

### B.2 Betroffenengruppen – wer bekommt welche Information?

| Gruppe | Verantwortlicher | Informationsweg im Set | Lücke | Prio |
|---|---|---|---|---|
| Kunden-Admins und Team-Mitglieder im Portal | Flubber (Konto, Abrechnung, Protokolle) | 4.1 beim Login ✅ | Team-Mitglieder werden vom Kunden eingeladen – sie sehen 4.1 erst nach Einladung; Protokollierung ihrer Aktionen (Rollen, Audit) ist Beschäftigtendatum und muss genannt werden. Rollen-Trennung: welche Daten verarbeitet Flubber hier als Verantwortlicher, welche als Auftragsverarbeiter? Die Gliederung vermischt beides („Plattformnutzung je Bereich"). | P1 |
| Website-Besucher lymbe.ai | Flubber | 4.1 ✅ | **Demo-Widget (D6)** nirgends: wo landen Demo-Chats, wie lange, Selbstlernen an?, Leads? Öffentliche Hilfeseite mit fremdem Logo-Abruf (C11) nicht erwähnt. | P1 |
| Endkunden auf Kundenwebsites (Widget) | Kunde | 1.3 Textbaustein ✅, 4.1 Abschnitt als Ergänzung ✅ | 1.3 muss ergänzen: Widget überträgt **bei jedem Seitenaufruf Referrer und IP** an app.lymbe.ai, auch ohne Chat (D1); Live-Chat-Übergabe an Menschen; Lead-Erfassung; Weiterleitung an Benachrichtigungsziele des Kunden (Slack/Teams, USA); Selbstlernen; Terminbuchung über Kalenderdienst; Bewertungen; Speicherfrist 90 Tage; Websuche nur, wenn im Widget verfügbar. Zusätzlich muss der Bot selbst **bei der Lead-Erfassung** informieren (Art. 13 „zum Zeitpunkt der Erhebung") – Textvorlage fehlt. | P1 |
| WhatsApp-Nutzer | Kunde | 1.3 nennt WhatsApp-Kanal | **Diese Personen sehen die Kundenwebsite nie.** Es braucht eine Erstnachricht/Antwort mit KI-Hinweis (Art. 50 KI-VO) und Link zur Datenschutzerklärung des Kunden. C4 (KI-Kennzeichnung) umfasst nur Widget und Portal, nicht WhatsApp. Vorlage fehlt. | P1 |
| Beschäftigte der Kunden (Digitaler Mitarbeiter, Frag Lymbe, Live-Chat-Agenten) | Kunde als Arbeitgeber | **nichts** | Textbaustein „Information der Beschäftigten" fehlt (Art. 13, § 26 BDSG/Art. 88, Hinweis auf Einsicht durch Admins, Websuche USA, Protokollierung, Mitbestimmung § 87 Abs. 1 Nr. 6 BetrVG). | P1 |
| Dritte in verbundenen Diensten (Mail-Absender, Kalenderteilnehmer, Shop-Kunden) | Kunde | – | Art. 14 beim Kunden; Set enthält weder Hinweis noch Pflicht des Kunden (AVV § 6). | P2 |

---

## C. KI-Verordnung (VO (EU) 2024/1689)

**Einstufung Flubber:** Anbieter eines KI-Systems (Art. 3 Nr. 3) – Lymbe wird unter eigenem Namen in Verkehr gebracht; die Modelle (Qwen, gpt-oss bei STACKIT, OpenAI, Azure) sind GPAI-Modelle Dritter, deren Pflichten (Art. 53 ff.) nicht Flubber treffen. **Kunden sind Betreiber** (Art. 3 Nr. 4). Flubber ist zugleich Betreiber für den eigenen Einsatz (Demo, Support-Postfach-Einordnung).

| Punkt | Befund | Prio |
|---|---|---|
| Art. 50 Abs. 1 – Kennzeichnung bei direkter Interaktion | Gilt **seit 02.08.2026**, also bereits bei Livegang. C4 (Widget, Portal-Chat) und 1.3 decken Website ab. Fehlt: WhatsApp-Kanal, Messenger/Instagram (laut A7 über dieselbe App!), Spracheingabe-Dialog, Demo-Widget, Mail-Antworten durch Abläufe (wenn ein Ablauf KI-generierte Mails verschickt, muss der Empfänger wissen, dass eine KI schreibt – „offensichtlich aus den Umständen" greift bei Mail nicht). Außerdem beim Live-Chat: Wechsel Mensch ↔ KI sichtbar machen, sonst ist die Kennzeichnung falsch, sobald der Bot nach der Übergabe wieder übernimmt. | P1 |
| Art. 50 Abs. 2 – maschinenlesbare Kennzeichnung synthetischer Inhalte (auch Text) | Als Anbieter eines textgenerierenden Systems grundsätzlich betroffen; Reichweite bei Chat-Antworten umstritten, Praxisleitfaden der Kommission ausstehend. Im Set nicht erwähnt. Minimal: KI-Antworten in API/HTML als solche markieren (Attribut/Metadatum), Entscheidung dokumentieren. | P3 (Anwalt), P2 (technische Markierung) |
| Hochrisiko (Art. 6, Anhang III) | Kundenservice-Bot, Wissens-Assistent, Terminbuchung, Websuche: **nein**. Risiken, die zur Hochrisiko-Einstufung beim Kunden führen können: Abläufe/Fähigkeiten, mit denen ein Kunde Bewerber bewertet, Mitarbeiterleistung bewertet oder Zugang zu Leistungen steuert (Anhang III Nr. 4, 5). Dann wird der Kunde nach Art. 25 selbst Anbieter. Nutzungsbedingungen müssen Anhang-III-Zwecke ohne Vereinbarung ausschließen; eine kurze schriftliche Einstufung (Zweckbestimmung, Begründung „nicht Hochrisiko") fehlt im Set. | P2 |
| Art. 5 – verbotene Praktiken | **Zu prüfen:** STACKIT-Modell gpt-oss-120b „für die Einordnung jeder Nachricht" (A3). Wenn diese Einordnung Stimmung/Emotion von Beschäftigten im Digitalen Mitarbeiter oder im Live-Chat ableitet, ist das Emotionserkennung am Arbeitsplatz (Art. 5 Abs. 1 lit. f, verboten seit 02.02.2025). Wenn nur Intent/Thema klassifiziert wird: unkritisch. Frage an Christian, Antwort dokumentieren. | P1 |
| Art. 4 – KI-Kompetenz | Gilt seit 02.02.2025 für Anbieter **und** Betreiber. Im Set nichts: weder interner Nachweis (Dennis, Christian, Marion) noch Hilfestellung für Kunden, deren Mitarbeiter den Bot betreuen. Ein zweiseitiges Merkblatt für Kunden plus interne Schulungsnotiz reicht. | P2 |
| Pflichten Anbieter vs. Betreiber | Set enthält keine Zuordnung. Nötig in Nutzungsbedingungen (1.0): Kunde ist Betreiber, hat Art. 26-ähnliche Sorgfalt (menschliche Aufsicht, zweckgemäße Nutzung, Information der Beschäftigten – Art. 26 Abs. 7 gilt formal nur für Hochrisiko, ist aber Best Practice und Arbeitsrecht), Flubber liefert Kennzeichnung, Dokumentation, Hinweise. | P2 |
| KI-Hinweis in 1.0/4.1 („Antworten können fehlerhaft sein") | ✅ vorgesehen. | – |

---

## D. TDDDG § 25 und Cookies/Browserspeicher

| Ort | Befund | Prio |
|---|---|---|
| Widget auf Kundenwebsites (D1) | localStorage `lymbe_ignore` (Nutzer hat Widget geschlossen) und sessionStorage-Marker für proaktive Ansprache. 1.3 behauptet „technisch erforderlich (§ 25 Abs. 2 Nr. 2)". Das Verzeichnis (0.5) sagt ausdrücklich, diese Einordnung „sollte bestätigt werden". Bewertung: `lymbe_ignore` ist vertretbar als vom Nutzer gewünschte Funktion (er hat geschlossen, will nicht wieder gestört werden). Der Marker für die **proaktive Ansprache** dient dem Anbieter (Ansprache nur einmal zeigen), nicht einem ausdrücklichen Nutzerwunsch – nach der DSK-Orientierungshilfe Telemedien ist das angreifbar. Empfehlung: Marker entfernen oder so umbauen, dass er erst nach einer Nutzerhandlung gesetzt wird; Bewertung auf einer Seite dokumentieren. Ungeklärt: speichert das Widget eine Gesprächs-/Sitzungs-ID zum Fortsetzen? Dann ebenfalls einordnen. | P1 (Dokumentation), P2 (Umbau) |
| Widget – Übertragung ohne Speicherung | Referrer und IP bei jedem Seitenaufruf: kein § 25-Fall (keine Speicherung auf dem Endgerät), aber DSGVO-Verarbeitung aller Besucher des Kunden, auch ohne Chat – muss in 1.3 und 4.1 stehen, Rechtsgrundlage Art. 6 Abs. 1 lit. f des Kunden. | P1 |
| Portal (Sitzungs-Cookie, CSRF-Token, OAuth-State) | § 25 Abs. 2 Nr. 2 ✅, kein Banner nötig. In 4.1 „Cookies und Browserspeicher" nennen. | – |
| Stripe | Stripe.js lädt laut 0.3/D4 nicht mehr; Checkout/Billing sind Weiterleitungen auf stripe.com, dort gelten Stripes Cookies und Stripes Datenschutzerklärung. 4.1 „inkl. Browser-Weiterleitung" ✅ – Text muss sagen: kein Stripe-Skript im Portal. Abschnitt H des Verzeichnisses („Stripe setzt im Browser eigene") ist veraltet, nicht übernehmen. | P2 |
| lymbe.ai Marketing-Seite | Keine Analyse, keine fremden Schriften (D7, H) ✅ – damit kein Consent-Banner. Demo-Widget (D6) speichert wie D1 → gleiche Bewertung, in 4.1 nennen. | P1 |
| Login Google/GitHub | Cookies auf deren Domains, deren Verantwortung. Kein § 25-Problem bei Flubber. | – |
| Spracheingabe | Mikrofonfreigabe ist Browser-Berechtigung, kein § 25. Aber: wird Audio lokal zwischengespeichert? Falls ja, einordnen. | P3 |
| Fehlendes Dokument | Eine Seite „§ 25-Bewertung Browserspeicher" (je Eintrag: Name, Zweck, Dauer, Rechtsgrund) – Grundlage für 1.3 und für die Kunden, die es in ihre Cookie-Hinweise übernehmen müssen. | P1 |

---

## E. Drittlandübermittlung

| Empfänger | Daten | Rolle | Absicherung im Set | Lücke | Prio |
|---|---|---|---|---|---|
| OpenAI Ireland / OpenAI L.L.C. (USA) – Websuche | Vom Modell formulierter Suchbegriff + Land DE. **Nicht** „nur der Suchbegriff" im Sinne von „keine personenbezogenen Daten": Der Suchbegriff wird aus der Nutzerfrage gebildet und kann Namen, Orte, Firmen, Gesundheitsbezüge enthalten. OpenAI speichert API-Eingaben standardmäßig bis 30 Tage zur Missbrauchskontrolle. | Unterauftragsverarbeiter | 3.1: DPA mit SCC ✅; 4.1 Hinweis ✅; C5 Hinweis vor Suche ✅ | **Transfer-Folgenabschätzung (TIA) fehlt** – bei SCC Pflicht (Klausel 14). Prüfen, ob OpenAI L.L.C. im Data Privacy Framework gelistet ist (dann DPF als Hauptgrundlage, SCC als Rückfall). Hinweistext darf nicht „keine personenbezogenen Daten" behaupten. Weisung des Kunden (A, lit. a). Werkstatt läuft laut Verzeichnis **noch** bei OpenAI (Schweden-Residenz, aber US-Mutter mit Zugriff) – bis C1 umgesetzt ist, muss Anlage 2 das sagen. | P1 (Hinweistext, Anlage 2), P2 (TIA) |
| Stripe Payments Europe (IE) → Stripe Inc. (USA) | Name, E-Mail, Rechnungsanschrift, USt-ID, Zahlungsverlauf der Kunden-Firmen; IP auf Stripe-Seiten | Eigener Auftragsverarbeiter/teils Verantwortlicher von **Flubber** | 3.1 SCC ✅, 4.1 ✅ | Aus § 4 AVV entfernen (Rollenfehler). DPF-Zertifizierung von Stripe Inc. in 4.1 nennen. | P1 |
| Meta Platforms Ireland → Meta Inc. (USA) – WhatsApp Cloud API | Telefonnummer, Profilname, vollständiger Nachrichtentext in beide Richtungen | Laut E3: vom Kunden verbundener Dienst. Tatsächlich: Kunde verbindet per Embedded Signup **über Lymbes Meta-App**, Access-Tokens liegen bei Lymbe, Inngest verarbeitet die Nachrichten (B6). Lymbe steht als „Solution Provider" im Datenfluss. | 1.1 § 5, 1.3, 4.1, C6 ✅ | Rolle Metas (Auftragsverarbeiter des Kunden nach WhatsApp Business Data Processing Terms, Übermittlung über DPF) nirgends dokumentiert; Lymbes eigener Vertrag mit Meta (Business Solution Provider Terms) fehlt in 3.1/3.2. WhatsApp-Nutzer erhalten keine Information (B.2). Messenger/Instagram laufen „über dieselbe App" (A7) – im Set nicht erwähnt. | P1 (Nutzerinfo), P2 (Rollendoku, Vertrag ablegen) |
| Google / GitHub (USA) – Login | E-Mail, Name, Profilbild (einmalig) | Eigenständige Verantwortliche, vom Nutzer gewählt | 4.1 „Login über Google/GitHub" ✅, 1.1 § 5 ✅ | DPF-Status beider nennen; Hinweis, dass Profilbild einmal übernommen und dann lokal gespeichert wird (0.1). GitHub zusätzlich: Wächter (GitHub Actions, nur Ja/Nein, keine personenbezogenen Daten) und vermutlich Code-Hosting – im Art.-30-Verzeichnis erwähnen, kein AVV nötig, solange keine Kundendaten im Repo. | P2 |
| Let's Encrypt / ISRG (USA) | **Jede Kundendomain**, Mandanten-Slugs, Server-IP, admin@lymbe.ai; Domains landen zusätzlich öffentlich in Certificate-Transparency-Logs | Eigenständiger Verantwortlicher, kein AVV erhältlich | **nirgends** (weder 3.1, 4.1 noch 5.1) | Art.-30-Karte, Abschnitt in 4.1 („Zertifikate"), Rechtsgrundlage Art. 6 Abs. 1 lit. f, Übermittlung: Art. 49 Abs. 1 lit. b/c oder Erforderlichkeit; Kunden darauf hinweisen, dass ihre Domain in CT-Logs erscheint (meist unkritisch, da DNS ohnehin öffentlich; bei Einzelunternehmern mit Namensdomain personenbezogen). ZeroSSL als Rückfall ebenfalls nennen (Caddy-Standard). | P2 |
| Spamhaus (Spamhaus Technology Ltd, UK / Spamhaus Project, Andorra) | Absender-IP und Link-Domains jeder eingehenden Mail an lymbe.ai | Eigenständiger Verantwortlicher | 4.1 „Spamhaus-Abfrage" ✅, 5.1 E-Mail ✅ | UK und Andorra haben Angemessenheitsbeschlüsse – keine SCC nötig, aber Angemessenheit in 4.1 nennen; prüfen, welche Spamhaus-Gesellschaft bei DQS-Schlüssel Vertragspartner ist. | P3 |
| Microsoft Ireland – Azure OpenAI (Werkstatt), Azure Speech Frankfurt | Beschreibungstexte, Ablaufdefinitionen; Sprachaufnahmen | Unterauftragsverarbeiter | 3.1 „nicht nötig (EU-Datenzone)" | Zu absolut: Die EU-Datengrenze deckt Kundendaten, nicht alle Support-/Telemetriedaten; Microsofts DPA enthält dafür SCC und Microsoft Corp. ist DPF-zertifiziert. Anlage 2: „EU-Datenzone; Rest-Übermittlungen über SCC/DPF". Azure Speech ist im Dienstleisterverzeichnis **gar nicht enthalten** (J.3). | P1 (Anlage 2 richtigstellen), P3 |
| Slack / Microsoft Teams / freie https-Adresse (C10) | Name, E-Mail, Nachricht des Besuchers | Vom Kunden bestimmter Empfänger (häufig USA) | 1.1 § 5 ✅, C6 ✅ | Endkunden müssen es in der Datenschutzerklärung des Kunden erfahren → 1.3 ergänzen. | P1 |
| Calendly (USA), Cal.com, Shopify (Kanada, Angemessenheit), Shopware/WooCommerce (Shop des Kunden) | Buchungen, Bestellungen | Vom Kunden verbunden | 1.1 § 5 ✅ | Hinweis im Portal (C6) muss den Standort des Dienstes nennen, sonst kann der Kunde seine Art.-13-Pflicht nicht erfüllen. | P2 |
| Mistral AI (Frankreich) | „Rückfallebene" (G2) | – | nirgends | EU, kein Drittland – aber als potenzieller Empfänger entweder ausbauen oder in Anlage 2. | P2 |

---

## F. Weitere Pflichtdokumente und Prozesse

| Pflicht | Status im Set | Befund | Prio |
|---|---|---|---|
| Art. 30 Abs. 1 (eigenes Verzeichnis) **und** Art. 30 Abs. 2 (Verzeichnis als Auftragsverarbeiter) | 5.1 eine Kartenliste | Zwei Verzeichnisse mit unterschiedlichen Pflichtfeldern. Abs. 1: Kundenkonten, Abrechnung, Website, Demo, Support-Mail, Protokolle, Wächter, Zertifikate. Abs. 2: je Kunde/Kategorie die Auftragsverarbeitungen (Kundenservice, Digitaler Mitarbeiter, Frag Lymbe, Abläufe) mit Unterauftragsverarbeitern und Drittland. Fehlende Karten: Leads, Termine, Bewertungen, Live-Chat, Spracheingabe, Demo-Instanz, Hilfeseite, Vektorspeicher (B3), Inngest-Ereignisdaten (B6). Löschfristen je Karte fehlen, solange 5.5 nicht existiert. | P1 (Trennung + Karten), P2 (Fristen) |
| Art. 32 TOMs | Anlage 1 Kurzfassung (P1), 5.4 ausführlich nach Livegang | Akzeptabel, wenn die Kurzfassung die in A (c) genannten Punkte enthält. 26lab-TOMs als Anlage zu 2.1 ✅. Nachweise Hetzner/STACKIT (ISO 27001, C5) für die Auftragskontrolle ablegen. | P2 |
| Art. 33/34 Meldeprozess | 5.6 **nach** Livegang | Widerspruch zum Vertrag: AVV verspricht 24 h ab Tag 1, 2.1 verlangt 12 h von 26lab. Ohne Prozess kann keine Frist eingehalten werden. Minimum vor Livegang: eine Seite mit Meldekette, Kontaktdaten LDI NRW (Meldeformular-Link), Vorlage für Kundenmeldung, Entscheidungsbaum „meldepflichtig ja/nein", Dokumentationspflicht Art. 33 Abs. 5 (auch für nicht gemeldete Vorfälle). | P1 |
| Art. 35 DSFA | 5.2 Vorprüfung vor Livegang ✅, volle DSFA danach | Erwartbares Ergebnis der Vorprüfung: **DSFA-pflichtig**, denn Nr. 11 der DSK-Muss-Liste („Einsatz von KI zur Steuerung der Interaktion mit Betroffenen") trifft Kundenservice-Bots direkt; dazu Art.-9-Daten bei Gesundheits-/Rechtskunden und WhatsApp-Nachrichtentexte. Die DSFA-Pflicht trifft formal die **Kunden** (Verantwortliche) – Flubber muss sie unterstützen (Art. 28 Abs. 3 lit. f) und sollte eine DSFA-Vorlage/Plattform-DSFA liefern, die Kunden übernehmen können. Für Flubbers eigene Verantwortlichkeit (Demo, Support-Einordnung) ist eine DSFA eher nicht nötig. Wenn die Pilotkundin ein Gesundheits-/Therapiebetrieb ist: ihre DSFA vor Livegang (Art. 35 Abs. 1 „vor der Verarbeitung"). | P1 (Vorprüfung + ggf. Pilotkundin), P2 (Vorlage) |
| Art. 37 DSB-Pflicht | Projektplan: „vermutlich nein unter 20 Personen", Anwalt | **Begründung unvollständig.** § 38 Abs. 1 S. 2 BDSG: Wer Verarbeitungen vornimmt, die einer DSFA unterliegen, muss **unabhängig von der Personenzahl** einen DSB benennen – gilt nach Wortlaut für Verantwortliche und Auftragsverarbeiter. Ergibt 5.2 „DSFA ja", folgt daraus die DSB-Pflicht sofort. Art. 37 Abs. 1 lit. b (Überwachung als Kerntätigkeit) trifft nicht zu; lit. c (umfangreiche Art.-9-Verarbeitung als Kerntätigkeit) wird relevant, sobald mehrere Gesundheits-/Rechtskunden Bots betreiben. Externer DSB ist kurzfristig buchbar. | P1 (Begründung korrigieren, Entscheidung mit 5.2 koppeln), P3 (Anwalt) |
| Art. 29 / Art. 32 Abs. 4 Vertraulichkeit | 5.3 ✅ | Ergänzen: Protokollierungspflicht und Vier-Augen-Regel (2.2) als Teil der Verpflichtung; später jede Person mit Zugriff ✅. Bei Berufsgeheimnisträger-Kunden zusätzlich Verpflichtung nach **§ 203 Abs. 4 StGB** für Dennis und Christian (siehe G). | P1 bei entsprechender Pilotkundin, sonst P2 |
| Betroffenenrechte-Prozess | 5.7 nach Livegang | Siehe A (e): eine Seite vor Livegang. Technische Frage dazu: Kann der Kunde eine einzelne Person vollständig löschen (Gespräche, Leads, Vektorspeicher, Gedächtnis, Inngest-Events, Backups nach Ablauf)? Wenn nein, muss der Prozess sagen, wer das bei 26lab macht und in welcher Frist. | P1 |
| Löschkonzept | 5.5 nach Livegang | Vertretbar, **wenn** die im AVV genannten Fristen technisch laufen. Das Verzeichnis belegt nur: Abläufe 30 Tage, Backups 30 Tage, Mailvolume/DKIM nur im Server-Snapshot (Frist unbekannt). **Nicht belegt: automatische Löschung von Gesprächen nach 90 Tagen.** Vor Livegang bestätigen lassen oder § 8 anpassen. | P1 (Abgleich), P2 (Konzept) |
| Auftragskontrolle Unterauftragsverarbeiter (Art. 28 Abs. 1, 4) | 3.1 Checkliste, 2.1 Anlage TOMs/Zugriffsliste, 2.2 vierteljährliche Aktualisierung ✅ | Gut. Fehlt: Erstprüfung 26lab dokumentieren (Datum, wer, Ergebnis), Zertifikate der Cloud-Anbieter ablegen, Vertragsinhaber klären (J.5). | P2 |
| Versionsnachweis Vertragsfassungen | Checkbox mit Fassung ✅ (0.7) | Fassungsnummern uneinheitlich (J.6). Vier Bestandsmandanten ohne Nachweis. Verfahren für Textänderungen (v1.6) fehlt. Archiv alter Fassungen (AVV v1.5, Datenschutz v1.4, Anlage 2 mit Cloudflare-Abgang) anlegen – das Verzeichnis macht es mit „A6 bleibt als Abgang stehen" vor. | P1 (Bestandsmandanten), P2 (Verfahren) |
| Impressum (§ 5 DDG) | 4.2 „OS-Plattform-Link ergänzen" | **Nicht ergänzen.** Die EU-Streitschlichtungsplattform wurde mit VO (EU) 2024/3228 abgeschafft und am 20.07.2025 abgeschaltet; ein Link darauf ist inzwischen irreführend. § 36 VSBG-Hinweis: Pflicht erst ab mehr als 10 Beschäftigten; bei B2B-Angebot ohnehin ohne Verbraucher. Nur prüfen, ob ein freiwilliger Satz „nicht bereit/verpflichtet zur Teilnahme" stehen soll. | P1 (Fehler vermeiden) |
| Nutzungsbedingungen (1.0) – datenschutzrelevante Pflichten | vorgesehen | Ergänzen: Nutzung nur durch Unternehmer (B2B), Kunde stellt sicher: Art.-13/14-Information, Beschäftigteninformation, Mitbestimmung, keine privaten Postfächer, keine Anhang-III-Zwecke, Art.-9-Daten nur mit Zusatzvereinbarung, Kunde bleibt für Inhalte der Fähigkeiten/Prompts verantwortlich. | P1 |

---

## G. Besonderheiten dieses Produkts

| Thema | Befund | Prio |
|---|---|---|
| **Selbstlernen** (Bot speichert aus Gesprächen ins Gedächtnis) | Personenbezogene Inhalte aus Gesprächen (90-Tage-Frist) werden dauerhaft Wissen und können **anderen Nutzern** ausgespielt werden (Querleck zwischen Endkunden). Rechtsgrundlage beim Kunden: Art. 6 Abs. 1 lit. f mit Zweckänderung (Art. 6 Abs. 4) – fragwürdig, solange Personenbezug nicht gefiltert wird. Betroffeneninfo: in 1.3 nicht vorgesehen. Löschung einzelner Personen aus Qdrant/Gedächtnis: nicht beschrieben. Empfehlung: Standard **aus**, Aktivierung = dokumentierte Weisung (Portal-Hinweis), Filter auf Namen/Kontaktdaten vor Übernahme, Abschnitt in 1.3 und AVV Anlage 3. Bei Art.-9-Kunden zwingend aus. | P1 (Default aus + Hinweis), P2 (Filter, Löschweg) |
| **Leads** (Bot erfasst Kontaktdaten) | Art. 13 zum Zeitpunkt der Erhebung → der Bot muss beim Fragen nach Name/E-Mail/Telefon einen Satz mit Zweck und Link ausgeben; Vorlage fehlt. Weiterleitung an Slack/Teams/freie Adresse (C10) ist Übermittlung an vom Kunden gewählte Empfänger – Endkunde muss es erfahren. Löschfrist für Leads fehlt in § 8. Minderjährige: siehe unten. | P1 |
| **Terminbuchung** | Termindaten gehen an Google/Microsoft/Calendly/Cal.com (Kundenkonto). Bei Therapie-/Arzt-/Anwaltskunden ist schon der Termin ein Art.-9-Datum (Gesundheit) bzw. Mandatsgeheimnis. Dann: Kalenderanbieter des Kunden muss das tragen (Google Workspace mit AVV ja, privates Gmail nein) → Hinweis beim Verbinden (C6) und in 1.0. | P1 bei Pilotkundin aus Gesundheits-/Rechtsbereich, sonst P2 |
| **Live-Chat-Übergabe** | Mitarbeiter des Kunden sehen Gespräche – im Rahmen der Kundenverantwortung in Ordnung. Fehlt: Rollenkonzept (wer sieht welche Gespräche, Protokollierung), sichtbarer Wechsel KI ↔ Mensch (Art. 50 KI-VO, Treu und Glauben), Name/Kürzel des Agenten gegenüber Endkunden ist Beschäftigtendatum. | P2 |
| **Bewertungen** | Bewertet der Endkunde die KI-Antwort: unkritisch. Bewertet er nach Übergabe einen **Menschen**: Leistungsbewertung von Beschäftigten → § 87 Abs. 1 Nr. 6 BetrVG beim Kunden, Information der Beschäftigten, Löschfrist. AVV § 6/1.0 muss den Kunden darauf stoßen. | P2 |
| **IMAP-Postfächer** (vollständige Mails Dritter inkl. Anhänge) | Größter Datenumfang mit geringster Kontrolle. Nötig: Datenkategorie und Betroffene in § 2 (A); Pflicht des Kunden in § 6: nur dienstliche Postfächer, keine private Nutzung erlaubt (sonst Fernmeldegeheimnis-Diskussion beim Arbeitgeber), Art.-14-Information oder Ausnahme Art. 14 Abs. 5 lit. b dokumentieren; Speicherfrist der abgerufenen Mails in Lymbe (Mandanten-DB? Inngest?) – nicht definiert; Weitergabe der Mailtexte an STACKIT (A3 „E-Mail-Texte") in Anlage 3 nennen; Admin-Postfach-Zugriff von 26lab auf Kundenmails ausschließen oder protokollieren. | P1 (§ 2, § 6, Frist), P2 (Rest) |
| **Mitarbeiter-Bereich** (Digitaler Mitarbeiter, Frag Lymbe) | Beschäftigtendaten: Fragen der Mitarbeiter sind Verhaltensdaten; Admin-Einsicht in Chats = potenzielle Verhaltenskontrolle → Mitbestimmung § 87 Abs. 1 Nr. 6 BetrVG bei Kunden mit Betriebsrat; Rechtsgrundlage beim Kunden Art. 6 Abs. 1 lit. b/f (§ 26 BDSG nach EuGH C-34/21 nur noch eingeschränkt tragfähig). Websuche schickt aus Mitarbeiterfragen gebildete Suchbegriffe in die USA. Set hat: nichts für diese Gruppe. Nötig: Textbaustein Beschäftigteninformation, Hinweis in 1.0/§ 6, Portal-Einstellung „Admins sehen Frag-Lymbe-Verläufe ja/nein" (Empfehlung: nein als Standard). Art. 5 KI-VO-Prüfung der „Einordnung jeder Nachricht" (C). | P1 |
| **Übernahme von Frag-Lymbe-Antworten ins Gedächtnis** | Antworten aus Websuche enthalten Daten Dritter aus dem Netz (Namen, Firmen) und werden dauerhaft Unternehmenswissen → Art. 14 beim Kunden, Richtigkeit (Art. 5 Abs. 1 lit. d), Halluzinationen werden „Wissen". Pflicht des Kunden zur Prüfung vor Übernahme + Kennzeichnung der Quelle; Hinweis in 1.0. | P2 |
| **Sprachaufnahmen** (Azure Speech Frankfurt) | Keine biometrische Identifizierung → kein Art. 9 per se, aber Stimme + Inhalt sind sensibel. Offen: Wird Audio gespeichert oder nur transkribiert? Azure Speech protokolliert standardmäßig nicht – bestätigen. 4.1 ✅ vorgesehen. Microsoft fehlt im Dienstleisterverzeichnis (J.3) – also ist entweder das Verzeichnis unvollständig oder die Funktion nicht live. | P1 (klären) |
| **Art.-9-Daten in Chats** (Friseur, Therapie, Arzt, Anwalt) | 1.0 schließt Art.-9-Daten „ohne Vereinbarung" aus – die Realität eines Therapie-Bots liefert sie in jedem zweiten Gespräch. Nötig: Zusatzvereinbarung Art. 9 (Rechtsgrundlage beim Kunden meist Art. 9 Abs. 2 lit. h i. V. m. § 22 BDSG oder ausdrückliche Einwilligung lit. a), **§ 203 Abs. 4 StGB-Verpflichtung** von Flubber und 26lab als „mitwirkende Personen", Websuche und Selbstlernen für solche Mandanten aus, Benachrichtigungsziele außerhalb EU aus, DSFA des Kunden, erhöhte TOMs (Verschlüsselung at rest je Mandant). Für die Pilotkundin: Branche klären – entscheidet über die Hälfte der P1-Punkte. | P1 wenn Pilotkundin betroffen, sonst P2 |
| **Minderjährige als Website-Besucher** | Chats auf Art. 6 Abs. 1 lit. f brauchen keine Altersprüfung (Art. 8 gilt nur für Einwilligung bei Diensten der Informationsgesellschaft). Aber: Lead-Erfassung bei Minderjährigen, proaktive Ansprache und KI-VO Art. 5 Abs. 1 lit. b (Ausnutzung altersbedingter Schwäche) – Bot-Prompts dürfen nicht drängen. 1.0: Portal nur für Unternehmer; Hinweis an Kunden mit jungem Publikum (Friseur, Taxi). | P3 |
| **Kontingent / Abrechnungsdaten** | Zählung der KI-Antworten pro Mandant ist Vertragsdatum (lit. b) – unkritisch, wenn nicht pro Mitarbeiter ausgewertet (sonst Leistungskontrolle). Rechnungsdaten 10 Jahre (§ 147 AO); Stripe erhält Abo-/Zahlungsverlauf; Löschfrist in 4.1 und 5.5. | P2 |
| **Admin-Zugriff 26lab auf alle Mandanten** | Faktisch: eine Person mit Vollzugriff auf alle Kundengespräche, Dokumente, Mails. 2.2 sieht Vier-Augen-Prinzip und Protokollierung vor – bei zwei Personen bedeutet das: jeder Zugriff auf Mandanteninhalte nur mit Freigabe von Dennis und mit technischem Protokoll (nicht nur Absichtserklärung). Kunden müssen in AVV/TOMs erfahren, dass Support-Zugriff auf Inhalte möglich ist und nur auf Weisung/Ticket erfolgt. Fehlerprotokoll (B10) und Admin-Postfach (D5) sind solche Zugriffswege. | P1 (Regel + Protokoll), P2 (technische Beschränkung, z. B. Break-Glass) |
| **Backups 7 Tage vs. Löschfristen** | Vertrag 7 Tage, Maschine 30 Tage (C2 offen). Server-Snapshot (Hetzner) mit Mailvolume und DKIM-Schlüssel ohne genannte Frist. Einzel-Löschung in Backups nicht möglich → AVV § 8 muss sagen „Löschung aus Sicherungen mit Ablauf der Sicherungsfrist, Wiederherstellung nur mit erneuter Löschung". Wöchentliche Restore-Probe (E4) ✅ als TOM aufnehmen. | P1 |
| **Demo-Instanz** (lymbe.ai lädt Demo-Widget, D6) | Flubber ist hier **Verantwortlicher**. Nicht im Set: Speicherort/Mandant der Demo-Chats, Frist, Selbstlernen (muss aus sein), Lead-Erfassung (muss aus sein oder mit Info), KI-Kennzeichnung, Art.-30-Abs.-1-Karte, Abschnitt in 4.1. Einfachste Lösung: Demo-Chats nach 24 h löschen, kein Gedächtnis, keine Leads. | P1 |
| **Öffentliche Hilfeseite mit fremdem Logo (C11)** | Kunde trägt eine Logo-URL ein → IP und User-Agent jedes Hilfeseiten-Besuchers gehen an den fremden Server. Entweder Logo serverseitig spiegeln (wie bei Baustein-Logos 0.9 bereits gelöst) oder Hinweis in 1.3. | P2 |
| **Messenger/Instagram über dieselbe Meta-App (A7)** | Im gesamten Set nur WhatsApp. Wenn Messenger/Instagram verbindbar sind, gelten alle WhatsApp-Punkte entsprechend; sonst im Portal deaktivieren. | P1 (klären) |

---

## H. Abgleich mit dem Dienstleisterverzeichnis

Legende: ✅ abgedeckt · ⚠️ teilweise/unscharf · ❌ nirgends

### A – Externe Empfänger

| Pos. | Anbieter | Abgedeckt in | Befund |
|---|---|---|---|
| A1 | 26lab.io | 1.1 § 4, 2.1, 2.2, 3.1, 5.3 | ✅ Vollständig. Offen nur Vertragsinhaberschaft der Cloud-Konten (J.5). |
| A2 | Hetzner (Server, Cloud-API für Zertifikate/DNS, zwei öffentliche IPs) | 1.1 § 4, 3.1, 4.1 Empfänger, 5.1 | ✅ Anbieter ✅. ⚠️ Widerspruch, ob Hetzner Unterauftragsverarbeiter von Flubber (3.1 „Kundenkonto per Klick") oder von 26lab (2.1) ist. Server-Snapshots (Frist) fehlen in § 8. |
| A3 | STACKIT (Chat, Vision, Einordnung, Embeddings) | 1.1 § 4, 3.1, 4.1, 5.1 | ✅. ⚠️ Anlage 3 sollte nennen, dass auch E-Mail-Texte, Bilder und Dokumente dorthin gehen (nicht nur „Chat-Modelle"); Modellnamen (gpt-oss ≠ OpenAI) kurz erklären, um Nachfragen zu vermeiden. „Einordnung jeder Nachricht" → Art.-5-Prüfung (C). |
| A4 | OpenAI Ireland (Websuche + **Werkstatt**) | 1.1 § 4, 3.1 (nur Websuche), 4.1 (nur Websuche), 5.1 Frag Lymbe | ⚠️ Werkstatt-Nutzung fehlt im Set, weil E1 die Umstellung auf Azure voraussetzt; solange C1 offen ist, ist Anlage 2 falsch. Suchbegriff-Beschreibung zu beschönigend (E). TIA fehlt. |
| A5 | Stripe | 3.1, 4.1, 5.1 Abrechnung; **1.1 § 4 (falsch)** | ⚠️ Rollenfehler: raus aus § 4, rein in 4.1 mit DPF/SCC. |
| A6 | Cloudflare (gestrichen) | – | ✅ Konsistent entfernt. Empfehlung: Abgang in Anlage-2-Historie dokumentieren (für Bestandskunden, die Fassung 1.2 gesehen haben). |
| A7 | Meta (WhatsApp, Messenger, Instagram) | 1.1 § 5, 1.3, 4.1, 5.1 Kundenservice-Chats | ⚠️ Nur WhatsApp im Set; Messenger/Instagram ❌. Metas Rolle und Lymbes eigener Meta-Vertrag ❌ (3.1/3.2). WhatsApp-Nutzer-Information ❌. |
| A8 | GitHub (Login, Release-Abfrage, Wächter) | 4.1 Login, 1.1 § 5 Login-Anbieter | ⚠️ Login ✅. Wächter und Release-Abfrage ❌ (keine personenbezogenen Daten – kurze Art.-30-Notiz genügt). Code-Hosting ❌ – 2.2 Exit „Code" setzt Kenntnis des Speicherorts voraus. **Meldeweg des Wächters** („über einen Weg, der mit unserem Mailserver nichts zu tun hat") ist ein ungenannter Dienst – nachfragen und listen. |
| A9 | Let's Encrypt (ISRG) | **nirgends** | ❌ Siehe E. Betrifft jede Kundendomain. |
| A10 | Spamhaus | 4.1 E-Mail-Verkehr, 5.1 E-Mail-Verkehr | ✅. Kein AVV nötig (eigenständiger Empfänger, Angemessenheit). |

### B – Selbst betrieben

| Pos. | Komponente | Abgedeckt in | Befund |
|---|---|---|---|
| B1 | PostgreSQL zentral (Konten, Abrechnung) | 5.1 Kundenkonten, 4.1 Registrierung | ✅ Art. 30 Abs. 1. |
| B2 | PostgreSQL je Mandant (Gespräche, Kontakte, Dokumente, Aufgaben) | 5.1, 1.1 Anlage 3 | ⚠️ Mandantentrennung als TOM in Anlage 1 nennen. „Kontakte/Aufgaben" = Leads/Termine – eigene Karten fehlen. |
| B3 | Qdrant (Vektorspeicher) | 5.1 Digitaler Mitarbeiter (implizit) | ⚠️ Löschung aus dem Vektorspeicher (Art. 17) nirgends; gehört in 5.5 und in den Betroffenenrechte-Prozess. |
| B4 | MinIO (Uploads, Anhänge, Logos) | 5.1 Dokumente | ✅ (0.8 behoben). Frist in § 8/5.5. |
| B5 | Redis (IP-Zähler, Cache) | 5.1 Betriebsprotokolle (implizit) | ⚠️ IP-Zähler = personenbezogen; Zweck Ratenbegrenzung und Frist (Minuten/Stunden) in Art. 30 Abs. 1 und 4.1 (berechtigtes Interesse). |
| B6 | Inngest (Ereignisdaten inkl. WhatsApp-Nachrichten) | – | ❌ Ereignisspeicher mit Nachrichteninhalten; Frist nirgends. In 5.1, § 8 und 5.5 aufnehmen. |
| B7 | Caddy (Zugriffsprotokolle mit IP) | 5.1 Betriebsprotokolle | ⚠️ Frist fehlt (üblich 7–14 Tage). |
| B8 | Pyodide-Sandkasten | – | ✅ Keine Datenschutzpflicht; als TOM in Anlage 1 nennen. |
| B9 | Mailserver (Postfix, rspamd, ClamAV, Unbound; Mailvolume, DKIM nur im Snapshot) | 4.1 E-Mail-Verkehr, 5.1, 5.5 (nach Livegang) | ✅ Grundsätzlich. ⚠️ Admin-Postfach (D5) = Zugriff 26lab auf Support-Mails der Kunden → Vertraulichkeit/Protokoll. ClamAV-Signaturabruf (F3) ohne Personenbezug ✅. |
| B10 | Fehlerprotokoll und Betriebsprüfung | 5.1 „Fehlerprotokoll" | ⚠️ Enthält Fehlermeldungen mit möglichen Nutzerkennungen/Inhalten; Frist fehlt; Zugriff nur 26lab. |

### C – Verbindungen, die der Kunde herstellt

| Pos. | Dienst | Abgedeckt in | Befund |
|---|---|---|---|
| C1 | Google Calendar | 1.1 § 5, 4.1, C6, 5.1 Abläufe | ✅ Dienst. ⚠️ Datenkategorie „Teilnehmer, freie Zeiten" in § 2; Art.-9-Risiko bei Gesundheitskunden. |
| C2 | Microsoft Outlook/Graph (Termine, Kalender, E-Mail je Baustein) | wie C1 | ✅/⚠️ „E-Mail je Baustein" = Postfachzugriff wie C8 – gleiche Pflichten. |
| C3 | Calendly | wie C1 | ✅ Dienst; ⚠️ Standort USA beim Verbinden nennen (C6). |
| C4 | Cal.com | wie C1 | ✅/⚠️ wie C3. |
| C5 | Shopify (Bestellungen, Kundendaten, Sendungsstatus) | 1.1 § 5, 4.1 | ✅ Dienst; ⚠️ Datenkategorie Shop-Kunden fehlt in § 2. Shopify-Partner-App: Lymbe hat eigenen Partnervertrag mit Shopify → in 3.2 ablegen. |
| C6 | Shopware / WooCommerce (Admin-API-Schlüssel) | 1.1 § 5 | ✅/⚠️ Admin-API-Schlüssel = Vollzugriff auf Shop; Hinweis beim Verbinden auf minimal berechtigte Schlüssel (Art. 32). |
| C7 | Google-/GitHub-Login | 4.1, 1.1 § 5 | ✅. Profilbild-Handhabung (0.1) in 4.1 kurz nennen. |
| C8 | IMAP-Postfächer (vollständige E-Mails) | 1.1 § 5 | ⚠️ Nur als Dienst genannt. Datenkategorie, Betroffene, Kundenpflichten, Frist fehlen (G). |
| C9 | 718 Bausteine mit Kontoanbindung | 1.1 § 5 (generisch) | ✅ Generische Klausel ist der einzige gangbare Weg; ⚠️ im Portal muss jeder Baustein beim Verbinden den Anbieter und Standort zeigen (C6), sonst ist die Klausel leer. |
| C10 | Benachrichtigungsziele (Slack, Teams, freie https-Adresse) | 1.1 § 5 ✅ | ⚠️ 1.3 (Endkundeninfo) ❌; 4.1 „verbundene Dienste" sollte es nennen. |
| C11 | Vom Kunden gesetzte Abrufadressen (Crawl, API-Import, Hilfeseiten-Logo) | 1.1 § 5 „Abrufadressen" ✅ | ⚠️ Crawl/API-Import ✅ (0.12 abgesichert). Hilfeseiten-Logo ❌ (Besucher-IP an Fremdserver). |

### D – Was im Browser passiert

| Pos. | Vorgang | Abgedeckt in | Befund |
|---|---|---|---|
| D1 | Chat-Widget (localStorage, sessionStorage, Referrer, IP) | 1.3, 4.1 Besucher/Cookies, 5.1 | ⚠️ § 25-Einordnung als gesichert dargestellt, im Verzeichnis als offen (0.5). Referrer/IP bei jedem Seitenaufruf in 1.3 ❌. |
| D2 | Sicherheitsprüfung (eigene Rechenaufgabe) | – | ✅ Kein Empfänger mehr; als TOM nennen. |
| D3 | Profilbilder lokal | 4.1 Login | ✅/⚠️ kurz nennen. |
| D4 | Stripe.js entfernt, Checkout serverseitig | 4.1 Zahlung | ✅ Text muss D4 abbilden, nicht Abschnitt H des Verzeichnisses. |
| D5 | HTML-Mails im Admin-Postfach (Bildsperre) | 2.1/TOMs | ⚠️ Als TOM ✅; Zugriffsregel für 26lab auf Kundenmails ❌. |
| D6 | Marketing-Seite lädt Demo-Widget | **nirgends** | ❌ Siehe G Demo-Instanz. |
| D7 | Schriften lokal | 4.1 | ✅ (Negativaussage optional). |
| D8 | Baustein-Logos über eigenen Server | – | ✅ Nichts nötig; cdn.activepieces.com erhält nur Server-IP (F2). |
| D9 | Polaris-CSS entfernt | – | ✅ Nichts nötig. |

### E – Abläufe-Kern

| Pos. | Punkt | Abgedeckt in | Befund |
|---|---|---|---|
| E1 | Telemetrie aus | – | ✅ Als TOM/Negativaussage in 4.1 möglich; keine Pflicht. |
| E2 | Katalogabgleich aus | – | ✅ Nichts nötig. Hinweis: Wer nachzieht, holt wieder fremden Code – Change-Regel in 2.2 (Informationspflicht) deckt das ab. |
| E3 | 718 verbundene Bausteine | 1.1 § 5 | ✅ wie C9. |
| E4 | Aufbewahrung 30 Tage, Sandbox, Netzwerk strict, Backups 30 Tage, wöchentliche Restore-Probe | 1.1 § 8 „Abläufe 30 Tage" ✅ | ⚠️ Backups 30 vs. 7 (J.1). Restore-Probe als TOM in Anlage 1 ❌. |

### Weitere Verzeichnis-Positionen außerhalb A–E

| Pos. | Punkt | Befund |
|---|---|---|
| F1–F4 | Bezugsquellen (npm, activepieces-CDN, ClamAV, jsdelivr/pypi) | ✅ Kein Personenbezug; Lieferketten-Risiko (fremder Code) gehört in TOMs 5.4, nicht ins Datenschutz-Set. |
| G1 | Azure OpenAI – vorhanden, nicht geschaltet | ⚠️ Wird mit E1 zum aktiven Empfänger; 3.1 führt Microsoft bereits so, als wäre es umgestellt. |
| G2 | Mistral AI – Rückfallebene | ❌ Nirgends. Ausbauen oder Anlage 2. |
| G3 | Activepieces-Enterprise-Module (PostHog, Cloudflare-SaaS, AppSumo) | ✅ Nicht aktiv; Change-Regel 2.2 muss greifen, bevor jemand AP_EDITION umstellt. |
| H | „Nur technisch notwendige Cookies … Stripe setzt im Browser eigene (A5)" | ⚠️ Intern veraltet (0.3/D4). Verzeichnis beim nächsten Quartalsupdate korrigieren. |

---

## I. Fehlende Dokumente

### P1 – vor Livegang (05.10.2026)

| Nr. | Dokument | Begründung |
|---|---|---|
| I-1 | **Technisches Freigabeprotokoll „Vertrag = Maschine"** (eine Seite, Christian bestätigt mit Datum) | Das Verzeichnis zeigt das Muster „Zusage nicht belegbar" (0.7). Vor Livegang bestätigen: C1 Werkstatt auf Azure, C2 Backups 7 Tage, automatische Löschung Gespräche 90 Tage **existiert**, Selbstlernen Standard aus, Admin-Zugriffsprotokoll aktiv, Mistral-Rückfall aus, Messenger/Instagram aus oder gleichwertig abgedeckt, Azure Speech live ja/nein, „Einordnung jeder Nachricht" ohne Emotionserkennung. Ohne dieses Protokoll verspricht der AVV v1.6 Dinge, die am Tag 1 nicht gelten. |
| I-2 | **Rollen-Matrix** (eine Seite) | Je Verarbeitung: Flubber Verantwortlicher / Auftragsverarbeiter / Dritter. Grundlage für 4.1 (Trennung), 5.1 (Abs. 1 vs. Abs. 2), § 4 (Stripe raus), 2.1 (26lab ist für Flubbers eigene Daten direkter Auftragsverarbeiter, für Kundendaten Unterauftragsverarbeiter – beides muss 2.1 abdecken). |
| I-3 | **Vorfall-Prozess Kurzfassung** (Art. 33/34) | AVV verspricht 24 h, 2.1 verlangt 12 h – ohne Meldekette unerfüllbar. Inhalt: Meldekette, LDI-NRW-Kontakt, Kundenmeldungs-Vorlage, Dokumentation nach Art. 33 Abs. 5. |
| I-4 | **Betroffenenanfragen Kurzprozess** (Art. 12, 28 Abs. 3 lit. e) | Postfach, Zuständiger, Weiterleitung an Kunden, Löschweg (DB, Qdrant, MinIO, Inngest, Backups). |
| I-5 | **Vorlage WhatsApp-/Messenger-Erstnachricht** mit KI-Hinweis und Datenschutzlink | Einzige Informationsmöglichkeit für diese Gruppe (Art. 13, Art. 50 KI-VO). C4 deckt sie nicht ab. |
| I-6 | **Bot-Textvorlage Lead-Erfassung** (Art. 13 bei Erhebung) | Ein bis zwei Sätze, die der Bot vor der Abfrage von Kontaktdaten ausgibt, mit Link auf die Datenschutzerklärung des Kunden. |
| I-7 | **Textbaustein „Information der Beschäftigten"** für Kunden | Digitaler Mitarbeiter, Frag Lymbe, Live-Chat-Agenten: Art. 13, Einsichtsrechte der Admins, Websuche USA, Protokollierung, Hinweis auf Mitbestimmung. |
| I-8 | **Zusatzvereinbarung Art. 9 / § 203 StGB** (nur wenn Pilotkundin Gesundheits-/Rechtsbereich) | Verpflichtungserklärung nach § 203 Abs. 4 StGB für Dennis und Christian, Websuche/Selbstlernen aus, DSFA-Unterstützung, Kalender-/Benachrichtigungsdienste nur EU mit AVV. |
| I-9 | **§ 25-Bewertung Browserspeicher** (eine Seite) | Grundlage für die Behauptung „technisch erforderlich" in 1.3; Kunden müssen die Einträge in ihre Cookie-Hinweise übernehmen. |
| I-10 | **Ergänzung 1.3** (kein neues Dokument, aber Inhalt fehlt) | Referrer/IP bei jedem Seitenaufruf, Live-Chat, Leads, Benachrichtigungsziele, Selbstlernen, Termine, Bewertungen, Speicherfrist, Löschkontakt. |
| I-11 | **Demo-Instanz-Regel** (Absatz in 4.1 + Art.-30-Karte) | Flubber ist Verantwortlicher; Frist, kein Gedächtnis, keine Leads, KI-Hinweis. |
| I-12 | **DSB-Entscheidung mit Begründung** (halbe Seite) | § 38 Abs. 1 S. 2 BDSG koppelt DSB-Pflicht an DSFA-Pflicht – die 5.2-Vorprüfung entscheidet mit. Externer DSB kurzfristig benennbar; Benennung an LDI NRW melden (Art. 37 Abs. 7). |
| I-13 | **AVV-Nachweis Bestandsmandanten** | Vier Mandanten verarbeiten jetzt Daten ohne nachweisbaren AVV-Abschluss (Art. 28 Abs. 3, 9). Erneute Zustimmung per Checkbox beim nächsten Login, nicht rückdatieren (Verzeichnis 0.7 sagt das richtig). |
| I-14 | **Impressum-Korrektur** | ODR-Link **nicht** aufnehmen (Plattform seit 20.07.2025 abgeschaltet); D8 im Projektplan streichen. |

### P2 – vor breitem Verkauf

| Nr. | Dokument | Begründung |
|---|---|---|
| I-15 | Transfer-Folgenabschätzung OpenAI (SCC Klausel 14) + Microsoft-Rest-Übermittlung | Pflichtbestandteil bei SCC; DPF-Status prüfen. |
| I-16 | DSFA-Vorlage für Kunden („Plattform-DSFA") | DSK-Muss-Liste Nr. 11; Art. 28 Abs. 3 lit. f. |
| I-17 | KI-VO-Einstufung (Zweckbestimmung, Nicht-Hochrisiko-Begründung, Art.-50-Umsetzung, Art.-50-Abs.-2-Entscheidung) | Nachweis gegenüber Marktüberwachung und Kunden. |
| I-18 | KI-Kompetenz-Nachweis intern + Kunden-Merkblatt (Art. 4 KI-VO) | Gilt seit 02.02.2025. |
| I-19 | Löschkonzept (5.5) inkl. Qdrant, Inngest, Caddy-Logs, Fehlerprotokoll, Redis, Snapshots, Rechnungen 10 Jahre, Demo | Fristen in § 8 müssen vollständig werden. |
| I-20 | AVV-Änderungsverfahren (Textfassungen) | 1.4 deckt nur Unterauftragsverarbeiter. |
| I-21 | Anlage „Ansprechpartner und weisungsberechtigte Personen" zum AVV | Art. 28 Abs. 3 lit. a praktisch. |
| I-22 | Meta-Rollendokumentation + Ablage Business-Solution-Provider-Vertrag; Shopify-Partnervertrag | Lymbe steht im Datenfluss, nicht nur der Kunde. |
| I-23 | Let's Encrypt/ZeroSSL: Art.-30-Karte, 4.1-Absatz, Kundenhinweis CT-Logs | Bisher nirgends. |
| I-24 | Nachweise Hetzner/STACKIT/Microsoft (ISO 27001, C5) in 03_Dienstleister | Auftragskontrolle Art. 28 Abs. 1. |
| I-25 | Export-/Rückgabeformat (Art. 20, § 8) | Zusage „Rückgabe" ohne Format ist nicht prüfbar. |
| I-26 | Mitbestimmungs-/Beschäftigtendatenschutz-Hinweis in 1.0 und § 6 | § 87 Abs. 1 Nr. 6 BetrVG beim Kunden. |
| I-27 | Rollen-/Rechtekonzept Portal (Team-Rollen, Live-Chat-Sicht, Admin-Einsicht in Frag-Lymbe) | TOM und Beschäftigtendatenschutz. |
| I-28 | Dienstleisterverzeichnis-Korrektur (Azure Speech, Wächter-Meldeweg, Abschnitt H Stripe, Vertragsinhaber je Konto) | Es ist die „Basis für alles Weitere" (Projektplan) – dann muss es stimmen. |

### P3 – Anwalt klärt

| Nr. | Frage |
|---|---|
| I-29 | DSB-Pflicht nach § 38 Abs. 1 S. 2 BDSG für Auftragsverarbeiter – Auslegung. |
| I-30 | Reichweite Art. 50 Abs. 2 KI-VO (maschinenlesbare Kennzeichnung) für Chat-Text. |
| I-31 | Rolle Flubber bei Frag Lymbe (Auftragsverarbeiter oder gemeinsame Verantwortlichkeit, Art. 26) und beim Demo-Widget. |
| I-32 | Rechtsgrundlage Websuche: Hinweis genügt (lit. f) oder Einwilligung (lit. a)? |
| I-33 | Meta-Rollenkette (Solution Provider, Data Processing Terms) und E3-Entscheidung „keine Unterauftragsverarbeiter". |
| I-34 | § 203 StGB-Konstruktion bei Berufsgeheimnisträger-Kunden mit zweistufiger Auftragskette. |
| I-35 | Haftungsverteilung 50/50 (2.2) vs. Art. 82 Abs. 4/5 DSGVO (gesamtschuldnerische Außenhaftung, Innenregress nach Verantwortungsanteil). |
| I-36 | Minderjährige und Lead-Erfassung. |

---

## J. Widersprüche

| Nr. | Widerspruch | Quellen | Folge | Prio |
|---|---|---|---|---|
| J.1 | **Backups 7 Tage** im AVV § 8 und E2 – auf der Maschine **30 Tage** | 01 § 8; 00 E2/C2 „offen"; Verzeichnis E (S. 14/15) | AVV sagt am 05.10. etwas Falsches, wenn C2 bis dahin nicht umgestellt und bestätigt ist. | P1 |
| J.2 | **Werkstatt „nur über Azure"** (E1, 3.1 Microsoft „Azure OpenAI") – gemessen: **OpenAI** (AI_PROVIDER_WERKSTATT=openai, Azure nicht geschaltet) | 00 E1/C1 „offen"; Verzeichnis 0.4, A4, G1 | Anlage 2 und 4.1 nennen Microsoft als Empfänger, der es nicht ist, und verschweigen OpenAI für die Werkstatt. | P1 |
| J.3 | **Azure Speech Frankfurt** steht in 3.1, 4.1 und im Briefing – im Dienstleisterverzeichnis („ausschließlich das, was heute im Projekt ist") gibt es **keinen Microsoft-Eintrag** | 01 3.1/4.1; Verzeichnis A1–A10, G | Entweder Spracheingabe ist nicht live (dann aus 4.1 raus bis sie kommt) oder das Verzeichnis ist unvollständig (dann ist seine Vollständigkeitsaussage falsch). | P1 |
| J.4 | **Stripe als Unterauftragsverarbeiter** (§ 4) – tatsächlich Zahlungsdienstleister für Flubbers eigene Abrechnung | 01 § 4; Verzeichnis A5; 01 3.1 „Zahlung" | Rollenfehler im Kunden-AVV; Kunden könnten gegen Stripe „widersprechen", was sinnlos ist. | P1 |
| J.5 | **Vertragsinhaber der Cloud-Konten unklar**: 3.1 sagt Hetzner „Kundenkonto, per Klick" (Flubber?), 2.1 sagt Hetzner ist Unterauftragsverarbeiter **von 26lab**, C3 lässt **Christian** die AVV-Nachweise ablegen, 2.2 Exit „Übergabe von Zugängen" | 01 2.1, 3.1; 00 C3 | Wenn 26lab die Konten hält: Hetzner/STACKIT/OpenAI/Microsoft sind Sub-Sub-Prozessoren, Flubber muss deren AVVs über 2.1 durchreichen und hat selbst keine Vertragsbeziehung – § 4 des Kunden-AVV muss das richtig darstellen. Wenn Flubber sie hält: 2.1 ist falsch. | P1 |
| J.6 | **Fassungsnummern**: Verzeichnis 0.6 „Fassung 1.2" (17.09.), Projektplan „AVV v1.5, Sept. 2026", Ziel v1.6; Datenschutz „v1.4" → „v1.5" | Verzeichnis 0.6; 00 Bestandsaufnahme; 01 | Der Zustimmungsnachweis speichert eine Fassungsnummer – welche? Ein Nachweis mit uneindeutiger Nummer ist kein Nachweis. | P1 |
| J.7 | **„Livegang mit erster Pilotkundin"** – das Verzeichnis zeigt **fünf Mandanten-Datenbanken in Produktion**, **vier Bestandsmandanten** ohne AVV-Nachweis und WhatsApp „seit 14.09.2026 bestätigt in Betrieb" | 00 Kopf, 01 Kopf; Verzeichnis 0.7, 0.8, A7 | Das System ist bereits im Betrieb. Dann ist „Bestandsmandanten nach Livegang" nicht haltbar – entweder sind es Testmandanten (dann dokumentieren und Daten löschen) oder echte Kunden (dann P1). | P1 |
| J.8 | **1.3 behauptet § 25 Abs. 2 „technisch erforderlich"** – Verzeichnis 0.5: „sollte bestätigt werden", D1 „§ 25 TDDDG prüfen" | 01 1.3; Verzeichnis 0.5, D1 | Offene Prüffrage als Ergebnis verkauft; Kunden übernehmen das in ihre Cookie-Hinweise. | P1 |
| J.9 | **„Gespräche 90 Tage"** (§ 8) – im Verzeichnis ist **keine Gesprächslöschung** gemessen, nur Abläufe 30 Tage und Backups 30 Tage | 01 § 8; Verzeichnis E | Gleiches Muster wie 0.7: Zusage ohne Beleg. | P1 |
| J.10 | **Vorfall-Prozess „nach Livegang"** (E13, 5.6) – AVV § 7 verspricht 24 h ab Tag 1, 2.1 verlangt 12 h | 00 E13; 01 § 7, 2.1, 5.6 | Vertragliche Frist ohne Prozess. | P1 |
| J.11 | **Impressum: „OS-Plattform-Link ergänzen"** (D8, 4.2) – Plattform seit 20.07.2025 abgeschaltet (VO (EU) 2024/3228) | 00 D8; 01 4.2 | Aufgabe erzeugt einen Fehler statt ihn zu beheben. | P1 |
| J.12 | **„Nur der Suchbegriff geht raus"** (Briefing, C5, 4.1) – A4: Suchbegriff „den das Modell formuliert hat" aus der Nutzerfrage, plus Land | Briefing; 00 C5; Verzeichnis A4 | Hinweistext darf nicht suggerieren, es gingen keine personenbezogenen Daten. | P1 |
| J.13 | **E3 „verbundene Dienste sind keine Unterauftragsverarbeiter"** – Meta/WhatsApp läuft über **Lymbes eigene Meta-App** (Embedded Signup, Tokens bei Lymbe, Inngest verarbeitet Nachrichten) | 00 E3; Verzeichnis A7, B6 | Für Kalender/Shops trägt E3. Für Meta steht Lymbe selbst im Vertrag mit Meta – reine Einordnung als „Kundenkonto" greift zu kurz. | P2/P3 |
| J.14 | **3.1 Microsoft „Drittland nicht nötig (EU-Datenzone)"** – Microsofts DPA sieht Rest-Übermittlungen mit SCC vor | 01 3.1 | Zu absolute Aussage in Anlage 2. | P2 |
| J.15 | **Verzeichnis H „Stripe setzt im Browser eigene Cookies"** – Verzeichnis 0.3/D4: Stripe.js lädt nicht mehr | Verzeichnis intern | 4.1 muss D4 folgen; Verzeichnis korrigieren. | P2 |
| J.16 | **Wächter-Meldeweg** „über einen Weg, der mit unserem Mailserver nichts zu tun hat" – kein Anbieter genannt, obwohl das Verzeichnis Vollständigkeit beansprucht | Verzeichnis 0.11, A8 | Unbenannter Dienst (vermutlich Push-/SMS-Dienst) → nachtragen. | P2 |
| J.17 | **Mistral AI „Rückfallebene"** (G2) – Anlage 2 ohne Mistral | Verzeichnis G2; 01 § 4 | Wenn der Rückfall automatisch greifen kann, ist Mistral ein Empfänger. | P2 |
| J.18 | **Projektplan-Nummer C6 doppelt** („Hinweis im Portal beim Verbinden" vor Livegang; „Dienstleister-AVVs ablegen" nach Livegang) | 00 | Verwechslungsgefahr in Aufgabenlisten; umbenennen. | P2 |
| J.19 | **5.1 nennt acht Karten** – Verzeichnis zeigt zusätzlich Leads/Kontakte, Aufgaben, Termine, Bewertungen, Live-Chat, Sprach­eingabe, Demo, Hilfeseite, Vektorspeicher, Inngest, Zertifikate | 01 5.1; Verzeichnis B, C, D | Verzeichnis unvollständig gegenüber dem, was läuft. | P1 (Karten), P2 (Fristen) |
| J.20 | **2.2 Haftung „50/50 intern"** – Art. 82 Abs. 4/5 DSGVO: Außenhaftung gesamtschuldnerisch, Innenregress nach Verantwortungsanteil; 2.2 nennt zugleich „Freistellung bei technisch verursachten Verstößen" | 01 2.2 | 50/50 und Freistellung nach Verursachung widersprechen sich innerhalb desselben Dokuments. | P3 |

---

## Zusammenfassung der P1-Punkte (Reihenfolge nach Wirkung)

1. Freigabeprotokoll Technik: C1, C2, 90-Tage-Löschung, Selbstlernen-Default, Admin-Protokoll, Mistral, Azure Speech, Messenger/Instagram, Einordnung ohne Emotionserkennung (I-1).
2. Rollen-Matrix und Korrektur § 4 (Stripe raus, Vertragsinhaber klären) (I-2, J.4, J.5).
3. AVV § 2 Datenkategorien/Betroffene vollständig (IMAP-Dritte, Shop-Kunden, Kalenderteilnehmer, WhatsApp-Nutzer, Sprache, Art. 9) und § 8 Fristen ehrlich (A).
4. Betroffeneninformation für WhatsApp-Nutzer, Beschäftigte, Leads, Demo (I-5 bis I-7, I-11).
5. Vorfall- und Betroffenenanfragen-Kurzprozess (I-3, I-4).
6. Pilotkundin-Branche klären → ggf. Art.-9-/§ 203-Paket und DSFA (I-8).
7. DSB-Begründung korrigieren, mit 5.2 koppeln (I-12).
8. Bestandsmandanten-Nachweis (I-13, J.7).
9. 1.3 ergänzen und § 25-Bewertung dokumentieren (I-9, I-10, J.8).
10. Websuche-Hinweistext und Anlage 2 (OpenAI-Werkstatt bis C1) richtigstellen (J.2, J.12).
11. Impressum: ODR-Link nicht einfügen (J.11).
12. Art. 50 KI-VO: Kennzeichnung auch für WhatsApp, Mail-Antworten aus Abläufen, Demo, Wechsel Mensch/KI (C).
