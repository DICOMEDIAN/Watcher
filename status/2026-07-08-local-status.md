# Local Hermes Status — 2026-07-08

This is a point-in-time status snapshot.

## Installed Hermes

```text
C:\Users\user\AppData\Local\hermes\hermes-agent
```

Config:

```text
C:\Users\user\AppData\Local\hermes\config.yaml
C:\Users\user\AppData\Local\hermes\.env
```

Gateway startup script:

```text
C:\Users\user\AppData\Local\hermes\gateway-service\Hermes_Gateway.cmd
```

UTF-8 environment was added to the gateway script.

## Cron Jobs

| ID | Name | Script | Schedule | Last known status |
|---|---|---|---|---|
| `917ea83a739e` | SafeRT Notion Queue Broker Monitor | Hermes skill/no script | every 5m | ok |
| `6338ee72ffba` | SafeRT Notion Archive Housekeeping | `safert_notion_archive_housekeeping.py` | every 15m | ok |
| `0b1d07f60605` | SafeRT Hermes Smartie Bridge | `safert_smartie_bridge.py` | every 1m | recently error in status snapshot |
| `117533735ca0` | SafeRT Hermes DEV Bridge | `safert_dev_bridge.py` | every 1m | recently error in status snapshot |
| `f3c29875ddef` | SafeRT Hermes STEIN Bridge | `safert_stein_bridge.py` | every 1m | ok |

Note: Smartie/DEV recent `error` statuses should be diagnosed separately. They had previously been installed and tested successfully.

## Known Working Confirmations

- STEIN Codex continuity loaded.
- STEIN UTF-8 corrected with `korean_call_name: 스타인`.
- STEIN Notion READY posted.
- STEIN bridge cron tick succeeded.
- USER-facing metadata stripping added to SMARTIE/DEV/STEIN bridges.
- Internal `conversation_id` added to bridge prompts.

