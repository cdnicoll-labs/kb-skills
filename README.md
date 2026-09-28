# kb-skills

The client-neutral half of the shared knowledge base: one Claude Code plugin, `kb-core`, with the skills everyone uses whatever client they are working for.

This repo root *is* the plugin, and it is also its own marketplace, so people add it directly:

```bash
claude plugin marketplace add cdnicoll-labs/kb-skills
claude plugin install kb-core@kb-skills
```

Client marketplaces do not list `kb-core` themselves. A cross-repo entry is fetched over SSH and fails
for anyone without an SSH key on GitHub (tested 2026-09-24), so each person adds this marketplace
alongside their client's.

```
.claude-plugin/plugin.json   the kb-core manifest
skills/kb-save/              draft, get a yes, then save a document
skills/kb-ingest/            turn an outside document into knowledge
skills/kb-retrospective/     run and record a retrospective
skills/kb-decision/          record a decision and the options considered
skills/kb-profile/           write or update your own profile, and only your own
skills/kb-setup-workspace/   create a person's folder for one client, and its connection
```

`kb-setup-workspace` carries `templates/` for the files it writes into a new workspace. Placeholders are
`{{NAME}}`, and every one a template uses has to be documented in the skill. `npm run check:plugins` in
`shared-context` renders them and fails on a typo, or on JSON that would not parse.

No client vocabulary belongs here. Anything that mentions a particular client's sites, products, or people goes in that client's `kb-<client>` repo.

These skills talk to a `kb-<client>` MCP server, which is run separately and is not public.

## Writing a skill

Skills are installed, copied, and may be published, so they follow three rules:

- **No real people.** No names, handles, or anything that points to a person, not even as an example. That includes the team, clients' staff, and the author.
- **No real client situations.** No client names, sites, incidents, tickets, or hosts in examples. A client's own skill, in that client's private repo, may name the client itself, and nothing about its customers or people.
- **Placeholders first.** Show structure with `<display name>`, `<client>`, `<slug>`. Use an invented name only when a sentence needs a person or company to read naturally, and keep it obviously invented (`acme`, `Sam`).

The same rules apply to the golden set in `evals/`. Its cases use one invented cast: `acme` and `otherco` as clients, the HBR shop (Harbour Goods) on HostCo, and Sam, Alex, Jordan, Dana and Riley as people. Reuse them rather than inventing new ones.

And keep skills simple. Every line is read on every use. Rules stay; examples and explanations are the first thing to cut.

## Changing a skill

Edit the skill, bump `version` in `.claude-plugin/plugin.json`, and bump the matching `kb-core` entry in every client marketplace that lists it. Nothing propagates without the version bump. Everyone picks the change up on their next session; there is no gatekeeper and no message to send.

```bash
claude plugin validate --strict .
```
