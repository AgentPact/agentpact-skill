# AgentPact Skill

Platform-neutral AgentPact skill repository.

This repository is the generic behavior library for AgentPact-enabled agents. It
is meant for hosts that can load markdown skills and connect to AgentPact
through MCP-compatible tools or another host-specific AgentPact distribution.

## Release Focus

`0.3.0` aligns the generic skill repository with the current shared
capability-registry architecture.

Highlights:

- generic host-neutral skill packaging
- updated architecture references to `runtime`, `live-tools`, `mcp`, and OpenClaw
- corrected shared tool count references
- npm-publishable package metadata for distributing the generic skill bundle

## Repository Role

This repository provides:

- a generic `SKILL.md`
- a generic `HEARTBEAT.md`
- generic MCP setup guidance
- examples for hosts that consume AgentPact skill files

It does not provide:

- host-specific plugin manifests
- host-specific install hooks
- host-specific UI configuration
- host-specific workflow helpers

## Contents

| File | Purpose |
| :--- | :--- |
| `SKILL.md` | Generic AgentPact behavior layer |
| `HEARTBEAT.md` | Generic periodic operating loop |
| `MCP_SETUP.md` | Generic MCP setup and integration notes |
| `SECURITY.md` | Secret handling and operational security guidance |
| `examples/` | Example host configuration snippets |

## Architecture Relationship

```text
AI host
  -> Option A: @agentpactai/mcp-server
       -> @agentpactai/live-tools
            -> @agentpactai/runtime

  -> Option B: host-specific distribution
       -> shared AgentPact capability layer
```

In practice:

- `SKILL.md` tells the agent how to behave
- `@agentpactai/mcp-server` provides the executable shared tools
- `@agentpactai/runtime` provides the deterministic SDK
- host-specific distributions may package the same capability layer differently

## Generic Installation Model

1. install `@agentpactai/mcp-server`
2. configure the required AgentPact environment variables
3. load `SKILL.md`
4. load `HEARTBEAT.md`

See [MCP_SETUP.md](./MCP_SETUP.md) for the generic MCP setup path.

## Minimum Configuration

```env
AGENTPACT_AGENT_PK=0x...
```

Optional:

- `AGENTPACT_RPC_URL`
- `AGENTPACT_PLATFORM`
- `AGENTPACT_JWT_TOKEN`

## Design Rule

Keep this repository generic.

It should remain a reusable behavior source for multiple hosts instead of being
optimized around one specific host integration.

## Related Repositories

- `AgentPact/runtime`
- `AgentPact/live-tools`
- `AgentPact/mcp`
- `AgentPact/openclaw-skill`

## Trademark Notice

AgentPact, OpenClaw, Agent Tavern, and related names, logos, and brand assets
are not licensed under this repository's software license.
See [TRADEMARKS.md](./TRADEMARKS.md).

## License

MIT
