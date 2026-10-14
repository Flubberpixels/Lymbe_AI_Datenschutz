# Gegenprüfung B – Zugriff, Protokoll, Mandantentrennung (nur lesend im Code)

**Repo:** `/home/claude/lymbe-ai`, Arbeitsstand Commit `923f8ee` (flache Kopie, nur ein Commit sichtbar – `git show 3d97dfd` nicht möglich; die Schwärzung ist aber im Code vorhanden, siehe Punkt 11).
**Verträge:** AVV 1.7 (§ 3 Abs. 1 und 5, § 5 Abs. 4, § 8 Abs. 4, § 12 Abs. 5/6, Anlage 1), DSE 1.6 Abschnitt 10. Freigabeprotokoll 5.9 (A7, A8, A9, A14, A16, A17, A18, A20, A21, B5–B8).
**Methode:** Read/Grep/Glob, keine Skripte, keine Datenbank, kein Deploy. Was nur am laufenden System messbar ist, steht als „nicht im Code prüfbar“.

---

## 1. Selbstlernen: Auslieferungszustand aus, Einschalten protokolliert (AVV § 2 Abs. 1, § 3 Abs. 1 · A7)

**Urteil: belegt (Auslieferungszustand) · teilweise (Protokoll)**

Auslieferungszustand aus – an vier Stellen:
- `prisma/tenant/schema.prisma:592` – `selfLearningMode SelfLearningMode @default(DISABLED)`
- `lib/db/provisioning.ts:188` – `"selfLearningMode" "SelfLearningMode" NOT NULL DEFAULT 'DISABLED'` (Neuanlage einer Mandanten-DB)
- `server/actions/bot-actions.ts:85` – `selfLearningMode: z.enum([...]).default('DISABLED')` (Server-Validierung)
- `components/platform/bot-config/defaultConfig.ts:65` – `selfLearningMode: 'DISABLED'` (Formular)
- Wirksamkeit: `app/api/widget/[botId]/chat/route.ts:1551-1552` – `const selfLearningMode = botCfg?.selfLearningMode || 'DISABLED'; if (selfLearningMode !== 'DISABLED' …)` und `inngest/functions/knowledge/generate-suggestion.ts:123` – `if (!config || config.selfLearningMode === 'DISABLED')` → keine Vorschläge.

Protokoll beim Speichern:
- `server/actions/bot-actions.ts:1134-1146` – `action: 'BOT_UPDATED', resource: 'Bot', resourceId: botId, details: { botName, changes: validated }` mit `actorId: session.user.id, actorRole`; `createdAt @default(now())` (`prisma/schema.prisma:125`). `validated` enthält `selfLearningMode` (Zeile 1065).

Was fehlt:
- Kein eigener Eintrag „Selbstlernen eingeschaltet“, kein Vorher/Nachher – das Einschalten ist nur durch Vergleich zweier `BOT_UPDATED`-Zeilen erkennbar (so auch A7 vermerkt).
- `BOT_UPDATED` in `bot-actions.ts:1134` setzt **kein `tenantId`** (im Gegensatz zu `BOT_CREATED`, das es nur in `details` ablegt, Zeile 608). Das Modell hat die Spalte (`prisma/schema.prisma:112`). Eine Auswertung „alle Weisungen dieses Mandanten“ findet die Zeile nur über `resourceId`.
- Der Eintrag ist für den Kunden nicht sichtbar: Einstellungen → Datenschutz zeigt nur `SupportZugang`/`BetriebsZugriff` (`server/actions/support-zugang-actions.ts:95-137`), das Audit-Log ist Admin-intern (`app/admin/audit-logs`). AVV § 3 Abs. 1 verlangt nur Protokollierung, nicht Sichtbarkeit – kein Verstoß, aber Hinweis.
- Aufbewahrung Audit-Log: 2 Jahre, Nachweise 3 Jahre (`inngest/functions/data/audit-aufbewahrung.ts:6-26`) – passt zu § 8 Abs. 3 (Weisungen 3 Jahre) nur, wenn `BOT_UPDATED` unter `NACHWEIS_AKTIONEN` fällt; nicht geprüft, ob es dort steht (lib/admin/audit-domain.ts nicht Teil dieser Prüfung).

## 2. Portal-Einstellungen protokolliert: Websuche, Benachrichtigungsziele, Dienst verbinden (AVV § 3 Abs. 1 · A8)

**Urteil: teilweise – deckt sich mit A8 (❌ im Protokoll)**

Schreibt ins Audit-Log:
- Websuche abbestellen (Admin): `server/actions/tenant-actions.ts:663-675` – `action: 'TENANT_UPDATED', tenantId, details: { websucheAbbestellt: abbestellen }`, mit `actorEmail`. Nur durch Lymbe-Personal (`requireRole(['SUPERADMIN','PLATFORM_ADMIN'])`, Zeile 654) – Umsetzung einer Textform-Weisung, keine Kundeneinstellung.
- Selbstlernen: siehe Punkt 1.
- Workspace-Webhooks: `server/actions/webhook-actions.ts:64-78` – `WEBHOOK_CREATED` mit `tenantId`, `url`, `events` (weitere Einträge Zeile 161, 213).
- API-Schlüssel: `server/actions/api-key-actions.ts:54, 166`.
- Dokumente/Wissensquellen: `server/actions/knowledge-actions.ts:383` ff. (`DOCUMENT_UPLOADED` mit `tenantId`).

Schreibt **nicht** ins Audit-Log (0 Treffer auf `auditLog` in der Datei):
- Benachrichtigungsziele (E-Mail, Slack, Teams, Webhook je Assistent): `server/actions/integration-actions.ts:57-84` `createIntegration` → nur `tenantDb.botIntegration.create(...)`; ebenso `updateIntegration` (86-120) und `deleteIntegration` (122). Das Modell `BotIntegration` hat nur `createdAt/updatedAt`, **keine Person** (`prisma/tenant/schema.prisma:1086-1111`).
- Kalender verbinden: `server/actions/calendar-actions.ts:418` `integrationCredential.upsert` – Modell ohne Person (`prisma/tenant/schema.prisma:1189-1210`).
- Shops: `server/actions/shop-actions.ts:275, 338, 455` – `ShopConnection`/`BotShopBinding` ohne Person (`prisma/tenant/schema.prisma:1885-1916`).
- WhatsApp: `server/actions/whatsapp-actions.ts:231, 243`; Meta: `server/actions/meta-actions.ts:287, 299` – keine Audit-Zeile.
- Postfächer: `server/actions/email-mailbox-actions.ts` – keine Audit-Zeile (betrifft Personal-Postfächer, s. u.).
- Verbindungen in den Abläufen liegen im Kern (`AP_*`), nicht in diesem Repo – nicht im Code prüfbar.

Folge: Für diese Weisungen ist der Zeitpunkt (createdAt) belegt, der Nutzer nicht. AVV § 3 Abs. 1 Satz 3 („mit Zeitpunkt **und Nutzer** protokolliert“) ist für Benachrichtigungsziele und das Verbinden von Diensten nicht erfüllt.

## 3. Support-Zugriff, Admin-Einsicht, Zugriffsprotokoll für den Kunden (AVV § 3 Abs. 5, Anlage 1 · A9, B5)

**Urteil: belegt (Zugang, Protokoll, Kundensicht, 365 Tage) · teilweise (Lückenlosigkeit „jede Seite“, Admin-Wege) · Vier-Augen-Freigabe nicht im Code (organisatorisch, wie B5 sagt)**

Tor für Plattform-Personal:
- `lib/support-zugang.ts:48-61` `personalDarf(...)`: ohne laufenden `SupportZugang` → `null`; `schreiben` verlangt `umfang === 'bearbeiten'`. Ausnahme nur der Vorlagen-Workspace von Lymbe (`istVorlagenWerkstatt`, Zeile 39-56).
- Angebunden an die zentrale Rechteauflösung: `lib/tenant-permissions.ts:179-183` – `const zugang = … personalDarf(...)`; `if (!isOwner && !isPlatformStaff && !member) return null;` – und „nur ansehen“ wird zu Nur-Lesen (`nurAnsehen`, Zeile 204, 212). Weitere Tore: `lib/tenant.ts:72, 252, 319`, `lib/auth-helpers.ts:15, 52`.
- Öffnen mit Grund (10–500 Zeichen), Umfang, Dauer 30/120/480 min: `lib/support-zugang-domain.ts:22-49`; Zeile schreibt `userId, userName, userEmail, grund, umfang, beginn, endetAm, ip` (`server/actions/support-zugang-actions.ts:39-51`).
- Seitenprotokoll: `supportAufrufVermerken` (`support-zugang-actions.ts:70-82`) – nur Pfad ohne Query (`protokollPfad`, Domain Zeile 60-64), Dedupe 60 s. Aufgerufen aus `components/platform/SupportZugangLeiste.tsx:27-30` (Client-`useEffect` bei Pfadwechsel); die Leiste wird im Layout nur bei laufendem Zugang gerendert (`app/[tenantSlug]/layout.tsx:84-85, 251-256`).
- Admin-Einsicht: `lib/betrieb/einsicht.ts:14-28` schreibt `BetriebsZugriff` `art: 'admin'`, Dedupe 30 min, „Ohne Protokoll keine Einsicht: scheitert die Zeile, wirft die Funktion“ (kein try/catch um `create`). Aufrufer: `admin-tenant-bot-actions.ts:33, 76` (Liste/Assistent samt Konfiguration), `admin-tenant-team-actions.ts:37`, `admin-tenant-activity-actions.ts:27`, `tenant-actions.ts:379` (Stammdaten/Abo), `support-actions.ts:390` (Ticket), `admin-vorlagen-actions.ts:138, 162`.
- Live-Log: `app/api/live-log/stream/route.ts:28-33` → `BetriebsZugriff art 'live-log'` (ohne tenantId, da workspace-übergreifend).
- Datenbank/Container: `scripts/zugriff.sh:38-39` erzwingt `--person` und Grund ≥ 10 Zeichen, Zeile 82 `insert into "BetriebsZugriff" (id, art, person, grund, "tenantId", befehl)`.
- Kundensicht: `app/[tenantSlug]/settings/privacy/page.tsx:105` `<SupportZugriffListe zeilen={await ladeSupportZugriffe(tenant.id)} />`; `ladeSupportZugriffe` (`support-zugang-actions.ts:140-143`) verlangt `settings:data_export` und liefert Support-Zugänge **und** `BetriebsZugriff` des Workspace ohne den Befehl (Zeile 103-110: „ohne den Befehl selbst, der bleibt bei Lymbe“).
- 365 Tage: `SUPPORT_AUFBEWAHRUNG_TAGE = 365` (`lib/support-zugang-domain.ts:29`), Löschung `inngest/functions/data/cleanup-conversations.ts:264, 281-282` (`supportZugang.deleteMany`, `betriebsZugriff.deleteMany` älter als Cutoff); Test `tests/support-zugang.test.mts:53`.

Lücken / Admin-Wege am Support-Zugang vorbei:
- **„Jede Seite protokolliert“ hängt am Browser-JavaScript** (`useEffect` in der Leiste, Fehler werden verschluckt: `.catch(() => {})`). Server Actions und API-Routen, die Personal mit laufendem Zugang direkt aufruft (ohne Seitenwechsel), erzeugen keinen `SupportAufruf`. Der Zugang selbst (Grund, Umfang, Frist) ist serverseitig protokolliert – die Seitenliste ist Beiwerk, nicht Beweis.
- **`updateTenantBotForAdmin`** (`server/actions/admin-tenant-bot-actions.ts:122-208`): Personal (`requireRole(['SUPERADMIN','PLATFORM_ADMIN'])`, Zeile 132) ändert Name, Systemprompt, Tonalität, Rückfalltext eines Kunden-Assistenten **ohne Support-Zugang**. Protokoll nur im zentralen Audit-Log (`BOT_UPDATED`, `via: 'admin_override'`, Zeile 189-205) mit `.catch(...)` – scheitert die Audit-Zeile, geht die Änderung trotzdem durch (Zeile 206-208). Nicht in `BetriebsZugriff`, also für den Kunden unter Datenschutz **unsichtbar**. Das ist Schreibzugriff auf Kundeninhalte (Systemprompt) außerhalb des § 3-Abs.-5-Wegs.
- **Lesen von Assistent samt Konfiguration** (`getTenantBotForAdmin`, Zeile 74-105, inkl. `config: true` = Systemprompt, Dokumentnamen) braucht ebenfalls keinen Support-Zugang, ist aber als Admin-Einsicht protokolliert und für den Kunden sichtbar (`art 'admin'` → „Einsicht (Admin-Bereich)“, `support-zugang-actions.ts:117`). Mit Grund/Umfang im Sinne des Vertrags ist dort nur die feste Zeile „Einsicht im Admin-Bereich: …“ – kein individueller Grund, keine Freigabe.
- **Sicherungs-Download** (`app/api/sicherung/download/route.ts:22-60`): Superadmin lädt die verschlüsselte Gesamtsicherung (alle Mandanten) herunter; Protokoll nur `auditLog` (Zeile 60 ff.), nicht in `BetriebsZugriff` → für Kunden unsichtbar. Vertraglich ist das Zugriff auf Inhalte aller Mandanten.
- **Support-Ticket-Stream** `app/api/support/customer/stream/route.ts:36-37`: Staff (auch Rolle SUPPORT) liest Ticket-Threads ohne Zugang; das sind Supportnachrichten an Lymbe, keine Mandanteninhalte – vertretbar.
- **E-Mail-Anhänge** `app/api/email/attachments/[id]/download/route.ts:29-32` (`user.role !== 'SUPERADMIN'`): betrifft Personal-Postfächer (`EmailAccount` ohne `tenantId`, `prisma/schema.prisma:703-719`), keine Kundendaten.
- Vier-Augen-Prinzip (§ 3 Abs. 5 Satz 2): technisch nicht vorhanden; `supportZugangOeffnen` legt den Zugang sofort an (`support-zugang-actions.ts:34-52`). Wie B5 sagt: organisatorisch über Register 5.15 – **nicht im Code prüfbar**.
- Aufbewahrung des zentralen Audit-Logs (2 Jahre) ≠ 365 Tage der Support-Tabellen – zwei Fristen für „Zugriffsprotokoll“; der AVV nennt in § 8 Abs. 1 „Zugriffs- und Betriebsprotokolle 14 Tage“ (Server-Logs) und in § 8 Abs. 3 „Protokolle über … Weisungen drei Jahre“ – die 365 Tage der Support-Zugriffe stehen in keinem Vertragstext (Hinweis, kein Widerspruch).

## 4. Mandantentrennung (Anlage 1, DSE 10 · A16)

**Urteil: belegt (DB, Qdrant, MinIO, Tests) · teilweise (Redis-Präfix, „zentraler Wrapper aus der Sitzung“)**

- Eigene Postgres-DB je Workspace: `prisma/schema.prisma:2080-2095` `model TenantDatabaseConfig { tenantId @unique, host, dbName @unique, username, encryptedPassword … }`; Auflösung `lib/db/tenant.ts:125-143` (`resolveTenantDbName`), Verbindungspool je `tenantId` (`getTenantDb`, Zeile 42-60); Fallback-Namen `lymbe_tenant_<slug>` (Zeile 149).
- Qdrant je Workspace **und** Assistent: `lib/rag/collection-name.ts:25-28` `tenant_${tenantId}_bot_${botId}` (+ `__<space>` bei neuem Embedding-Raum).
- MinIO-Präfix: `lib/storage/minio.ts:269, 280` `tenants/${tenantId}/…`; Portal-Chat-Anhänge `lib/portal-chat/attachment-domain.ts:328`; Erscheinungsbild `lib/erscheinungsbild/storage.ts:19-20`; Löschregel `lib/mandant/regeln.ts:183` (`tenants/`, `assistenten-bilder/`, `support-pages/` je tenantId). Ein Bucket, Ordner je Workspace (wie A16).
- Redis: nur teilweise mandantenpräfixiert – `live:tenant:${tenantId}` (`lib/live-chat/redis-pubsub.ts:70`), `tenant-plan-structure:${tenantId}` (`lib/cache/tenant-plan-cache.ts:28`). Andere Schlüssel laufen über Bot-/Gesprächs-IDs (`analytics:badorigin:${botId}`, `kanal:offline:${conversationId}`, `proactive:lock:…`, `oauth:state:…`) – weltweit eindeutige IDs, aber kein Mandanten-Präfix. Deckt sich mit „bewusst offen“ in A16.
- Zentraler Wrapper: Es gibt **keinen** Wrapper, der die Mandanten-ID aus der Sitzung ableitet. Muster ist stattdessen: `tenantId` kommt vom Aufrufer (Parameter der Server Action oder `?tenantId=` / `body.tenantId` in API-Routen) und wird serverseitig gegen die Sitzung geprüft (`requirePermission`/`requireEinsicht`/`getTenantActor` → `tenantActorFuer`, `lib/tenant-permissions.ts:172-183`; `requirePortalChatActor`, `lib/portal-chat/access.ts:56-90`; `resolveAgentContext`, `verifyTenantAccess`). Stichprobe aller 31 API-Routen, die `tenantId`/`tenantSlug` aus Query oder Body lesen: jede hat eine Zugehörigkeitsprüfung (`checkPermission`, `verifyTenantAccess`, `glockenWorkspace`, `getTenantActor`, `requirePortalChatActor`, `requireAllPermissions` in `app/api/portal/gespraeche/[id]/pdf/route.ts:28`, `requireSpracheActor` in `app/api/portal/sprache/route.ts:25`, `pruefeProfilAenderung` in `app/api/users/[userId]/avatar/route.ts:139, 190`, Owner/Admin-Abfrage in `app/api/billing/desktop-app/checkout/route.ts:28-44`); Webhooks (`calcom`, `calendly`) prüfen Signatur; `app/api/widget/[botId]/live/stream/route.ts:59-100` verifiziert `tenantId` gegen `botId` + `sessionId`. Absicherung ist also dezentral, aber vollständig in der Stichprobe; `tests/action-audit.test.mts` verlangt für jede Server Action einen Wächter aus `WAECHTER` (Zeile 24-45).
- Test „Mandant B sieht nichts von A“: `tests/mandantentrennung-a30.test.mts` (M1 fremde MinIO-Pfade, M2 Glocke, M3 Desktop-App 410, L1–L5). Es sind Quelltext-Regex-Tests, keine Laufzeittests gegen zwei Mandanten-DBs.

## 5. Zugangsdaten verbundener Dienste AES-256-GCM (AVV § 5 Abs. 4, Anlage 1, DSE 10 · A17)

**Urteil: belegt · Klartext-Geheimnisse wie in A17 benannt, plus zwei weitere**

- `lib/encryption.ts:8` `const ALGORITHM = 'aes-256-gcm'`, Schlüssel 32 Byte aus `ENCRYPTION_KEY` (Zeile 13-22), `encrypt`/`decrypt` (31, 46).
- Verwendet für: Kalender (`lib/calendar-connectors/factory.ts:35-51` → `IntegrationCredential.encryptedCredentials`), Shops (`lib/shop-connectors/factory.ts`, `shopify-persist.ts`, `server/actions/shop-actions.ts`), WhatsApp (`whatsapp-actions.ts`, Modell `encryptedCredentials` `prisma/tenant/schema.prisma:1784`), Meta (`meta-actions.ts`, Modell ab 1844), API-Datenquellen inkl. Header (`lib/documents/api-quelle.ts:72-76`), Mandanten-DB-Passwort (`lib/db/provisioning.ts`, `TenantDatabaseConfig.encryptedPassword`), Desktop-App-Gerätetoken (`prisma/schema.prisma:1753`).
- Abläufe-Kern: eigener Schlüssel `AP_ENCRYPTION_KEY` (nur in `scripts/backup-datenbanken.sh` referenziert) – **nicht im Code prüfbar** (Kern nicht im Repo).

Im Klartext:
- Signatur-Geheimnisse ausgehender Webhooks: `server/actions/webhook-actions.ts:53` `const secret = \`whsec_${nanoid(32)}\`` → `Webhook.secret String` (`prisma/tenant/schema.prisma:1465`, zentral `prisma/schema.prisma:332`); `BotWebhook.secret` (`prisma/tenant/schema.prisma:745`). Wie A17 vermerkt.
- Benachrichtigungsziele: Slack-/Teams-Webhook-URLs (die URL **ist** das Geheimnis) in `BotIntegration.target String` (`prisma/tenant/schema.prisma:1094`) – nicht in A17 genannt. Sie sind „Zugangsdaten eines verbundenen Dienstes“ im Sinne von § 5 Abs. 1/4 (Benachrichtigungsziele sind dort ausdrücklich aufgezählt).
- TOTP-Geheimnis der Nutzer: `User.twoFactorSecret String?` (`prisma/schema.prisma:1435`), gespeichert als Base32 (`server/services/totp-service.ts:74`); Prisma-`omit` verhindert nur das versehentliche Mitlesen (`lib/db/central.ts:19`). Betrifft Konten, nicht verbundene Dienste – Hinweis.
- OAuth-Tokens der Anmeldung (Google/GitHub) in `Account.access_token/refresh_token/id_token` (`prisma/schema.prisma:12-22`) – Konto-Login, vom AVV ausgenommen (§ 1 Abs. 2); Hinweis für die DSE.

## 6. Export im Portal (AVV § 8 Abs. 4 · A18)

**Urteil: nicht belegt – Vertrag verspricht mehr als der Code liefert (deckt sich mit A18 ❌)**

- `server/actions/gdpr-actions.ts:13-105` `exportTenantData` (Recht `settings:data_export`, Zeile 20): eine JSON-Struktur mit `bots` (Zähler), `conversations` nur Besucher-Gespräche inkl. `messages`, `summary` (Zeile 78-90; Mitarbeiter-Chats bewusst ausgeschlossen, Kommentar 74-77), `leads`, `appointments`, `handovers` (91-93), `documents` **nur Metadaten** (`id, originalName, fileType, fileSizeMB, status, createdAt, uploadedById`, Zeile 94-104).
- Nicht enthalten: Gedächtnis-Einträge (kein `memory`/`knowledge`-Modell im Export), Dokumente im Originalformat, Abläufe. Es gibt im Portal auch keinen Einzel-Download eines Dokuments (`server/actions/document-actions.ts` exportiert nur upload/get/delete/reprocess; keine `documents/*/download`-Route).
- Weitere Exporte: Gespräche und Leads als Excel/CSV/PDF (`app/api/portal/gespraeche/export`, `app/api/portal/leads/export`, `app/api/portal/gespraeche/[id]/pdf`, Auswertung `app/api/portal/auswertung/export`), Frag-Lymbe-Verlauf einzeln (`app/api/portal/threads/[id]/export`).
- § 8 Abs. 4 verspricht „Gespräche, Kontakte, **Dokumente und Gedächtnis-Einträge** … exportieren, **Dokumente im Originalformat**“. Dokumente und Gedächtnis fehlen. Der Satz „Auf Verlangen stellt Lymbe einen Gesamtexport bereit“ ist nicht im Code prüfbar.

## 7. Workspace-Formular und AvvZustimmung (AVV Vertragsparteien, § 11 Abs. 5, § 12 Abs. 6 · A20, B7)

**Urteil: belegt (Pflichtfelder, Nachweis) · nicht belegt (Fassungsnummer 1.7)**

- Pflichtfelder: `lib/mandant/vertragsangaben.ts:83-106` – `rechtsform: z.enum(['einzel','gesellschaft'])`, `firma: pflicht(...)`, `strasse`, `plz`, `ort`, `land`, `vertreterName`, `vertreterFunktion`, `mitteilungsEmail` (E-Mail-Pflicht), `telefon` (mind. 6 Ziffern, Zeile 75-81, Fehlertext „… bei einem Datenschutz-Vorfall erreichbar“), optional `datenschutzName/-Email`; `.strict()`.
- Serverseitig erzwungen: `server/actions/onboarding-v2-actions.ts:385-398` – ohne `avvAkzeptiert` kein Workspace, ohne `angaben` kein Workspace; Schema `angaben: vertragsangabenSchema.optional()` (Zeile 71) + Pflichtprüfung Zeile 395.
- Nachweis in derselben Transaktion wie der Mandant: `onboarding-v2-actions.ts:459-472` `tx.avvZustimmung.create({ fassung: AVV_FASSUNG, akzeptiertVon: session.user.id, ip: clientIpAusKopfzeilen(await headers()), name, email, angaben })`; Modell `prisma/schema.prisma:2587-2610` (`akzeptiertAm @default(now())`, bewusst ohne Fremdschlüssel).
- **Gespeicherte Fassungsnummer: `lib/legal/avv.ts:79` `export const AVV_FASSUNG = '1.6';`** `AVV_STAND = 'Oktober 2026'` (Zeile 82). Der eingebettete Vertragstext ist Fassung 1.6 (`lib/legal/avv-text.ts:2`, im Text „Stand Fassung 1.6“). Unter `app/(marketing)/avv/` liegt nur `fassung-1-5` als Altfassung. Die Fassung 1.7 vom 11.10.2026 ist im Code (Stand dieser Kopie) **nicht** hinterlegt; neue Zustimmungen würden mit „1.6“ protokolliert und der Kunde sähe im Onboarding den 1.6-Text. Bis zum Einspielen von 1.7 gilt für Neukunden also 1.6.

## 8. Verbinden-Dialog: Anbieter, Sitz, Datenfluss (AVV § 5 Abs. 1 · A21)

**Urteil: belegt**

- Liste `lib/integrations/anbieter.ts:30-135`: Google Calendar (Google Ireland Limited, Irland, dpf, Drittland USA), Microsoft Outlook/Teams (Microsoft Ireland Operations Limited, Irland, dpf), Calendly (Calendly LLC, USA, pruefen), Cal.com (Cal.com, Inc., USA, pruefen), Shopify (Shopify International Limited, Irland, angemessen/Kanada), Shopware/WooCommerce („der Betreiber Ihres Shop-Servers“, eigen), WhatsApp (WhatsApp Ireland Limited (Meta), dpf), Messenger/Instagram (Meta Platforms Ireland Limited, dpf), Slack (Slack Technologies, LLC (Salesforce), USA, dpf), Webhook und API-Datenquelle („pruefen“).
- Text `verbindenText` (Zeile 140-165): erster Absatz `Anbieter: ${a.anbieter}, Sitz: ${a.sitz}. Sie verbinden Ihr eigenes Konto – dafür gelten die Bedingungen und der Datenschutz von ${a.anbieter}. Daten, die über diese Verbindung fließen: ${a.daten}. Sie sind dafür verantwortlich, dass Sie mit ${a.anbieter} die nötigen Verträge haben und Ihre Datenschutzerklärung das abdeckt.`
- **Exakter Satz für DPF-Anbieter** (Zeile 148): `Daten können in ${a.drittland} gehen. ${a.anbieter} ist nach dem EU-US Data Privacy Framework zertifiziert.` – also z. B. „Daten können in die USA gehen. Google Ireland Limited ist nach dem EU-US Data Privacy Framework zertifiziert.“ (Hinweis: zertifiziert ist jeweils die US-Muttergesellschaft, der Satz nennt die irische Vertragspartei – inhaltlich zu prüfen durch Dennis, A12 in 08_Gegenpruefung.)
- Weitere Absätze: Postfach-Hinweis (146), Angemessenheitsbeschluss (150), „Grundlage prüfen“ (151-156), WhatsApp/Meta-Hinweis mit Erstantwort-Text (158-163).
- Verwendung: `components/platform/VerbindenHinweis.tsx`, `bot-config/NotifySection.tsx`, `bot-config/sections/ToolsSection.tsx`, `portal-chat/AppsVerbinden.tsx`. Ob jeder Verbinden-Knopf den Dialog wirklich davorschaltet, ist eine UI-Frage – im Code nur über die Einbindung belegt, nicht geklickt.

## 9. Frag-Lymbe-Verläufe nur für die Person; Dokumente nur mit knowledge:view (B6, B8, § 12 Abs. 5)

**Urteil: belegt**

- `lib/portal-chat/access-domain.ts:22-26` `isThreadVisibleTo(thread, actorUserId)`: `return thread.userId === actorUserId;` – nimmt „absichtlich KEINE Rolle, KEIN Flag und KEINEN Tenant entgegen“ (Kommentar 17-20). Einzige Ausnahme: aktive Freigabe durch den Besitzer (`isSharedThreadVisibleTo`, Zeile 45-50).
- `lib/portal-chat/access.ts:56-90` `requirePortalChatActor`: nur Inhaber oder `TenantMember` mit `internal:chat`/`lymbe:chat`; bewusst nicht `verifyTenantAccess` (Kommentar 19-21), damit Plattform-Personal nicht durchkommt. Auch ein Support-Zugang „bearbeiten“ hilft hier nicht, weil `personalDarf` in dieser Datei nicht vorkommt.
- Weitere Leser von `portalThread/portalMessage` außerhalb des Portal-Chats filtern auf `thread: { userId: session.user.id }` (`server/actions/area-actions.ts:100, 215`; `home-actions.ts:76, 194`) oder zählen nur (`lib/data-retention/vorschau.ts:50`); `app/api/portal/attachments/[id]/download/route.ts:11-28` verzichtet ausdrücklich auf die SUPERADMIN-Ausnahme. Keine Admin-Einstellung zur Einsicht gefunden – B8 „keine Einsicht“ bestätigt.
- Dokumente: `server/actions/document-actions.ts:205` `requireEinsicht(tenantId, 'knowledge:view')`; `knowledge-actions.ts:1791, 1842, 1889` `assertAccess(tenantId, 'knowledge:view')`; Seite `app/[tenantSlug]/knowledge/page.tsx:40` `requirePageAccess(tenant.id, 'knowledge:view')`. Mitglieder mit diesem Recht sehen alle Dokumente der ihnen zugewiesenen Assistenten – entspricht § 12 Abs. 5 („alle Mitglieder … können die hochgeladenen Dokumente abfragen“) und B6.

## 10. Admin-Bereich verlangt 2FA; Portal-eigenes TOTP (Anlage 1, DSE 10 · A14)

**Urteil: teilweise**

- Portal-eigenes TOTP existiert: `server/services/totp-service.ts` (speakeasy, Zeile 8-26, `verifyTOTPCode` 41), Backup-Codes `server/services/backup-codes-service.ts`, Einrichtung `app/setup-2fa/page.tsx`, Verwaltung `app/settings/security/page.tsx:79` `<TwoFactorSection …>`.
- Erzwungen für Admin-Seiten: `app/admin/layout.tsx:30-40` – `if (!u?.twoFactorEnabled) redirect('/setup-2fa')` für SUPERADMIN, PLATFORM_ADMIN, SUPPORT.
- Login mit Passwort: `lib/auth.ts:282-290` verlangt TOTP, wenn `twoFactorEnabled`.
- Lücken: (a) `requireRole` (`lib/auth.ts:598-602`) prüft nur die Rolle, nicht `twoFactorEnabled` → Admin-Server-Actions und `/api/admin/*`, `/api/internal/*` sind für ein Personalkonto **ohne** eingerichtete 2FA aufrufbar (das Layout greift nur bei Seitenaufrufen). (b) Anmeldung über Google/GitHub (`signIn`-Callback `lib/auth.ts:354-401`) hat keinen TOTP-Schritt; die Pflicht hängt dann am Fremdanbieter. (c) `proxy.ts:238-281` schützt `/admin` nach Rolle, nicht nach 2FA. DSE 10 „Multi-Faktor-Authentifizierung für alle administrativen Zugänge“ ist im Portal damit auf Seitenebene erzwungen, auf API-/Action-Ebene nicht; die Konten bei Hetzner, GitHub, STACKIT usw. sind nicht im Code prüfbar (A14 offen).

## 11. Protokolle ohne Inhalte (AVV § 8 Abs. 1, A6b/A31)

**Urteil: belegt (Mechanismus) · teilweise (Reichweite der Regeln)**

- Zentrale Schwärzung aller `console.*`-Aufrufe vor Ausgabe und Live-Log: `instrumentation.ts:81-118` (`ohneInhalt`, `fuerAusgabe`), aktiv nur in `NEXT_RUNTIME === 'nodejs'` (Zeile 48). Regeln: Prisma-Fehler auf Kopfzeile + Grund gekürzt (ohne Aufruf-Argumente), E-Mail → `<e-mail>`, Telefon → `<telefon>`, Zitate ≥ 40 Zeichen in `"…"`/`'…'` → `"…"`; Fehlerobjekte zu Name/Code/Meldung + 6 Stapelzeilen; wenn Schwärzen scheitert, wird die Zeile verworfen (Zeile 125-128). Gleiche Regeln im Fehlerprotokoll `lib/betrieb/fehler.ts:72-85` `schwaerzen`.
- Gezielt entschärfte Stellen: `app/api/widget/[botId]/chat/route.ts:931-935` loggt nur `${suchtext.length} Zeichen` („Nur Längen, kein Wortlaut (06.10.2026)“); SpamGuard Zeile 380-386 ohne Inhalt; Werkstatt-Logs mit Zählern/Arten.
- Verbleibende Stellen mit Wortlaut (keine Besucherinhalte, aber Kundentexte):
  - `lib/ai/prompt-helpers.ts:150-153` – `console.info('[Prompt] Rueckfallsatz gekuerzt …', removed)` gibt den entfernten Teil des vom Kunden konfigurierten Rückfalltexts aus (Bot-Konfiguration, kein Personenbezug; ungeschwärzt, wenn < 40 Zeichen bzw. ohne Anführungszeichen).
  - `app/api/portal/ablaeufe/werkstatt/route.ts:470` – `fragen: rueckfragen.map((f) => f.frage)` (systemgenerierte Rückfragen, kein Nutzertext).
  - `inngest/functions/whatsapp/answer-message.ts:145`, `inngest/functions/meta/answer-message.ts:135` – `gesendet.fehler.text` (Fehlertext von Meta; kann die Empfängernummer enthalten → würde als `<telefon>` geschwärzt).
  - `app/api/integrations/*/callback/route.ts:155/159/196` – `rawMessage` des OAuth-Fehlers (kann die Konto-E-Mail enthalten → geschwärzt).
  - `lib/docs/content.ts:1000` `console.log('Lead erfasst:', lead)` ist Dokumentationstext (Beispielcode in der Hilfe), läuft nicht.
- Grenzen des Mechanismus: Freitext **ohne** Anführungszeichen und unter 40 Zeichen (z. B. ein Name oder ein kurzer Besuchersatz als eigenes String-Argument) passiert die Regex ungeschwärzt; Namen werden grundsätzlich nicht erkannt. Die Zusage „Logger schwärzt Nachrichten“ gilt also für Nachrichten, die als JSON-Zitat oder als Fehlerobjekt im Log landen, nicht für jeden denkbaren String. In der Stichprobe (`grep` über `app lib server inngest` nach `console.*` mit `message|content|prompt|text|frage|visitor|email|phone`) wurde keine Stelle gefunden, die Besucher- oder Kundennachrichten direkt loggt. Skripte unter `scripts/` und der Abläufe-Kern laufen außerhalb des Next-Prozesses und damit außerhalb dieser Schwärzung – nicht im Code prüfbar.
- Commit `3d97dfd` ist in dieser flachen Kopie nicht adressierbar; der beschriebene Code ist vorhanden (Kommentar „A31 (08.10.2026)“ in `instrumentation.ts:81`).

---

## Zusammenfassung – Abweichungen Vertrag ↔ Code

1. **AVV_FASSUNG = '1.6'** (`lib/legal/avv.ts:79`) – Fassung 1.7 ist im Code nicht hinterlegt; Zustimmungen werden mit 1.6 protokolliert, Onboarding zeigt den 1.6-Text.
2. **§ 3 Abs. 1 „mit Zeitpunkt und Nutzer“**: Benachrichtigungsziele (`integration-actions.ts`), Kalender, Shops, WhatsApp, Meta schreiben keine Audit-Zeile; Modelle kennen nur `createdAt`, keine Person. Selbstlernen nur als Gesamt-`BOT_UPDATED` ohne Vorher/Nachher und ohne `tenantId`.
3. **§ 8 Abs. 4 Export**: nur Gespräche, Leads, Termine, Übergaben und Dokument-Metadaten; keine Dokumente im Original, kein Gedächtnis, keine Abläufe, kein Einzel-Download.
4. **§ 3 Abs. 5 Support-Zugriff**: Zugang mit Grund/Umfang/Frist und Kundensicht sind sauber; aber `updateTenantBotForAdmin` ändert Systemprompt eines Kunden ohne Support-Zugang und ohne Kundensicht; Sicherungs-Download und Admin-Einsicht laufen ohne individuellen Grund/Freigabe; Seitenprotokoll hängt am Browser-JS. Vier-Augen-Prinzip nur organisatorisch.
5. **§ 5 Abs. 4 / Anlage 1 „Zugangsdaten verschlüsselt“**: Webhook-Signaturgeheimnisse **und** Slack-/Teams-Webhook-URLs (`BotIntegration.target`) liegen im Klartext.
6. **DSE 10 / Anlage 1 „Mehr-Faktor für alle administrativen Zugänge“**: 2FA nur am `/admin`-Layout erzwungen, nicht in `requireRole`, Server Actions, `/api/admin`, nicht beim OAuth-Login.
7. **Mandantentrennung**: DB/Qdrant/MinIO belegt; Redis nur teilweise präfixiert; kein zentraler Sitzungs-Wrapper, sondern Prüfung je Route (Stichprobe vollständig).
8. **Protokolle ohne Inhalte**: Mechanismus vorhanden; Lücke bei kurzen, unzitierten Strings und Namen; Skripte/Kern außerhalb.
9. Belegt ohne Abweichung: Selbstlernen-Vorgabe aus, Pflichtfelder + AvvZustimmung (Name, E-Mail, IP, Zeit, Angaben), Verbinden-Dialog mit DPF-Satz, Frag-Lymbe-Verläufe nur für die Person, Dokumente nur mit `knowledge:view`, Support-Protokoll 365 Tage mit Löschlauf.
