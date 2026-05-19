# n8n Workflow Setup Guide (Non-Technical Operator Version)

This guide explains how to set up the Employee Pulse MVP in n8n Cloud.

---

## Before you start
You need:
- n8n Cloud account
- Gmail account (recommended: dedicated operations mailbox)
- Google Sheet with planned tabs
- OpenAI API key
- Looker Studio access

Recommended Google Sheet tabs:
1. Roster
2. Weekly_Records
3. Monthly_Profile
4. Team_Heatmap

---

## Workflow 1 — Weekly Question Sender

**Purpose:** send 3 questions to each employee every week.

Nodes (simple flow):
1. **Schedule Trigger** (weekly, e.g., Monday 9:00 AM Africa/Lagos)
2. **Google Sheets: Read Roster** (active staff only)
3. **Function/Set Node** (attach role-specific questions)
4. **Gmail Send** (one email per employee)

Important settings:
- Subject format: `Pulse Check | Week of {{date}} | {{name}}`
- Keep all replies in same thread when possible.

---

## Workflow 2 — Reply Collector + Analyzer

**Purpose:** read approved replies and convert to structured indicators.

Nodes:
1. **Schedule Trigger** (every 2–4 hours)
2. **Gmail Search** (filter by label, e.g., `pulse-replies`)
3. **Deduplicate** (skip already-processed message IDs)
4. **OpenAI API Node** (use prompt from file 05)
5. **JSON Parse + Validate** (against file 06 schema)
6. **Google Sheets Append** (`Weekly_Records`)

Important settings:
- Read only messages from the approved label/thread.
- If JSON is invalid, send operator alert email and skip write.

---

## Workflow 3 — Monthly Summary + Raw Data Cleanup

**Purpose:** create person-level monthly summaries and remove temporary raw text.

Nodes:
1. **Schedule Trigger** (end/start of month)
2. **Google Sheets Read** (`Weekly_Records` for month)
3. **Aggregate by person**
4. **OpenAI API summary step** (short management-focused summary)
5. **Write to `Monthly_Profile`**
6. **Delete/exclude raw reply text store** (if maintained separately)

Important settings:
- Keep trend scores, summary, and suggestions.
- Remove raw reply details after monthly output is confirmed.

---

## Workflow 4 — Team Heatmap Builder

**Purpose:** generate dashboard-friendly rows.

Nodes:
1. **Trigger** (after weekly/monthly updates)
2. **Read `Weekly_Records` + `Monthly_Profile`**
3. **Transform to long/heatmap format**
4. **Write to `Team_Heatmap`**

Example heatmap row:
- period_label: `2026-W20`
- person: `E001`
- indicator_name: `workload_score`
- indicator_value: `38`

---

## Looker Studio setup notes
- Connect to the Google Sheet.
- Build charts:
  1. Weekly status table
  2. Per-person trend lines
  3. Indicator heatmap
  4. Monthly summary cards

---

## Operator checklist (weekly)
- Confirm weekly emails were sent.
- Confirm replies were tagged with correct Gmail label.
- Confirm JSON outputs were saved to `Weekly_Records`.
- Review high-risk items manually.

## Operator checklist (monthly)
- Confirm monthly profiles generated.
- Confirm team heatmap updated.
- Confirm raw reply text cleanup completed.
