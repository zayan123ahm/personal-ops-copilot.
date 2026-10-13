# Personal Ops Copilot
A multi-agent AI assistant that answers questions about your meetings, emails and sales leads from one simple chat page.

- **Live demo:** personal-ops-copilot.netlify.app 
- **Built by:** Zayan, SMIT / Saylani Capstone Project

## Problem
Busy professionals and small teams keep their work scattered across calendars, inboxes and lead sheets. To answer a simple question like "What meetings do I have?" or "Which leads need follow-up?", they have to open several apps and search manually. This wastes time and things get missed.

## Target Users
- Freelancers and small business owners
- Sales and support teams who track leads and emails daily
- Anyone who wants a quick daily overview without opening multiple tools

## Solution
Personal Ops Copilot is a single chat interface. The user types a question, and the system routes it to the right AI agent:

| Question contains | Agent | Data source |
| --- | --- | --- |
| "meeting" | Calendar agent | calendar_events |
| "mail" | Email agent | emails |
| "lead" | Leads agent | leads |

Each agent fetches the relevant rows, summarizes them with Groq AI (Qwen-3.8-27B), and returns a clear, readable answer in the chat.

## Architecture
```text
index.html (chat UI) 
  | 
  | GET ?question=... 
  v 
Make.com Webhook 
  | 
  v 
Router (keyword filters) 
  |----------|----------| 
Calendar   Email      Leads 
  |----------|----------| 
Supabase Search Rows (per route) 
  | 
  | 
Text Aggregator 
  | 
  | 
Groq AI / Qwen (summarize) 
  | 
  | 
Webhook Response (with CORS header) 
  v 
Answer shown in the chat page
