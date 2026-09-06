# Publication readiness — 2026-09-03

Not yet submission-ready. Resolve these before recording the final demo:

- The real call was placed through the CALL-E dashboard, not this local SDK integration. It proves provider runtime use and supplies a fixture; it does not establish end-to-end execution of this application.
- The auditor is a strict English text-comparison prototype, not a semantic or legal compliance guarantee. Extra speech is a review finding, not proof of harmful disclosure. Provider transcript accuracy has not been independently verified against audio.
- Separate unkeyed hashes identify input bytes; they do not authenticate consent, prove origin, sign the record, or create tamper-proof storage.
- Attempt count, voicemail detection, and hang-up actor currently come from supplied data. Missing evidence must not be presented as a verified pass. A human-answered test did not test voicemail behavior.
- The preflight currently checks declared scope, not actual recipient ownership, semantic task scope, or provider-enforced one-shot dialing. Document these limitations and strengthen recipient binding before live reuse.
- Ordinary authorized publishing is not automatically a Founder gate. Inspect the actual GitHub/video account and terms boundary when ready; do not invent a blanket publication approval requirement.

September 4 update: exact task/recipient binding and demo-only execution rejection are implemented, and malformed evidence checks are covered by 15 passing local tests. These checks do not authenticate consent or enforce provider-side retry policy. Next bounded work: prepare a truthful local demo that explicitly distinguishes fixture replay from live execution. No further call is authorized.
