# Broker Copilot: Renewal Orchestration Assistant
## Round 1 Proposal - Techfest 2025-26

### 1. Problem Understanding
Insurance brokers face a "fragmented data" crisis during renewals. Key information is scattered across CRMs, disparate emails, calendar invites, and static policy documents. 
**The Core Pain Point:** Brokers spend 60-70% of their time manually hunting for data across these silos just to prepare for a renewal, leading to:
* **Missed Opportunities:** High-priority renewals are lost in the noise.
* **Slow Turnaround:** Preparation takes days instead of minutes.
* **Generic Outreach:** Lack of context leads to impersonal client communication.

**Our Solution:** A "Connector-First" Broker Copilot that acts as an intelligent orchestration layer. Instead of creating a new database, it pulls live signals from existing tools (CRM, Outlook, Teams) to generate Just-in-Time (JIT) insights, prioritizing renewals dynamically and drafting context-aware outreach instantly.

---

### 2. Proposed Architecture & Workflow
Our system utilizes a **"Zero-Persistence" Passthrough Architecture**. Data is fetched, processed, and presented in real-time without being stored in a secondary database.

**Data Flow:**
1.  **Ingest (Connectors):** System wakes up on schedule or user request. Connectors fetch live metadata from:
    * *CRM* (Policy expiration dates, premiums).
    * *Mail-Miner* (Recent sentiment, negotiation threads).
    * *Calendar* (Recent/Upcoming meetings).
2.  **Synthesize (Orchestration Engine):**
    * Data is normalized in memory.
    * **Explainable Priority Score (EPS)** is calculated based on rules (Premium size + Time to expiry + Client Sentiment).
3.  **Intelligence (LLM Layer):** * Structured prompts are built using the live JSON data.
    * LLM generates a "Renewal Brief" and "Draft Email" using *In-Context Learning* (No RAG/Vector DB).
4.  **Act (Presentation Layer):** Broker views the brief, edits the email, and triggers the send action via Outlook API.

**Textual Diagram:**
`[Sources: CRM / Outlook / Teams] <==> [Secure Connectors (OAuth)] <==> [Orchestration Engine (FastAPI)] <==> [LLM (Azure OpenAI)] ==> [Frontend Dashboard (React)]`

---

### 3. Technology Stack
* **Frontend:** React.js (Responsive dashboard for pipeline and briefs).
* **Backend:** FastAPI (Python) - High-performance async handling for concurrent connector requests.
* **LLM:** Azure OpenAI (GPT-4o mini) - For summarization and drafting.
* **Connectors:** * *Microsoft Graph API* (Outlook, Teams, Calendar).
    * *Salesforce/HubSpot API* (Simulated CRM).
* **Auth:** Auth0 / OAuth 2.0 (Secure token management).
* **Hosting:** Vercel (Frontend) + Render/Azure Functions (Backend).

---

### 4. Security & Data Privacy Strategy
We strictly adhere to the **"No Ingestion"** policy:
1.  **No Database Storage:** We do not use SQL/NoSQL to store client records. We only store IDs/links to the original source.
2.  **Passthrough Processing:** Data is held in volatile memory (RAM) only for the duration of the session.
3.  **Source of Truth:** All data displayed includes a direct hyperlink to the original record (e.g., "View in Salesforce"), ensuring traceability.
4.  **Token Security:** OAuth access tokens are encrypted and managed via secure HttpOnly cookies, never exposed to the client side.
5.  **No Vector DB:** We rely purely on live context injection, eliminating the risk of stale or hallucinated data from embeddings.

---

### 5. Prototype Implementation Plan (Timeline)
* **Nov 24 - Nov 30 (Connectors):** Build valid OAuth adapters for Microsoft Graph (Email/Calendar) and Mock CRM.
* **Dec 1 - Dec 5 (Pipeline Logic):** Implement the "Explainable Priority Scoring" algorithm.
* **Dec 6 - Dec 10 (LLM Integration):** Develop the prompt engineering pipeline for Brief Generation and Chat.
* **Dec 11 - Dec 13 (Frontend):** Build the React dashboard and "One-Page Brief" view.
* **Dec 14:** End-to-End testing and video recording.
* **Dec 15:** **Round 2 Submission.**

---

### 6. Unique Innovations
1.  **Explainable Priority Score (EPS):** unlike black-box AI, our scoring is transparent. Brokers can click "Why High Priority?" to see the exact math (e.g., "+20 points for Premium > $100k", "+10 points for 'Urgent' sentiment in recent email").
2.  **"Risk Radar" Sentiment Analysis:** The system analyzes the *tone* of the last 3 emails from the client. If the tone is "Frustrated," the renewal is automatically flagged as "At Risk" regardless of premium size.
3.  **Connector-Backed "Fact Check":** Every sentence in the AI-generated brief will have a citation footnote like `[Source: Email from John, Nov 12]` that links to the actual item.
