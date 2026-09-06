# Three-minute demo script

Production constraints reverified September 4: show actual local execution footage; keep below three minutes; clearly label fixture replay and unverified SDK execution. The final video must be public on YouTube or Vimeo, not merely a Drive link or GitHub release. Do not present draft narration as stronger evidence than READINESS.md permits. Current test count: 15.

## 0:00–0:20 — The problem

Show the title: **Consent Envelope: success is not compliance**.

Narration: “Phone agents report whether a task completed. Consent Envelope checks the harder question: did the agent stay inside the permission it was given?”

## 0:20–0:55 — Pre-call authorization

Open `examples/authorization.json`, then run the dry-run example.

Point out the authorization source, purpose, expiry, allowed disclosures, and `voicemail_allowed: false`. Show that the preview redacts the phone number and makes no network request.

## 0:55–1:25 — Fail closed

Run the unit tests or briefly show the fail-closed test. Explain that revoked, expired, off-purpose, and over-disclosure requests are rejected before the SDK can run. Emphasize that live mode needs both `--execute` and `--confirm-call` plus an environment-held key.

## 1:25–1:55 — Genuine runtime evidence

Show a redacted screenshot of the CALL-E record: one attempt, 33 seconds, bot hang-up. Do not show the phone number, account details, API key, audio, or recipient speech beyond the already approved confirmation phrase.

Narration: “The recipient owned the number, consented to exactly one AI call, heard the AI disclosure, confirmed the test, and CALL-E ended the call.”

## 1:55–2:35 — The finding

Run:

```powershell
python outcome_audit.py examples/redacted_runtime_result.json
```

Highlight `compliant: false` and the residual bot speech. Explain that CALL-E inserted “Can you hear me?” and spoke a control-instruction fragment. The call succeeded operationally, but exceeded the approved speech budget.

## 2:35–2:55 — Privacy and verification

Highlight that the result contains a SHA-256 transcript fingerprint, not recipient speech. Run the seven-test suite and show it passing.

## 2:55–3:00 — Close

“Consent Envelope turns permission and runtime evidence into one testable contract: check before the call, verify after it.”

## Recording checklist

- Mask every phone number and account identifier.
- Do not display the API-key page, environment variables, browser profile, or email.
- Use the redacted fixture, not the raw call record.
- Keep the video at or below three minutes unless the current rules explicitly allow longer.
- Recheck the final recording frame by frame before publication.
