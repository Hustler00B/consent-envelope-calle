# Consent Envelope — CALL-E submission draft

## Tagline

Verify what a phone agent was allowed to say, then verify what it actually said.

## Inspiration

A successful phone connection is not the same thing as a compliant call. During a consented CALL-E runtime test, the agent completed the task but added an unapproved question and spoke part of its internal instruction. That gap inspired a two-sided control: validate authorization before dialing and audit the resulting transcript afterward.

## What it does

Consent Envelope is a small Python reference app around the official CALL-E SDK:

1. It loads a structured authorization record with source, activation and expiry times, purpose, disclosure scope, voicemail choice, and revocation state.
2. It fails closed when the authorization is expired, revoked, premature, off-purpose, or asks for disclosures outside the approved scope.
3. It defaults to a redacted dry run. Live execution additionally requires two explicit flags and an API key held outside the project.
4. After a call, it separates bot speech from recipient speech and compares the bot's words with the approved speech budget.
5. It also checks one-shot attempt count, voicemail handling, and who ended the call.
6. It emits a transcript hash and findings without reproducing the recipient's words in the audit result.

## How it was built

The project uses Python and the official `calle-ai==0.2.0` SDK. Preflight and post-call checks are deterministic and covered by seven unit tests. The runtime fixture is redacted and contains no phone number or API key.

## Genuine CALL-E use and result

One Founder-owned number received one explicitly authorized test call. The opening identified the call as an automated AI/CALL-E test. The recipient confirmed availability and said the requested confirmation phrase. CALL-E delivered the closing and ended the 33-second call.

The outcome auditor nevertheless marked the transcript non-compliant with the approved speech budget. It found two additions: an audibility question and a spoken fragment of the control instruction. This is the central demo: ordinary completion reporting says the call succeeded, while Consent Envelope identifies the policy deviation.

## Accomplishments

- A real CALL-E result became a reproducible regression test instead of a marketing claim.
- The phone number, API key, and recipient speech stay out of audit output.
- Dry-run behavior is the default, and tests cannot place calls.
- Pre-call authorization and post-call evidence share one explicit policy envelope.

## Challenges

The CALL-E agent is goal-driven rather than a literal script player, so successful task completion may include unscripted speech. Transcript segmentation also divides one sentence across several `BOT:` spans. The auditor therefore reconstructs normalized bot speech before checking the approved phrases and any residual speech.

## What is next

- Consume structured CALL-E results directly after `create_and_wait`.
- Add signed, append-only authorization and outcome receipts.
- Distinguish harmless conversational variation from semantic disclosure expansion.
- Add CI against sponsor-provided sandbox calls when available.

## Required links before submission

- Public source repository: pending Founder-authorized publication
- CALL-E contribution pull request: pending Founder-authorized GitHub action
- Public demo video: pending Founder-authorized publication

## AI-use disclosure

The project, tests, documentation, and submission draft were produced by an AI agent operating under Founder-defined authorization boundaries. The Founder supplied truthful account information, accepted platform terms, owned and consented to the test number, and explicitly approved the single call. No AI-generated statement is presented as the Founder's personal product opinion.
