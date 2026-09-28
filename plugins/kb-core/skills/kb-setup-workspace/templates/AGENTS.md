# Working in this folder

This is {{PERSON}}'s {{CLIENT_NAME}} workspace. It holds their private notes and the connection to the `kb-{{CLIENT}}` shared knowledge base.

## The line that matters

**Private, stays here:** working notes, drafts, their read on people and how the work is going, anything half-formed.

**Shared, goes to the knowledge base:** what the {{CLIENT_NAME}} team agrees is true. How a system is set up, how something works, what was decided and why, what an incident taught.

The test: if a teammate would benefit from it and it would still be true after {{PERSON}} stopped working here, it is shared.

Never move something from `notes.md` or `drafts/` into the knowledge base without asking. Drafting is private; saving is the moment it becomes the team's.

## Using the knowledge base

Tools come from the `kb-{{CLIENT}}` server: `whoami`, `search`, `get_document`, `who_knows`, `save_document`.

- **Before answering from memory, search.** The knowledge base is the team's record; this session's guesses are not.
- **Cite what you used**, by title and slug.
- **No results means no results.** Say the knowledge base does not cover it rather than filling the gap.
- **Saving follows the `kb-save` skill**, which drafts, checks, and waits for an explicit yes.

## Never

- Never put a password, key, or token in any file here, or in the knowledge base. The server refuses them; point at the 1Password item instead. The one exception is `{{PERSON}}`'s own knowledge base token in `.claude/settings.local.json`, which is gitignored and must stay that way.
- Never save raw transcripts or email bodies. Keep the fact and record where it came from.
- Never write anything about a named person that they would not want read back to them. Client staff are referred to by role.

## Housekeeping

Committing is a good habit and costs nothing:

```bash
git add -A && git commit -m "notes"
```

Started {{DATE}}.
