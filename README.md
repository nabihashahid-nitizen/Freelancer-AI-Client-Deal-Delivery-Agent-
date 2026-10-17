Freelancer AI Client Deal & Delivery Agent (Human-in-the-Loop)
An end-to-end multi-agent n8n workflow designed to automate a client-facing freelance/agency service lifecycle. It seamlessly handles lead intake, requirement analysis, proposal generation, human approval gates, automated content delivery, quality assurance, revision loops, and invoicing.

📌 Key Features & Architecture
1. Client Intake & Context Building
Multi-channel lead capture via Facebook Messenger Webhook or custom Webhooks.

Normalizes client inputs, assigns unique Project IDs, and cleans data.

Integrates with Google Sheets to fetch agency settings and historical client feedback (last 5 interactions) for personalized processing.

2. AI Requirement Analysis & Automated Clarification
AI Requirements Analyst checks if client instructions are clear and detailed.

Auto-Clarification Loop: If information is missing or the client sends a vague greeting ("Hi", "Hello"), the AI drafts tailored clarifying questions and dispatches them via Gmail, logging status as NEEDS_INFO.

3. Proposal Generation & Gate 1 Approval (Human-in-the-Loop)
AI Proposal Writer generates project scopes and pricing.

Includes code-based guardrails to validate proposal parameters.

Gate 1: Sends an interactive email to the admin for approval.

Approved: Sends proposal to client (PROPOSAL_SENT).

Rejected: Notifies client and marks status as REJECTED.

4. Delivery Engine & Autonomous QA Loop
AI Content Creator generates deliverables upon client acceptance (ACCEPTED).

AI QA Critic scores the work. If QA fails, it triggers an iterative revision loop using critique feedback until quality standards are met or max retries are reached.

5. Gate 2 Approval, HTML Invoicing & Delivery
Gate 2: Final draft is emailed to the admin for review (WORK_REVIEW).

Approve: Generates a custom HTML Invoice and delivers both invoice and final assets to the client (DELIVERED).

Request Changes: Applies feedback and re-triggers creation engine.

Reject / Timeout: Updates project logs and triggers automated follow-ups.

6. Error Handling & Audit Trail
Centralized Error Trigger Node alerts admin instantly via Gmail on workflow failures.

Comprehensive status updates continuously synced to Google Sheets.

🛠️ Tech Stack
Automation Engine: n8n (66 Nodes Architecture)

LLM Engine: OpenAI / Google Gemini API

Triggers / Channels: Facebook Messenger Webhook, Custom Webhooks, Gmail

Database & Logs: Google Sheets API
