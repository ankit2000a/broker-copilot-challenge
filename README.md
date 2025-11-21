# Broker Copilot Challenge - Techfest 2025-26

**Renewal Orchestration Assistant for Insurance Brokers**

## Overview

This repository contains our submission for the Techfest 2025-26 Broker Copilot Challenge - an intelligent assistant that helps insurance brokers manage policy renewals efficiently by connecting with existing systems (CRM, email, calendar, Teams, broker apps) through secure connectors.

## Challenge Objective

Build a proof-of-concept "Broker Copilot" that:
- ✅ Automatically populates renewal pipelines from connected data sources
- ✅ Prioritizes upcoming policy expiries with explainable scoring
- ✅ Generates one-page renewal briefs summarizing key insights
- ✅ Drafts template-based outreach emails
- ✅ Recommends negotiation actions and tracks renewal progress

**Goal:** Reduce broker preparation time by 50%+, increase renewal speed, and standardize outcomes.

## Key Constraint

🚫 **NO document ingestion, RAG, or vector databases**  
✅ **Connector-first, in-context data synthesis ONLY**

All data is fetched live from source systems, processed in-memory, and immediately discarded.

## Repository Structure

```
broker-copilot-challenge/
├── round1/                  # Round 1 Submission (Due: Nov 23, 2025)
│   ├── proposal.md          # 2-page proposal document
│   ├── architecture.md      # Technical architecture details
│   └── presentation/        # Optional slide deck
├── round2/                  # Round 2 Prototype (Due: Dec 15, 2025)
│   ├── backend/            # Backend services and connectors
│   ├── frontend/           # Web dashboard
│   ├── docs/               # Technical documentation
│   └── demo/               # Demo scripts and walkthrough
├── docs/
│   ├── ARCHITECTURE.md     # System architecture
│   ├── SECURITY.md         # Security & privacy approach
│   └── API.md              # API documentation
└── README.md               # This file
```

## Timeline

| Date | Event |
|------|-------|
| Nov 20, 2025 | Registration Deadline ✅ |
| **Nov 23, 2025** | **Round 1 Submission** 📝 |
| Dec 15, 2025 | Round 2 Prototype Submission |
| Dec 22-24, 2025 | Final Presentation |

## Round 1 Submission Checklist

- [ ] Problem understanding documented
- [ ] Architecture diagram created
- [ ] Technology stack defined
- [ ] Security approach documented
- [ ] Implementation timeline prepared
- [ ] Unique innovations identified
- [ ] 2-page proposal/5-slide deck finalized
- [ ] Submitted via [Google Form](https://forms.gle/fUf65DxS6d598jR79)

## Core Technologies (Planned)

**Backend:** Python FastAPI / Node.js Express  
**Connectors:** Microsoft Graph API, CRM APIs (Salesforce/AMS)  
**AI/LLM:** Azure OpenAI GPT-4 (prompt-based synthesis)  
**Frontend:** React + Next.js + Tailwind CSS  
**Auth:** OAuth 2.0 / MSAL  
**Deployment:** Azure App Service / Docker

## Key Features

### 1. Multi-System Connectors
- CRM (AMS, Salesforce)
- Email (Outlook via Microsoft Graph)
- Calendar (Outlook Calendar)
- Microsoft Teams
- Broker Applications

### 2. Intelligent Prioritization
- Multi-factor explainable scoring
- Premium at risk analysis
- Time-to-expiry urgency
- Claims history impact
- Carrier responsiveness tracking

### 3. One-Page Renewal Briefs
- Auto-generated summaries
- Source attribution for every data point
- Clickable links to original records
- Suggested next actions

### 4. Template-Based Outreach
- Editable email templates
- Auto-fill client/policy data
- Schedule and send via connected systems
- Track response rates

### 5. Connector-Backed Q&A
- Natural language queries
- Answers from live connector data
- Confidence scoring
- Source links for verification

### 6. Dashboards & Analytics
- Upcoming renewals overview
- Win/loss tracking
- Template effectiveness
- Broker performance metrics

## Innovation Highlights

🎯 **Explainable AI Prioritization** - Visual decision trees showing exact score calculation  
🧠 **Sentiment Analysis** - NLP on email threads to detect client satisfaction signals  
📊 **Predictive Analytics** - Win/loss probability and optimal timing recommendations  
🤝 **Teams Integration** - Real-time collaboration workspace with shared briefs  
📱 **Mobile-First** - PWA with voice commands and push notifications

## Security & Privacy

- OAuth 2.0 for all external connections
- In-memory processing only (no data storage)
- All API calls over HTTPS/TLS 1.3
- Source attribution and audit trails
- GDPR/HIPAA compliance ready
- Granular user consent management

## Success Metrics

- **Integration Coverage:** 80%+ of required systems
- **Answer Accuracy:** 80%+ with source verification
- **Time Savings:** 50%+ reduction in prep time
- **Source Traceability:** 90%+ of answers with correct citations
- **Usability:** 4/5+ broker satisfaction rating

## Team

[Add team member names and roles]

## License

[Add license information]

## Contact

For questions or feedback, please open an issue or contact [your email].

---

**Last Updated:** November 21, 2025  
**Challenge:** Techfest 2025-26 - Broker Copilot Challenge