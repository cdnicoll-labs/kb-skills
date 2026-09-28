---
name: kb-decision
description: Record a decision in the team knowledge base, with why it was made and what it changes. Use when the user says we decided, we agreed, record the decision, decision log, ADR, or when a call or thread settled a direction that others need to follow.
---

# Decision

A decision record captures one choice so nobody has to reconstruct why later. It states what was decided, not who argued for what.

## Interview

Ask one question at a time. Skip what is already known.

1. What was decided, in one or two sentences?
2. What problem or question forced the decision?
3. What alternatives were considered, and why were they not chosen?
4. What changes because of it? Who or what has to do something differently?
5. What would make it worth revisiting?
6. When was it decided, and where is the record: call, thread, document, ticket?
7. Does it replace an earlier decision? If so, `search` for it.

## Draft

- `kind`: `decision`
- `slug`: `YYYY-MM-DD-short-subject`, using the date decided
- Title: the decision itself, for example "Merge feature branches to main; the owner deploys"
- Body sections, in order: **Decision**, **Why**, **Alternatives not taken**, **Consequences**, **Revisit when**
- `sources`: every record from question 6
- `metadata`: `{ "decided": "YYYY-MM-DD" }`, plus `"supersedes": "<slug>"` when it replaces an earlier decision
- Links: in **Why** or **Consequences**, link the documents the decision rests on or changes, following the Links section of `kb-save`. When it supersedes an earlier decision, **Decision** ends with `Supersedes [[<slug>]].`

If it supersedes an earlier decision, also propose an update to that document: add a first line `Superseded by [[<new slug>]].` Save both only on the user's yes.

## Finish

Follow the `kb-save` skill from step 3 (check the draft) through step 8.
