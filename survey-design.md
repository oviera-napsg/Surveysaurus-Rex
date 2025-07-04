# Survey Design

The Surveysaurus Rex Survey123 form is designed to intake access requests, technical support tickets, NSARGC engagement requests, and team onboard launches related to SARCOP.

![image](https://github.com/user-attachments/assets/f784c53d-de7f-4e5a-b322-a082d608b23e)

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

This is a broad, conceptual overview and may not capture all of the nuance within Survey123 Web Designer or exact field / feature types.

--- 

### 📃 Page: Start / Request Type and Contact

#### Group: Request Type and Contact

Surveysaurus begins with a simple intake page listing the request type and contact information.  The `request_type` is mutli-select; the selection(s) trigger the appropriate follow-up pages.  All submissions triggers utilize `contains` logic using the `request_type` field.

![image](https://github.com/user-attachments/assets/ba1060bf-280d-4207-8623-a6ab6f3dadf5)

![image](https://github.com/user-attachments/assets/4a6853f9-63af-48d2-89b8-fb6497daabfc)


#### Group: SARCOP Access Request

If `request_type` contains `apply_for_access`, a SARCOP Access Request application page becomes visibile.

![image](https://github.com/user-attachments/assets/65ddf6a8-ae9e-4656-adef-5cad82f32bf0)
![image](https://github.com/user-attachments/assets/b5b21ce6-4a26-4090-aa53-3dc7f09f008c)
![image](https://github.com/user-attachments/assets/0e7f29ec-c586-4959-a253-7511fee5743e)
![image](https://github.com/user-attachments/assets/539e152f-f6ab-4071-ad9b-b12545636f2a)
![image](https://github.com/user-attachments/assets/ace6c4bf-e446-4a01-ade2-975e44af21f6)
![image](https://github.com/user-attachments/assets/e58fc530-9306-4f13-a5cb-c0ba0928ec9b)


Hidden fields 


---

## 🔁 Logic and Routing

### `request_type`

- If = _"...join the NSARGC Community and/or keep informed on updates to SARCOP"_
  - User completes **User Info** group
  - Submission triggers
    - post to Admin MS Teams channel (🖥️ Core)
    - Email to user: thank you, confirmation of submission, what to look out for next
    - Added to monthly SARGEO Hangout list and Constant Contact SAR Tracks distribution list

- If = _"...request view-only access to SARCOP data for my incident, future incidents, or for my own GIS products"_
  - User completes **User Info** group
  - User prompted with **Access Request** page and completes
  - Submission triggers
    - post to Admin MS Teams channel (🖥️ Core)
      - If `urgency` = `supporting`, MS Teams post marked as **! High Importance**
    - If `agency_type` = `FEMA_Task_Force`, `DOI`, `USCG`, `T32`, `T10`, email Paul cc: Jared, Adam, Orlando
    - If `agency_type` = `State`, `Local`, `Territorial`, `Tribal`, `Other`, email Jared cc: Paul, Adam, Orlando
    - Email to user: confirmation of submission, what to look out for next

- If = _"...onboard my SAR Team to SARCOP"_
  - User completes **User Info** group
  - User prompted with **SARCOP Team Onboard Request** page
  - Submission triggers
    - post to Admin MS Teams channel (🖥️ Core)
      - If `urgency` = `supporting`, MS Teams post marked as **! High Importance**
    - new page in OneNote > NSARGC Notebook > Geospatial Gameplans > Inbox with `feature_attributes` template and submissions
      - when processed, manually file new page into appropriate place in Geospatial Gameplans
    - Email to user: confirmation of submission, next steps
      - If `agency_type` = `FEMA_Task_Force`, `DOI`, `USCG`, `T32`, `T10`, email Paul cc: Jared, Adam, Orlando
      - If `agency_type` = `State`, `Local`, `Territorial`, `Tribal`, `Other`, email Jared cc: Paul, Adam, Orlando
      - If `urgency` = `supporting`, emails are marked as **! High Importance**

- If = _"...submit a technical issue I found in SARCOP"_
  - User completes **User Info** group
  - User prompted with **SARCOP Issue Ticket** page
  - Submission triggers
    - post to Issue Ticket MS Teams channel (🪓 Operations)
      - If `urgency` = `supporting`, MS Teams post marked as **! High Importance**

---

> 📌 *This document will evolve alongside the Survey123 schema and integration workflows.*
