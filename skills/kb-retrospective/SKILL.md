---
name: kb-retrospective
description: Write a blameless retrospective for the team knowledge base after an incident, outage, failed launch, data problem, or anything resolved that taught something. Use when the user says retro, retrospective, postmortem, post-mortem, incident write-up, or "what did we learn from".
---

# Retrospective

A retrospective records one resolved incident so the team does not relearn it. It is blameless: it names roles and systems, never people, including the team.

## Interview

Ask one question at a time. Skip anything the user has already answered. Pull detail from local notes, tickets, or logs the user points to.

1. What happened, and how was it noticed?
2. When did it start and end? (For the filename-style slug and the body's first line only.)
3. What was affected, and how badly? Plain terms; no customer or order data.
4. What was the root cause, and what made it possible?
5. What fixed it?
6. What changed so it does not happen again? If nothing, why not?
7. Where is the record: ticket, call, thread, document?

If the incident is still open, stop: a retrospective is for resolved incidents. Offer to save a short note instead, or come back when it is resolved.

## Draft

- `kind`: `retrospective`
- `slug`: `YYYY-MM-DD-short-subject`, using the date it started
- Title: short and specific, for example "Nightly import timed out after a plugin update"
- Body sections, in order: **What happened**, **Impact**, **Cause**, **Fix**, **What changed**. First line of the body: the date range.
- `sources`: every record from question 7
- `metadata`: `{ "started": "YYYY-MM-DD", "resolved": "YYYY-MM-DD", "affects": ["<system, site, or product>"] }`
- Links: `search` for each affected system, and link its page (a site page, for example) where the body first names it. Link earlier retrospectives on the same cause in **Cause**, and decisions that came out of it in **What changed**. Follow the Links section of `kb-save`.

Open follow-up work is not part of the retrospective. List it for the user at the end so they can ticket it.

## Finish

Follow the `kb-save` skill from step 3 (check the draft) through step 8. When suggesting who to tell, use the affected systems as the topic.
