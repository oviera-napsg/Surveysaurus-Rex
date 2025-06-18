# Survey Design

The Surveysaurus Rex Survey123 form is designed to intake access requests, technical support tickets, NSARGC engagement intentions, and onboard launches related to SARCOP.

---

## 🧭 Purpose

This form consolidates multiple workflows into a single, trackable system that integrates with:
- Microsoft Teams (automated messages)
- Microsoft Outlook (email notifications)
- OneNote (logging)
- ArcGIS Online (hosted feature layers, dashboards, and Experience Builder)
- PowerAutomate (node/hub for all-of-the-above)

## Credential Ground Rules

All workflow configuration must be done using NSARGC accounts where applicable to ensure seamless integration in PowerAutomate.  Utilizing a single, head-less NSARGC account solves common authentication / token issues in PowerAutomate, and ensures the NSARGC / NAPSG teams can access necessary input-output integrations and troubleshoot.  This ensures scalable, future-proof access.

When creating, enhancing, or troubleshooting, use:
- nsargc_napsg (ArcGIS Online)
- nsargc@publicsafetygis.org (Outlook / M365)



---

## 📋 Field Overview

### Section: Request Info

| Field Name     | Label            | Type        | Required | Description                 |
|----------------|------------------|-------------|----------|-----------------------------|
| `request_type` | Type of Request  | select_one  | Yes      | Access, Support, Feedback   |
| `urgency`      | Urgency Level    | select_one  | Yes      | Normal, High                |
| `description`  | Issue Description| multiline   | Yes      | What the user needs help with |

### Section: User Info

| Field Name   | Label         | Type  | Required | Description                    |
|--------------|---------------|-------|----------|--------------------------------|
| `full_name`  | Full Name     | text  | Yes      | Who is submitting              |
| `email`      | Email Address | email | Yes      | For notifications and routing |
| `agency`     | Agency / Org  | text  | No       | Optional for group context     |


---

## 🔁 Logic and Routing

- If `urgency = High`, the submission triggers an extra Teams notification and logs to a separate OneNote section.
- If `request_type = Access`, a follow-up workflow checks existing group permissions and routes to the admin team.
- Emails are sent to the `assigned_to` user if filled in by internal team via Experience Builder.

---

> 📌 *This document will evolve alongside the Survey123 schema and integration workflows.*
