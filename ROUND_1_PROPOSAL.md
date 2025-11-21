Broker Copilot: Renewal Orchestration Assistant

Round 1 Proposal - Techfest 2025-26

1. Problem Understanding & Solution

The Challenge: Insurance brokers face a "fragmented data" crisis. Critical renewal information is trapped in silos—CRM records, scattered email threads, calendar invites, and Teams chats.
The Pain Point: Brokers spend 60-70% of their time manually hunting for data just to prepare for a renewal. This leads to:

Missed Opportunities: High-priority renewals slip through cracks.

Slow Turnaround: Prep takes days instead of minutes.

Generic Outreach: Lack of context results in impersonal emails.

Our Solution: A "Connector-First" Broker Copilot. Instead of creating a new database or ingesting documents, our system acts as an intelligent orchestration layer. It pulls live signals from existing tools (CRM, Outlook, Teams) to generate Just-in-Time (JIT) insights, prioritize renewals dynamically, and draft context-aware outreach instantly.

2. Proposed Architecture & Workflow

We utilize a "Zero-Persistence" Passthrough Architecture. Data is fetched, processed in memory, and presented in real-time without being stored in a secondary database or vector store.

System Diagram

graph TD
    subgraph "Data Sources (Live Connectors)"
        A[CRM <br/>(Salesforce/HubSpot)] -->|Policy Data| D(Secure Connector Layer)
        B[Email <br/>(Mail-Miner/Outlook)] -->|Sentiment & Threads| D
        C[Calendar <br/>(Teams/Outlook)] -->|Meeting Notes| D
    end

    subgraph "Broker Copilot Core (Zero-Persistence)"
        D{OAuth 2.0 / Auth0} <-->|JSON Signals| E[Orchestration Engine <br/>(FastAPI)]
        E -->|Context + Metadata| F[Prioritization Logic <br/>(EPS Algorithm)]
        F -->|Structured Prompt| G[LLM Layer <br/>(Azure OpenAI)]
    end

    subgraph "Broker Experience"
        G -->|Drafts & Briefs| H[Frontend Dashboard <br/>(React)]
        H -->|User Action| I[Send Email / Update CRM]
        I -.->|Write Back| A
        I -.->|Write Back| B
    end

    style D fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#bbf,stroke:#333,stroke-width:2px


Workflow Steps:

Ingest (Connectors): System authenticates via OAuth and fetches live metadata (Policy expiry, Email sentiment, Last meeting date).

Synthesize (Orchestration): Data is normalized in RAM. The Explainable Priority Score (EPS) is calculated.

Intelligence (LLM): Structured prompts are built using live JSON data. The LLM generates a "Renewal Brief" using In-Context Learning.

Act (Presentation): Broker views the brief, edits the AI-drafted email, and sends it via the Outlook API.

3. Technology Stack

Frontend: React.js (Responsive dashboard for pipeline and briefs).

Backend: FastAPI (Python) - High-performance async handling for concurrent connector requests.

LLM: Azure OpenAI (GPT-4o mini) - Selected for low latency and high reasoning capability.

Connectors:

Microsoft Graph API (Outlook, Teams, Calendar).

Mock Adapter (Simulating generic Broker CRM/Mail-Miner interaction).

Auth: Auth0 / OAuth 2.0 (Secure token management).

Hosting: Vercel (Frontend) + Render (Backend).

4. Security & Data Privacy Strategy

We strictly adhere to the "No Ingestion" policy to ensure enterprise-grade security:

No Database Storage: We do not use SQL/NoSQL to store client records. We only store IDs/links to the original source.

Passthrough Processing: Data is held in volatile memory (RAM) only for the duration of the session.

Token Security: OAuth access tokens are encrypted and managed via secure HttpOnly cookies.

No Vector DB/RAG: We rely purely on live context injection. This eliminates the risk of "stale data" and ensures privacy by design.

5. Prototype Implementation Plan (Timeline)

Nov 24 - Nov 30 (Connectors): Build valid OAuth adapters for Microsoft Graph and Mock CRM.

Dec 1 - Dec 5 (Pipeline Logic): Implement the "Explainable Priority Scoring" algorithm.

Dec 6 - Dec 10 (LLM Integration): Develop prompt engineering for Brief Generation and Chat.

Dec 11 - Dec 13 (Frontend): Build React dashboard and "One-Page Brief" view.

Dec 14: End-to-End testing and video recording.

Dec 15: Round 2 Submission.

6. Unique Innovations

Explainable Priority Score (EPS): Unlike black-box AI, our scoring is transparent. Brokers can click "Why High Priority?" to see the exact math (e.g., "+20 pts for Premium > $100k", "+15 pts for 'Urgent' sentiment in recent email").

"Risk Radar" Sentiment Analysis: The system autonomously scans negotiation threads to detect churn risk. If the tone is "Frustrated," the renewal is flagged as "At Risk" regardless of premium size.

Hallucination-Free Citations: Every claim in the AI-generated brief includes a citation footnote (e.g., [Source: Email from Client, Nov 12]) that links directly to the original item in Outlook or CRM.

7. Target Success Metrics

Metric

Target Goal

Measurement Method

Time Saved

50% reduction

Comparison of "Manual Prep" vs "Copilot Brief" duration.

Accuracy

100% Traceability

Every insight links to a valid Source ID.

Integration

4+ Systems

CRM, Outlook, Teams, and Calendar working simultaneously.

Prioritization

Grade A

90% of high-priority renewals have explainable factors.
