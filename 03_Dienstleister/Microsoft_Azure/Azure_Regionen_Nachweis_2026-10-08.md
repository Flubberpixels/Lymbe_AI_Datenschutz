# Azure: Regionen und Bereitstellungsart – Nachweis

**Abgefragt:** 08.10.2026 über die Azure-Verwaltungsschnittstelle (Azure MCP, angemeldetes Konto), Abonnement „Azure subscription 1“ (`6a340424-5602-4b7c-8497-b954cf8c61e3`).
**Zweck:** Notion A26, 5.9 A1, 3.1 Nr. 4 – die Werkstatt muss in der EU laufen.

## Von Lymbe genutzt

Laut laufendem App-Container (08.10.2026, über `scripts/zugriff.sh` protokolliert): `AZURE_OPENAI_RESOURCE=lymbe-ai`, `AZURE_SPEECH_RESOURCE=lymbe-ai-sprache`.

| Ressource | Ressourcengruppe | Region | Zweck |
|---|---|---|---|
| `lymbe-ai` (Cognitive Services / Azure OpenAI) | lymbe-ai | **Germany West Central** (Frankfurt) | Werkstatt für Abläufe |
| `lymbe-ai-sprache` (Cognitive Services / Speech) | lymbe-ai | **Germany West Central** (Frankfurt) | Spracheingabe |

Bereitstellungen in `lymbe-ai`:

| Bereitstellung | Modell / Version | Bereitstellungsart (SKU) | Datenzone |
|---|---|---|---|
| `gpt-6.1-sol` | gpt-6.1-sol / 2026-09-29 | **DataZoneStandard** | **EUR** |
| `model-router` | model-router / 2025-11-18 | **DataZoneStandard** | **EUR** |
| `text-embedding-3-small` | text-embedding-3-small / 1 | **DataZoneStandard** | **EUR** |

„DataZoneStandard“ mit Zone „EUR“ heißt: Speicherung in der Region Germany West Central, Verarbeitung nur in Rechenzentren innerhalb der EU-Datenzone.

## Nicht genutzt – Altbestand

| Ressource | Ressourcengruppe | Region | Bereitstellung | Art |
|---|---|---|---|---|
| `info-4285-resource` (mit Projekt `info-4285`) | rg-info-8226 | Sweden Central | `model-router` | **GlobalStandard** (Verarbeitung weltweit möglich) |

Die App greift darauf nicht zu. Empfehlung: Ressourcengruppe `rg-info-8226` löschen, damit dort nicht versehentlich etwas mit globaler Verarbeitung angebunden wird.

## Ergebnis

✅ Die Werkstatt läuft in Germany West Central mit Datenzone EU. Eine Umstellung ist nicht nötig.

## Nachtrag 08.10.2026

Die alte Ressourcengruppe `rg-info-8226` samt `info-4285-resource` ist gelöscht (Chris, 08.10.2026). Foundry zeigt danach unter „Alle Ressourcen“ nur noch `lymbe-ai`.

Screenshots aus dem Portal, aufgenommen am 08.10.2026, liegen daneben:
- `Azure_Ressource_lymbe-ai_Germany-West-Central_2026-10-08.jpg` – Azure-Portal, Übersicht der Ressource: Standort Germany West Central
- `Azure_Bereitstellungen_lymbe-ai_DataZone-EUR_2026-10-08.jpg` – Foundry, Bereitstellungen: alle drei mit Bereitstellungstyp „Datenzonenstandard (EUR)“
- `Azure_Alle_Ressourcen_nur-lymbe-ai_2026-10-08.jpg` – Foundry, Alle Ressourcen (1): nur noch lymbe-ai
