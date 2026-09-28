---
name: kb-ingest
description: Turn raw material (a meeting transcript or summary, an email thread, a chat export, a long document) into knowledge-base documents without storing the raw material. Use when the user pastes or points at a call, thread, or document and wants what matters captured for the team.
---

# Ingest

Raw material stays where it lives: the meeting recorder, the inbox, the drive. What reaches the knowledge base is the facts and decisions it contains, rewritten, with a pointer back to the original.

## Steps

1. **Read all of it first.** Save nothing yet.
2. **List candidates.** Each is one fact, decision, lesson, or change to something already documented that would still be true and useful to someone else on the team in a month. Most of a transcript will not qualify. Leave out:
   - small talk, opinions about people, and anything personal
   - client staff names (use roles)
   - open work, next steps, and status (list these separately for the user to ticket)
   - credentials, prices from client systems, customer data
3. **Check what exists.** For each candidate, `search` the knowledge base. A candidate that changes an existing document is an update to it, not a new one.
4. **Show the plan.** A short table: candidate, new or update (with slug), kind, one line on the content. Then the list of open work you left out. Ask which to keep.
5. **Draft each kept item.** Use `kb-decision` for decisions and `kb-retrospective` for resolved incidents; otherwise draft as in `kb-save`. Every draft's `sources` points to the original: title, date, and link or identifier (for example the recording URL or email subject). Quote only a short passage when the exact wording is the point, with the speaker as a role.
6. **Save one at a time**, following the `kb-save` skill from step 3 through step 8 for each. Suggest who to tell once at the end, not after every document.

Never save the transcript, the thread, or a summary of the whole meeting as a document.
