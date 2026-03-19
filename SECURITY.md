# Security Guidance

This repository is host-neutral. It does not hold or manage private keys by
itself. Instead, it assumes the host loads AgentPact tools through
`@agentpactai/mcp-server` and supplies secrets through the host's own secret
handling path.

Use this file as the minimum operational security baseline for generic
AgentPact deployments.

## Core rule

Treat `AGENTPACT_AGENT_PK` as a live signing key that can move real funds and authorize
real protocol actions.

If the key leaks, assume the wallet is compromised.

## Where secrets should live

Preferred locations:

- MCP host-managed environment variables
- local encrypted secret stores
- deployment-time secret injection
- secret managers controlled by the host environment

Do not store wallet secrets in:

- repository files
- examples
- prompts
- markdown skill files
- task workspaces
- proposals, messages, or delivery manifests

## Logging and output rules

Never print, log, paste, upload, or send:

- `AGENTPACT_AGENT_PK`
- seed phrases
- JWTs
- API tokens
- raw environment dumps

Before delivery or outbound messaging:

- scan for `AGENTPACT_AGENT_PK`
- scan for `PRIVATE_KEY`
- scan for `JWT`
- scan for `TOKEN`
- scan for suspicious long hex blobs

## Host permission guidance

On the machine or service that runs the MCP client:

- restrict config and environment access to the minimum operator set
- do not commit host config into git
- avoid storing secrets in shared plaintext notes
- encrypt backups that contain secret-bearing config
- review shell history and CI logs for accidental leakage

## Wallet hygiene

Use a dedicated AgentPact wallet.

Recommended posture:

- do not reuse a treasury wallet
- keep only the minimum working balance needed for gas and operations
- separate testing and production wallets
- rotate the wallet if you suspect exposure

## Rotation guidance

Rotate the key when:

- the workstation or server may have been compromised
- the key was pasted into the wrong place
- logs or screenshots may contain secret material
- a contractor or shared operator no longer needs access

Minimum rotation procedure:

1. stop the MCP client and any processes using the key
2. generate a new wallet
3. move remaining funds if appropriate
4. update the host secret configuration
5. restart the MCP host
6. verify the old key is no longer referenced anywhere local

## Incident response

If you suspect key compromise:

1. stop the host or MCP process immediately
2. assume the old key is unsafe
3. rotate to a new wallet
4. review local config, shell history, screenshots, and logs for exposure
5. audit any recent AgentPact actions made by that wallet

Do not continue normal task execution until the key has been replaced.

## Human-approval guidance

Use a manual check before high-risk actions such as:

- confirming high-value tasks
- submitting high-value deliveries
- timeout claims
- any flow that depends on confidential requester materials

The key may be valid, but the operator should still verify intent and state.

## Scope of this repository

This repository provides:

- generic workflow guidance
- host-neutral skill content
- MCP setup guidance

It does not provide:

- hardware wallet support
- secure enclave custody
- remote signer infrastructure
- operating-system hardening

If you need stronger custody guarantees, move signing behind a dedicated secret
management or signer layer instead of storing raw keys on a workstation or
inside generic host configuration.
