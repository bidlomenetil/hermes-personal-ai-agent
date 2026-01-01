# Hermes personal AI agent

A configurable personal AI agent with CLI, tools, durable session state, scheduled work, messaging gateways and desktop/web interfaces.

## Architecture and stack

`run_agent.py` and `agent/` execute turns; `hermes_cli/` implements user commands; `tools/` registers actions; `gateway/` hosts messaging adapters; `cron/` schedules jobs; `hermes_state*.py` implements persistent state; `pm/` owns managed tools and environments.

## Requirements

The project supports Python >=3.11,<3.15, with runtime tools/environments controlled by `pm/lock.json`; frontend Node requirements are declared in `package.json`. A bare Python installation is not a complete runtime.

## Installation and local development

Use the repository source-checkout activation path:

```sh
source ./activate
hermes --help
```

Read `setup-hermes.sh` for the installer and `pm/` for managed environment preparation. `setup.py` deliberately blocks ordinary wheel/sdist builds; `pip install .` is not the distribution workflow.

## Configuration

Use `cli-config.yaml.example` and `.env.example` as configuration references. User state is profile-aware via `get_hermes_home()`; keep provider keys local and isolate gateway profiles. Docker and Nix deployment definitions are included.

## Testing

Always use `scripts/run_tests.sh`, which prepares the test environment and runs isolated per-file pytest processes. Example: `scripts/run_tests.sh tests/agent/`. Do not replace this with bare pytest; it bypasses repository isolation rules.

## Deployment and integrations

Review `docker-compose.yml`, `Dockerfile` and `flake.nix` for supported distribution paths. Persist profile/session state and test backup/restore. Tool and gateway integrations can access external systems according to configured credentials.

## Source provenance and license

This repository imports source from [NousResearch/Hermes-Agent](https://github.com/NousResearch/Hermes-Agent). Original product functionality belongs to its upstream contributors. The local history begins with a November 2026 source snapshot; it does not retain upstream development history or prove the exact upstream revision. GitHub reports the upstream repository was created on 2025-07-22; that is repository-origin evidence, not the date of this contribution. Existing year folders are retained as local organization.

Preserve `LICENSE` and existing third-party notices when redistributing. Missing root license text was recovered from the upstream repository during this maintenance pass; existing license files were preserved.

## Validation status

Setup and test commands above were checked against this checkout’s manifests, scripts and entry points. Full dependency installation, application builds and integration tests were not performed in this maintenance pass. The default Python 3.9 is below the declared >=3.11 floor and Node 22 is below the frontend Node 26 floor; managed runtime/test environments were not provisioned. These instructions identify the supported workflow without claiming a successful product build.

See [source provenance](SOURCE_PROVENANCE.md) for pinned upstream license retrieval evidence and redistribution limitations.
