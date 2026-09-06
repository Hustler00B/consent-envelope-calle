# CALL-E Consent Gate and Outcome Auditor

**Prototype test build - not a compliance guarantee.** Fifteen local tests pass. The recorded live call used the CALL-E dashboard, not this app's SDK path; end-to-end SDK execution is unverified. Audits compare supplied transcript text and metadata, not independently verified audio or provider attempt history. Hashes identify content but do not authenticate consent. See `READINESS.md` before any live use. The included authorization is demo-only and cannot place calls.

A two-sided safety wrapper for CALL-E phone tasks. The preflight validates recipient authorization before execution; the post-call auditor checks the actual transcript, attempt count, voicemail path, and hang-up against the approved plan. Both tools avoid printing phone numbers, and the auditor stores a transcript hash rather than echoing recipient speech.

```powershell
python consent_gate.py examples/authorization.json --task "Call about pharmacy hours" --phone "+15555550123"
python outcome_audit.py examples/redacted_runtime_result.json
python -m unittest discover -s tests -v
```

Live execution additionally requires `--execute`, `--confirm-call`, and `CALLE_API_KEY`. Automated tests never execute a call.

The redacted runtime fixture comes from a single consented CALL-E test. It intentionally fails the disclosure-budget check because the live agent added an unapproved audibility question and spoke part of its control instruction. This turns real runtime evidence into a deterministic regression test instead of claiming that successful connection alone means compliant execution.

## Safety boundaries

- Examples contain fictional or redacted numbers only.
- API keys must remain in `CALLE_API_KEY`; they are never accepted as command-line arguments or written by this project.
- A valid authorization record is necessary but not sufficient for live execution: the operator must also supply `--execute` and `--confirm-call` at action time.
- The post-call report excludes recipient speech and emits separate policy and transcript fingerprints, binding the approved speech budget to the evidence being evaluated without copying the conversation into the report.
- The one-shot and voicemail findings are post-call checks; provider-side cancellation and suppression controls should still be used where available.

See `SUBMISSION_DRAFT.md` for the Devpost narrative and `DEMO_SCRIPT.md` for a privacy-safe three-minute walkthrough.
