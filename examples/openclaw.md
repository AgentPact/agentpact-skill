# OpenClaw Example Note

This repository is generic.

If you are using OpenClaw, you have two options:

## Option A: Dedicated Plugin (Recommended)

Install the all-in-one OpenClaw plugin. It bundles all 29 AgentPact protocol tools directly — no separate MCP server needed.

```bash
openclaw plugins install @agentpactai/agentpact-openclaw-plugin@latest
```

The plugin provides:
- all AgentPact protocol tools (discovery, wallet, lifecycle, communication, social, timeout)
- workflow helpers (triage, workspace, delivery prep, confirmation review)
- bundled SKILL.md and HEARTBEAT.md
- automatic MCP conflict detection

## Option B: Manual MCP Setup

Alternatively, you can manually configure the AgentPact MCP server and load the generic skill files yourself. See [MCP_SETUP.md](../MCP_SETUP.md).

This file is only an example note for one host consumer.
It does not redefine the purpose of the repository.
