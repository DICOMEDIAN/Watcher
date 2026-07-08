# Skill: remote-agent-attach

## Purpose

Attach agents running on other PCs to the same Notion-mediated Hermes team.

## Preferred Topology

Each remote PC should run its own local Hermes or lightweight bridge runner.
The shared coordination layer is Notion.

```text
PC A Hermes/Bridge -> Notion <- PC B Hermes/Bridge
```

This avoids depending on one Windows machine being reachable from all other
machines and keeps local sessions local.

## Alternative

Remote agents may call a central Hermes instance over the internal network only
if:

- the port is intentionally bound to LAN
- authentication is configured
- firewall rules are explicit
- logs do not expose secrets

## Setup Checklist

1. Clone `DICOMEDIAN/Watcher`.
2. Install Hermes or bridge runner.
3. Add project/channel map.
4. Add local agent session binding.
5. Run UTF-8 tests.
6. Run Notion read/write tests.
7. Register the agent in the shared registry.

