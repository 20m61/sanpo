# Requirements Analysis

## Functional Requirements

1. Users can create an outing session.
2. Two users can join the same outing session.
3. Users can input outing plan and relationship context.
4. sanpo generates conversation cue cards.
5. sanpo displays cue cards as notifications or XR-like overlays.
6. sanpo provides timing-based interventions.
7. sanpo can generate follow-up messages after the outing.

## Non-Functional Requirements

1. Low cost.
2. Stable AWS-first architecture.
3. Privacy-conscious design.
4. No always-on audio recording.
5. No constant GPS polling.
6. Minimal LLM calls.
7. MVP must be feasible quickly.

## Constraints

- Use AWS resources as much as possible.
- Use Amazon Bedrock for generation.
- Use Strands Agents for third-friend behavior.
- Use mock XR for MVP.
- Avoid expensive real-time infrastructure unless justified.

## Out of Scope for MVP

- Native mobile app
- Full ARKit / ARCore implementation
- Continuous audio analysis
- Continuous location tracking
- Production-grade push notifications
- Long-term RAG memory
