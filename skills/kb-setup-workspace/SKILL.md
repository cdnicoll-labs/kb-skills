---
name: kb-setup-workspace
description: Set up a personal Claude Code workspace for a client's shared knowledge base. Use on a person's first day, or when they say they were given a knowledge base token, want to connect to a kb-<client> server, cannot see the knowledge base tools, or want a folder for their own notes on a client. Creates the folder, writes the connection, and never handles the token itself.
---

# Set up a knowledge base workspace

One folder per client on this person's machine. It holds their own private notes and the connection to that client's shared knowledge base. Opening that folder is what turns the knowledge base tools on; every other folder has no access at all, which is what stops anything being saved to the wrong client.

This runs once per client, per person. It is usually the first thing they do after installing the plugin.

## Never touch the token

**Do not ask for the token, do not accept it if it is pasted, and never write it to a file.** It identifies that person on every call. If they paste it into the chat, tell them plainly to have it rotated, and carry on without it.

This skill writes a placeholder. The person replaces it themselves, in their own editor. You never see the value, and you never need to.

## Where the token goes, and why

It goes in `.claude/settings.local.json` inside the workspace, as an `env` entry, and that file is gitignored.

Verified 2026-09-23 against Claude Code Desktop on macOS: **a shell profile does not reach the desktop app.** `KB_<CLIENT>_TOKEN` exported in `~/.zshrc` and `~/.zprofile`, with both interactive and login shells confirmed to have it and the app fully quit and relaunched, still did not reach the session. An `env` entry in `.claude/settings.local.json` did.

So: do not tell anyone to edit a shell profile. It works from the CLI and fails silently on the desktop, which is the worst combination.

The token stays out of `.mcp.json` because that file is committed to their workspace repo.

## Step 1. Check the platform first

Before asking anything, check the operating system.

**Windows:** stop here. Say this and nothing more:

> Setup on Windows needs a path that has not been written and tested yet. Tell whoever set up your access and they will walk you through it directly. Nothing has been created, so there is nothing to undo.

Do not improvise a Windows equivalent. A setup that looks successful and then fails is worse than one that stops.

**macOS or Linux:** continue.

## Step 2. Work out which client, and the server address

Both come from the onboarding message that came with their 1Password item. Ask for them together, in one question:

> Which client is this for, and what is the knowledge base URL? Both are in the message that came with your token. The URL ends in `/mcp`.

The client slug is lowercase, for example `acme`. Derive the environment variable name from it: `acme` becomes `KB_ACME_TOKEN`, and a hyphen becomes an underscore, so `acme-co` becomes `KB_ACME_CO_TOKEN`.

The URL is not a secret. The token is.

## Step 3. Ask the four questions

One at a time. Offer the default, accept a plain yes.

1. **Where should the folder go?** Default `~/<client>-context`, for example `~/acme-context`. Anywhere they like, as long as it is not inside another git repository.
2. **What name should appear on what you save?** Their display name. Also ask for their handle if it is not obvious; it is lowercase and matches the one in their token.
3. **Keep a history of your notes with git?** Default yes. It costs nothing and means nothing is lost.
4. **Do you want a private backup of that history somewhere like GitHub?** Default no, and "maybe later" is a fine answer. Later is easy; it is one command to add a remote.

## Step 4. Handle a folder that is already there

If the target folder exists, **never overwrite anything.** List what is already there, then offer to add only the files that are missing and leave the rest alone. If `.mcp.json` exists and points somewhere else, show both and ask which is right. If `.claude/settings.local.json` exists, leave it completely alone; it may already hold a working token. If they want a clean start, they move the old folder aside themselves.

## Step 5. Show what will be created, and wait

List every file and where it will go. Wait for a yes. Then create the folder and copy the templates from `${CLAUDE_PLUGIN_ROOT}/skills/kb-setup-workspace/templates/`, substituting:

| Placeholder | Becomes |
|---|---|
| `{{CLIENT}}` | the client slug, for example `acme` |
| `{{CLIENT_NAME}}` | the client's display name, for example `Acme` |
| `{{URL}}` | the knowledge base URL |
| `{{TOKEN_VAR}}` | the environment variable name, for example `KB_ACME_TOKEN` |
| `{{TOKEN_REF}}` | that variable as Claude Code reads it, for example `${KB_ACME_TOKEN}`. The token itself never appears |
| `{{PERSON}}` | their display name |
| `{{HANDLE}}` | their handle |
| `{{DATE}}` | today, as YYYY-MM-DD |

| Template | Goes to |
|---|---|
| `mcp.json` | `.mcp.json`, the connection. Committed, and holds no secret |
| `settings.local.json` | `.claude/settings.local.json`, where the token goes. Gitignored |
| `gitignore` | `.gitignore` |
| `AGENTS.md` | `AGENTS.md`, how this folder works and what stays private |
| `README.md` | `README.md`, what this is and how to use it |
| `notes.md` | `notes.md`, working memory |
| `drafts-README.md` | `drafts/README.md` |

```
<folder>/
├── .mcp.json
├── .claude/settings.local.json
├── .gitignore
├── AGENTS.md
├── README.md
├── notes.md
└── drafts/README.md
```

Check that both JSON files parse before moving on.

## Step 6. The token, which is theirs to paste

Tell them, with the real path:

> Open `<folder>/.claude/settings.local.json` in your editor and replace `PASTE-YOUR-TOKEN-HERE` with your token from 1Password. Save it. Do not paste it into this chat.

Then check they have done it, without reading the value:

```bash
grep -q 'PASTE-YOUR-TOKEN-HERE' <folder>/.claude/settings.local.json && echo "still the placeholder" || echo "filled in"
```

Do not continue while it is still the placeholder. A workspace that exists but cannot connect is the confusing failure this check prevents.

Confirm that file is ignored before anything is committed:

```bash
cd <folder> && git check-ignore .claude/settings.local.json
```

It must print the path. If it does not, stop and fix `.gitignore` first. Committing that file would put their token in git history.

## Step 7. Git, if they said yes

```bash
git init -b main
git add -A
git commit -m "Set up my {{CLIENT_NAME}} workspace"
```

Then confirm the token file did not go in:

```bash
git show --stat --name-only HEAD | grep settings.local.json && echo "PROBLEM: the token file was committed" || echo "good: token file not committed"
```

If they wanted a remote, give them the two commands and let them create the repository themselves. **Say out loud that it must be private**, because it will hold their notes on a client.

## Step 8. Tell them the one step that is theirs

This is the step people miss, so say it plainly and do not treat setup as finished without it:

> Open `<folder>` in Claude Code as its own project. This session cannot use the connection, because it only applies to sessions started in that folder. Claude Code will ask once whether to trust the `kb-{{CLIENT}}` server; say yes. Then ask "who am I in the knowledge base". If it answers with your name and role, you are done.

If `whoami` fails when they try it, the causes in order:

1. The folder was not opened as its own project.
2. `.claude/settings.local.json` still has the placeholder, or the token was pasted with a stray quote or space.
3. The token was changed after the session started, so the session needs restarting. The session, not the app.
4. The token was revoked. Ask whoever administers the knowledge base.

**Never tell them to put the token in a shell profile.** It does not reach the desktop app, and it fails silently.

## Step 9. One short summary

What was created, where, and the one thing they still have to do. No more than five lines.

End with one suggestion for their first session in the new folder, since it is the best first save there is:

> Once you are connected, ask your agent to add your profile. It asks a few questions about your role and how you work, and it is what teammates find when they ask who does what.
