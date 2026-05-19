# n8n Workflow Setup Guide (Non-Technical Operator Version)

This guide explains how to set up the Employee Pulse MVP in n8n Cloud.

---

## Before you start
You need:
- n8n Cloud account
- Gmail account (initial operations sender: **mwddmmde12@gmail.com**)
- Google Sheet with planned tabs
- OpenAI API key
- Looker Studio access

Recommended Google Sheet tabs:
1. Roster
2. Role_Questions
3. Weekly_Records
4. Monthly_Profile
5. Team_Heatmap
6. Send_Log

---

## Mode setup (important)
This MVP supports:
- **test mode**
- **production mode**

**Warning:** Always run test mode first using `pmalex@ngfortunehouse.com` before sending to real employees.

Operator should set a single mode variable in n8n (example: `selected_mode = test` or `selected_mode = production`).

---

## Required Google Sheet design
### A) Roster tab
Columns: `person_id, full_name, preferred_name, role_type, primary_email, alternate_emails, mode, status, notes`

Rules:
- Use `primary_email` for sending weekly check-ins.
- Use both `primary_email` and `alternate_emails` for reply matching.
- Use `person_id` as permanent identity in structured records.

### B) Role_Questions tab
Columns: `role_type, question_1, question_2, question_3`

Example role_type values:
- `qc_manager`
- `performance_bridge`
- `set_operations`



### C) Send_Log tab
Columns:
- `send_id`
- `person_id`
- `full_name`
- `role_type`
- `mode`
- `week_start_date`
- `primary_email`
- `email_subject`
- `gmail_thread_id`
- `gmail_message_id`
- `sent_at`
- `reply_status`
- `processed_status`

Purpose:
- Create a reliable link between outgoing check-ins and incoming replies.
- Prevent ambiguous matching in test mode when multiple rows share one email address.

---

## Workflow 1 — Weekly Question Sender (No Function Node)

**Purpose:** send 3 questions to each employee every week.

Nodes (simple flow):
1. **Schedule Trigger** (weekly, e.g., Monday 9:00 AM Africa/Lagos)
2. **Set Node** to define `selected_mode` (`test` or `production`)
3. **Google Sheets: Read Roster**
4. **Filter Node** keep only rows where:
   - `status = active`
   - `mode = {{$json.selected_mode}}`
5. **Loop Over Items** (one person at a time)
6. **Google Sheets: Lookup in Role_Questions** using `role_type`
7. **Set Node** (map placeholders and use `primary_email` as receiver)
8. **Gmail Send** from `mwddmmde12@gmail.com` (initial setup)
9. **Google Sheets Append** to `Send_Log` with:
   - `person_id`, `full_name`, `role_type`, `mode`, `week_start_date`, `primary_email`
   - `email_subject`, `gmail_thread_id`, `gmail_message_id`, `sent_at`
   - initialize `reply_status = pending`, `processed_status = pending`

Important settings:
- Subject format: `Pulse Check | {{person_id}} | Week of {{week_start_date}} | {{preferred_name}}`
- Keep all replies in same thread when possible.
- Ensure every sent email creates one `Send_Log` row.

---

## Workflow 2 — Reply Collector + Analyzer

**Purpose:** read approved replies and convert to structured indicators.

Nodes:
1. **Schedule Trigger** (every 2–4 hours)
2. **Set Node** to define `selected_mode` (`test` or `production`)
3. **Gmail Search** (label: `pulse-replies`)
4. **Data Store or Sheet Check** (skip already-processed message IDs)
5. **Google Sheets Read Roster**
6. **Filter Node** keep rows where:
   - `status = active`
   - `mode = {{$json.selected_mode}}`
7. **Primary matching step (priority 1):** match incoming `gmail_thread_id` to `Send_Log.gmail_thread_id`.
8. **Fallback matching (priority 2):** if thread ID is unavailable, parse `person_id` from subject pattern:
   - `Pulse Check | {{person_id}} | Week of {{week_start_date}} | {{preferred_name}}`
9. **Final fallback (priority 3):** if still unmatched, match sender email against:
   - `Roster.primary_email`
   - OR emails listed in `Roster.alternate_emails`
10. **Ambiguity rule:** if sender email matches multiple active rows, route to operator review (do not auto-assign).
11. **Use matched row person_id/full_name/role_type** for identity and context
12. **Google Sheets Lookup (Role_Questions)** by `role_type`
13. **OpenAI API Node** (use prompt from file 05)
14. **JSON Parse + Validate** (against file 06 schema)
15. **Google Sheets Append** (`Weekly_Records`)
16. **Google Sheets Update `Send_Log`** set `reply_status/processed_status` for matched send record

Important settings:
- Keep Gmail label exactly: `pulse-replies`.
- Matching priority must be: thread ID -> subject person_id -> sender email.
- If no match is found, route to operator review.
- If JSON is invalid, send operator alert email and skip write.

---

## Workflow 3 — Monthly Summary + Raw Data Cleanup

**Purpose:** create person-level monthly summaries and remove temporary raw text.

Nodes:
1. **Schedule Trigger** (end/start of month)
2. **Google Sheets Read** (`Weekly_Records` for month)
3. **Aggregate by person_id** (no-code summarize node)
4. **OpenAI API summary step** (short management-focused summary)
5. **Write to `Monthly_Profile`**
6. **Delete/exclude raw reply text store** (if maintained separately)

---

## Workflow 4 — Team Heatmap Builder

**Purpose:** generate dashboard-friendly rows.

Nodes:
1. **Trigger** (after weekly/monthly updates)
2. **Read `Weekly_Records` + `Monthly_Profile`**
3. **Transform to long/heatmap format**
4. **Write to `Team_Heatmap`**

Indicators:
- `workload_score`
- `clarity_gap_score`
- `collaboration_friction_score`
- `resource_gap_score`

---

## Operator checklist (weekly)
- Confirm selected mode is correct (`test` or `production`).
- Before running test mode, confirm each sent email creates a `Send_Log` row.
- Confirm weekly emails were sent only to active rows in selected mode.
- Confirm replies are tagged with `pulse-replies`.
- After receiving replies, confirm matching happens by `gmail_thread_id` or `person_id` first (not only sender email).
- Confirm fallback sender matching works for `primary_email` and `alternate_emails`.
- Review unmatched sender emails manually.

## Operator checklist (monthly)
- Confirm monthly profiles generated by `person_id`.
- Confirm team heatmap updated.
- Confirm raw reply text cleanup completed.
