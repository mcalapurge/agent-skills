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

## Install

See the [main README](../README.md#install). The skill itself is [`skills/session-clean-up/SKILL.md`](../skills/session-clean-up/SKILL.md).
