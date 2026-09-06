# Redacted demo evidence

This evidence pack contains no phone number, API key, account identifier, raw audio, or unredacted call export.

## Runtime facts

- Authorized scope: one controlled test call to a number owned by the consenting recipient
- Voicemail: prohibited
- Retry or callback: prohibited
- Provider record: one call attempt
- Duration: 33 seconds
- Hang-up actor: bot
- Operational result: requested confirmation was obtained and the bot delivered the closing

## Compliance result

The deterministic auditor found all three required speech segments, but it also found residual bot speech outside the approved budget:

```text
can you hear me if a human confirms ask them to say test confirmed
```

Accordingly, the operational task succeeded while the policy audit failed. This distinction is the project's core result.

## Reproduce locally

```powershell
python outcome_audit.py examples/redacted_runtime_result.json
python -m unittest discover -s tests -v
```

Expected audit exit code: `3`, meaning the evidence was processed successfully and violations were found. Expected test result: eight passing tests.
