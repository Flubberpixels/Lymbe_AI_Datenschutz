# Code-Gegenprüfung C – Websuche, KI-Anbieter, Widget, Browserspeicher, Cookies, Demo, Wächter, Meta

Nur lesende Prüfung des Repos `/home/claude/lymbe-ai` (Stand Commit `923f8ee`, 12.10.2026) gegen Kunden-AVV 1.7, Datenschutzerklärung 1.6, Freigabeprotokoll 5.9 (A1, A10–A13, A22, B1–B4, C1–C7) und 1.5 Widget-/Kanaltexte (Fassung 1.1 vom 11.10.2026). Keine Skripte, keine Datenbank, kein Server. Was nur am laufenden System prüfbar ist (Umgebungsvariablen, Azure-Region, GitHub-Einstellungen), steht als „nicht im Code prüfbar“.

Urteile: **belegt** · **teilweise** · **nicht belegt** · **nicht im Code prüfbar**

---

## 1. Websuche in Frag Lymbe (AVV § 3 Abs. 10, Anlage 2 Nr. 5, Anlage 3; DSE 4 und 5; 5.9 A10, B1)

**Urteil: belegt** – mit zwei Hinweisen (latenter OpenAI-Pfad „Rechnen“, Wortlaut der Nachweise).

| Zusage | Code | Befund |
|---|---|---|
| Suchbegriff wird von einem STACKIT-Modell nach fester Anweisung gebildet | `lib/ai/suchbegriff/anweisung.ts:15-22` (`GENERATOR_ANWEISUNG`: „Niemals: Vor- oder Nachnamen, Initialen … E-Mail-Adressen, Telefonnummern … Höchstens 12 Wörter“), Prüfsumme `:25`; `lib/ai/suchbegriff/modelle.ts:33` `model: getModelForTask('summarize')` → bei `AI_PROVIDER=stackit` `Qwen/Qwen3.8-27B` (`lib/ai/providers.ts:159`) | belegt. Der Generator läuft beim **aktiven** Anbieter (`providers.ts:423-426`); in Produktion laut A1 `stackit`. Wäre `AI_PROVIDER=openai`, liefe auch der Generator bei OpenAI – dann ginge das „Anliegen“ dorthin (Konfiguration, nicht Code). |
| Regex-Filter | `lib/ai/suchbegriff/filter.ts:29-50` (E-Mail, @-Name, IBAN, Telefon, ≥6 Ziffern, Datum, PLZ+Ort, Anschrift, Geburtsangabe), `:58` erlaubte Zeichen, `:96` max. 12 Wörter | belegt. Hinweis `:13-17`: allgemeine Namensregeln (Vornamenliste) sind seit 06.10. bewusst **aus**; Namen fangen Generator, Sperrliste, Zweitprüfung. |
| Sperrliste je Workspace | `lib/ai/suchbegriff/sperrliste.ts:27-66`: Namen aus Leads, Gesprächen, Terminen (je 5000 jüngste) und Team-Mitgliedern der Mandanten-DB; 10 Min. Prozess-Cache, nicht Redis (`:10-13`) | belegt. |
| Zweitprüfung | `modelle.ts:46-58` zweites Modell `getModelForTask('classify')` (STACKIT `openai/gpt-oss-20b`, `providers.ts:155`) mit `ZWEITPRUEFUNG_ANWEISUNG` (`anweisung.ts:31-34`), sieht nur den Begriff | belegt. |
| Reihenfolge, geschlossen bei Fehler | `lib/ai/suchbegriff/pipeline.ts:74-106`: Generator → `contains_person` → Muster → Sperrliste → Zweitprüfung; Modellfehler → `status: 'fehler'` → **nicht gesucht** (`web-suche.ts:135-138`); unlesbare Antwort gilt als Personenbezug (`pipeline.ts:62-63, 68-71`) | belegt. |
| Blockiermeldung 1.5 G | `lib/ai/suchbegriff/texte.ts:10-11` wortgleich mit 1.5 G; Rückgabe an das Modell `web-suche.ts:126-134` („Gib dem Nutzer genau diese Meldung wörtlich wieder“); Anzeige im Portal `components/platform/portal-chat/PortalChatThread.tsx:911` | belegt. |
| An OpenAI geht nur Suchbegriff + „DE“ | `web-suche.ts:142-161`: `generateText({ model: openAiSuchModell(), system: 'Du bist ein Suchdienst…', prompt: suchbegriff, tools: { web_search: openAiWerkzeuge.webSearch({ searchContextSize: 'high', userLocation: { type: 'approximate', country: 'DE' } }) }, providerOptions: { openai: { store: false } }, stopWhen: stepCountIs(3) })`. Kein Verlauf, kein `user`, keine Metadaten (`:144, :156`) | belegt. |
| Endpunkt/Modell | `providers.ts:418-420` `openAiSuchModell()` = `sprachmodell('openai', 'gpt-5.4-mini')` → `openaiProvider(id)` = Responses-API von `@ai-sdk/openai` (`:406`); Werkzeug `web_search` (`:374`) | belegt (Responses-API, `gpt-5.4-mini`, `web_search`, `store:false`). |
| `store:false` | `web-suche.ts:157` | belegt. |
| Nachweis-Log 14 Tage | `lib/ai/suchbegriff/nachweis.ts:17-36`: je Aufruf eine Zeile `WebsucheNachweis` (userId, status, stufe, Begriff **nur** wenn gesendet, Anweisungs-Hash); `anweisung.ts:37` `NACHWEIS_TAGE = 14`; Löschung `inngest/functions/data/cleanup-conversations.ts:159` `websucheNachweis.deleteMany({ erstelltAm < jetzt-14 Tage })` | belegt. |
| Hinweis bei jeder Suche / Erklärung beim ersten Öffnen | `texte.ts:14-15` (🔍-Zeile, Anhängen an gespeicherte Antwort `:37-40`), `texte.ts:66-68` + `components/platform/portal-chat/WebsucheErklaerung.tsx:16-31` (localStorage `lymbe_websuche_erklaert:{userId}`) | belegt, Wortlaut gleich 1.5 G. |
| Abbestellen je Workspace wirkt auf den Suchpfad | Feld `prisma/schema.prisma:1159` `websucheAbbestelltAm`; Admin-Aktion `server/actions/tenant-actions.ts:653-676` (nur SUPERADMIN/PLATFORM_ADMIN, Audit-Zeile `TENANT_UPDATED`, `details: { websucheAbbestellt }`). **Wirkung:** `app/api/portal/chat/route.ts:746` `const mitWebsuche = capabilities.usesWebSearch && kannImNetzSuchen() && !tenantMarke?.websucheAbbestelltAm;` und `:891` nur dann Werkzeug; gleiches in `lib/aufgaben/lauf.ts:340, 347` (Aufgaben) und `components/platform/portal-chat/ChatScreens.tsx:181-184` (Erklärung nur anzeigen, wenn Suche möglich); Tests `tests/suchbegriff.test.mts:255-259` nageln die Zeilen fest | belegt – das Feld wird bei jedem Zug gelesen, ohne Werkzeug kann das Modell nicht suchen. Nur Bereich `allgemein` hat die Suche überhaupt (`lib/portal-chat/mode-domain.ts:49, 54`); „Digitaler Mitarbeiter“ (business) nie. |
| Kein anderer Pfad zu api.openai.com mit Nutzertext/Dokumenten/Gedächtnis | Grep `OPENAI_API_KEY|api.openai.com` (ohne Doku/Skripte): (a) `providers.ts:289` Provider-Objekt – nur über `openAiSuchModell()` und `openAiWerkzeuge` erreichbar, sonst nur wenn `AI_PROVIDER`/`AI_PROVIDER_WERKSTATT`/`AI_EMBEDDING_PROVIDER` = `openai` (Env); (b) `providers.ts:613` Health-Check `/v1/models` nur wenn `AI_PROVIDER=openai`; (c) **`lib/ai/openai-dateien.ts:13-36`** lädt Dateien zu `https://api.openai.com/v1/files` (`purpose: user_data`) und `lib/ai/rechnen.ts:51-58` Code-Interpreter – aber nur wenn `kannRechnen()` = `activeProvider() === 'openai'` (`rechnen.ts:27-29`) **und** kein Haus-Sandkasten (`app/api/portal/chat/route.ts:757-759, 850-859`). | belegt für den Produktionsstand (`AI_PROVIDER=stackit`, A1); der Rechen-Upload ist ein **latenter Pfad**, der ausschließlich an der Env hängt. Empfehlung: `kannRechnen()` zusätzlich hart abschalten oder Rechen-Upload entfernen, damit ein Anbieterwechsel die Zusage nicht still bricht (dieselbe Überlegung wie `web-suche.ts:23-26` für die Suche). Skripte `scripts/modell-vergleich.cjs:134` rufen `api.openai.com` direkt – Entwicklerwerkzeug, nicht Betrieb. |

Ergänzung zu Anlage 2 Nr. 5: Der Code sendet Suchbegriff + Land „DE“ + einen festen System-Satz („Du bist ein Suchdienst…“, `web-suche.ts:145-148`) – kein Personenbezug, aber der Vertrag nennt den System-Satz nicht; unschädlich.

---

## 2. KI-Anbieter (Anlage 2 Nr. 3/4; 5.9 A1, A11, B4; DSE 2.7, 7)

**Urteil: belegt** (Rückfall), **nicht im Code prüfbar** (welcher Wert in Produktion gesetzt ist), **teilweise** (Speicherung bei Einordnung – siehe Cache).

- **Anbieter:** `lib/ai/providers.ts:58` `type AiProviderId = 'openai' | 'azure' | 'stackit'`. Kein Mistral mehr; `readProvider()` `:234-241` nimmt nur diese drei, alles andere → Vorgabe mit `console.error`. Vorgabe Chat `stackit` (`:250-252`), Embeddings `stackit` (`:283-287`). Keine Mistral-Abhängigkeit in `package.json:80-82` (nur `@ai-sdk/azure`, `@ai-sdk/openai`); Treffer auf „mistral“ im Code sind Kommentare, Modell-ID-Migration und der Embedding-Name `intfloat/e5-mistral-7b-instruct` bei STACKIT (`:81, :168`) – ein offenes Modell bei STACKIT, kein Mistral-Dienst. → **A11 belegt.**
- **Kein automatischer Rückfall bei Fehlern:** Grep nach Fallback/Rückfall in `lib/ai` findet nur Textrückfälle (Rückfallsatz, `JUST_BROWSING` `intent-classifier.ts:104, 298-305`) – nie einen Anbieterwechsel. `werkstatt/route.ts:956-968` wiederholt mit `maxRetries: 1` **beim selben Modell**. Websuche: Fehler → „nicht erreichbar“, keine Suche (`web-suche.ts:169-172`). → **belegt.**
- **Werkstatt-Anbieter:** `providers.ts:230-232` `TASK_PROVIDER_ENV = { werkstatt: 'AI_PROVIDER_WERKSTATT' }`, `:423-426` `providerForTask('werkstatt')` = `readProvider('AI_PROVIDER_WERKSTATT', activeProvider())`. Gewählt in `app/api/portal/ablaeufe/werkstatt/route.ts:957` `getModelForTask(task)`. Fehlt die Variable oder ist sie falsch geschrieben, fällt sie auf den aktiven Anbieter (`stackit`), **nicht** auf OpenAI. Auf OpenAI nur, wenn jemand `AI_PROVIDER_WERKSTATT=openai` setzt – `docs/SERVICES.md:55` beschreibt genau das als „Rückweg“. Ob in Produktion `azure` steht (A1): **nicht im Code prüfbar**. Azure-Modell `gpt-6.1-sol` über Chat Completions (`providers.ts:119, 398-400`); Region hängt am Ressourcennamen `AZURE_OPENAI_RESOURCE` (`:305-309`), nicht im Code.
- **Modelle Einordnung/Stimmung (B4):** Einordnung `lib/ai/intent-classifier.ts:283` `getModelForTask('classify')` → STACKIT `openai/gpt-oss-20b` (`providers.ts:155`) – **nicht 120b** (120b nur `authoring`, `:161`). Labels `intent-classifier.ts:8-19` inkl. `FRUSTRATION`. Stimmungs-Auswertung `server/services/analytics-service.ts:454-512` mit `getModelForTask('draft')` (= `Qwen/Qwen3.8-27B`, `providers.ts:160`) über bis zu 30 Gesprächsproben (`filterPII`, 600 Zeichen), nur Assistenten mit `trackUserSentiment: true` (`:468`) und nur Kundengespräche (`textAuswertungWhere` → `kundenGespraechWhere`, `:53-55`); Ergebnis ist eine Summe positiv/neutral/negativ je Assistent (`:495-507`). Mitarbeiter-Chats (`PortalThread`) haben strukturell keine Stimmungsspalten (`prisma/tenant/schema.prisma:60-69`). → **belegt.** Hinweis: DSE 2.7 sagt „ordnet jede Nachricht nach … Stimmung ein“ – im Code gibt es je Nachricht nur die Absicht (mit `FRUSTRATION`); die Stimmung positiv/neutral/negativ entsteht nachträglich in der Auswertung. Sinngemäß gedeckt.
- **Was wird gespeichert:** Das Klassifikationsergebnis (`intent`, `confidence`, `reasoning`, `extractedFields`, `searchQuery`) liegt **900 s im Redis-Cache** unter einem Hash des Prompts (`intent-classifier.ts:113, 275-277, 196-203`). Der Schlüssel enthält keinen Text, der **Wert** aber `reasoning` und `extractedFields` (Werte aus der Nachricht, bis 200 Zeichen `:116`) – kurzlebig, aber kein reiner „Hash-Cache“. `Conversation.sentiment` (`schema.prisma:782`) wird im aktuellen Code nirgends geschrieben (nur gelesen, `conversation-inbox-actions.ts:178, 274`) – Altspalte. → **teilweise**: Zusage „nur Summe je Assistent“ hält; der 15-Minuten-Cache mit `extractedFields` ist in keinem Text erwähnt (unkritisch, aber zu wissen).

---

## 3. Azure Speech (Anlage 2 Nr. 4, Anlage 3 „Spracheingabe“; DSE 4, 5; 5.9 A12, B3)

**Urteil: belegt** (kein Speichern, kein Logging-Parameter) · **nicht im Code prüfbar** (Region).

- Endpunkt aus Umgebung: `lib/sprache/transkription.ts:72-74` `https://${ressource}.cognitiveservices.azure.com/speechtotext/transcriptions:transcribe?api-version=2025-10-15`, `ressource` = `AZURE_SPEECH_RESOURCE` (`:84-91`). Die Region steckt in der Azure-Ressource, nicht im Code → „Germany West Central“ nur per Azure-Portal prüfbar.
- Audio-Logging: Request-`definition` enthält nur `locales` und `profanityFilterMode: 'None'` (`:115-118`) – kein Logging-Schalter gesetzt. Dass Microsoft bei Fast Transcription standardmäßig nicht speichert, ist eine Anbieteraussage (B3), nicht Code.
- Aufnahme verworfen: Bytes nur im Prozess (`:23-24`), `formular.append('audio', new Blob(...))` (`:112`), Rückgabe nur `{ text, sekunden }` (`:171`). Routen `app/api/portal/sprache/route.ts:46-53` und `app/api/widget/[botId]/sprache/route.ts` (Kopf: „Die Aufnahme wird weder gespeichert noch an das Gespräch gehängt“) schreiben keinen MinIO/DB-Eintrag; Logs nur `art`, `sekunden`, `zeichen` (`portal:52`, `widget:96`). Kein Audio-Logging gefunden. → **belegt.**
- Hinweis: Anlage 3 nennt als Betroffene der Spracheingabe nur „Nutzer des Portals“; es gibt aber auch die **Widget**-Spracheingabe für Website-Besucher (`app/api/widget/[botId]/sprache/route.ts`). 1.5 B und DSE 2.7 decken das ab; Anlage 3 nicht wörtlich.

---

## 4. Widget-Texte nach 1.5 (AVV § 6 Abs. 2; 5.9 A22, A13)

**Urteil: teilweise** – Mechanik vollständig, Wortlaut entspricht 1.5 **Fassung 1.0**, nicht 1.1.

| Element | Code | Befund |
|---|---|---|
| Startdialog A/P mit Checkbox | `lib/legal/widget-legal.ts:164-183` (`startPunkte`), `:447-451` (`consentIntro`, `consentLabel: 'Ich habe die rechtlichen Hinweise gelesen.'`); Checkbox `components/widget/ConsentGate.tsx:115-122` | belegt. Abweichung (dokumentiert `widget-legal.ts:21`): Punkt „Bei Bedarf übernimmt ein Mitarbeiter …“ nur, wenn Übergabe möglich (`humanHandover`). |
| Bestätigung mit Fassung/Zeitpunkt | `components/widget/WidgetChat.tsx:272-307` `lymbe_consent_{botId}` = `{ version, acceptedAt }`, Gültigkeit `CONSENT_TTL_DAYS = 180` (`widget-legal.ts:63`), neue Fassung → erneut (`:290`); serverseitig `Conversation.consentAcceptedAt/consentVersion` (`schema.prisma:777-778`) | belegt. |
| Gate abschaltbar | `BotConfig.legalRequireConsent` (Default true, `schema.prisma:640`) und `legalEnabled` sind **Kundenschalter** (`components/platform/bot-config/sections/AdvancedSection.tsx:235-249`). Ohne Gate bleibt eine passive KI-Zeile (`WidgetChat.tsx:2478-2490`); bei `legalEnabled=false` fehlt auch die (`app/widget/[botId]/page.tsx:191-212`, `legal = null`). | teilweise: Kennzeichen „KI“ im Kopf bleibt immer (`components/widget/WidgetHeader.tsx:84, 210, 285-296`), aber der Kunde kann Startdialog **und** Rechtstext abschalten – AVV § 6 Abs. 2 verspricht die Kennzeichnung durch Lymbe; der Kopf-Badge erfüllt das minimal. |
| KI-Kennzeichen / Wechsel Mensch↔KI | Kopf-Badge „KI“/„Mensch“ (`WidgetHeader.tsx:285-296`); Zeilen 1.5 E `lib/legal/widget-texte.ts:34-50` („… ist jetzt im Chat – ab hier schreibt ein Mensch.“ / „Der KI-Assistent ist wieder da. … hat den Chat verlassen.“), Einsatz `WidgetChat.tsx:1331, 1404`, `server/actions/live-chat-actions.ts:217`, `app/api/desktop-app/live/[conversationId]/release/route.ts:84`; nur Vorname (`widget-texte.ts:27-31`, `live-chat-actions.ts:86`) | belegt. |
| Blockiermeldung Websuche | siehe 1 | belegt (Portal, nicht Widget – richtig so). |
| WhatsApp/Messenger/Instagram-Erstnachricht J | `lib/kanal/erstnachricht.ts:22` 90 Tage, `:33-50` Text wortgleich 1.5 J (ohne Link, falls kein `legalPrivacyUrl`), § 12-Zusatz `:25-26` bei `tenant.berufsgeheimnis`, Kanalname eingesetzt; Fälligkeit `:53-56` je Gespräch/Absender; Versand vor jeder Antwort `inngest/functions/whatsapp/answer-message.ts:94-140`, `inngest/functions/meta/answer-message.ts:90ff` | belegt. |
| Sprach-Hinweis K beim ersten Mikrofon-Klick | `widget-texte.ts:82-89`, `components/widget/ChatInput.tsx:42-44, 181` (sessionStorage `lymbe_sprache_hinweis`) | belegt; Wortlaut sagt „bei Microsoft **in Frankfurt**“, 1.5 K (1.1) sagt „in Deutschland“. |
| Demo-Text L | Kein eigener Text im Code. Der Demo-Workspace nutzt den normalen Startdialog, die Frist wird zu „24 Stunden“ (`widget-legal.ts:148-150` `frist(1)`, `lib/data-retention/policy.ts:197-202`). | **nicht belegt** als Wortlaut 1.5 L („Hi, ich bin Lymbe … ich lerne nichts dazu … Bitte keine echten Kundendaten eingeben“) – stattdessen Startdialog A mit 24 Stunden. Sinnabweichung: „lernt nichts dazu“ und „keine echten Kundendaten“ fehlen. |
| Weitere 1.5-Texte | D (`widget-texte.ts:60-79`) und Prompt-Regel `:97-103` belegt. **C** Proaktive Ansprache: Text wird vom Modell erzeugt (`app/api/widget/[botId]/proactive/route.ts:315`), nicht fester Satz. **F** Bewertung: `components/widget/RatingDialog.tsx:95, 116` „Ihre Meinung ist uns wichtig / Ihr Feedback hilft uns …“ statt „War das hilfreich? … Ihre Bewertung ist anonym.“ **M** Portal-Hinweis `lib/legal/portal-hinweise.ts:24-30` sagt „KI-Modelle in Deutschland“, 1.5 M (1.1) „in Deutschland und der EU“. | Sinnabweichungen C, F, M. |

**Abweichungen Rechtstext B (Code = 1.5 Fassung 1.0 vom 06.10., Vorlage = 1.1 vom 11.10.):**
1. `widget-legal.ts:54` `WIDGET_TEXT_FASSUNG = 'Fassung 1.0, Oktober 2026'`, `WIDGET_LEGAL_VERSION = '2026-10-06.1'` – 1.5 sagt „Fassung 1.1, 11. Oktober 2026“.
2. Datenliste `:275-285`: es fehlen (a) „das KI-Modell ordnet jede Nachricht nach Anliegen und Stimmung ein … nur als Summe je Assistent“, (b) der Besuchsanalyse-Zusatz (erste Seite, Scrolltiefe, Sitzungskennung, Do-Not-Track/GPC), (c) „Name des übernehmenden Mitarbeiters“ und (d) der Merker für den Widerspruch gegen die Besuchsanalyse (`lymbe_ignore`). Code nennt stattdessen „Merker … Chat-Fenster von selbst geöffnet …“.
3. Empfänger `:333-339`: STACKIT ohne „(Verarbeitung in der EU, nach Angabe des Anbieters in deutschen Rechenzentren)“; Microsoft „Rechenzentrum Frankfurt“ statt „in einem Rechenzentrum in Deutschland“; Satz `:346` „Alle Empfänger verarbeiten die Daten **in Deutschland**“ – 1.5 (und AVV 1.7 Anlage 2 Nr. 3: STACKIT „EU/EWR (vertraglich)“) sagen „in Deutschland oder der EU“. Das ist die gewichtigste Textabweichung: der Widget-Rechtstext verspricht mehr, als der AVV zusichert.
4. Speicherdauer `:361-371`: Code nennt zusätzlich Termine, Nachweis der Bestätigung (bis 1095 Tage) und „Sicherungskopien: bis zu 14 Tage“; 1.5 „7 Tage …, bis zu 14 Tage“ – sinngleich.
Die Textfassung wird nach 1.5-Änderung nicht automatisch nachgezogen; Besucher müssten bei neuer `WIDGET_LEGAL_VERSION` erneut bestätigen (`WidgetChat.tsx:290`).

---

## 5. Widget ohne Chat (DSE 2.7, Anlage 3 „Kundenservice“; 5.9 C2)

**Urteil: belegt.**

- **Beim Seitenaufruf:** `public/widget.js:480-484` `GET /api/widget/{bot}/bootstrap?tenant=&key=` mit `credentials: 'omit'` (Referer-Header setzt der Browser); iframe `:287-288` `GET /widget/{bot}?tenant=&key=`; die Bootstrap-Route wertet weder Referer noch IP aus (kein Treffer in `app/api/widget/[botId]/bootstrap/route.ts`), IP landet nur in Container-Logs (Caddy/Next, Frist 14 Tage – Teil C von Prüfung A).
- **Events:** `widget.js:526-620`: Puffer, Batch ≤ 20 an `/api/widget/{bot}/events` (`sendBeacon`/`fetch keepalive`, `credentials: 'omit'`); je Event `id, ts, type, url` (volle `location.href`), `ref = document.referrer` nur beim ersten `page_view` (`:578-581`), `scroll` in Schwellen (`:648-662`), `sid` zufällig je Seitenladen, nicht gespeichert (`:555, events/route.ts:141`).
- **Vorgabe an/aus:** `BotConfig.enableAnalytics @default(true)` (`schema.prisma:626`), Bootstrap liefert `enableAnalytics: bot.config?.enableAnalytics !== false` (`bootstrap/route.ts:111`); Loader-Default `false` bis Bootstrap da ist (`widget.js:533`). → **Vorgabe an**, wie in C2 beschrieben.
- **DNT/GPC/Opt-out:** `widget.js:736-755`: `navigator.doNotTrack === '1'` → aus (wenn `respectDoNotTrack`), `navigator.globalPrivacyControl === true` → aus (wenn `respectGlobalPrivacyControl`), `?lymbe_track=off` setzt `localStorage.lymbe_ignore = '1'`, gesetzt → aus; `navigator.webdriver` → aus. Beide Respekt-Schalter sind per Bot abschaltbar (Default true, `schema.prisma:633-634`, UI `AdvancedSection.tsx:225-229`) – DSE sagt „bleibt das aus“ ohne Vorbehalt → kleine Lücke, falls ein Kunde den Schalter umlegt.
- **IP bei Events:** `app/api/widget/[botId]/events/route.ts:85-86` IP nur für Rate-Limit und Ausschlussliste; `:132-136` `visitorHash = SHA256(dailySalt:botId:ip:ua:host)` (`lib/analytics/visitor.ts:42-53`), `sessionHash` = Hash aus visitorHash + 8 Zufallsbytes, 30 Min. in Redis (`:59-72`); gespeichert werden `visitorHash`, `sessionHash`, `country`, `url` (nur Pfad + UTM, `normalizeUrl`), `referrer` normalisiert – **keine Roh-IP** (`schema.prisma:1298-1300` Kommentar „nie Roh-IP“, „IP wird danach verworfen“). → gehasht, tagesrotierend. Hinweis: DSE/1.5 nennen nur die „zufällige Sitzungskennung“; der zusätzliche tagesrotierende `visitorHash` (aus IP+UA) ist pseudonym, aber in keinem Text genannt.
- `Conversation.visitorIp` (`schema.prisma:767`) existiert, wird im aktuellen Code nirgends geschrieben (nur gelesen `conversation-inbox-actions.ts:173, 268`).

---

## 6. Browserspeicher des Widgets (DSE 2.7, 6; 1.5 B; 5.9 C3)

**Urteil: belegt** – Liste vollständig, ein Name ist in DSE/1.5 ungenau.

| Schlüssel | Speicher | Dauer | Code |
|---|---|---|---|
| `lymbe_chat_{bot}` | localStorage | 12 h (`CONVERSATION_TTL_MS`) | `WidgetChat.tsx:208-211, 229-265` (id, sessionId, ts, ended) |
| `lymbe_consent_{bot}` | localStorage | 180 Tage | `WidgetChat.tsx:277-307`, `widget-legal.ts:63` |
| `lymbe_ignore` | localStorage | bis Widerruf, nur auf Wunsch (`?lymbe_track=off`) | `widget.js:746-754` |
| `lymbe_proactive_seen:{pfad}` | sessionStorage | Sitzung | `widget.js:786, 802-808` |
| `lymbe_proactive_last` | sessionStorage | Sitzung | `widget.js:787, 808-815` |
| `lymbe_auto_open_done:{bot}` | sessionStorage | Sitzung | `widget.js:1044-1059` |
| `agent_name_{bot}` | sessionStorage | Sitzung | `WidgetChat.tsx:312-325` – **Zufallsname des Assistenten** aus `bot.agentNames`, nicht der Name des übernehmenden Mitarbeiters |
| `lead_captured_{bot}` | sessionStorage | Sitzung | `WidgetChat.tsx:532, 2585` |
| `lead_form_shown_{bot}` | sessionStorage | Sitzung | `WidgetChat.tsx:1575-1579` |
| `lymbe_sprache_hinweis` | sessionStorage | Sitzung | `ChatInput.tsx:42-44, 181` |

Weitere Schlüssel: keine (Grep über `components/widget`, `public/widget.js`, `app/widget`). `lymbe_websuche_erklaert:{userId}` ist Portal, nicht Widget. **Cookies:** kein `document.cookie`, kein `Set-Cookie` in Widget-Code oder `app/api/widget/*`; alle Loader-Abrufe `credentials: 'omit'`; `proxy.ts:124` lässt `/widget` ohne Auth durch. → keine Cookies. Abweichung: DSE 2.7/1.5 B beschreiben `agent_name_` als „Name des übernehmenden Mitarbeiters“ – im Code ist es der gewürfelte Anzeigename des KI-Assistenten (der Mitarbeiter-Vorname kommt per Live-Kanal, nicht aus dem Speicher).

---

## 7. Portal-Cookies, fremde Skripte/Schriften, Stripe (DSE 2.1, 6; 5.9 C5, C7)

**Urteil: belegt** – mit einer Ungenauigkeit beim Sitzungs-Cookie.

- Cookies (`lib/auth.ts:90-119`): `__Secure-authjs.session-token`, `__Secure-authjs.callback-url`, `__Host-authjs.csrf-token`; `onboarding-tenant-id` httpOnly, 1 h (`server/actions/onboarding-v2-actions.ts:320-327`, gelöscht `:1160`). Weitere `cookies().set` gibt es nicht. → vier Cookies, wie DSE 6 beschreibt.
- **Ungenauigkeit:** DSE 6 nennt das Session-Cookie „wird beim Schließen des Browsers gelöscht“. Auth.js setzt mit `session.maxAge = LEERLAUF_S` (`lib/auth.ts:85-88`, `lib/sitzung-dauer.ts:31` = 12 h) ein **Ablaufdatum** – das Cookie überlebt das Schließen des Browsers bis zu 12 Stunden (Superadmin 1 h). Nicht im Code widerlegbar, aber Auth.js-Standardverhalten bei gesetztem `maxAge`; am Browser prüfen.
- Schriften: `next/font/local` in `app/layout.tsx:2`, `app/(marketing)/layout.tsx:1`, `app/(auth)/layout.tsx:2`; kein `fonts.googleapis`/`gstatic`. → belegt.
- Stripe: `package.json:140` nur Server-SDK `stripe`, kein `@stripe/stripe-js`; `components/platform/billing/AvailablePlansCard.tsx:18-20` dokumentiert den Ausbau; kein `js.stripe.com`, kein `loadStripe`. → belegt.
- Fremde Skripte: einziges `<script src>` ist `https://demo.lymbe.ai/widget.js` auf der Marketing-Seite (`app/(marketing)/layout.tsx:93-99`) – eigene Domain. → belegt.

---

## 8. Demo-Workspace (DSE 2.1; 5.9 C1; 1.5 L)

**Urteil: teilweise.**

- Löschung 24 h: `lib/data-retention/policy.ts:197-202` `DEMO_TAGE = 1`, `mitDemoFrist` setzt `conversationDays/leadDays/appointmentDays = 1` für `Tenant.istDemo`; angewandt in `lib/data-retention/laden.ts:77`; stündlicher Lauf `inngest/functions/data/cleanup-conversations.ts:502-538` (`cron '20 * * * *'`, registriert `app/api/inngest/route.ts:19, 79`). → **belegt** (Gespräche, Leads, Termine; faktisch ≤ 25 h).
- Selbstlernen aus / Leads an: keine Kopplung an `istDemo` im Code (Grep `istDemo` zeigt nur Abrechnung, Fristen, Dashboard). Es sind Bot-Einstellungen des Demo-Assistenten (`selfLearningMode @default(DISABLED)`, Lead-Capture). → **nicht im Code prüfbar**, nur Konfiguration (C1 sagt: Selbstlernen aus, Kontaktfrage im Chat an).
- Demo-Text 1.5 L: nicht umgesetzt (siehe 4) – der Startdialog A mit „24 Stunden“ steht stattdessen.

---

## 9. Google/GitHub-Login – Profilbild (DSE 2.2; 5.9 C6)

**Urteil: belegt.**

`lib/auth.ts:132-163` legt `image: null` an statt der Anbieter-URL; JWT-Callback `:438-441` ruft bei `provider === 'google' || 'github'` `anmeldefotoUebernehmen()`. `lib/profile/anmeldefoto.ts:38-41` Positivliste `lh3.googleusercontent.com`, `avatars.githubusercontent.com`; `:91-95` wer schon ein eigenes Foto hat → kein Abruf; `:97-116` einmaliger `fetch` (4 s, `redirect: 'error'`), Typ/Größe geprüft, `fotoSpeichern` in eigene Ablage, `User.image` = eigene Route (`avatarUrl`), alte Fotos entfernt. Danach kein Abruf bei Google/GitHub mehr. Fehler lassen die Anmeldung nicht scheitern (`:119-122`).

---

## 10. Wächter (DSE 4 „GitHub Inc. – Verfügbarkeitsprüfung“; 5.9 C4)

**Urteil: belegt** (Code) · **nicht im Code prüfbar** (Mail-Empfänger, Actions-Einstellungen bei GitHub).

`.github/workflows/waechter.yml`: Takt `*/30 * * * *` (`:38`), zusätzlich `17 4 1 * *` (`:40`). Job `puls` (`:66-98`): `GET https://app.lymbe.ai/api/puls` (nur `{"ok":true/false}`, `app/api/puls/route.ts` – `SELECT 1`, keine Zahlen, keine Mandanten), `GET https://lymbe.ai/` (HTTP-Code), TLS-Ablauf von `app.lymbe.ai:443` per `openssl` (≥ 10 Tage). Keine Personendaten, keine Secrets außer `github.token`. Job `wachhalten` (`:50-64`): nur am Monatstermin oder von Hand, `gh api -X PUT repos/…/actions/workflows/waechter.yml/enable` mit `permissions: actions: write` – setzt die 60-Tage-Abschaltung zurück. Meldeweg laut Kommentar `:30-32`: GitHubs eigene Fehl-Mail an die Person, die die cron-Zeilen zuletzt geändert hat – das ist GitHub-Verhalten, nicht Code.

---

## 11. Messenger/Instagram über die Meta-App (AVV § 5; DSE 2.8; 5.9 A13)

**Urteil: belegt.**

Webhook `app/api/meta/webhook/route.ts:45-57` prüft Signatur, `:85-105` ordnet jede Nachricht über `prisma.metaRoute` einer `zielId` (Seiten-/Konto-ID) zu; **ohne Route wird verworfen** („Eine Seite ohne Wegweiser gehört uns nicht (mehr)“, `:94-108`). Routen entstehen nur in `server/actions/meta-actions.ts:204-306` (`metaVerbinden`): angemeldeter Nutzer, `requirePermission(tenantId, 'assistants:edit')` (`:214`), Seite aus der eigenen OAuth-Anmeldung (`:218-229`), dann `tenantDb.metaConnection.upsert` und `prisma.metaRoute.upsert` (`:285-303`). Erstnachricht für Messenger/Instagram wie WhatsApp (`lib/kanal/erstnachricht.ts:5-19`, `inngest/functions/meta/answer-message.ts:90ff`). Kein Admin- oder Plattform-Pfad, der eine Route ohne Kundenverbindung anlegt.

---

## Zusammenfassung – Abweichungen Vertrag/DSE/1.5 ↔ Code

1. **Widget-Rechtstext ist 1.5 Fassung 1.0, nicht 1.1** (`lib/legal/widget-legal.ts:54`): Es fehlen Stimmungs-Einordnung, Besuchsanalyse-Zusatz (Scrolltiefe, Sitzungskennung, DNT/GPC), `lymbe_ignore`-Merker und Mitarbeiter-Name in der Datenliste; STACKIT-Zusatz „EU“ fehlt.
2. **Widget sagt „Alle Empfänger verarbeiten die Daten in Deutschland“** (`widget-legal.ts:346`) – AVV 1.7 Anlage 2 und 1.5 (1.1) sagen für STACKIT „EU/EWR (vertraglich)“ bzw. „Deutschland oder der EU“. Text verspricht mehr als der Vertrag.
3. **Demo-Text 1.5 L nicht im Code**; Demo zeigt Startdialog A mit „24 Stunden“ – „lerne nichts dazu“ und „keine echten Kundendaten“ fehlen. Selbstlernen aus/Leads an ist Bot-Konfiguration, nicht an `istDemo` gekoppelt.
4. **Sprach-Hinweis K / Empfänger / Portal M** nennen „Frankfurt“ bzw. „in Deutschland“; 1.5 (1.1) sagt „in Deutschland“ bzw. „Deutschland und der EU“. Region selbst nicht im Code prüfbar.
5. **1.5 F (Bewertung)** und **C (proaktive Ansprache)** sind nicht als fester Wortlaut umgesetzt (eigener Text bzw. modellgeneriert).
6. **Latenter OpenAI-Pfad:** `lib/ai/openai-dateien.ts` + `lib/ai/rechnen.ts` laden Nutzerdateien zu `api.openai.com/v1/files`, sobald `AI_PROVIDER=openai` und kein Sandkasten – heute inaktiv, hängt nur an der Env. Gleiches gilt für `AI_PROVIDER_WERKSTATT=openai` (dokumentierter „Rückweg“).
7. **Kunde kann Startdialog und Rechtstext abschalten** (`legalEnabled`, `legalRequireConsent`); es bleibt nur das Kopf-Kennzeichen „KI“ – § 6 Abs. 2 sollte das abdecken oder der Schalter eingeschränkt werden.
8. **DNT/GPC-Respekt ist je Bot abschaltbar** (Default an); DSE 2.7 formuliert ohne Vorbehalt.
9. **Session-Cookie** hat 12 h `maxAge` (Auth.js) – DSE 6 „wird beim Schließen des Browsers gelöscht“ ist vermutlich falsch (am Browser prüfen).
10. **`agent_name_`** ist der Zufallsname des Assistenten, nicht „Name des übernehmenden Mitarbeiters“ (DSE 2.7, 1.5 B, C3).
11. **Intent-Cache** (Redis, 900 s) hält `reasoning`/`extractedFields` aus Besuchernachrichten – nirgends erwähnt; Stimmung je Nachricht gibt es nicht, nur `FRUSTRATION` + Summenauswertung (sinngemäß gedeckt).
12. Websuche (Generator, Filter, Sperrliste, Zweitprüfung, `store:false`, nur Begriff + „DE“, Nachweis 14 Tage, Abbestellen wirksam), Anbieterliste ohne Rückfall, Speech ohne Speicherung, Profilbild, Wächter, Meta-Routen: **belegt**.
