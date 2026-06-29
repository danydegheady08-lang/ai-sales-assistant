# AI Sales Assistant + Outreach Automation

A Node.js pipeline that automates hyper-personalized B2B outreach for sales and GTM teams.

## What it does

1. Reads a prospect list from a CSV file (name, company, email, LinkedIn URL, personalization hook)
2. Drafts a personalized cold email for each prospect using the Claude API
3. Pushes each draft directly to Gmail via the Gmail API — ready to review and send

No templates. Each email is written around a specific hook from the prospect's LinkedIn activity or recent work. The goal is one human-sounding email per prospect, not volume blasting.

## Stack

- Node.js
- Anthropic Claude API (claude-sonnet-4-6)
- Gmail API (OAuth2)
- CSV parsing with `csv-parser`
- Secure API routing via Cloudflare Worker proxy

## How it works

```
prospects.csv
     │
     ▼
outreach.js  ──►  Claude API (via Cloudflare proxy)
     │
     ▼
Gmail Draft (per prospect)
```

## Setup

```bash
npm install
```

Add your credentials to a `.env` file:

```
ANTHROPIC_API_KEY=your_key
GMAIL_CLIENT_ID=your_id
GMAIL_CLIENT_SECRET=your_secret
GMAIL_REFRESH_TOKEN=your_token
```

Run:

```bash
node outreach.js
```

## CSV format

```csv
first_name,last_name,company,email,hook
James,Whipp,Pivotal Partners,james@pivotalpartners.io,"saw your post on GTM hiring trends in SaaS"
```

## Context

Built as part of [Degheady Consulting](https://danydegheady08-lang.github.io/degheady-consulting-demos/) — an AI automation consultancy for B2B sales and finance teams.
