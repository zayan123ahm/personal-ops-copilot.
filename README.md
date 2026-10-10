# Personal Ops Copilot

A multi-agent AI assistant that answers questions about your meetings, emails and sales leads from one simple chat page.

*Live demo:* personal-ops-copilot.netlify.app
*Built by:* Zayan, SMIT / Saylani Capstone Project

## Problem

Busy professionals and small teams keep their work scattered across calendars, inboxes and lead sheets. To answer a simple question like "What meetings do I have?" or "Which leads need follow-up?", they have to open several apps and search manually. This wastes time and things get missed.

## Target Users

- Freelancers and small business owners
- Sales and support teams who track leads and emails daily
- Anyone who wants a quick daily overview without opening multiple tools

## Solution

Personal Ops Copilot is a single chat interface. The user types a question, and the system routes it to the right AI agent:

| Question contains | Agent | Data source |
|---|---|---|
| "meeting" | Calendar agent | calendar_events |
| "mail" | Email agent | emails |
| "lead" | Leads agent | leads |

Each agent fetches the relevant rows, summarizes them with Google Gemini, and returns a clear, readable answer in the chat.

## Architecture


index.html (chat UI)
      |
      |  GET ?question=...
      v
Make.com Webhook
      |
      v
   Router (keyword filters)
   |        |         |
Calendar   Email     Leads
   |        |         |
Supabase Search Rows (per route)
   |        |         |
Text Aggregator
   |        |         |
Google Gemini (summarize)
   |        |         |
Webhook Response (with CORS header)
      |
      v
Answer shown in the chat page


## Tech Stack

- *Make.com*: workflow automation, webhook, router and agent logic
- *Supabase*: PostgreSQL database (calendar_events, emails, leads)
- *Google Gemini*: generates the natural-language answers
- *Google Calendar / Gmail APIs*: source of meeting and email data
- *HTML, CSS, JavaScript*: lightweight frontend (single file)
- *GitHub + Netlify*: code hosting and deployment

## How to Use

1. Open the live demo link.
2. Click a suggested question or type your own, for example:
   - "What meetings do I have?"
   - "Show my emails"
   - "Which leads need follow-up?"
3. The matching agent replies in a few seconds.

## Project Files

- index.html: the complete chat interface (the Make.com webhook URL is set in the WEBHOOK constant)
- README.md: project documentation

## Notes

- The Make.com Webhook response modules send the header Access-Control-Allow-Origin: * so the page can read the answers.
- Questions that do not match meetings, emails or leads get a short help message.
