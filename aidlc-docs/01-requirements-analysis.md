# Requirements Analysis

## Intent Summary

Two-person outings concentrate all conversation labor on two people. sanpo externalizes part of that labor by acting as a cute, gently present third friend that suggests topics, eases silence, and helps maintain atmosphere — without recording audio, polling location, or running heavy realtime infrastructure.

## Functional Requirements

| ID    | Requirement                                                                 | Acceptance                                                                                                             |
|-------|-----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| FR-1  | A user can create an outing session and obtain a join code/link.            | POST creates a session; response returns sessionId and a 6-char join code.                                             |
| FR-2  | A second user can join an existing session via the join code.              | Both users are listed on the session; status transitions `created` → `active`.                                          |
| FR-3  | Users can input outing plan and lightweight relationship context.          | Stored fields: plan text, relationship summary, knownTopics[], avoidTopics[], tone.                                     |
| FR-4  | sanpo generates conversation cue cards from the session context.           | At session activation, 10–20 cue cards are produced via Bedrock and persisted.                                          |
| FR-5  | Both users see the same cards and the same XR third-friend presence.       | Same payload returned to both userIds for the same sessionId.                                                           |
| FR-6  | A user can request "help me out" to surface a fresh card immediately.     | Tap → next unused card appears within 2s without a new LLM call when cache is warm.                                     |
| FR-7  | sanpo provides time-based interventions during the outing.                 | EventBridge Scheduler-driven nudges fire at preconfigured offsets (e.g., +10m, +30m).                                   |
| FR-8  | sanpo generates a follow-up message draft after the outing ends.           | One Bedrock call; users can copy/share text; nothing auto-sent.                                                          |
| FR-9  | A user can pause sanpo or end the session.                                 | Pause halts scheduled triggers; end transitions status to `ended` and surfaces follow-up.                                |
| FR-10 | sanpo never claims to be human and is always labeled as AI.                | UI shows "AI" badge; copy avoids deceptive first-person human claims.                                                    |

## Non-Functional Requirements

| ID     | Category      | Target                                                                 |
|--------|---------------|------------------------------------------------------------------------|
| NFR-1  | Cost          | MVP monthly cost during prototype usage stays within AWS free tier or under ~$5/mo. |
| NFR-2  | Latency       | Card fetch p95 < 500 ms; help-tap → card visible < 2s (cache hit).     |
| NFR-3  | LLM frugality | Default ≤ 3 Bedrock invocations per outing (start + help burst + follow-up). |
| NFR-4  | Privacy       | No always-on audio. No continuous GPS. No raw conversation storage.     |
| NFR-5  | Availability  | Stateless Lambda + DynamoDB; no always-on compute, no WebSocket in MVP. |
| NFR-6  | Buildability  | MVP demoable end-to-end within hackathon timeline; static web + API.    |
| NFR-7  | Safety        | All AI output passes a Bedrock-side or prompt-level safety guard before display. |
| NFR-8  | Observability | CloudWatch logs for Lambda; per-session metric: cards generated, help taps, cost units. |

## Constraints

- AWS-first.
- Generation via Amazon Bedrock (default model: a low-cost text model in ap-northeast-1).
- Third-friend behavior orchestrated via Strands Agents.
- Mock XR overlay (CSS/Canvas) is acceptable for MVP; no native AR SDKs.
- Synchronization via short-interval polling, not WebSocket, for MVP.

## Out of Scope (MVP)

- Native iOS/Android app
- ARKit / ARCore
- Continuous audio analysis
- Continuous location tracking
- APNs/FCM production push
- Long-term RAG memory across outings
- Multi-language model fine-tuning

## Assumptions

- Users have modern smartphone browsers with camera permission optional (mock XR works without it).
- Both users are willing to share a join code via existing chat tools (LINE/SMS).
- Demo is presented in Japanese; copy is JP-first.
