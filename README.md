# Fair AI Resume Screener

A tool that scores a candidate's resume against a job's requirements using AI — and then checks its own work, so you can see not just **"is this a strong candidate?"** but **"can I actually trust this score?"**

## Try it now

👉 **[Open the live tool](https://claude.ai/code/artifact/1daf4be6-265e-48e3-8815-1c8ba1fd67df)**

No install, no account setup beyond your own Claude login, nothing to configure. Open the link, confirm the job details, paste in a resume (or use the example one that's pre-filled), and click **Score this candidate**.

> The link above is the only place this tool actually works. This GitHub repo holds the source code and a preview page — see [Why the code here doesn't fully run](#why-the-code-here-doesnt-fully-run) below.

## What this is for

Most AI resume screeners just hand you a number and expect you to trust it. This one is built around a different question: **an AI score is only useful if you also know how reliable it is.**

So every time you check a candidate, the tool does two separate things:

1. **Scores the candidate** — reads the resume, compares it to the job's requirements, and gives an overall fit score with a plain-English summary of their strengths and gaps.
2. **Tests its own score for bias and consistency** — it re-runs the same resume with small, controlled changes (like swapping the candidate's name, or changing how long a career break lasted) to check whether the AI's score is being influenced by things it shouldn't be influenced by. If a check turns up something concerning, the tool flags it and recommends a human take a look — it never lets a good-looking score override a check that failed.

## What it checks for

| Check | What it's looking for |
|---|---|
| **Name–Gender Bias** | Does the score change if the candidate's name sounds like a different gender or ethnicity? It shouldn't. |
| **Accommodation Bias** | Does mentioning a workplace accommodation or caregiving responsibility ever count against someone? It shouldn't. |
| **Career-Gap Bias** | Does the *length* of a career break move the score by itself? It shouldn't. |
| **Education & GPA Consistency** | If school or GPA changes, does that spill over into unrelated parts of the score? It shouldn't. |
| **Prompt-Injection Robustness** | Could someone manipulate their score by hiding a fake instruction inside their resume? It shouldn't work. |

Every candidate is measured against the exact same job requirements, scoring weights, and fairness rules — set once at the start of a session — so comparisons between candidates stay fair.

## This is an early version (MVP)

A few things to know before using this for anything real:

- **Resume text extraction is basic.** Uploading a PDF pulls out raw text using a general-purpose reader, not a commercial resume-parsing service. It won't identify fields like work history or education separately, and can scramble multi-column layouts. A production version should use a dedicated resume-parsing API instead.
- **Nothing is saved anywhere.** Each session lives only in your browser tab. There's a "download report" button if you want to keep a record of an evaluation, but nothing is stored on a server.
- **The fairness checks measure *sensitivity*, not proof.** A flag means "this is worth a second look," not "this is confirmed bias." That's true even when a check passes — it's evidence the score held up under one kind of test, not a guarantee.
- **The default job (AI Deployment Strategist) and its scoring weights are a starting example**, meant to be reviewed and adjusted for whatever role you're actually hiring for.

## Why the code here doesn't fully run

`index.html` in this repo is the exact same file published at the link above — this repo also serves it as a plain webpage via GitHub Pages, so you can preview the interface and read the code without opening Claude.

But the actual scoring only works when the page is opened *inside Claude* — that's what lets it ask an AI to read a resume without you needing your own API key or server. Opened as a plain webpage (like the GitHub Pages copy), you can click through the setup screens and see how everything is laid out, but the **Score this candidate** button will be disabled, since there's no Claude connection to send the request to.

If you want to actually use the tool, use the [live link](https://claude.ai/code/artifact/1daf4be6-265e-48e3-8815-1c8ba1fd67df) at the top of this page.

## Nothing you paste is stored by us

Resume text you enter is sent only to Claude (under your own account) to produce the evaluation, and is scanned for things like email addresses and phone numbers, which are automatically removed before scoring. Nothing is written to a database or server that this project controls.
