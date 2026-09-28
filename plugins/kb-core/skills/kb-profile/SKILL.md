---
name: kb-profile
description: Write or update your own profile in the team knowledge base (a kb-<client> MCP server) by answering a few questions, so teammates know your role, what to come to you for, and how you like to work. Use when someone says add my profile, introduce me, who I am, update my profile, or on a person's first day after they connect to the knowledge base. Only ever for the person asking, never about someone else.
---

# Your profile

One page per person, written by that person, so anyone on the team can ask "what does <name> do?" or "who handles hosting?" and get an answer the person themselves agreed to. It is the first thing most people save.

Finish by following the closing steps of `kb-save`, with the differences below. Its rules for anything saved apply here too.

## Only your own

**A profile is written by the person it describes, and nobody else.** That is the whole point of this skill: what the team knows about a person is what that person chose to say.

- Take identity from `whoami`. The profile is for that handle and no other.
- If asked to write or change someone else's profile, decline plainly, and offer a short message the user can send that person instead, suggesting they add their own.
- Before writing, `get_document` the slug (their handle). If a document with that slug exists and its `author` is not this person, **stop**. Do not overwrite it. Tell them what is there and who wrote it, and ask them to raise it with that person or whoever administers the knowledge base.
- If their own profile exists, propose an update to it rather than starting over.

## Ask, one question at a time

Offer to skip any of them. A short profile they are happy with beats a full one they are not.

1. **Your role on this team,** in a sentence. Not a job title for its own sake; what you actually do here.
2. **What people should come to you for.** The questions you are the right person to answer.
3. **What to take elsewhere, and to whom.** Things people often bring you that someone else handles better. Teammates may be named; client staff by role.
4. **How you like to work.** Which channels, whether you prefer written or a quick call, and roughly how fast you reply.
5. **Time zone and usual working hours.**
6. **Languages you work in.**

## Never in a profile

- Anything personal beyond work: family, health, home, personal circumstances.
- Personal contact details. Name the channel ("Slack", "email"), never a phone number or address.
- Opinions about other people, or about clients.
- **Current workload, availability this week, or what you are working on right now.** It is stale in days and belongs in the ticketing system or a message. A profile says what stays true.

If an answer drifts into any of these, leave that part out and say why, briefly.

## The page

- **Kind:** `profile`
- **Slug:** their handle, exactly as `whoami` returns it
- **Title:** `<display name>, <role in a few words>`
- **Domains:** empty, so the whole team can find it
- **Sources:** `{"title": "Written by <display name>", "note": "<date>"}`

Body, in this order, leaving out any section they skipped:

```markdown
## Role
## Come to me for
## Take elsewhere
## How I work
## Hours
## Languages
```

Link to documents they own or maintain where the text mentions them, following the Links rules in `kb-save`.

## Finishing

Follow `kb-save` steps 3 to 6 and 8: check the draft against the rules, confirm the client and person with `whoami`, show the whole page, save only on an explicit yes, report the slug.

**Skip step 7**, the who-to-tell note. A profile is not a topic `who_knows` can match on. Instead, offer one line they can post to the team if they want to:

> My profile is in the {client} knowledge base. Ask your agent "what does {first name} do?" if you ever wonder who to ask.
