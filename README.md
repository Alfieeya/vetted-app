# Vetted

A candidate screening tool for ranking resumes against a job description, and auditing resumes for completeness - built as a single static web app, powered by the Gemini API.

> Built by me while working as an IT recruiter, to speed up my own resume screening and shortlisting.

**Live app:** https://alfieeya.github.io/vetted-app/

## What it does

### Rank Resumes
- Paste a job description (or drop a JD file straight into the box)
- Add any extra requirements not covered in the JD
- Upload any number of resumes (PDF, DOCX, or TXT)
- Click **Rank candidates** to get every candidate scored against the role

Each result shows the candidate's name and match score, with three expandable panels:
- **Matching skills** - what they demonstrably bring, with relevance
- **Required skills** - gaps against the role
- **Overall analysis** - a short written assessment of fit

### Updation Required
- Drop resumes to audit
- Click **Check resumes** to flag which ones look stale or incomplete - missing/vague dates, no current role, missing sections, unexplained gaps - with a plain-language explanation for each

## Setup

No installation, build step, or backend required — it's one HTML page.

1. Open the live link above (or open `index.html` locally in a browser)
2. Get a free Gemini API key at [aistudio.google.com/apikey](https://aistudio.google.com/apikey) (sign in with Google, click *Create API key*)
3. Paste the key into the **Gemini API key** box in the sidebar and click **Save**

The key is stored only in your own browser's local storage - it is never written into the code or the repo, and isn't sent anywhere except directly to Google's API.

## How it works

- Resume text is extracted entirely in the browser: [pdf.js](https://mozilla.github.io/pdf.js/) for PDFs, [mammoth.js](https://github.com/mwilliamson/mammoth.js) for DOCX, plain text for TXT
- The extracted text, JD, and any extra requirements are sent to the Gemini API (`gemini-3.1-flash-lite`), which returns structured JSON that the page renders into the result cards
- Nothing is stored server-side - there is no server. Refreshing the page clears results; re-run ranking/audit as needed

## Tech stack

- Plain HTML / CSS / JavaScript - no framework, no build tools
- [pdf.js](https://mozilla.github.io/pdf.js/) and [mammoth.js](https://github.com/mwilliamson/mammoth.js) (loaded via CDN) for in-browser file parsing
- [Google Gemini API](https://ai.google.dev/) for resume scoring and auditing

## Notes

- Gemini occasionally renames or retires model versions. If ranking/auditing stops working, check [ai.google.dev/gemini-api/docs/models](https://ai.google.dev/gemini-api/docs/models) for the current model name and update the `model` value in the fetch URL inside the script.
- Free-tier API keys have daily/per-minute rate limits — if you hit them, wait a bit and try again.
