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
2. Role_Questions
3. Weekly_Records
4. Monthly_Profile
5. Team_Heatmap

---

## Required Google Sheet design
### A) Roster tab
Columns: `person_id, full_name, preferred_name, role_type, email, status`

### B) Role_Questions tab
Columns: `role_type, question_1, question_2, question_3`

Example role_type values:
- `qc_manager`
- `performance_bridge`
- `set_operations`

This allows no-code question lookup without using a Function node.

---

## Workflow 1 — Weekly Question Sender (No Function Node)

**Purpose:** send 3 questions to each employee every week.

Nodes (simple flow):
1. **Schedule Trigger** (weekly, e.g., Monday 9:00 AM Africa/Lagos)
2. **Google Sheets: Read Roster** (filter status = active)
3. **Loop Over Items** (one person at a time)
4. **Google Sheets: Lookup in Role_Questions** using `role_type`
5. **Set Node** (map fields for email placeholders)
6. **Gmail Send** (one email per employee)

Important settings:
- Subject format: `Pulse Check | Week of {{date}} | {{name}}`
- Keep all replies in same thread when possible.

---

## Workflow 2 — Reply Collector + Analyzer

**Purpose:** read approved replies and convert to structured indicators.

Nodes:
1. **Schedule Trigger** (every 2–4 hours)
2. **Gmail Search** (filter by label, e.g., `pulse-replies`)
3. **Data Store or Sheet Check** (skip already-processed message IDs)
4. **Google Sheets Lookup (Roster)** by sender email to get `person_id/full_name/role_type`
5. **Google Sheets Lookup (Role_Questions)** by `role_type` to attach question context
6. **OpenAI API Node** (use prompt from file 05)
7. **JSON Parse + Validate** (against file 06 schema)
8. **Google Sheets Append** (`Weekly_Records`)

Important settings:
- Read only messages from the approved label/thread.
- If JSON is invalid, send operator alert email and skip write.

---

## Workflow 3 — Monthly Summary + Raw Data Cleanup

**Purpose:** create person-level monthly summaries and remove temporary raw text.

Nodes:
1. **Schedule Trigger** (end/start of month)
2. **Google Sheets Read** (`Weekly_Records` for month)
3. **Aggregate by person** (Item Lists / Summarize style no-code node)
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
3. **Transform to long/heatmap format** (no-code transform node)
4. **Write to `Team_Heatmap`**

Indicators for heatmap:
- `workload_score`
- `clarity_gap_score`
- `collaboration_friction_score`
- `resource_gap_score`

Important interpretation:
- Higher score always means higher risk / more management attention needed.

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
