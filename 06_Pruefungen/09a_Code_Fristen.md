# Code-Gegenprüfung A – Fristen, Löschung, Sicherung

**Geprüft:** Repository `/home/claude/lymbe-ai` (Stand Commit 923f8ee, 11.10.2026), nur lesend.
**Gegen:** Kunden-AVV 1.7 § 8 Abs. 1 und 3, Anlage 1 (Verfügbarkeit); Datenschutzerklärung 1.6 Abschnitt 11; Freigabeprotokoll 5.9 (A2, A2b, A3, A4, A5, A6a, A6b, A15, A19).
**Nicht geprüft:** laufendes System, Cron-Tabellen auf dem Server, Hetzner-Einstellungen, das getrennte Repository `lymbe-ablaeufe` (Ablauf-Kern). Was nur dort steht, ist als „nicht im Code prüfbar“ markiert.

Urteile: **belegt** · **teilweise** · **nicht belegt** · **nicht im Code prüfbar**

---

## 1. Gespräche 90 Tage nach letzter Nachricht; kürzere Frist je Workspace; aktive geplante Aufgabe bleibt

**Urteil: belegt** (mit einer Präzisierung zu Christians Beleg A3)

- Vorgabe und Obergrenze 90 Tage: `lib/data-retention/policy.ts:2` `conversationDays: 90`, `policy.ts:52` `AVV_HOECHSTFRISTEN.conversationDays: 90`; `policy.ts:63-66` kappt jeden gespeicherten Wert auf die Höchstfrist (`Math.min(hoechstens, …)`).
- Frist zählt ab der **letzten Nachricht**, nicht ab `updatedAt`: `lib/data-retention/loeschregeln.ts:27-32`
  ```ts
  createdAt: { lt: cutoff },
  messages: { none: { createdAt: { gte: cutoff }, role: { not: 'system' } } },
  ```
  Interne Notizen (`role: 'system'`) verlängern nicht. Hinweis: Christians Beleg in 5.9 A3 nennt „Regel `updatedAt < 90 Tage`“ – das war der Stand bis 28.09.2026 (Kommentar `loeschregeln.ts:16-21`); der Code ist heute strenger und deckt den Vertragswortlaut „nach der letzten Nachricht“ genauer.
- Löschlauf täglich 02:00 UTC: `inngest/functions/data/cleanup-conversations.ts:366-371` (`cron: '0 2 * * *'`), je Workspace mit dessen wirksamer Frist (`cleanup-conversations.ts:388-390`). Registriert in `app/api/inngest/route.ts:78`.
- Gelöscht werden Gespräch samt Nachrichten (Cascade `prisma/tenant/schema.prisma:883`), Zusammenfassungen (Cascade `schema.prisma:845`), Übergaben (`cleanup-conversations.ts:114-116` `handover.deleteMany`), Glocken-Meldungen mit Besuchernamen (`cleanup-conversations.ts:143`).
- Live-Chat ist Teil derselben Tabelle `Conversation` (`channel`, `schema.prisma:764`), die Übergabe (`Handover`) geht mit.
- Digitaler Mitarbeiter / Frag Lymbe = interner Portal-Chat (`PortalThread`): eigene Frist `portalThreadDays: 90` (`policy.ts:14`, Höchstfrist `policy.ts:58`), Löschung `cleanup-conversations.ts:167-191`, ab letzter Nachricht (`loeschregeln.ts:74-80`). Anhänge im Objektspeicher werden mit entfernt (`cleanup-conversations.ts:183-207`).
- Kürzere Frist je Workspace: `policy.ts:128-132` Stufen 7/14/30/60/90, `policy.ts:168-186` `wirksameAufbewahrung` (eigene Wahl, nie länger als Plattform/Tarif), gespeichert über `server/actions/aufbewahrung-actions.ts:41-45,92`; der Nachtlauf liest sie über `lib/data-retention/laden.ts:103-115`.
- Aktive geplante Aufgabe bleibt: `loeschregeln.ts:86` `aufgabeAktivWhere = { aktiv: true, faelligAm: { not: null } }`, angewandt `cleanup-conversations.ts:176-177` (`id: { notIn: aufgabenThreads }`). Pausierte/erledigte Aufgaben fallen mit (Kommentar `loeschregeln.ts:66-72`) – entspricht „solange die Aufgabe aktiv ist“.

## 2. Kontakte 90 Tage nach letzter Bearbeitung; Termine 90 Tage nach dem Termin; Bewertungen mit dem Gespräch

**Urteil: belegt**

- Leads: `policy.ts:3` `leadDays: 90`; `loeschregeln.ts:35-37` `{ updatedAt: { lt: cutoff } }` („letzte Bearbeitung“); Löschung `cleanup-conversations.ts:135`.
- Termine: `policy.ts:4` `appointmentDays: 90`; `loeschregeln.ts:40-44` `OR: [{ endTime: { lt: cutoff } }, { endTime: null, startTime: { lt: cutoff } }]` – zählt ab dem Termin, künftige nie; Löschung `cleanup-conversations.ts:136`. Vor der Gesprächslöschung werden Termine entkoppelt (`cleanup-conversations.ts:106-109`), damit sie ihre eigene Frist behalten.
- Bewertungen liegen am Gespräch (`feedbackScore`, `feedbackComment`, `feedbackAt` – `prisma/tenant/schema.prisma:783-790`) und an der Nachricht (`Message.feedback`, `schema.prisma:880`, Cascade `:883`) → gehen mit dem Gespräch.
- Kürzere Wahl je Workspace für Leads und Termine gemeinsam: `policy.ts:181-183`.

## 3. Ausgeführte Abläufe im Portal 90 Tage; Schrittprotokolle im Ablauf-Kern spätestens 30 Tage

**Urteil: teilweise** (Portal belegt; 30-Tage-Grenze des Kerns nicht in diesem Repo)

- Portal-Läufe (Eingaben/Ergebnis, `PortalWorkflowRun`, `prisma/tenant/schema.prisma:245-262`): gelöscht mit der Gesprächsfrist, `cleanup-conversations.ts:144` mit `loeschregeln.ts:101-106` (offene Freigaben erst nach 31 Tagen Stillstand).
- Laufzeilen im Kern-Schema `ablaeufe.flow_run` samt Protokolldatei: `lib/data-retention/kern.ts:144-186` löscht abgeschlossene/verworfene Läufe älter als die Gesprächsfrist des Workspaces, Wartepunkte ohne Lauf (`kern.ts:191-196`) und – nur wenn die Workspace-Frist kürzer als 30 Tage ist – die Ausführungsdateien (`kern.ts:202-221`). Aufruf je Workspace `cleanup-conversations.ts:237-241, 400`.
- Die Zusage „spätestens 30 Tage“ für Schrittprotokolle hängt am Kern selbst: `kern.ts:63-78` dokumentiert `KERN_PROTOKOLL_TAGE = 30` als Spiegel von `AP_EXECUTION_DATA_RETENTION_DAYS` in `lymbe-ablaeufe/docker/docker-compose.prod.yml`; `tests/aufbewahrung-kern-sicherung.test.mts:103` prüft nur die Konstante. **Weder `docker/docker-compose.prod.yml` noch `.env.example` dieses Repos enthalten `AP_EXECUTION_DATA_RETENTION_DAYS`** (Grep ohne Treffer) – der Wert 30 ist hier nicht prüfbar.
- Einschränkung: Der Portal-Lauf löscht Kern-Dateien nur mit `"s3Key" IS NULL` (`kern.ts:183, 215`); Dateien im Objektspeicher des Kerns bleiben dem Kern überlassen. Abgerufene Daten aus verbundenen Diensten (E-Mails samt Anhängen) laufen also ausschließlich über die Kern-Frist.
- Fazit: Portal 90 Tage **belegt**; „Kern spätestens 30 Tage“ **nicht im Code prüfbar** (anderes Repository). Christians A4 nennt den Wert aus dem Kern – stimmig mit dem Kommentar, aber hier nicht nachweisbar.

## 4. Messenger-Ereignisdaten (Inngest) 30 Tage; Zugriffs-/Betriebsprotokolle 14 Tage; Fehlerprotokoll 30 Tage

**Urteil: teilweise** (Skripte belegt, Cron nicht prüfbar; Mail-Versandprotokoll 30 statt 14 Tage)

- Inngest 30 Tage: `scripts/aufbewahrung-server.sh:24` `INNGEST_TAGE=30`, löscht über `scripts/aufbewahrung-inngest.sh:57-64` die Tabellen `events`, `function_runs`, `function_finishes`, `history`, `traces`, `spans`, `trace_runs`, `event_batches`. Der tägliche Cron 04:45 steht nur als Kommentar (`aufbewahrung-server.sh:15-16`) → **Cron nicht im Code prüfbar**.
- Container-Logs 14 Tage: `aufbewahrung-server.sh:25` `LOG_TAGE=14`, Kürzung aller `*-json.log` nach Zeitstempel (`:52-68`). Caddyfile ohne `log`-Direktive (Grep `docker/caddy/Caddyfile` ohne Treffer) → Caddy schreibt nur in Container-Logs, wie A6a sagt. Keine `logging`-Begrenzung in `docker/docker-compose.prod.yml` – ohne das Skript wüchsen die Logs unbegrenzt; die Einhaltung hängt am Cron.
- Fehlerprotokoll 30 Tage: `policy.ts:19` `platformLogDays: 30`, `cleanup-conversations.ts:280` `fehlerprotokoll.deleteMany({ where: { zuletzt: { lt: protokollCutoff } } })` (ab letztem Auftreten). **Belegt.**
- **Abweichung:** Das Mail-Versandprotokoll (`MailVersand`, Empfängeradresse + Betreff, `prisma/schema.prisma:2466-2486`) wird mit `platformLogDays = 30` gelöscht (`cleanup-conversations.ts:278`). Es ist ein Betriebsprotokoll → Vertrag sagt 14 Tage. Christians A6b nennt es korrekt unter „30 Tage“, der Vertragstext ordnet es aber nicht dem Fehlerprotokoll zu.
- Sicherheitsmetadaten (IP in `AuditLog`/`UserSession`) werden nach `securityLogDays: 30` (`policy.ts:6`) nur anonymisiert, nicht gelöscht (`cleanup-conversations.ts:266-277`) – als „Zugriffsprotokoll“ wären 14 Tage zugesagt; die IP bleibt 30 Tage.

## 5. Einwilligungs-/Widerrufsnachweise 3 Jahre; Zustimmungs-/Weisungsprotokolle 3 Jahre nach Vertragsende

**Urteil: teilweise** (Chat-Nachweise belegt; Zustimmungs-/Weisungsprotokolle überleben die Löschung nach Vertragsende nicht)

- Chat-Einwilligung/Widerruf: `ConsentEvent` ohne Relation zum Gespräch (`prisma/tenant/schema.prisma:816-831`, „ohne Chatinhalt“); Frist `policy.ts:5` `consentDays: 1095` (= 3 Jahre), Höchstfrist `policy.ts:55`; Löschung `cleanup-conversations.ts:137-139`. **Belegt.**
- Zustimmungsprotokoll (`AvvZustimmung`, `prisma/schema.prisma:2587-2610`): keine eigene Frist, aber **`onDelete: Cascade` am Tenant (`schema.prisma:2607`)**. Die Workspace-Löschung entfernt die Tenant-Zeile (`lib/mandant/loeschung.ts:134`, „alles andere hängt per Cascade daran“) 30 Tage nach Vertragsende (`lib/mandant/regeln.ts:14`). Damit ist der Zustimmungsnachweis nach spätestens 30 Tagen weg – § 8 Abs. 3 und DSE 11 sagen „3 Jahre nach Vertragsende“. Kein Code, der ihn vorher kopiert (Grep `avvZustimmung`: nur Anlegen und Anzeigen). **Nicht belegt.**
- Weisungen (z. B. Websuche abbestellen) landen im Audit-Log mit `tenantId` (`server/actions/tenant-actions.ts:663-675`, Aktion `TENANT_UPDATED`). Audit-Log-Aufbewahrung: 2 Jahre allgemein, 3 Jahre nur für `TENANT_DELETED`, `USER_DELETED`, `DATA_CLEANUP` (`lib/admin/audit-domain.ts:78-80`, `inngest/functions/data/audit-aufbewahrung.ts:19-27`). Zusätzlich löscht die Workspace-Löschung **alle** Audit-Zeilen des Workspaces (`loeschung.ts:130` `auditLog.deleteMany({ where: { tenantId } })`). Weisungsprotokolle überleben das Vertragsende also nicht. **Nicht belegt.**
- Erhalten bleiben nur: der Löschnachweis `TENANT_DELETED` ohne `tenantId` (`loeschung.ts:163-188`, 3 Jahre) und `SupportZugang`/`BetriebsZugriff` (1 Jahr, `lib/support-zugang-domain.ts:29`, `cleanup-conversations.ts:281-282`; `SupportZugang` hat ebenfalls Cascade am Tenant, `schema.prisma:2635`).

## 6. Datensicherungen 7 Tage, verschlüsselt, Kopie zweiter Standort, vom Server nicht löschbar; wöchentliche Wiederherstellungsprobe

**Urteil: teilweise** („nicht löschbar“ und Cron nicht im Code; Rest belegt)

- 7 Tage: `scripts/backup-datenbanken.sh:63` `TAGE="${BACKUP_TAGE:-7}"`, Aufräumen `:249-272`; die jüngste vollständige Sicherung bleibt auch über die Frist hinaus stehen (`:244-263`) – für den Vertrag unschädlich, solange täglich eine gelingt, bei dauerhaftem Fehler aber länger als 7 Tage.
- Verschlüsselt: `scripts/backup-gpg.sh:38-42` `gpg --symmetric --cipher-algo AES256`; Dumps gehen direkt aus `pg_dump` in gpg (`backup-datenbanken.sh:106`), ebenso Objektspeicher, Mail-Zustand, .env-Dateien (`:133-208`).
- Kopie zweiter Standort: `backup-datenbanken.sh:298-319` rsync per SSH an `BACKUP_EXTERN_ZIEL` (laut Kommentar `:286-287` Storage Box Falkenstein) – nur nach fehlerfreier Nacht. Ziel-Adresse kommt aus der `.env`, **nicht im Repo prüfbar**.
- „Vom Server aus nicht löschbar“: Der Server spiegelt mit `--delete` (`:310`) und kann dort löschen; der Schutz sind laut Kommentar (`:288-290`) die täglichen Snapshots der Storage Box – eine Hetzner-Einstellung, **nicht im Code prüfbar**. Anlage 1 verspricht die Eigenschaft; der Code allein belegt sie nicht (so auch Christians A14b).
- Wöchentliche Probe: `scripts/backup-wiederherstellen-probe.sh` entschlüsselt, spielt in `lymbe_restore_probe` zurück, zählt Tabellen (`:66-94`), meldet in `Sicherungsstand` (`:36-47`). Nur mit `lymbe_tenant_demo` (`:22`). „Sonntags 04:30“ steht nur als Cron-Hinweis in A15 → **Cron nicht im Code prüfbar**; die Betriebsprüfung meldet eine ausbleibende Probe nach 8 Tagen (`lib/betrieb/sicherung.ts:22, 90-110`) und eine ausbleibende Sicherung nach 26 Stunden (`:20, 58-87`), Kopie außerhalb nach 26 Stunden (`:118-144`).
- Hetzner-Server-Abbilder (A2b): nichts im Code → **nicht im Code prüfbar**.

## 7. Löschung nach Vertragsende innerhalb 30 Tagen (DB, Qdrant, MinIO, Inngest, Cache); Demo 24 Stunden

**Urteil: teilweise** (Inngest nicht je Mandant, Redis nicht je Mandant – beide laufen über Fristen aus; Rest belegt)

- 30 Tage: `lib/mandant/regeln.ts:14` `VERTRAGSENDE_LOESCHEN_TAGE = 30`, Stichtag nach Berliner Kalendertag (`regeln.ts:51-53`), Lauf täglich 05:15 UTC `inngest/functions/data/vertragsende.ts:219`, Vorwarnung 7 Tage vorher (`regeln.ts:16`). Schalter `LOESCHUNG_NACH_VERTRAGSENDE=aus` setzt den Lauf auf „nur zählen“ (`vertragsende.ts:204-206`) – ob er in Produktion aus ist, ist **nicht im Code prüfbar**.
- Reihenfolge `lib/mandant/loeschablauf.ts:137-264`: Abos (`:165-184`), Aufgaben-Verzeichnis (`:187`), **Qdrant** nach Präfix `tenant_<id>_` (`:190`, `loeschung.ts:103-114`), **MinIO**-Ordner `tenants/<id>/`, `assistenten-bilder/<id>/`, `support-pages/<id>/` (`:191-193`, `regeln.ts:182-184`), **Ablauf-Kern** (`:196`), **Mandanten-DB samt Rolle** (`:201-205`), Ordner zweiter Durchgang (`:213-215`), zentrale Zeile (`:226`), Konten (`:230-248`), Nachweis + Mail (`:251-262`).
- **Inngest:** kein Schritt je Mandant; Ereignisse laufen über die 30-Tage-Frist aus Punkt 4 aus. Ergibt rechnerisch bis zu 30 Tage nach der Workspace-Löschung, also bis zu 60 Tage nach Vertragsende für Ereignisdaten – A19 sagt „innerhalb der Frist aus § 8 Abs. 3“, das stimmt nur, wenn man die 30 Tage ab Vertragsende und nicht ab Workspace-Löschung zählt; Ereignisse, die in den letzten 30 Tagen des Vertrags entstanden, liegen länger. Geringfügig, aber nicht exakt belegt.
- **Cache:** `cacheLeeren` ist nur der prozessinterne Tarif-Cache (`loeschung.ts:200` → `lib/cache/tenant-plan-cache.ts:30-32`, 60 s). Redis-Schlüssel des Mandanten (Antwort-Cache, Analytics-Puffer, Kontingente) werden nicht gezielt gelöscht; sie laufen über TTL aus (Punkt 9). Längste gefundene TTL mit Mandantenbezug: `analytics:last:<botId>` 30 Tage (`lib/analytics/buffer.ts:90`) – ohne Personendaten.
- Datensicherungen: 7 Tage eigene + 7 Tage Abbilder = 44 Tage nach Vertragsende, stimmig zu § 8 Abs. 3.
- **Demo 24 Stunden:** `policy.ts:197-202` `DEMO_TAGE = 1` für Gespräche, Leads, Termine (`mitDemoFrist`), angewandt in `laden.ts:77`; stündlicher Lauf `cleanup-conversations.ts:502-537` (`cron: '20 * * * *'`), Kommentar `:499` „höchstens 25 Stunden“. Interne Chats des Demo-Workspace behalten die normale Frist (`policy.ts:194-195`). **Belegt.**

## 8. Jeder Löschlauf schreibt eine Protokollzeile; Betriebsprüfung meldet ausbleibende Läufe

**Urteil: belegt** (für den Gesprächs-Löschlauf; andere Löschläufe ohne Zeile)

- `laufProtokollieren` (`cleanup-conversations.ts:324-364`) schreibt je Lauf eine Zeile `LoeschLauf` (`art`, `beginn`, `fehlerfrei`, `workspaces`, `zahlen`, `fehler`; Modell `prisma/schema.prisma:2667-2681`) und für Nacht- und Hand-Läufe zusätzlich `DATA_CLEANUP` ins Audit-Log mit `actorId: null` (`:352-363`) – die Korrektur aus A3 (Fremdschlüssel `'system'`). Aufgerufen in allen drei Funktionen (`:410-422`, `:479-491`, `:532-534`); der Demo-Lauf schreibt nur, wenn es Demo-Workspaces gibt (`:515`).
- Betriebsprüfung: `lib/betrieb/pruefungen.ts:134-147` liest den letzten Lauf `nacht`/`hand`; `lib/betrieb/loeschlauf.ts:14-36` meldet „ausgeblieben“ nach 26 Stunden und „mit Fehlern“ bei `fehlerfrei = false`. Eingehängt in `alleBefunde` (`pruefungen.ts:168`).
- Nur Zahlen, keine Inhalte (`zahlen` = Zählwerte je Workspace, `:335`).
- **Lücke:** Die übrigen Löschläufe schreiben keine `LoeschLauf`-Zeile und werden nicht überwacht: Vertragsende (`vertragsende.ts`, nur Audit-Nachweis je gelöschtem Workspace + Mail bei Problemen), Audit-Aufbewahrung (`audit-aufbewahrung.ts`, nur Logger), Analytics-Ereignisse (`cleanup-events.ts`, nur Logger), Server-Skript Inngest/Logs (nur Logdatei). Die Zusage in A3 bezieht sich auf den Gesprächs-Löschlauf – dort erfüllt.

## 9. Redis-Antwort-Cache mit Ablauf; IP in Redis höchstens 24 h

**Urteil: belegt**

- Antwort-Cache: `lib/ai/answer-cache.ts:29` `DEFAULT_TTL_SECONDS = 3600`, Schreiben `:55-63` über `cacheSet` → `lib/redis.ts:64` `redis.set(key, …, 'EX', ttlSeconds)`. `ANSWER_CACHE_TTL_SECONDS=0` schaltet aus (`:28, :43, :57`). Absichts-Cache 900 s (`lib/ai/intent-classifier.ts:116`).
- IP-Schlüssel: Ratenbegrenzung `lib/rate-limit.ts:371-389` `expire(key, fensterSekunden + 1)`, längstes Fenster 3600 s (`:133, :191, :250, :253`); Spam-Schutz `lib/limits/spam-guard.ts:247` Tageszähler `incrWithExpire(visitorDayKey, 86_400)` – Schlüssel mit IP (`lib/limits/spam-domain.ts:30-35`), **24 h** ist die längste gefundene IP-TTL; Verstoßzähler 3600 s (`spam-guard.ts:106`), Anmelde-Sperre je IP 900 s (`rate-limit.ts:176`). Analytics speichert statt der IP einen täglich rotierenden Hash (`prisma/tenant/schema.prisma:1298`, Salz 48 h `lib/analytics/visitor.ts:20`).
- Kein Redis-`set` ohne TTL mit Personenbezug gefunden (Grep über `redis.set|incr|sadd|zadd`); `analytics:pending` (`buffer.ts:84`) enthält nur Workspace-Slugs.

## 10. Speicherorte mit Personendaten ohne Frist bzw. nicht in AVV § 8 genannt

| Speicherort | Datei | Personendaten | Frist im Code | In § 8 genannt? |
|---|---|---|---|---|
| Audit-Log (zentral) | `prisma/schema.prisma:110-134`, `lib/admin/audit-domain.ts:78-80`, `inngest/functions/data/audit-aufbewahrung.ts` | `actorEmail`, `ipAddress`, `userAgent`, Details | 2 Jahre; Löschnachweise 3 Jahre; IP nach 30 Tagen genullt; je Workspace bei Löschung sofort | **nein** (nur „Protokolle über Vertragsabschluss, Fassungen und Weisungen 3 Jahre“ – die werden tatsächlich nach 2 Jahren bzw. mit dem Workspace gelöscht) |
| Widget-Analyse-Ereignisse `/api/widget/{bot}/events` | `prisma/tenant/schema.prisma:1285-1310`, `inngest/functions/analytics/cleanup-events.ts:47-61` | Seitenadresse, Referrer, Land, Gerät, rotierender `visitorHash` (keine Roh-IP) | tarifabhängig `PlanLimits.analyticsRetentionDays`, Vorgabe 30, laut Kommentar bis 180 Tage; **nur für Workspaces ACTIVE/TRIAL** (`:30`) | **nein** (DSE Abschnitt 11 nennt sie nicht; DSE 1.3/C2 beschreibt sie als „ohne Personenbezug“) |
| Analytics-Tagesaggregate | `cleanup-events.ts:18, 62-68` | aggregiert, kein Personenbezug | 24 Monate | nein |
| Support-Zugriffsprotokoll `SupportZugang`/`SupportAufruf` | `prisma/schema.prisma:2618-2639, 2684-2692`, `lib/support-zugang-domain.ts:29` | Name/E-Mail des Lymbe-Personals, IP, Grund | 365 Tage; Cascade mit Tenant | **nein** |
| Betriebszugriffe `BetriebsZugriff` | `prisma/schema.prisma:2646-2661`, `cleanup-conversations.ts:282` | Person, Grund, Befehl | 365 Tage | nein |
| Löschlauf-Protokoll `LoeschLauf` | `schema.prisma:2667-2681`, `cleanup-conversations.ts:284` | nur Zahlen | 365 Tage | nein (unschädlich) |
| Mail-Versandprotokoll `MailVersand` | `schema.prisma:2466-2486`, `cleanup-conversations.ts:278` | Empfängeradresse (auch Besucher), Betreff | 30 Tage | nur als „Betriebsprotokoll 14 Tage“ → **Abweichung** |
| Übergaben `Handover` | `prisma/tenant/schema.prisma:1132-1152`, `cleanup-conversations.ts:114-116` | Grund, zugewiesene Person | mit dem Gespräch (90) | implizit („Live-Chat“) – in Ordnung |
| Glocken-Meldungen `Notification` | `prisma/tenant/schema.prisma:1445-1457`, `cleanup-conversations.ts:143` | Besuchername/-anliegen im Text | Gesprächsfrist (90) | nein, aber gleiche Frist |
| Wissensvorschläge `KnowledgeSuggestion` | `prisma/tenant/schema.prisma:1000-1029` | `triggerQuestion` (Besucherfrage, „PII-gefiltert“) | **keine**; wird beim Gesprächslöschen nur entkoppelt (`cleanup-conversations.ts:110-113`) | **nein** |
| Datenauskunfts-Anfragen `DataRequest` | `prisma/tenant/schema.prisma:1474-1486` | `email`, `reason` | **keine** (kein `deleteMany` gefunden) | **nein** |
| Websuche-Nachweis `WebsucheNachweis` | `prisma/tenant/schema.prisma:1949`, `lib/ai/suchbegriff/anweisung.ts:37`, `cleanup-conversations.ts:158-163` | `userId`, gesendeter Suchbegriff | 14 Tage fest | nein (§ 3 Abs. 10 „regelmäßige Prüfung“; Kommentar `:153-155` behauptet „so steht es im AVV“ – in § 8 steht es nicht) |
| Support-Threads Portal `SupportThread`/`SupportMessage` | `prisma/schema.prisma:647-682` | Text, Absender | **keine** (Cascade mit Tenant) | nein; DSE 11 nennt „Supportanfragen per E-Mail max. 6 Monate“ – im Code nicht umgesetzt |
| Staff-Webmail `EmailMessage` (zentral) | `schema.prisma:751+` | E-Mail-Inhalte | **keine** zeitliche Frist (nur manuelles Löschen `server/actions/email-mailbox-actions.ts:536`) | nein |
| Sitzungen `UserSession` | `schema.prisma:1550-1569`, `cleanup-conversations.ts:270-277` | IP, Standort, Gerät | IP/Standort nach 30 Tagen genullt; Zeile bleibt bis Kontolöschung | nein („Zugriffsprotokoll 14 Tage“ wäre die nächste Kategorie) |
| Portal-Gedächtnis `PortalUserMemory`, Ablauf-Werkstatt-Verlauf `AblaufWerkstattVerlauf`, Aufgaben-Läufe `PortalAufgabeLauf` | `prisma/tenant/schema.prisma:520, 267-273, 318-333` | Mitarbeiterinhalte | keine / mit Aufgabe (Cascade) | Gedächtnis: „bis Löschung durch Kunden“ ✓; Werkstatt-Verlauf nicht genannt |

---

## Zusammenfassung – Abweichungen zwischen Vertrag und Code

1. **Zustimmungs- und Weisungsprotokolle (§ 8 Abs. 3, DSE 11 „3 Jahre nach Vertragsende“):** `AvvZustimmung` hat `onDelete: Cascade` am Tenant (`prisma/schema.prisma:2607`), die Workspace-Löschung entfernt zudem alle Audit-Zeilen des Workspaces (`lib/mandant/loeschung.ts:130`). Beides ist 30 Tage nach Vertragsende weg. **Nicht belegt – größte Abweichung.**
2. **Audit-Log allgemein 2 Jahre** (`audit-domain.ts:78`), nur Löschnachweise 3 Jahre; Weisungen (`TENANT_UPDATED`) fallen unter 2 Jahre.
3. **Mail-Versandprotokoll 30 Tage** (`platformLogDays`) statt „Betriebsprotokolle 14 Tage“; IP in `AuditLog`/`UserSession` 30 statt 14 Tage.
4. **Ablauf-Kern „spätestens 30 Tage“** nur als Konstante gespiegelt; `AP_EXECUTION_DATA_RETENTION_DAYS` liegt im fremden Repo `lymbe-ablaeufe`, hier nicht prüfbar. Kern-Dateien mit `s3Key` löscht das Portal nicht.
5. **Inngest** wird bei Vertragsende nicht je Mandant gelöscht; Ereignisse der letzten Vertragstage können bis ~60 Tage nach Vertragsende liegen (A19 nennt es, rechnet aber knapp).
6. **Redis** wird bei Vertragsende nicht je Mandant geleert; nur TTL (bis 30 Tage, ohne Personendaten).
7. **„Vom Server nicht löschbar“** (Anlage 1): rsync `--delete`; Schutz nur durch Hetzner-Snapshots – außerhalb des Codes. Cron-Zeiten für Sicherung, Probe und Server-Aufbewahrung sind Kommentare, nicht prüfbar.
8. **Ohne Frist und nicht im Vertrag:** `KnowledgeSuggestion.triggerQuestion`, `DataRequest`, `SupportThread`/`SupportMessage` (DSE sagt 6 Monate), Staff-`EmailMessage`.
9. **Widget-Analyse-Ereignisse** tarifabhängig bis 180 Tage, nur für aktive Workspaces bereinigt, nicht in § 8 oder DSE 11 genannt (pseudonym, kein Roh-IP).
10. Nur der Gesprächs-Löschlauf schreibt `LoeschLauf` und wird überwacht; Vertragsende-, Audit-, Analytics- und Server-Läufe nicht.
11. Christians Beleg A3 („`updatedAt < 90 Tage`“) ist veraltet – der Code zählt seit 28.09.2026 ab der letzten Nachricht (`loeschregeln.ts:27-32`), was dem Vertrag genauer entspricht.
12. Positiv belegt: 90/90/90-Fristen mit Kundenwahl, aktive Aufgabe bleibt, Bewertungen mit Gespräch, Einwilligungsnachweise 3 Jahre, Fehlerprotokoll 30 Tage, Inngest-/Log-Skripte 30/14 Tage, Sicherung 7 Tage AES-256 mit Kopie und Probe, Löschablauf DB/Qdrant/MinIO/Kern, Demo 24 h, Redis-TTLs ≤ 24 h für IP.
