# Employee Pulse Agent MVP — Project Overview

## What this project is
This is a **no-code Employee Pulse Agent MVP** for a small Nigeria content production team.  
It is designed for only 3 team members in the first version.

The system will run later with:
- **n8n Cloud** (workflow automation)
- **Gmail** (sending questions and reading replies)
- **Google Sheets** (structured data storage)
- **OpenAI API** (reply analysis to structured scores)
- **Looker Studio** (dashboard/heatmap visualization)

---

## Team members in scope (MVP)

1. **Fad / Fadiran Olumide**  
   Role: Senior Project Executive & QC Manager  
   Role type key: `qc_manager`  
   Focus: first review, execution quality, response discipline, AI boundary checks, compliance and asset quality checks.

2. **Chiemeli Kanikwu**  
   Role: Structural Bridge / Performance Check  
   Role type key: `performance_bridge`  
   Focus: making script intent executable by actors and shoot teams.

3. **Chinonyerem Emmanuella**  
   Role: Set Coordinator / Field Operations  
   Role type key: `set_operations`  
   Focus: local set readiness, actor coordination, props/location/timing, and field blockers.

---

## Operating modes
This MVP supports two operating modes:

1. **Test mode**
   - Operations/sender Gmail: `mwddmmde12@gmail.com`
   - Receiver email for all test rows: `pmalex@ngfortunehouse.com`
   - Test identities: `TEST001`, `TEST002`, `TEST003`

2. **Production pilot mode**
   - `E001` Fadiran Olumide (`qc_manager`)
   - `E002` Chiemeli Kanikwu (`performance_bridge`)
   - `E003` Chinonyerem Emmanuella (`set_operations`)

Identity rule:
- Use `person_id` as the permanent identity in long-term records.
- Do not use email address as long-term identity.

## MVP goals
Every week, the system should:
1. Send each person **3 check-in questions** by email.
2. Read replies only from a **specific Gmail label or thread**.
3. Analyze replies into 5 indicators:
   - `workload_score`
   - `clarity_gap_score`
   - `collaboration_friction_score`
   - `resource_gap_score`
   - `risk_level`
4. Save a short **weekly structured record**.

Every month, the system should:
5. Generate a **monthly profile summary** for each person.
6. Generate **team-level heatmap data**.
7. Delete/exclude raw reply text after monthly summarization.
8. Keep only structured scores, short summaries, and management suggestions.

---

## Unified indicator direction (important)
All four numeric indicators use the same direction:
- **Higher score = higher operational risk / stronger management attention needed**

Definitions:
- `workload_score`: 0 = very light/manageable, 100 = overloaded
- `clarity_gap_score`: 0 = very clear, 100 = very unclear
- `collaboration_friction_score`: 0 = smooth, 100 = severe friction
- `resource_gap_score`: 0 = no gap, 100 = severe resource gap

Risk thresholds:
- `high`: two or more thresholds triggered
- `medium`: one threshold triggered
- `low`: none triggered

Threshold values:
- `workload_score > 70`
- `clarity_gap_score > 70`
- `collaboration_friction_score > 70`
- `resource_gap_score > 70`

---

## Non-negotiable safety and fairness rules
- This is **not** a medical or psychological diagnosis tool.
- Do **not** infer mental illness, personality defects, or private-life issues.
- Focus only on work pressure, clarity gaps, collaboration blockers, and resource needs.
- Do not make automatic punishment or HR decisions.
- Human management review is required for action.
- Raw employee replies are temporary and should not be retained long-term.

---

## Success criteria for MVP
- Weekly check-ins are sent reliably.
- Replies are processed into valid structured JSON.
- Weekly and monthly summaries are understandable by a non-technical manager.
- Heatmap trends are available in Looker Studio.
- Retention policy is followed consistently.
