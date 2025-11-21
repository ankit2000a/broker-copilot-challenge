# Broker Copilot: Renewal Orchestration Assistant
## Round 1 Proposal - Techfest 2025-26

---

## 1. Problem Understanding & Solution

### The Challenge
Insurance brokers face a **"fragmented data" crisis**. Critical renewal information is trapped in silos—CRM records, scattered email threads, calendar invites, and Teams chats.

### The Pain Point
Brokers spend **60-70% of their time** manually hunting for data just to prepare for a renewal. This leads to:

- **Missed Opportunities:** High-priority renewals slip through cracks
- **Slow Turnaround:** Prep takes days instead of minutes
- **Generic Outreach:** Lack of context results in impersonal emails

### Our Solution
A **"Connector-First" Broker Copilot**. Instead of creating a new database or ingesting documents, our system acts as an intelligent orchestration layer. It pulls live signals from existing tools (CRM, Outlook, Teams) to generate Just-in-Time (JIT) insights, prioritize renewals dynamically, and draft context-aware outreach instantly.

### Expected Impact
- ✅ **50%+ time savings per renewal** - Reduce prep from hours to minutes
- ✅ **Improved win rates** - Better prioritization of high-value renewals
- ✅ **Standardized outcomes** - Consistent, data-driven approach across all brokers

> **🚫 NO RAG • NO Vector DB • NO Embeddings**  
> **✅ ONLY Live Connector Data - Zero Storage Architecture**

---

### 2. Proposed Architecture & Workflow

We utilize a **"Zero-Persistence" Passthrough Architecture**. Data is fetched, processed in memory, and presented in real-time without being stored in a secondary database or vector store.

### System Architecture

```text
┌─────────────────────────────────────────────────┐
│        Data Sources (Live Connectors)           │
│ ┌──────────┐   ┌──────────┐    ┌──────────┐     │
│ │    CRM   │   │   Email  │    │ Calendar │     │
│ │Salesforce│   │ Outlook  │    │   Teams  │     │
│ └─────┬────┘   └─────┬────┘    └─────┬────┘     │
└───────┼──────────────┼───────────────┼──────────┘
        │              │               │
        └──────────────┼───────────────┘
        ┌──────────────▼───────────────┐
        │    Secure Connector Layer    │
        │     (OAuth 2.0 / Auth0)      │
        └──────────────┬───────────────┘
                 JSON Signals
        ┌──────────────▼───────────────┐
        │     Orchestration Engine     │
        │          (FastAPI)           │
        └──────────────┬───────────────┘
              Context + Metadata
        ┌──────────────▼───────────────┐
        │     Prioritization Logic     │
        │       (EPS Algorithm)        │
        └──────────────┬───────────────┘
              Structured Prompt
        ┌──────────────▼───────────────┐
        │          LLM Layer           │
        │       (Azure OpenAI)         │
        └──────────────┬───────────────┘
               Drafts & Briefs
        ┌──────────────▼───────────────┐
        │      Frontend Dashboard      │
        │           (React)            │
        └──────────────────────────────┘

```


### Workflow Steps

1. **Ingest (Connectors):** System authenticates via OAuth and fetches live metadata
   - Policy expiry dates
   - Email sentiment analysis
   - Last meeting notes

2. **Synthesize (Orchestration):** Data is normalized in RAM
   - Explainable Priority Score (EPS) is calculated
   - Source links preserved for traceability

3. **Intelligence (LLM):** Structured prompts built using live JSON data
   - LLM generates "Renewal Brief" using In-Context Learning
   - No RAG, no vector database, no embeddings

4. **Act (Presentation):** Broker interacts with insights
   - Views the brief with source citations
   - Edits AI-drafted email
   - Sends via Outlook API

---

## 3. Technology Stack

### Frontend
- **Framework:** React.js
- **Purpose:** Responsive dashboard for pipeline and briefs
- **UI Library:** Tailwind CSS + Shadcn/UI

### Backend
- **Framework:** FastAPI (Python)
- **Rationale:** High-performance async handling for concurrent connector requests
- **Features:** OAuth management, connector orchestration, in-memory data processing

### AI/LLM
- **Provider:** Azure OpenAI
- **Model:** GPT-4o-mini
- **Rationale:** Low latency, high reasoning capability, enterprise compliance

### Connectors
- **Microsoft Graph API** - Outlook, Teams, Calendar integration
- **Mock CRM Adapter** - Simulating generic Broker CRM/Mail-Miner interaction
- **Future:** Salesforce, HubSpot, custom AMS systems

### Authentication & Security
- **Auth:** OAuth 2.0 / Auth0
- **Token Management:** Secure HttpOnly cookies, encrypted storage
- **Permissions:** Read-only, least privilege access

### Hosting & Deployment
- **Frontend:** Vercel (optimized for Next.js/React)
- **Backend:** Render or Azure App Service
- **CI/CD:** GitHub Actions

---

## 4. Security & Data Privacy Strategy

We strictly adhere to the **"No Ingestion"** policy to ensure enterprise-grade security:

### Core Principles

1. **No Database Storage**
   - We do NOT use SQL/NoSQL to store client records
   - Only store: User preferences, template definitions, audit logs
   - Never store: Policy data, client info, emails, documents

2. **Passthrough Processing**
   - Data held in volatile memory (RAM) only during active session
   - Typical lifespan: 5-30 seconds
   - Immediate cleanup after response delivery

3. **Source Attribution & Traceability**
   - Every data point includes: System Name (e.g., "Salesforce CRM"), Record ID with deep link, and Fetch timestamp
   - Brokers can verify any claim by clicking the source link

4. **Token Security**
   - OAuth access tokens encrypted and managed via secure HttpOnly cookies
   - Auto-refresh before expiration; immediate revocation on logout

5. **No Vector DB / No RAG**
   - We rely purely on live context injection
   - Eliminates risk of "stale data" or hallucinations

### Compliance Considerations
- **GDPR:** No data storage = easier compliance, instant "right to erasure"
- **SOC 2:** Audit logging, access controls, vendor security assessments

---

## 5. Implementation Timeline (Round 2 Roadmap)


| Phase | Dates | Deliverables |
|-------|-------|-------------|
| **Connectors** | Nov 24 - Nov 30 | Build valid OAuth adapters for Microsoft Graph and Mock CRM |
| **Pipeline Logic** | Dec 1 - Dec 5 | Implement Explainable Priority Scoring (EPS) algorithm |
| **LLM Integration** | Dec 6 - Dec 10 | Develop prompt engineering for Brief Generation and Q&A Chat |
| **Frontend** | Dec 11 - Dec 13 | Build React dashboard and "One-Page Brief" view |
| **Testing** | Dec 14 | End-to-end testing and demo video recording |
| **Submission** | Dec 15 | Round 2 Final Submission |

---

## 6. Unique Innovations

### 🎯 Innovation 1: Explainable Priority Score (EPS)

**The Problem:** Black-box AI scoring erodes broker trust.

**Our Solution:** Transparent, visual scoring breakdown.

**How it Works:**
- Click "Why High Priority?" to see exact calculation
- Example:

```text
  Total Score: 87/100
├─ Premium Risk (40%): 35/40 pts [Premium: $150K > $100K threshold]
├─ Time to Expiry (30%): 28/30 pts [14 days remaining, critical window]
└─ Claims History (10%): 8/10 pts [2 claims in 12 months]
```

---

### 🔍 Innovation 2: "Risk Radar" Sentiment Analysis

**The Problem:** Brokers miss emotional signals indicating client churn risk.

**Our Solution:** Autonomous sentiment scanning of negotiation threads via NLP.

**Example Alert:**
```text
⚠️ Risk Alert: Acme Corp Renewal
Sentiment trend: Positive → Neutral → Negative
Last email (Nov 18): Client mentioned "exploring other options"
```

---

### ✅ Innovation 3: Hallucination-Free Citations

**The Problem:** AI hallucinations erode trust.

**Our Solution:** Every claim includes a verifiable source citation.

**Example:**
- "Premium: $150,000 [Source: CRM Record #12345 ↗️]"
- "Client contacted us on Nov 15 [Source: Email Thread #67890 ↗️]"

---

## 7. Target Success Metrics

| Metric | Target Goal | Measurement Method |
|--------|------------|-------------------|
| **Time Saved** | 50% reduction | Compare "Manual Prep" (30 min) vs "Copilot Brief" (<15 min) |
| **Accuracy** | 100% Traceability | Every insight links to valid Source ID with clickable link |
| **Integration** | 4+ Systems | CRM, Outlook, Teams, Calendar working simultaneously |
| **Prioritization** | Grade A (90%+) | High-priority renewals have complete explainable breakdown |

---

## 8. Why Our Solution Wins

**Judges Evaluate On:**
- ✅ **Understanding:** We clearly articulate the "fragmented data crisis"
- ✅ **Feasibility:** Proven tech stack (FastAPI, React, Azure OpenAI) achievable in 3 weeks
- ✅ **Innovation:** EPS transparency, sentiment risk detection, hallucination-free citations
- ✅ **Technical Realism:** Production-ready tools, explicit no-storage architecture
- ✅ **Security Awareness:** Comprehensive OAuth, compliance, zero-persistence design

**Our Competitive Edge:**
- **Connector-First, Not Database-First:** We orchestrate, not duplicate
- **Trust Through Transparency:** Explainable scoring + source citations
- **AI as Copilot, Not Autopilot:** Brokers stay in control
- **Microsoft Ecosystem Native:** Deep integration with existing tools

---

## 9. Team & Contact Information

**Team Lead:** Akshay Singh (@ankit2000a)

**Project Repository:** https://github.com/ankit2000a/broker-copilot-challenge

**Submission Date:** November 21, 2025

**Contact Email:** akshay.singh@flame.edu.in

---

## 10. Conclusion

The Broker Copilot represents a paradigm shift: **from data silos to data orchestration**.

We're not building another database. We're building the **intelligent glue** that makes brokers superhuman.
