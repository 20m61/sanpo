# Risk Assessment

## Privacy Risk

sanpo handles relationship context and outing plans.

Mitigation:

- Avoid continuous audio recording.
- Avoid storing raw conversations.
- Store only user-provided summaries.
- Make data deletion easy.

## Cost Risk

LLM calls and real-time infrastructure can become expensive.

Mitigation:

- Generate topic cards in batches.
- Cache generated content.
- Use event-driven triggers.
- Avoid always-on WebSocket for MVP.

## UX Risk

Too many notifications may feel annoying.

Mitigation:

- Use gentle timing.
- Allow users to pause sanpo.
- Keep interventions short.
- Use a soft character tone.

## Social Risk

AI suggestions may feel intrusive or manipulative.

Mitigation:

- Present suggestions as optional.
- Avoid pretending to be a real human.
- Clearly identify sanpo as AI.
- Do not auto-send messages without approval.

## Technical Risk

XR and two-user sync can be complex.

Mitigation:

- Use mock XR for MVP.
- Start with shared topic cards.
- Add real-time sync only after core value is validated.
