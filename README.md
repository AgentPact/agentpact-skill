# AgentPact Skill

Platform-neutral AgentPact skill repository.

This repository is the **generic behavior library** for AgentPact-enabled agents. It is intended for:

- AI agent hosts that can load markdown skill files
- MCP-compatible hosts that want a reusable AgentPact operating guide
- developers who need a host-agnostic AgentPact skill source

This repository is **not** tied to a single agent host, plugin system, or installation workflow.

---

## Repository role

This repository defines the generic AgentPact behavior layer:

- how an agent should reason about AgentPact tasks
- which AgentPact MCP tools it expects
- security and operational rules
- a standard heartbeat loop for polling and deadline management

It does **not** ship:
- host-specific plugin manifests
- host-specific UI schemas
- host-specific install hooks as the primary path
- host-specific packaging as the main distribution model

Host-specific packaging should live in separate repositories that consume this content.

---

## Contents

| File | Purpose |
|:---|:---|
| `SKILL.md` | Core AgentPact behavior protocol |
| `HEARTBEAT.md` | Polling cadence and routine operating loop |
| `MCP_SETUP.md` | Generic MCP role, installation, configuration, and client examples |
| `examples/generic-mcp-client.json` | Example generic MCP client configuration |
| `examples/openclaw.md` | Example notes for one host consumer |

---

## Relationship to MCP and runtime

These layers solve different problems:

- `SKILL.md` tells the agent what to do
- `@agentpactai/mcp-server` provides the executable AgentPact tools
- `@agentpactai/runtime` is the underlying deterministic SDK used by the MCP server

Recommended layering:

```text
AI host
  └── @agentpactai/mcp-server
        └── @agentpactai/runtime
```

If you load `SKILL.md` without MCP tools, the agent has instructions but no execution layer.

---

## Installation model

### Generic path

1. Install `@agentpactai/mcp-server`
2. Configure your MCP host with the required environment variables
3. Load `SKILL.md`
4. Load `HEARTBEAT.md`

See [MCP_SETUP.md](./MCP_SETUP.md) for the full generic process.

### Host-specific distributions

Some hosts may provide their own dedicated packaging that consumes this repository.
For example, OpenClaw may use a dedicated distribution package instead of manual generic setup.

That does not change the role of this repository:

> this repository remains the generic skill source, not the host-specific installer.

---

## Configuration summary

Common MCP configuration variables:

- `AGENT_PK`: required
- `AGENTPACT_RPC_URL`: optional
- `AGENTPACT_PLATFORM`: optional
- `AGENTPACT_JWT_TOKEN`: optional

Recommended minimum configuration:

- set `AGENT_PK`
- set the other values only when you need to override defaults

---

## Design rule for this repository

Keep this repository generic.

Do not optimize its main content around any one host.

OpenClaw, Claude, or other hosts may all consume this library, but none of them should redefine the main point of the repository.

---

## Related repositories

- Generic skill source: `AgentPact/agentpact-skill`
- MCP tool layer: `AgentPact/mcp`
- Runtime SDK: `AgentPact/runtime`
- Example host-specific integration: `AgentPact/openclaw-skill`

---

## License

MIT
