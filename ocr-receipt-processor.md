# OCR Receipt Processor — n8n Automation

## Problem
Manually transcribing data from receipts and invoices (vendor, date, amount, line items) into a spreadsheet is slow and error-prone, especially when handling multiple documents at once.

## Solution
An n8n workflow that accepts one or more receipt images/PDFs through a form, extracts structured data using AI vision analysis, normalizes it into a consistent format, and appends it directly to a Google Sheet — no manual typing required.

## How it works
1. **Form submission (Tally)** — user submits one or more file URLs.
2. **Validation** — checks that files were actually provided before continuing.
3. **Split File URLs** — a Code node parses the file list into individual items.
4. **Per-file processing** — each file is downloaded and analyzed with an AI vision model to extract raw content, then passed through an LLM chain to convert it into structured JSON (vendor, date, total, items).
5. **Merge** — all processed files are combined into a single result set.
6. **Normalization** — a final LLM pass ensures every record follows the same JSON schema, regardless of receipt format or language.
7. **Google Sheets** — normalized data is appended automatically as new rows.

## Tech stack
- n8n (workflow engine)
- OpenAI (vision + text analysis via LLM Chain nodes)
- Google Sheets API
- JavaScript (Code node) for parsing

## Result
- Manual entry per receipt: ~2–3 minutes
- Automated processing: ~10–15 seconds, zero manual typing

## Known limitation & planned improvement
The current version routes files through a fixed number of parallel branches. A planned refactor replaces this with a `Loop Over Items` node so the workflow scales to any number of files without further architecture changes.

---
*Workflow JSON included in this repo — test data only, no real credentials or client information.*
