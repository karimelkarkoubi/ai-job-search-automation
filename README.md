# 🤖 AI Job Search Automation — N8N Pipeline

> Automated end-to-end recruitment pipeline powered by LLM, scraping job boards, scoring opportunities, and generating tailored application documents — fully on autopilot.

---

## 🧠 What It Does

Job hunting is repetitive. Scraping listings, filtering irrelevant roles, rewriting your CV summary, drafting cover letters — it all takes hours. I automated the entire process.

This pipeline runs on demand, scrapes hundreds of job postings across multiple markets, filters only the relevant ones using AI scoring, and outputs a ready-to-send application document for each match — tailored CV sections + cover letter in the right language. Everything is logged automatically to Google Sheets.

---

## ⚙️ How It Works

**1. Trigger & Configure**
Manual trigger with an editable URL node — set search query, location, market, and language before each run.

**2. Scrape**
Apify scrapes LinkedIn and Jobs.ch and returns raw job feed data.

**3. Loop & Retrieve CV**
For each posting, the pipeline fetches the latest CV from Google Docs as the base document.

**4. Filter with LLM**
Each job is scored by an LLM against the candidate profile. A JavaScript node parses the verdict. Only matching roles pass through (~15% pass rate from 100+ raw results).

**5. Tailor — Two Parallel Branches**
- **Tailor CV node**: rewrites City, Header, Summary, and Skills sections for the specific role
- **Cover Letter node**: generates a 3-paragraph cover letter (~250 words), language auto-detected (FR / EN / IT)

Both outputs are converted from HTML to Markdown.

**6. Output**
A new Google Doc is created (CV sections on page 1, cover letter on page 2), then logged as a new row in Google Sheets with job title, company, location, and document link.

---

## 🛠️ Stack

| Tool | Role |
|------|------|
| N8N | Workflow orchestration |
| Apify | LinkedIn + Jobs.ch scraping |
| LLM | Job scoring + document generation |
| Google Docs | CV retrieval + application output |
| Google Sheets | Job tracking & logging |

---

## 📸 Screenshots

### Workflow Canvas
![N8N Workflow](main/n8n_canvas.png)

### Google Sheets Output
![Google Sheets](main/google_sheets.png)

---

## 📌 Key Results

- **100+ job postings** scraped per run across multiple markets (Lyon, Geneva, Basel)
- **~15% pass rate** after LLM filtering — only relevant roles
- **~80% reduction** in manual application time
- **Multilingual output**: French, English, Italian — auto-detected per job

---

## 🔒 Note

Workflow logic, prompts, and JSON configuration are kept private. This repo documents the architecture and outputs only.

---

*Built by Karim El Karkoubi — [LinkedIn](https://linkedin.com/in/karimelkarkoubi)*
