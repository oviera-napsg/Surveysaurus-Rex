# Survey Design

The Surveysaurus Rex Survey123 form is designed to intake access requests, technical support tickets, NSARGC engagement intentions, and onboard launches related to SARCOP.

---

## 🧭 Purpose

This form consolidates multiple NSARGC administrative workflows into a single, trackable system that integrates with:
- Microsoft Teams (automated messages)
- Microsoft Outlook (email notifications)
- OneNote (logging, meeting notes, geospatial gameplans)
- ArcGIS Online (feature layers, Dashboards, and Experience Builder)
- **PowerAutomate (node/hub for all-of-the-above)**

## 🚨 Credential Ground Rules

All workflow configuration must be done using NSARGC accounts where applicable to ensure seamless integration in PowerAutomate.  Utilizing a single, head-less NSARGC account solves common authentication / token issues in PowerAutomate, and ensures the NSARGC / NAPSG teams can access necessary input-output integrations and troubleshoot.  This ensures scalable, future-proof access.

When creating, enhancing, or troubleshooting, always use:
- nsargc_napsg (ArcGIS Online)
- nsargc@publicsafetygis.org (Outlook / M365 / Teams / OneNote)

---

## 📋 Field Overview

This is a broad, conceptual overview and may not capture all of the nuance within Survey123 Web Designer or exact field / feature types.  As of 18 June 2025, hidden fields are not listed.

--- 

### 📃 Page: Start / User Info

#### Group: Request Type

| Field Name       | Label             | Type           | Required                      | Description                 |
|------------------|-------------------|----------------|-------------------------------|-----------------------------|
| `request_type`   | Type of Request   | multiple_select| Yes                           | NSARGC Interest List, Access Request, Team Onboard, Technical Issue |
| `urgency`        | Urgency Level     | single_select  | Yes                           | `I'm Not Currently Supporting an Active Incident`, `I'm Currently Supporting an Active Incident` |
| `description`    | Issue Description | multiline_text | Yes                           | What the user needs help with |

#### Group: User Info

| Field Name            | Label                       | Type            | Required                               | Description                   |
|-----------------------|-----------------------------|-----------------|----------------------------------------|-------------------------------|
| `first_name`          | First Name                  | singleline_text | Yes                                    | First name of who is submitting request |
| `last_name`           | Last Name                   | singleline_text | Yes                                    | Last name of who is submitting request
| `professional_title`  | Professional Title          | singleline_text | Yes                                    | Professional title |
| `work_email`          | Work Email Address          | email           | Yes                                    | For notifications and routing |
| `phone`               | Phone Number                | singleline_text | yes                                    | Cell number where person can be reached during an incident |
| `agency_type`         | Agency Type                 | single_select   | No                                     | Pull from RLTT domain? |
| `in_sar_catalog`      | In the SAR Catalog?         | single_select   | Yes                                    | `Yes`, `No`, `I don't know` | 
| `team_name`           | Agency/Department/Team Name | single_select   | No                                     | Pull from SAR Catalog         |
| `team_name_other`     | Other Team Name             | singleline_text | No                                     | If not listed in SAR Catalog  |

---

## 🔁 Logic and Routing

### `request_type`

- If = _"...join the NSARGC Community and/or keep informed on updates to SARCOP"_
  - User completes **User Info** group
  - Submission triggers
    - post to MS Teams channel
    - Email to user: thank you, confirmation of submission, what to look out for next
    - Added to monthly SARGEO Hangout list and Constant Contact SAR Tracks distribution list

- If = _"...request view-only access to SARCOP data for my incident, future incidents, or for my own GIS products"_
  - User completes **User Info** group
  - User prompted with **Access Request** page and completes
  - Submission triggers
    - post to MS Teams channel
      - If `urgency` = `supporting`, MS Teams post marked as **! High Importance**
    - If `agency_type` = `FEMA_Task_Force`, `DOI`, `USCG`, `T32`, `T10`, email Paul cc: Jared, Adam, Orlando
    - If `agency_type` = `State`, `Local`, `Territorial`, `Tribal`, `Other`, email Jared cc: Paul, Adam, Orlando
    - Email to user: confirmation of submission, what to look out for next

- If = _"...onboard my SAR Team to SARCOP"_
  - User completes **User Info** group
  - User prompted with **SARCOP Team Onboard Request** page
  - Submission triggers
    - post to MS Teams channel
      - If `urgency` = `supporting`, MS Teams post marked as **! High Importance**
    - new page in OneNote > NSARGC Notebook > Geospatial Gameplans > Inbox with `feature_attributes` template and submissions
      - when processed, manually file new page into appropriate place in Geospatial Gameplans
    - Email to user: confirmation of submission, next steps
      - If `agency_type` = `FEMA_Task_Force`, `DOI`, `USCG`, `T32`, `T10`, email Paul cc: Jared, Adam, Orlando
      - If `agency_type` = `State`, `Local`, `Territorial`, `Tribal`, `Other`, email Jared cc: Paul, Adam, Orlando
      - If `urgency` = `supporting`, emails are marked as **! High Importance**

- If = _"...submit a technical issue I found in SARCOP"_ > **SARCOP Issue Ticket** page
  
- If `urgency` = `Supporting`, the submission triggers a post to a Teams channel marked as **! High Importance** with `description`
- If `request_type = Access`, a follow-up workflow checks existing group permissions and routes to the admin team.
- Emails are sent to the `assigned_to` user if filled in by internal team via Experience Builder.

---

> 📌 *This document will evolve alongside the Survey123 schema and integration workflows.*
