# Recast

**One line:** Turns messy AI output into clean, valid JSON and shows every change that was made.  
**For:** Developers, automation builders, and anyone who needs reliable structured data from language models.  
**Status:** Live product (free trial + Pro) · https://recast-indol.vercel.app/  
**Role:** I designed and shipped this.

## The problem
Language models frequently produce almost-JSON that breaks in real workflows: single quotes instead of double quotes, Python-style `True`/`False`/`None`, trailing commas, markdown fences mixed with prose, truncated responses, or payloads buried inside larger text.  

These failures force people to manually clean the output or write fragile scripts. Existing online tools often upload the data to a server, which creates privacy and trust issues. This happens constantly when using LLMs to generate structured data for APIs, databases, or automation tools.

## What I shipped
- Client-side engine that repairs common AI JSON failures and produces valid JSON
- Clear, plain-language list of every change that was applied
- Support for single quotes, language constants, trailing commas, fences + chatter, truncation, and embedded payloads
- Optional JSON Schema validation
- Single and Batch modes
- Fully local execution — data never leaves the browser
- Free trial (10 cleans) + Pro

## Hardest engineering problem
Building a reliable multi-step repair process that could handle real-world messy LLM output without dropping data, inventing values, or becoming a black box. The solution prioritizes data integrity and explicit change reporting over aggressive guessing.

## How I used AI
I built Recast with Cursor and Grok. I used AI heavily for implementation speed, but I made the final decisions on architecture, repair order, privacy model, and what the tool was (and was not) allowed to change.

## Tradeoffs
- **Reliability:** Client-side only. Prioritizes “nothing was dropped” and transparent fixes.
- **Cost:** Core cleaning runs entirely in the browser (no server inference cost).
- **Privacy:** Data never leaves the page. No uploads, no server-side processing of user content.

## Evidence
- Live product: https://recast-indol.vercel.app/
- Screenshots in the repository
- Source is private. Collaborator access available in interviews.

## What’s next
Continuing to improve the repair engine and expand Pro capabilities.

## Eval set
Fixtures: [`evals/cases.md`](evals/cases.md)
