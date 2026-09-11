# AI Triage System

An n8n-based patient triage automation workflow that receives patient
information through a webhook, evaluates emergency conditions, assigns a
triage status and priority, generates an appropriate response message,
and stores the result in Google Sheets.

> **Important:** This project is a technical/educational automation
> prototype. It is not a medical device and must not be used as a
> substitute for professional medical assessment or emergency services.

## Overview

The workflow is designed around three triage outcomes:

-   **CRITICAL** --- triggered when a critical condition is detected.
-   **URGENT** --- triggered when the case is marked severe.
-   **NON-EMERGENCY** --- used for normal cases that do not meet the
    critical or severe conditions.

## Workflow

``` text
Patient / AI Voice Agent
          |
          v
      Webhook
          |
          v
     Edit Fields
          |
          v
  Critical Condition?
       /        \
     YES         NO
      |           |
      v           v
  CRITICAL   Severe or Normal?
                  /       \
               Severe     Normal
                 |           |
                 v           v
              URGENT     NON-EMERGENCY
                 \           /
                  \         /
                   v       v
                 Message
                    |
                    v
              Google Sheets
```

## Critical Conditions

The current workflow checks for:

-   Difficulty breathing
-   Heavy bleeding
-   Loss of consciousness

If any of these conditions is detected, the workflow routes the case to
the **Critical** branch.

## Technology Stack

-   **n8n** --- workflow automation
-   **Webhook** --- receives structured patient information
-   **Conditional logic** --- determines the triage pathway
-   **Google Sheets** --- stores triage records

## Input Data

The webhook is designed to receive structured fields such as:

``` json
{
  "patient_id": "P001",
  "name": "Example Patient",
  "age": 45,
  "symptom": "Example symptom",
  "severity": "Normal",
  "difficulty_breathing": false,
  "heavy_bleeding": false,
  "conscious": true
}
```

Use fictional/test data when experimenting with this repository.

## Output

Depending on the conditions, the workflow generates:

### Critical

-   Triage status: `NON-EMERGENCY` in the current V1 workflow
-   Priority: `NORMAL`
-   Emergency message

### Severe

-   Triage status: `URGENT`
-   Priority: `HIGH`
-   High-priority medical attention message

### Normal

-   Triage status: `NON-EMERGENCY`
-   Priority: `NORMAL`
-   Monitoring/consultation message

> **Note:** The Critical branch in the current V1 workflow uses
> `NON-EMERGENCY` and `NORMAL` as its stored status/priority while
> generating an emergency message. This is preserved from the original
> workflow and should be reviewed before real-world use.

## Repository Structure

``` text
AI-Triage-System/
├── README.md
└── Triage-System-v1.json
```

## Setup

1.  Install or access an n8n instance.
2.  Import `Triage-System-v1.json`.
3.  Configure your own Google Sheets credentials.
4.  Replace the Google Sheet reference with your own test sheet.
5.  Configure the webhook URL.
6.  Send test data using fictional patient information.
7.  Verify the resulting triage status, priority, message, and Google
    Sheets entry.

## Security

Do not commit:

-   API keys
-   OAuth credentials
-   Access tokens
-   Private webhook secrets
-   Real patient information
-   Private Google Sheet IDs or confidential links

The repository workflow has been cleaned to remove the original pinned
test patient data and private credential bindings.

## Project Status

**Version:** V1\
**Status:** Prototype / Educational Project

## Future Improvements

-   Add stronger input validation
-   Add patient ID generation
-   Add audit logging
-   Improve edge-case handling
-   Add authentication for the webhook
-   Add notification/escalation workflows
-   Add more comprehensive triage rules
-   Integrate the workflow with an AI voice agent
-   Add automated testing

## Author

**Utpal Parmar**

Built as an AI automation project using n8n.
