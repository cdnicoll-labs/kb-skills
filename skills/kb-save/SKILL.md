---
name: kb-save
description: Save knowledge to the team's shared knowledge base (a kb-<client> MCP server). Use when the user wants to add, record, capture, publish, or update something for the team, such as a how-to, a fact about a system, a lesson, or a note, and no more specific kb skill fits. Other kb skills finish by following this one's closing steps.
---

# Save to the knowledge base

The knowledge base is a shared database for one client team, reached through an MCP server named `kb-<client>`. Its tools are `whoami`, `search`, `get_document`, `who_knows`, and `save_document`; their full names end in `__whoami` and so on. Everyone on that client's team can read what you save.

Drafting is local and personal. Saving is the moment it becomes shared. Do not save anything the author has not read and approved.

## Rules for anything saved

- **Client staff by role, never by name.** "The shop owner", "the client's project lead". Team members may be named when it helps, neutrally.
- **Nothing about a person they would not want read back to them.** No opinions, blame, speculation, health, or personal circumstances. Facts about systems, products, and decisions.
- **No credentials.** Point to the 1Password vault and item. The server refuses anything that looks like a secret; if it does, remove it and tell the user to rotate anything real that was pasted.
- **No raw material.** No transcripts, email bodies, or exports. Keep the fact, and record where it came from in `sources`.
- **No open work or status.** Bugs, next steps, and who is waiting on what belong in the ticketing system. Save what stays true.
- **One subject per document.** Two subjects are two documents.
- **Links never reveal what a reader cannot see.** See Links below.

## Links

Link to another document by writing its slug in double brackets in the body: `[[<slug>]]`. This is the only way documents are connected; do not list related slugs in `metadata`. Link where the text refers to the other document, so the sentence says why they are related.

Before adding a link:

1. `get_document` the target. If it is not found, do not link; name the subject in plain words instead.
2. Compare `domains`. Link only when everyone who can read this document can also read the target:
   - The target has no domains: always fine.
   - The target has domains: fine only when this document has domains and every one of them is also on the target.
   - Otherwise leave the link out and describe the subject in plain words. A slug in a readable document tells every reader the target exists, even when they cannot open it.
3. When unsure, leave it out.

Changing a document's `domains` later can break this rule for links already in it or pointing to it. When widening a document's audience, check its links again.

## Steps

1. **Understand what to save.** Ask one question at a time until you know the subject, the facts, and where they came from. Read the user's local notes or files if they point you there. Before drafting, `search` for an existing document on the same subject; if one exists, `get_document` it and propose an update to it rather than a duplicate.
2. **Draft.** Write in markdown: a title, then the body in short sections. Choose a `kind` in kebab-case that describes the document (`note`, `how-to`, `reference`, or a kind a more specific skill uses). Leave `domains` empty unless the user says otherwise. List `sources` as `{title, url?, note?}`: a call, a thread, a ticket, a document. Link related documents found in step 1 following Links above. If the user wants to keep working on it, write the draft to a local file and stop; saving can happen in a later session.
3. **Check the draft against the rules above.** Fix anything that breaks them before showing it.
4. **Confirm the target.** Call `whoami` and say which client and person it will be saved as: "Saving to **<client>** as <handle>." If more than one `kb-*` server is connected and the working directory or conversation does not make the client obvious, ask which one.
5. **Show the final draft and get a yes.** Show title, kind, slug (kebab-case of the title unless updating an existing one), sources, and body. Save only on an explicit yes.
6. **Save.** Call `save_document`. To update, pass the existing slug. If the server refuses, show its message, fix the draft with the user, and try again.
7. **Suggest who to tell.** Call `who_knows` with the document's topic. If it returns anyone other than the author, print a short note the author can copy and send, then stop. Do not send anything yourself. If only the author comes back, or nobody, say nothing about it.

   Note format:

   > Added to the {client} knowledge base: **{title}**. {One sentence on what it says.} Ask your agent for "{title}" to read it. {One sentence on why this person, for example: Would value your eyes on it since you know the hosting side.}

8. **Report.** One line: created, updated, or unchanged, with the slug.
