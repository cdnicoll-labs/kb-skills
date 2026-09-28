# {{CLIENT_NAME}} workspace

{{PERSON}}'s folder for {{CLIENT_NAME}}. Two things live here: notes that are only yours, and the connection to the {{CLIENT_NAME}} shared knowledge base.

Open this folder in Claude Code as its own project. The knowledge base tools only exist in sessions started here, so another client's folder cannot reach {{CLIENT_NAME}}'s knowledge base, by accident or otherwise.

## Asking

Ask your agent an ordinary question:

> How is the newsletter set up?

It searches the knowledge base, reads what it finds, and answers with the documents it used. If the answer is not in there, it says so rather than guessing.

To see what exists at all: "list everything in the knowledge base", or "show me every retrospective".

## Adding

Tell your agent what you want the team to know and it drafts it, shows it to you, and saves it only when you say yes. Nothing is ever saved without your approval, and you never touch git to contribute.

Some things are refused on purpose: passwords and keys, raw transcripts and email bodies, anything about a person they would not want read back to them, and open work, which belongs in the ticketing system.

## What stays yours

`notes.md` and `drafts/` are yours. They are not shared, not reviewed, and never reach the knowledge base unless you decide a piece of it should.

## Your token

It lives in `.claude/settings.local.json` in this folder, and that file is ignored by git so it never leaves your machine. Nothing else here holds it. If you ever need to replace it, edit that file and restart the session.

Do not put it in a shell profile. That does not reach the desktop app.

## If the tools disappear

In order: this folder was not opened as its own project; the token in `.claude/settings.local.json` is still the placeholder or has a stray quote; you changed it and have not restarted the session; or it was revoked. Then ask whoever set up your access.
