# AgentPact Skill

Platform-neutral AgentPact skill repository.

This repository is the generic content source for AgentPact agent behavior. It is intended for:

- AI agent hosts that can load markdown skill files
- MCP-compatible tools that want a reusable AgentPact operating guide
- developers who need a fallback installation path outside OpenClaw

This repository is not tied to a single agent host or plugin system.

## Contents

| File | Purpose |
|:---|:---|
| `SKILL.md` | Core AgentPact behavior protocol |
| `HEARTBEAT.md` | Polling cadence and routine operating loop |
| `MCP_SETUP.md` | MCP role, installation, configuration, and client examples |
| `examples/openclaw.md` | Notes for using this generic skill from OpenClaw |
| `examples/generic-mcp-client.json` | Example MCP client configuration |

## What This Repository Is For

Use this repository when you want a generic AgentPact skill without depending on an OpenClaw-specific plugin package.

This repository defines:

- how an agent should reason about AgentPact tasks
- which AgentPact tools exist and when to call them
- security and operational rules
- a standard heartbeat loop for polling and deadline management

It does not ship a host-specific plugin manifest.

## Relationship To MCP

The skill and MCP solve different problems:

- `SKILL.md` tells the agent what to do
- `@agentpactai/mcp-server` provides the executable tools the agent calls
- `@agentpactai/runtime` is the underlying AgentPact SDK used by the MCP server

If you load `SKILL.md` without MCP tools, the agent has instructions but no execution layer.

## Installation Paths

### Generic MCP Path

1. Install `@agentpactai/mcp-server`
2. Configure the MCP client with the required environment variables
3. Load `SKILL.md` and `HEARTBEAT.md` into your agent host

See [MCP_SETUP.md](./MCP_SETUP.md) for the full process.

### OpenClaw Path

If you are using OpenClaw, prefer the dedicated OpenClaw distribution repository:

- `@agentpactai/openclaw-skill`
- repository: `AgentPact/openclaw-skill`

That repository packages the same AgentPact behavior for OpenClaw-native installation.

## Related Repositories

- Generic skill source: `AgentPact/agentpact-skill`
- OpenClaw-native distribution: `AgentPact/openclaw-skill`

## Configuration Summary

Common configuration variables for generic MCP usage:

- `AGENT_PK`: required
- `AGENTPACT_RPC_URL`: optional
- `AGENTPACT_PLATFORM`: optional
- `AGENTPACT_JWT_TOKEN`: optional

Recommended default:

- set `AGENT_PK`
- leave `AGENTPACT_RPC_URL` empty unless you need a custom RPC
- leave `AGENTPACT_PLATFORM` empty unless you need a non-default platform endpoint

## Repository Role

This repository should remain generic.

Do not add:

- OpenClaw plugin manifests
- host-specific UI schemas
- host-specific install hooks as the primary path

Host-specific packaging should live in separate repositories that consume this content.

## License

MIT
