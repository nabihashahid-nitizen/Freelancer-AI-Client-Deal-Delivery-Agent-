# Freelancer AI Client Deal & Delivery Agent 

A comprehensive multi-agent n8n workflow consisting of **66 nodes** designed to automate the full lifecycle of a content agency—from lead intake and AI requirements analysis to human approval gates, quality assurance loops, and automated invoicing.

---

## Project Overview

This system acts as an autonomous operations engine for freelancing and content writing businesses. It receives client messages via Facebook Messenger or custom webhooks, processes requests through specialized AI agents, enforces admin supervision (Human-in-the-Loop) for key decisions, and handles delivery with automated HTML invoices.

---

## Key Features & System Architecture

### 1. Lead Intake & Context Integration
* **Multi-Channel Triggers:** Ingests client messages through **Facebook Messenger** and custom **HTTP Webhooks**.
* **Context Engine:** Fetches system settings and the last 5 client feedback entries from **Google Sheets** to personalize responses and maintain continuity.

### 2. Requirements Analyst & Auto-Clarification
* **AI Requirements Analyst:** Evaluates incoming client requests for completeness (topic, word count, deadline).
* **Smart Clarification:** If the request is vague or a simple greeting (e.g., *"Hi"*, *"Hello"*), the AI drafts targeted questions and sends them via **Gmail**, logging the project status as `NEEDS_INFO`.

### 3. Proposal Generation & Gate 1 Approval
* **AI Proposal Writer:** Generates project proposals based on analyzed requirements.
* **Guardrail Validation:** Applies code-based checks to verify proposal parameters.
* **Gate 1 (Admin Review):** Sends an interactive approval email to the admin.
  * **Approved:** Proposal is emailed to the client (`PROPOSAL_SENT`).
  * **Rejected:** Updates status to `REJECTED` and sends a confirmation email.

### 4. Autonomous Content Creation & QA Loop
* **AI Content Creator:** Drafts the deliverable once the client accepts the proposal (`ACCEPTED`).
* **AI QA Critic:** Evaluates the draft against quality benchmarks. If it fails, the workflow loops back to regenerate the content using the QA feedback until standards are met or maximum retries are exhausted.

### 5. Gate 2 Approval, Invoicing & Delivery
* **Gate 2 (Final Review):** Sends the final draft to the admin (`WORK_REVIEW`).
  * **Approved:** Automatically generates an **HTML Invoice** and delivers both assets to the client via email (`DELIVERED`).
  * **Request Changes:** Applies admin feedback and re-executes the creation loop.
  * **Max Revisions / Timeout:** Automatically updates status and sends follow-up notifications.

### 6. Error Handling & Monitoring
* **Error Trigger:** Centralized failure alert system that sends instant Gmail notifications to the admin if any node encounters an execution error.
* **Audit Trail:** Continuously syncs status logs across all stages to **Google Sheets**.

---

##Tech Stack

* **Workflow Orchestration:** [n8n]([https://n8n.io/](https://bihashd1.app.n8n.cloud/assistant/fac5a74a-8564-4f82-9309-f1453960c249)) (66 Nodes)
* **AI & LLM Services:** OpenAI API / Google Gemini API
* **Communication Channels:** Facebook Messenger Graph API, Gmail API
* **Database & Logs:** Google Sheets API
* **Hosting / Deployment:** Alternate Clouds

---

