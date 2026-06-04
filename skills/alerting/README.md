# alerting

Unified Axiom alerting skill for managing monitors and notifiers via the Axiom v2 API.

## What This Skill Covers

- Monitor lifecycle: list, get, history, create, update, delete
- Notifier lifecycle: list, get, create, update, delete
- End-to-end workflow: create notifier, wire `notifierIds` into monitor, validate behavior

## Requirements

- `curl`
- `jq`
- `~/.axiom.toml` with at least one deployment

Example config:

```toml
[deployments.prod]
url = "https://api.axiom.co"
token = "xaat-your-token"
org_id = "your-org-id"
```

## Setup

```bash
skills/alerting/scripts/setup
```

## Quick Start

```bash
# List notifiers and monitors
skills/alerting/scripts/notifier-list prod
skills/alerting/scripts/monitor-list prod
```

## Common Commands

```bash
# Create notifier from JSON
skills/alerting/scripts/notifier-create prod ./notifier.json

# Create monitor from JSON
skills/alerting/scripts/monitor-create prod ./monitor.json

# Check monitor history in a time range
skills/alerting/scripts/monitor-history prod <monitor-id> 2026-05-03T00:00:00Z 2026-05-04T00:00:00Z
```

## JSON Notes

- Email notifier uses `emails`, not `recipients`.
- Monitor payload uses `notifierIds` to attach destinations.
- For noisy alerts, prefer `triggerAfterNPositiveResults` with `triggerFromNRuns`.

## Script Index

- `scripts/axiom-api <deploy> <method> <path> [body]`
- `scripts/monitor-list <deployment> [--json]`
- `scripts/monitor-get <deployment> <id>`
- `scripts/monitor-history <deployment> <id> <startTime> <endTime>`
- `scripts/monitor-create <deployment> <json-file>`
- `scripts/monitor-update <deployment> <id> <json-file>`
- `scripts/monitor-delete <deployment> <id>`
- `scripts/notifier-list <deployment> [--json]`
- `scripts/notifier-get <deployment> <id>`
- `scripts/notifier-create <deployment> <json-file>`
- `scripts/notifier-update <deployment> <id> <json-file>`
- `scripts/notifier-delete <deployment> <id>`
