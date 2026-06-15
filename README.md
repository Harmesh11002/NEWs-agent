# 📰 AI-Powered News Automation Workflow (n8n & Groq)
<img width="1096" height="647" alt="image" src="https://github.com/user-attachments/assets/97bdae77-8b3e-4cc4-97c3-a13527a3476a" />

An automated, multi-agent AI pipeline built in **n8n** that crawls live industry news daily, filters the top articles, passes them through a conversational AI agent for synthesis, and formats the final output to be sent automatically via messaging networks (like WhatsApp or SMS).

---

## 🚀 Workflow Architecture

The workflow is designed around a looping item processor that ensures individual articles are carefully analyzed rather than bundled into a single messy prompt.

```text
[EveryDay Timer] ──> [Fetch News from NewsAPI] ──> [Extract Articles] ──> [Limit to Top 2]
                                                                                │
  ┌─────────────────────────────────────────────────────────────────────────────┘
  ▼
[Loop Over Items] ──(Loop)──> [AI Agent + Groq Llama 3] ──> [Format Message via JS Code]
  │
  └──(Done)──> [Format WhatsApp Template] ──> [Send SMS/WhatsApp Message]
