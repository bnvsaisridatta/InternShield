# InternShield

A tool that screens internship offers for common fraud patterns and explains *exactly* why an offer looks risky — in plain language, not a black-box score.

**Live demo:** [InternShield](https://bnvsaisridatta.github.io/InternShield/)

---

## Why this exists

Internship and "work from home" scams are a real and growing problem for students — fake postings ask for registration fees, security deposits, or personal financial information before any real screening happens. InternShield was built to give students a fast, independent way to sanity-check an offer before acting on it.

## Two approaches, one problem

This repo contains two implementations of the same idea, built to explore a real engineering tradeoff: **LLM reasoning vs. rule-based transparency.**

| | `/api-version` | `/rule-based-version` |
|---|---|---|
| **Engine** | Gemini API (LLM reasoning over posting text) | Pure JavaScript heuristics — keyword scanning, regex, weighted scoring |
| **Stack** | Next.js | Single-file HTML/CSS/JS, zero dependencies |
| **Cost / latency** | API call per check, subject to rate limits and API cost | Instant, free, runs entirely client-side |
| **Explainability** | Model-generated reasoning (less predictable) | Every flag is a named rule with a fixed, auditable weight |
| **Offline use** | Requires internet + API key | Works fully offline, no server, no data leaves the browser |
| **Best for** | Nuanced, unstructured text where wording matters | Fast, transparent, zero-cost screening at scale |

Building both surfaced a genuine design question: an LLM can catch subtler fraud patterns buried in phrasing, but a rule-based engine is faster, free to run, and lets the end user see *precisely* which signal triggered the result — which matters a lot when the person reading it isn't technical and needs to trust the verdict.

## How the rule-based version works

- **Checkbox signals** — direct yes/no fraud indicators (fee requested, no interview conducted, informal-only communication channels, unverifiable company presence, artificial urgency).
- **Keyword scanning** — regex patterns run against any pasted job description or message to catch fee/deposit language, unrealistic earnings claims, urgency phrasing, and requests for sensitive data (OTP, bank details, ID numbers).
- **Email domain check** — flags recruiter contacts using free email providers (Gmail, Yahoo, etc.) instead of a company domain.
- **Weighted scoring** — each triggered signal adds a fixed point value; the total maps to a Low → Critical risk band.
- **Explainable output** — a risk gauge plus an itemized list of every flag that fired, its point weight, and a plain-language reason it matters.

Everything runs client-side in the browser. Nothing typed into the form is uploaded, logged, or sent to any server.

## Tech stack

- Vanilla HTML, CSS, JavaScript (rule-based version) — no build step, no external requests, no dependencies
- Next.js + Gemini API (API version)

## Disclaimer

This is a heuristic screening tool, not legal or professional advice. It's meant to help surface red flags for a second look — always verify an offer directly with the company through official channels.

## Author

Bhagavatula N V Sai Sri Datta
[GitHub](https://github.com/bnvsaisridatta) · [LinkedIn](https://linkedin.com/in/bnvsaisridatta)
