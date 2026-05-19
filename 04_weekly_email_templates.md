# Weekly Email Templates (Operator-Friendly)

These templates are for Gmail sending via n8n.

---

## A) Main weekly check-in email template

**Subject:**  
Pulse Check | Week of {{week_start_date}} | {{preferred_name}}

**Body:**

Hello {{preferred_name}},

This is your weekly Employee Pulse check-in.  
This check-in is used to understand work blockers, planning needs, and support needs. It is not a punishment or performance evaluation tool.  
Please reply in this same thread with short answers.

1) {{question_1}}  
2) {{question_2}}  
3) {{question_3}}

You can answer in bullets.

Thank you.

---

## B) Reminder template (if no reply within 24 hours)

**Subject:**  
Reminder: Pulse Check | Week of {{week_start_date}} | {{preferred_name}}

**Body:**

Hello {{preferred_name}},

Kind reminder to reply to your weekly pulse check when possible.  
Please answer the 3 questions in this same email thread.

Thank you.

---

## C) Confirmation template (optional)

**Subject:**  
Received: Pulse Check | Week of {{week_start_date}} | {{preferred_name}}

**Body:**

Hello {{preferred_name}},

Thank you — your weekly pulse reply has been received.

Best,
Operations

---

## Operator notes
- Keep all replies in one thread per person per week.
- Use a dedicated Gmail label (example: `pulse-replies`) for processing.
- Do not manually copy private details into long-term files.
