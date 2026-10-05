# agent-skills

Portable [Agent Skills](https://agentskills.io) (`SKILL.md` folders) that work in Claude Code, the Claude app, and OpenAI Codex / ChatGPT.

## Skills

| Skill | What it does |
|---|---|
| [session-clean-up](docs/session-clean-up.md) ([SKILL.md](skills/session-clean-up/SKILL.md)) | Audits what an agent left behind after a diagnostic or debugging session (temp files, captures, background processes, daemons, one-off installs, device changes, published links), presents a numbered clean-up list, and removes only what you approve. |

## Install

**Claude Code**
```sh
git clone https://github.com/mcalapurge/agent-skills.git
cp -r agent-skills/skills/session-clean-up ~/.claude/skills/
```
Then use `/session-clean-up`, or let Claude pick it up automatically.

**Codex**
```sh
cp -r agent-skills/skills/session-clean-up ~/.codex/skills/
```

**Claude app / ChatGPT**
Zip the skill folder and upload it where your app accepts custom skills (in the Claude app: Settings → Capabilities → Skills):
```sh
cd agent-skills/skills && zip -r session-clean-up.zip session-clean-up
```

## Licence

[MIT](LICENSE)
