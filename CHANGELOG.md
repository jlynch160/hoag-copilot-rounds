# Changelog

Every user-visible change to the Easy Health · Microsoft 365 + Copilot demo.
Newest on top.

Format loosely follows [Keep a Changelog](https://keepachangelog.com/) — grouped under **Added / Changed / Fixed / Removed** with a date header.

---

## 2026-04-21 — Fix: restore Copilot suggestion prompts

### Fixed
- **Recommended prompts were missing** from the Copilot panel welcome state in every app (Outlook, Teams, Word, Excel, PowerPoint, OneDrive, Home, agents, Agent 365). Root cause: when multi-turn chat was added, the old `<div class="copilot-input-message">` placeholder was replaced with a real `<textarea>`, but `renderCopilotWelcome()` still ran `document.querySelector('.copilot-input-message').textContent = …` on the now-missing element. The null-dereference threw, the function exited before rendering the 2-up suggestion grid, and the welcome view appeared blank.
- Switched the placeholder-update to target the new textarea's `placeholder` attribute.
- Added null-guards so a missing chip or textarea never blocks rendering the suggestion cards.

---

## 2026-04-21 — Agent 365 tabs wired

### Changed
- **Agent 365 tile icon** — replaced the generic shield glyph with a custom SVG: rounded blue-indigo square, stylized "a" letterform, shield + check cue bottom-right. Matches Microsoft Agent 365 visual language without reproducing their brand asset.
- **Agent 365 app-shell header** uses the same new mark.

### Added
- **All 6 Agent 365 tabs are now interactive** (Fleet / Identity & access / Policies / Incidents / Cost / Logs). Each has its own pane:
  - **Identity & access**: Entra Agent IDs table with scopes, last-rotated dates, Conditional Access status. Right-rail identity-health stats + role-to-agent mapping.
  - **Policies**: 10-policy table (enforcement, scope, 7d violations). Compliance frameworks mapped (HIPAA / HITRUST / SOC 2 / NIST AI RMF). Recent policy-change audit trail.
  - **Incidents**: 6 incidents across severities with actionable buttons (2 active, 1 monitoring, 3 resolved).
  - **Cost**: 4 KPIs + spend-by-agent breakdown + ROI ratio (172×) + 3 optimization tips.
  - **Logs**: 12-row audit table with timestamps, invokers, prompts, sensitivity labels, outcomes (✓ / ✕ DLP / ✕ CA).
- **`a365Tab()`** JS to swap panes and keep the active tab highlight in sync.
- **`.a365-code`** CSS for monospace Entra-ID badges, with dark-mode support.

---

## 2026-04-21 — Agent 365 added to CIO persona

### Added
- **Agent 365 tile** on the CIO persona home page (next to Admin Center).
- Full **Agent 365 app shell** (`app-agent365`):
  - Governance score ring (94/100).
  - 5 KPIs: Active agents, 24h invocations, Blocked actions, Shadow agents (3, red), Cost MTD.
  - 12-agent cross-vendor inventory: 5 Microsoft Copilot Studio agents, Epic/Salesforce/ServiceNow partner agents, 1 Azure-OpenAI custom agent, 3 quarantined shadow agents.
  - Live-activity feed that prepends a new event every 3.5–4.7 s, with timestamps that drift.
  - Tenant-wide policies block, incidents row, footer narrative.
- `startAgent365Feed()` animator (pauses when the view is inactive).
- Dark-mode overrides for all Agent 365 surfaces.

---

## 2026-04-21 — Initial deploy to Azure Static Web Apps

### Added
- **Deploy folder** at `easyhealth-m365-demo/` with `index.html` + 8 product logo PNGs + `staticwebapp.config.json` + `README.md`.
- **GitHub repo** `jlynch160/easyhealth-copilot-rounds` created (public).
- **Azure Static Web Apps** workflow (`.github/workflows/azure-static-web-apps-*.yml`) auto-added by Azure on app creation.

### Baseline feature set (before the repo existed, captured here for completeness)
- **Personas** — 4 roles (Sarah Chen RN, Dr. Patel MD, Maria Rodriguez charge RN, David Kim CIO) with filtered app tiles, custom agents, recents, and hero greetings.
- **Apps built out**: Outlook (inbox + calendar), Teams (channel switching + meeting recap), Word (appeal letter + populate animation), Excel (14-day staffing grid + risk highlighting), PowerPoint (blank → 6-slide branded deck), OneDrive (17 files + Copilot search), Copilot Pages (live co-editor cursors), Dragon Copilot (ambient SOAP note), Admin Center, Purview, Power BI, Copilot Studio full, Shifts, Rollout Plan.
- **Copilot panel** with multi-turn chat, persona-aware responses on focus/handoff/prebrief, time-saved counter in the top bar, before/after pills on every response.
- **Governance layer**: Purview sensitivity labels (PHI / Confidential / Internal / Public) on OneDrive, emails, Word, and in responses.
- **Citations side-sheet** opens on clickable citation numbers inside responses.
- **Custom agents** with on-brand SVG logos + Copilot Studio-style builder wizard (5 steps: Describe / Configure / Knowledge / Test / Publish) that publishes a working agent into the grid.
- **Live activity** — presence dots on Teams avatars, emails sliding into the inbox, "X is typing…" indicators, auto-animated DAX waveform.
- **Guided tour** — 9-step coach-mark tour that auto-walks the golden path (bottom-left "▶ Guided tour" button).
- **Dark mode** toggle, loading skeletons on first app open, MFA sign-in step, waffle app launcher.
- **Inbox reply pane** with Copilot-drafted replies matched to the email content.
- **Calendar event detail modal** with agenda, attendees, and Prep-with-Copilot shortcut.
- **Published-agent chat** — freshly-built agents have a working chat with in-character responses.
- **Toast notification** system.
