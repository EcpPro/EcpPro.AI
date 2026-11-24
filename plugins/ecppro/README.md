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
| `ecppro-signin-help` | a user who can't sign in: read the failure reason first, then unlock, reset the password or re-register MFA |
| `ecppro-compromised-account` | a suspected hacked account: risky sign-ins, inbox rules, delegates, then revoke sessions, block, reset, re-register MFA |
| `ecppro-security-review` | a read-only tenant health check: Secure Score, MFA, risky users, admins, baselines and CA, alerts, sharing, mail DNS - top 5 fixes |
| `ecppro-licence-review` | licence savings: reclaimable and unused licences, right-sizing, recommendations with cost, and unbilled services for the MSP |
| `ecppro-customer-report` | a monthly or QBR report for a customer: work done, security trend, licences and spend, recommendations - every number from EcpPro |
| `ecppro-seat-change` | a billed CSP seat change: current quantity, cancellation window, approver, then the subscription workflow after an explicit yes |
| `ecppro-workflow-troubleshoot` | why a workflow or scheduled action is stuck or failed: runs, steps, logs, bulk batches; then retry, skip, cancel, pause or resume |
| `ecppro-baseline-compliance` | baseline drift and compliance, accepted risks, Conditional Access readiness, scan permissions; re-scan or accept a risk (mode checked first) |
| `ecppro-patch-compliance` | a read-only Windows patch report for a tenant or all customers, separating missing updates from stale devices |
| `ecppro-mail-delivery` | email not arriving or going to junk: mail flow, MX / SPF / DKIM / DMARC, transport rules, address owner, junk and inbox rules |
| `ecppro-group-management` | find groups, check members and owners, add or remove people, create, rename or delete, and set outside-sender delivery |
| `ecppro-restore-deleted` | restore a deleted user with their groups, preview a OneDrive restore, and find restorable deleted sites and groups |
| `ecppro-tenant-connection` | why EcpPro can't manage a tenant: consent, Graph permissions, roles, GDAP; re-check or create a consent link |
| `ecppro-shared-mailbox` | create shared, room and equipment mailboxes; access, auto-reply, aliases and hiding from the address book |
| `ecppro-lost-device` | a lost or stolen device: block its sign-in, sign the user out, reset MFA if the phone went too; re-enable if found |
| `ecppro-msp-billing-check` | internal month-end check: unbilled services, billed vs actual, distributor drift, stuck purchases |

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
