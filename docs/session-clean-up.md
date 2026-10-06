# session-clean-up

Tidies up after a hands-on session with an AI agent.

When an agent debugs a network, tests a device or investigates a problem, it leaves things behind: scratch scripts, packet captures and logs, background monitors, services it loaded "just for this test", permissions you granted, test settings on devices, published pages. Some of that is clutter. Some keeps running, starts again at every boot, or holds sensitive data such as IP and MAC addresses or tokens.

This skill has the agent account for all of it and clean it up with your approval.

## What it does

1. **Lists what the session left behind.** The agent goes back over everything it created, started, installed, changed, granted or published, then checks each item is actually still there.
2. **Sorts each item** into:
   - **Remove:** session-specific leftovers. Anything holding sensitive data is listed first.
   - **Needs you:** steps that need `sudo`, a device or an account dashboard, with the exact command or settings path.
   - **Keeping:** deliverables you asked for, such as reports or final scripts.
   - **Leaving in place:** general development and debugging tools (Xcode, Wireshark, Python, …), which stay useful beyond the session.
   - **No action needed:** things that expire or clean themselves up, with the reason.
3. **Shows a numbered list and stops.** Nothing is deleted until you reply, e.g. `all`, `1-4` or `all except 3`.
4. **Removes only what you approved,** in a safe order (stop processes before deleting their files), checks again, and reports what's done and what's left for you.

## When to use it

At the end of any troubleshooting, debugging or experiment session, or whenever you'd ask "do I need to clean anything up?" or "what did you install?". In Claude Code you can also run it directly with `/session-clean-up`.

## Example output

```
## Session clean-up

**Still active**
1. rvi0 capture interface: mirrors the phone's traffic while plugged in
   run: sudo rvictl -x <device-id>

**Remove (sensitive first)**
2. scratchpad/capture.pcap: phone traffic, includes public IP
3. scratchpad/probe.py, monitor.py: one-off test scripts

**Needs you**
4. Capture helper service starts at every boot
   run: sudo launchctl unload -w /Library/.../com.apple.rpmuxd.plist

**Keeping**
- report.html: the report you asked for

**Leaving in place (general tools)**
- Xcode device tools: useful beyond this session

**No action needed**
- Test subscription on the bulb: lapses on its own

Reply with which numbers to remove ("all", "1-4", "all except 3").
```

## Supported platforms

| Platform | What it focuses on |
|---|---|
| Claude Code (CLI / desktop) | Real filesystem and shell: scratchpad, background tasks, services, published artifacts |
| Claude app | Connected drives, published artifacts and shared links. The sandbox is discarded on its own |
| ChatGPT | Files outside the sandbox, shared links, connector changes, commands you ran locally |
| Codex | Untracked files, temporary branches, worktrees and stashes, sandbox processes |

## Install with Claude Code

Install it as a plugin from this repo's marketplace:

```
/plugin marketplace add mcalapurge/agent-skills
/plugin install session-clean-up@nekaiko-skills
```

Run it with `/session-clean-up:session-clean-up`, or let Claude pick it up when you're wrapping up a session.

### One-click deep link

Paste this [deep link](https://code.claude.com/docs/en/deep-links) into your browser's address bar (Claude Code v2.1.91 or later). Claude Code opens with the install prompt already typed; read it, then press Enter.

```text
claude-cli://open?q=Install%20the%20session-clean-up%20skill%20as%20a%20Claude%20Code%20plugin%3A%20run%20%60claude%20plugin%20marketplace%20add%20mcalapurge%2Fagent-skills%60%20%28skip%20if%20the%20nekaiko-skills%20marketplace%20is%20already%20added%29%2C%20then%20%60claude%20plugin%20install%20session-clean-up%40nekaiko-skills%60.%20Then%20confirm%20it%20is%20installed%20and%20tell%20me%20to%20restart%20Claude%20Code%20or%20run%20%2Freload-plugins.
```

Or on macOS:

```sh
open "claude-cli://open?q=Install%20the%20session-clean-up%20skill%20as%20a%20Claude%20Code%20plugin%3A%20run%20%60claude%20plugin%20marketplace%20add%20mcalapurge%2Fagent-skills%60%20%28skip%20if%20the%20nekaiko-skills%20marketplace%20is%20already%20added%29%2C%20then%20%60claude%20plugin%20install%20session-clean-up%40nekaiko-skills%60.%20Then%20confirm%20it%20is%20installed%20and%20tell%20me%20to%20restart%20Claude%20Code%20or%20run%20%2Freload-plugins."
```

The prompt asks Claude to:

> Install the session-clean-up skill as a Claude Code plugin: run `claude plugin marketplace add mcalapurge/agent-skills` (skip if the nekaiko-skills marketplace is already added), then `claude plugin install session-clean-up@nekaiko-skills`. Then confirm it is installed and tell me to restart Claude Code or run /reload-plugins.

For Codex, the Claude app and ChatGPT, see [Install](../README.md#other-agents-manual-copy) in the main README. The skill itself is [`skills/session-clean-up/SKILL.md`](../skills/session-clean-up/SKILL.md).
