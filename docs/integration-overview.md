# Integration Guide: Project Sage Workflow (n8n + GPT-4o + Google Drive + Discord)

---

## 🔄 Overview

This integration defines the full n8n workflow for **Project Sage**, Menashi Consulting's AI-powered intake and summarization pilot. It ingests PDFs from a Google Drive folder, uses GPT-4o to generate structured summaries, and routes them to a designated Discord channel.

---

## 📂 Tech Stack

- **n8n** – Orchestration layer
- **Google Drive** – Document source
- **OpenAI (GPT-4o)** – Summarization engine
- **Discord** – Output channel for summaries

---

## ⚙️ Node-by-Node Workflow

### 1. **Trigger: Google Drive Watch**

- **Node Type:** Google Drive → *Watch Files*
- **Setup:**
  - Connect Google OAuth2 credentials
  - Monitor a specific folder
  - Trigger on `.pdf` file additions

### 2. **Filter: File Type**

- **Node Type:** IF
- **Condition:** MIME type = `application/pdf`
- **Fallback:** Route other file types to a logging path

### 3. **Action: Download File**

- **Node Type:** Google Drive → *Download File*
- **Input:** File ID from trigger node

### 4. **Process: Extract Text from PDF**

- **Options:**
  - Use community **PDF Extractor Node** in n8n
  - Or use external PDF API (e.g. PDF.co, Webhook to AWS Lambda/pdf2text)

### 5. **Summarization: OpenAI GPT-4o**

- **Node Type:** OpenAI → *Chat Completion*
- **Model:** `gpt-4o`
- **Prompt Template:**

```text
You are an assistant summarizing legal/business documents. Provide:
1. A plain-English summary
2. Key parties
3. Dates or deadlines
4. Red flags or missing info

Document Content:
{{ $json["text"] }}
```

### 6. **Output: Post to Discord**

- **Node Type:** Discord → *Send Message*
- **Setup:**
  - Add your Discord bot to your server
  - Use a bot token via n8n credentials
  - Configure it to post in a summary-specific channel
- **Message Body:**

```
**Document Summary:**
{{ $json["summary"] }}

_File:_ {{ $json["fileName"] }}
_Timestamp:_ {{ $json["timestamp"] }}
```

### 7. **(Optional) Log to Airtable or Notion**

- Store: file name, summary, status, timestamp

### 8. **(Optional) Error Handling Node**

- Use *Execute Workflow on Error* node
- Send error alerts via email or webhook

---

## 🚨 Security Notes

- Sanitize inputs to remove sensitive PII before passing to GPT-4o
- Use secure tokens stored in n8n credentials manager
- Restrict Discord bot permissions to write-only for specific channels

---

## 📄 Output Example

- Summary in Discord with file name and timestamp
- Optional backup in Airtable or Notion
- Workflow logs available in n8n UI

---

> This integration serves as the technical backbone for **Project Sage**, Menashi's flagship AI intake automation pilot.

Let us know if you need a prebuilt `.json` export of the workflow.

