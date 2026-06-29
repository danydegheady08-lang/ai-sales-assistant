# AI Sales Assistant

> Turns post-call notes into personalized follow-up emails and CRM-ready summaries. Built for sales reps and founders who lose 20 minutes after every call doing the same manual writeup.

**[Live Demo](https://danydegheady08-lang.github.io/degheady-consulting-demos/sales_assistant_demo.html)**

---

## The problem

You finish a call. You have notes. You need to:
- Write a follow-up email that doesn't sound like a template
- Log the summary into your CRM
- Do this 5–10 times a day

Most people either skip it, do it badly, or spend time they don't have.

## What this does

Paste your raw call notes. The assistant returns:

1. A personalized follow-up email, written in the rep's voice, referencing specifics from the call
2. A clean CRM summary — deal stage, next steps, key objections, decision timeline

Takes about 8 seconds.

---

## Architecture

```
Post-call notes (text input)
         │
         ▼
  Cloudflare Worker Proxy
  (api key never touches client)
         │
         ▼
  Anthropic Claude API
  (claude-sonnet-4-6)
         │
         ▼
  Follow-up email + CRM summary
```

---

## Outreach automation (this repo)

Separate from the demo, this repo also contains the outreach pipeline used for Degheady Consulting's own B2B prospecting:

```
prospects.csv  →  outreach.js  →  Claude API  →  Gmail Draft
```

- Reads prospect list (name, company, email, personalization hook)
- Drafts a hyper-personalized cold email per prospect via Claude
- Pushes each draft directly to Gmail via OAuth2 — ready to review and send
- No templates. No blasting. One researched email per person.

### Stack

```
Node.js · Anthropic Claude API · Gmail API (OAuth2) · csv-parser
```

### Setup

```bash
npm install
```

```env
ANTHROPIC_API_KEY=your_key
GMAIL_CLIENT_ID=your_id
GMAIL_CLIENT_SECRET=your_secret
GMAIL_REFRESH_TOKEN=your_token
```

```bash
node outreach.js
```

### Prospect CSV format

```csv
first_name,last_name,company,email,hook
James,Whipp,Pivotal Partners,james@pivotalpartners.io,"saw your post on GTM hiring trends in SaaS"
```

---

## Part of

[Degheady Consulting](https://danydegheady08-lang.github.io/degheady-consulting-demos/) — AI automation for B2B sales and finance teams.

