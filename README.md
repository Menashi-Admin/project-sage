# Project Sage: Smart Intake + Document Summarization Workflow

---

## 🔄 Project Overview
**Codename:** Project Sage  
**Goal:** Deploy a reusable AI workflow that takes uploaded documents, summarizes content, and routes to Airtable/Slack for action—enabling secure, low-code automation for modern client intake and review.  
**Use Case:** Client onboarding, legal intake, compliance reviews

---

## ⏳ Timeline (2 Weeks Total)
- **Week 1:** Build & Test Core Workflow
- **Week 2:** Polish, Document, Demo-ready Assets

---

## 📊 Task Board

### 1. Intake & Trigger Setup
- [ ] Create Typeform/Tally form (client info + file upload)
- [ ] Configure n8n webhook to trigger on form submission

### 2. File Handling + AI Summary
- [ ] Parse PDF content (use n8n + external PDF tool if needed)
- [ ] Send content to OpenAI API with summarization prompt
- [ ] Extract entities (names, dates, clauses) for tagging

### 3. Routing + Storage
- [ ] Write summary + metadata to Airtable (or Notion database)
- [ ] Send Slack/Email notification with summary link
- [ ] Log actions in audit trail (timestamp, user, action)

### 4. Security & Validation
- [ ] Validate file type + block invalid inputs
- [ ] Limit OpenAI prompt exposure (strip PII if needed)
- [ ] Add basic error handling + retry logic in n8n

### 5. Documentation & Demo Prep
- [ ] Create flow diagram (Whimsical, Lucidchart, or Canva)
- [ ] Record Loom walkthrough of the process
- [ ] Build Notion-based client-facing summary (with screenshots)

### 6. Feedback Loop (Optional)
- [ ] Add review/approval toggle in Airtable
- [ ] Route flagged entries to specific Slack channel or email

---

## 🏛️ Output Goals
- [ ] 1 Workflow (Live)
- [ ] 1 Walkthrough Video (Loom)
- [ ] 1 Documentation Page (Notion or PDF)
- [ ] 1 POC Pitch Slide (for LinkedIn, email outreach)
