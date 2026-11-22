# EcpPro.AI

EcpPro AI plugins and skills for Claude, ChatGPT and other AI assistants. They work with the
[EcpPro MCP server](https://www.ecppro.com/mcp/setup/): the server gives the assistant its tools (what it can do in
EcpPro), and these skills give it the playbook (how to do a common job well).

## Plugins

| Plugin | What it gives the assistant |
|---|---|
| [`ecppro`](plugins/ecppro) | Workflow skills: onboarding, offboarding, mailbox / calendar access, ticket triage, sign-in help, compromised account response, security and licence reviews, customer (QBR) reports, subscription seat changes |

## Install (Claude Code)

1. Connect the EcpPro MCP server for your instance - see https://www.ecppro.com/mcp/setup/. For example:
   `claude mcp add --transport http ecppro https://<instance>-mcp.ecppro.com/<instance>/mcp`
2. Add this marketplace and install the plugin:
   ```
   /plugin marketplace add EcpPro/EcpPro.AI
   /plugin install ecppro@ecppro-ai
   ```
3. Ask in plain words - "onboard Jane Citizen as a sales rep", "give Bob read access to Alice's calendar",
   "triage the next ticket for <customer>", "Bob can't sign in", "run a security review on Contoso",
   "where can Contoso save on licences?", "build last month's report for Contoso". `/skills` lists them.

The skills are guidance only. Every safety control - your EcpPro role and scope, the preview-and-confirm step on
high-impact changes, your organisation's read-only switch - is enforced by the EcpPro MCP server, whatever a skill says.

## Licence

[MIT](LICENSE)
