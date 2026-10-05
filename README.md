# agent-skills

Portable [Agent Skills](https://agentskills.io) (`SKILL.md` folders) that work in Claude Code, the Claude app, and OpenAI Codex / ChatGPT.

## Skills

| Skill | What it does |
|---|---|
| [session-clean-up](docs/session-clean-up.md) ([SKILL.md](skills/session-clean-up/SKILL.md)) | Audits what an agent left behind after a diagnostic or debugging session (temp files, captures, background processes, daemons, one-off installs, device changes, published links), presents a numbered clean-up list, and removes only what you approve. |

## Install

Every skill is a folder under `skills/` containing a `SKILL.md`. To install one, copy its folder to where your agent loads skills from. The examples below use `session-clean-up`; swap in the name of any skill from the table above.

```sh
git clone https://github.com/mcalapurge/agent-skills.git
```

| Agent | Example |
|---|---|
| Claude Code | `cp -r agent-skills/skills/session-clean-up ~/.claude/skills/` then run `/session-clean-up`, or let Claude pick it up automatically |
| Codex | `cp -r agent-skills/skills/session-clean-up ~/.codex/skills/` |
| Claude app / ChatGPT | `cd agent-skills/skills && zip -r session-clean-up.zip session-clean-up`, then upload the zip where your app accepts custom skills (Claude app: Settings → Capabilities → Skills) |

### Install from a Claude Code deep link

Claude Code (v2.1.91+) can open from a [`claude-cli://` deep link](https://code.claude.com/docs/en/deep-links) with an install prompt already typed in. Nothing runs until you read the prompt and press Enter.

GitHub strips `claude-cli://` links, so they can't be clicked here. Each skill's docs page has its link in a code block: paste it into your browser's address bar, or on macOS run it with `open`. For example, from the [session-clean-up docs](docs/session-clean-up.md#install-with-claude-code):

```sh
open "claude-cli://open?q=Install%20the%20session-clean-up%20skill%20from%20https%3A%2F%2Fgithub.com%2Fmcalapurge%2Fagent-skills%20into%20my%20Claude%20Code%20skills%3A%20download%20skills%2Fsession-clean-up%2FSKILL.md%20from%20the%20main%20branch%20into%20~%2F.claude%2Fskills%2Fsession-clean-up%2FSKILL.md%20%28create%20the%20folder%20if%20needed%2C%20and%20ask%20before%20overwriting%20an%20existing%20copy%29.%20Then%20confirm%20it%20is%20installed."
```

## Licence

[MIT](LICENSE)
