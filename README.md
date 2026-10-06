# agent-skills

Portable [Agent Skills](https://agentskills.io) (`SKILL.md` folders) that work in Claude Code, the Claude app, and OpenAI Codex / ChatGPT.

## Skills

| Skill | What it does | Install in Claude Code |
|---|---|---|
| [session-clean-up](docs/session-clean-up.md) ([SKILL.md](skills/session-clean-up/SKILL.md)) | Audits what an agent left behind after a diagnostic or debugging session (temp files, captures, background processes, daemons, one-off installs, device changes, published links), presents a numbered clean-up list, and removes only what you approve. | `/plugin install session-clean-up@nekaiko-skills` |

Claude Code installs need the marketplace added once; see [Claude Code plugin marketplace](#claude-code-plugin-marketplace).

## Install

### Claude Code plugin marketplace

This repo is a Claude Code [plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces) called `nekaiko-skills`, and each skill is its own plugin. Add the marketplace once:

```
/plugin marketplace add mcalapurge/agent-skills
```

Then install any skill from the table above by name, for example:

```
/plugin install session-clean-up@nekaiko-skills
```

Plugin skills are namespaced by plugin, so this one runs as `/session-clean-up:session-clean-up`, and Claude also picks it up automatically when it's relevant. Get updates with `/plugin marketplace update nekaiko-skills`. From a shell, use `claude plugin marketplace add …` and `claude plugin install …` instead.

#### One-click install with a deep link

Each skill's docs page has a Claude Code [deep link](https://code.claude.com/docs/en/deep-links) (v2.1.91+) that opens Claude Code with the install prompt already typed. Nothing runs until you press Enter. GitHub strips `claude-cli://` links, so the links are in code blocks: paste one into your browser's address bar, or on macOS run it with `open`. See [session-clean-up](docs/session-clean-up.md#install-with-claude-code) for an example.

### Other agents (manual copy)

Every skill is a folder under `skills/` containing a `SKILL.md`. Copy that folder to where your agent loads skills from. The examples use `session-clean-up`; swap in any skill name from the table.

```sh
git clone https://github.com/mcalapurge/agent-skills.git
```

| Agent | Example |
|---|---|
| Claude Code (without the plugin system) | `cp -r agent-skills/skills/session-clean-up ~/.claude/skills/`, then run `/session-clean-up` |
| Codex | `cp -r agent-skills/skills/session-clean-up ~/.codex/skills/` |
| Claude app / ChatGPT | `cd agent-skills/skills && zip -r session-clean-up.zip session-clean-up`, then upload the zip where your app accepts custom skills (Claude app: Settings → Capabilities → Skills) |

### Adding a skill to this repo

1. Add `skills/<name>/SKILL.md`.
2. Add an entry to `.claude-plugin/marketplace.json` with `"source": "./"` and `"skills": ["./skills/<name>"]`, so it installs as its own plugin.
3. Add `docs/<name>.md` and a row in the table above.
4. Check it with `claude plugin validate .`

## Licence

[MIT](LICENSE)
