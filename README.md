# kb-skills

The client-neutral half of the shared knowledge base: one Claude Code plugin, `kb-core`, with the skills everyone uses whatever client they are working for.

This repo is a marketplace holding one plugin, `kb-core`, laid out the way Anthropic's own marketplace is: the plugin in `plugins/kb-core/`, the marketplace at the root. It is public, so adding it needs no GitHub login.

In the Claude app: **Settings → Plugins → Add → Add marketplace**, then `https://github.com/cdnicoll-labs/kb-skills`. In Claude Code:

```bash
claude plugin marketplace add https://github.com/cdnicoll-labs/kb-skills.git
claude plugin install kb-core@kb-skills
```

Use the full `https://` URL, not `owner/repo`. The shorthand records an SSH remote, and updates then fail
for anyone without an SSH key on GitHub (found 2026-09-24).

Client marketplaces do not list `kb-core` themselves; each person adds this marketplace alongside their
client's.

```
.claude-plugin/marketplace.json             the marketplace, listing plugins/kb-core
plugins/kb-core/.claude-plugin/plugin.json  the kb-core manifest
plugins/kb-core/skills/kb-save/             draft, get a yes, then save a document
plugins/kb-core/skills/kb-ingest/           turn an outside document into knowledge
plugins/kb-core/skills/kb-retrospective/    run and record a retrospective
plugins/kb-core/skills/kb-decision/         record a decision and the options considered
plugins/kb-core/skills/kb-profile/          write or update your own profile, and only your own
plugins/kb-core/skills/kb-setup-workspace/  create a person's folder for one client, and its connection
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

Edit the skill, bump `version` in `plugins/kb-core/.claude-plugin/plugin.json` and in this repo's `.claude-plugin/marketplace.json`. Nothing propagates without the version bump. Everyone picks the change up on their next session; there is no gatekeeper and no message to send.

```bash
claude plugin validate --strict .
```
