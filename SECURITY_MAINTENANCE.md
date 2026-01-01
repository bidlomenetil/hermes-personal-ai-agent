# Imported test fixture credential review

On 2026-11-03, GitHub reported three open secret-scanning alerts of unknown validity in the initial published import `c7222240c504150e60075ba97e88b4a9c0b82dc9`:

| Alert | Type | Location | Source purpose |
|---|---|---|---|
| 1 | Google API key | `tests/fakes/providers/gemini_native.py:45` | Local fake Gemini HTTP provider fixture |
| 2 | Telegram bot token | `tests/gateway/test_weak_credential_guard.py:56` | Local non-placeholder token guard test |
| 3 | OpenAI API key | `tests/hermes_cli/test_sessions_export_md_cli.py:73` | Session-export redaction fixture |

No credential values are recorded here. The source context describes synthetic test data, not operational credentials. The Google and Telegram fixtures now use unmistakable local markers. The export test constructs a synthetic credential-shaped value only at runtime because it exercises the redactor’s prefix matching. No real credential was substituted, split or concealed.

Published history is preserved and still contains the original fixture literals. This forward change does not remove historical exposure, establish provider validity or close GitHub alerts. No provider authentication checks were made. If the repository owner determines any original literal was ever an issued credential, revoke/rotate it at the provider and review usage; deleting a current literal is not credential revocation. Do not mark an unknown alert resolved without evidence.

## Validation

- Python 3.13: imported the local Gemini fake and verified its environment configuration shares its marker.
- Python 3.13: production `agent.redact.redact_sensitive_text(..., force=True)` removed the synthetic export value while preserving its surrounding label.
- Direct Telegram auth helper import was blocked by missing `ruamel.yaml`; no claim of successful gateway validation.
- Canonical `scripts/run_tests.sh` suites were not run: no prepared test environment or pytest is available. No dependencies were installed.
