# 📰 AI-Powered News Automation Workflow (n8n & Groq)
<img width="1096" height="647" alt="image" src="https://github.com/user-attachments/assets/97bdae77-8b3e-4cc4-97c3-a13527a3476a" />

![n8n](https://img.shields.io/badge/Automation-n8n-FF6C37?style=for-the-badge&logo=n8n&logoColor=white)
![Groq](https://img.shields.io/badge/LLM_Engine-Groq_Cloud-F54C1E?style=for-the-badge)
![API](https://img.shields.io/badge/Data_Source-NewsAPI-0052CC?style=for-the-badge)

An elegant, autonomous multi-agent pipeline built in **n8n** that monitors global news endpoints daily, extracts targeted topics, processes them through isolated AI evaluation loops, and delivers highly summarized briefings straight to your messaging channels.

---

## 🎯 The Core Problem This Solves (Insights)

Most basic AI workflows try to bundle 10 different news articles into one massive prompt block and send it to an LLM. This causes massive issues:
* **Token Bloat & High Cost:** Sending massive raw text walls wastes API tokens.
* **Context Loss / Hallucinations:** Large Language Models naturally lose focus on items buried in the middle of a massive prompt.
* **Lack of Formatting Structure:** Raw bulk outputs usually format poorly on mobile messaging apps.

### 💡 The Solution: Isolated Item Looping
This architecture introduces a **Loop Over Items** structure. By separating data streams into distinct, sequential operations, the **Groq Llama 3 Agent** evaluates each news story inside its own clean environment. This guarantees hyper-accurate summaries, retains precise source context, and keeps output templates razor-sharp.

---------------------------------------------------------------------------------------------------------

⚙️ Deep Dive Component Breakdown:

1.The Pulse (EveryDay Trigger): Chronologically kicks off the workflow daily without human intervention.

2.Data Harvesting (Fetch AI News from NewsAPI): Connects to remote JSON endpoints, passing customizable queries (e.g., Tech, Economics, Business).

3.Data Distillation (Limit to Top 2): Actively filters workload to prevent API rate-limits and token exhaustion, prioritizing high-value alerts.

4.The Evaluation Engine (Loop Over Items + Groq Chat Model): Seamlessly sequences items into an advanced inference engine running on Groq Cloud for rapid, millisecond-level summarization.

5.Payload Compilation (JavaScript Code): Efficiently stitches independent summaries into a cohesive message array.

6.Last-Mile Delivery (WhatsApp/SMS Gateway): Formats structural spacing and alerts your personal device.

---------------------------------------------------------------------------------------------------------

🛠️ Prerequisites & Secure Setup
To set up this pipeline, ensure you have API tokens from the following platforms:

  1.n8n: A self-hosted or cloud instance.

  2.NewsAPI: A free developer key from NewsAPI.org.

  3.GroqCloud: An API authorization token from the Groq Cloud Console.

---------------------------------------------------------------------------------------------------------

📥 Deployment Instructions
  1.Clone/Download: Grab the News WM.json file directly from this repository.

  2.Import to Canvas: Open your n8n workspace, click the Three Dots (...) menu button in the top-right corner, and select Import from File.
(Alternatively: Open the JSON file, copy all text, click on your blank n8n canvas, and press Ctrl + V / Cmd + V).

  3.Configure the News Node: Open the Fetch AI News from NewsAPI node parameters:

   i.Set Authentication to None.
   ii.Under Query Parameters, add a property named apiKey and insert your token.

  4.Connect LLM Credentials: Open the red-flagged Groq Chat Model sub-node, click the credentials dropdown, select Create New Credential, and add your gsk_... key.

  5.Activate: Toggle the workflow from Inactive to Active in the top right to let it run autonomously!

---------------------------------------------------------------------------------------------------------

🛠️ Common Troubleshooting & Fixes

❌ Error: Credentials not found / Query Auth Failure
   1.Why it happens: The HTTP node is looking for an external login profile even though your API key is already attached.

   2.The Fix: Open the Fetch AI News node, locate the Authentication field, and explicitly change it from Generic Credential Type to None.

❌ Error: [object Object] or invalid syntax inside Expression Boxes
  1.Why it happens: Writing regular paragraphs inside n8n's Expression Mode breaks the JavaScript engine parser.

  2.The Fix: Ensure regular text boxes are toggled to Fixed Mode. If you must use Expression Mode, cleanly wrap your strings in quotes and concatenate with plus signs:

---------------------------------------------------------------------------------------------------------
JavaScript
{{ "Topic Summary: " + $json.output + " - Checked Daily." }}

---------------------------------------------------------------------------------------------------------
## 🚀 Workflow Architecture

```text
[EveryDay Timer] ──> [Fetch News from NewsAPI] ──> [Extract Articles] ──> [Limit to Top 2]
                                                                                │
  ┌─────────────────────────────────────────────────────────────────────────────┘
  ▼
[Loop Over Items] ──(Loop)──> [AI Agent + Groq Llama 3] ──> [Format Message via JS Code]
  │
  └──(Done)──> [Format WhatsApp Template] ──> [Send SMS/WhatsApp Message]








