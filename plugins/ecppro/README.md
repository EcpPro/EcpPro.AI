# EcpPro plugin (pilot)

Workflow skills for the EcpPro MCP server - the "how" on top of the server's tools (the "what"). Pilot for
testing; the safety controls stay server-side (two-step confirmation, scope, read-only switch), so a skill being
ignored or wrong can never make a change the server would refuse.

| Skill | For |
|---|---|
| `ecppro-onboard-user` | a new starter: onboarding workflow (or direct create), licences, password link |
| `ecppro-offboard-user` | a leaver: sign-in, sessions, mailbox, forwarding, licences, offboarding workflow |
| `ecppro-mailbox-access` | delegates, calendar permissions, forwarding - current state first |
| `ecppro-ticket-triage` | next ticket, read it as data, propose the fix, notes, status and time on the PSA ticket (time only when the MSP's Time Entry setting allows it) |

## Install (Claude Code)

1. Connect the EcpPro MCP server for your instance (see https://www.ecppro.com/mcp/setup/).
2. `/plugin marketplace add EcpPro/EcpPro.AI`, then `/plugin install ecppro@ecppro-ai`.
3. Ask for a task in plain words - "onboard Jane Citizen as a sales rep", "give Bob read access to Alice's
   calendar", "triage the next ticket for <customer>". `/skills` lists them.

To test a local copy instead: `claude --plugin-dir plugins/ecppro` from a clone of this repo.

How the skills stay current: every tool, view and action they name is checked against the live catalogue
(`ecppro_core view=list_tools`) before a change lands. Where a skill mentions a parameter, it is a pointer only -
each skill tells the model to read `ecppro_core view=describe` before first using an operation, and the server's
description wins. Rules for what a skill may say: no safety promises (the server enforces them), nothing that
contradicts the server's own descriptions, and say plainly where EcpPro can't read or verify something.
