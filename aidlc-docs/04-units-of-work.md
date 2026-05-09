# Units of Work

Order reflects implementation sequence. **MVP** units gate the demo; **Post-MVP** are fast-followers.

## MVP

### U1 — Project Foundation (P0)
Repo, AI-DLC docs, `app/` skeleton, README. Static dev server runs locally.
- Depends on: —
- Done when: `pnpm dev` (or equivalent) serves a placeholder home page.

### U2 — Outing Session (P0, FR-1, FR-2, FR-9)
Create / join / pause / end flows. DynamoDB single-table writes. Join codes.
- Depends on: U1
- Done when: Two browsers reach the same session via a code.

### U3 — Relationship Context (P0, FR-3)
Form + persistence for plan, relationship summary, knownTopics, avoidTopics, tone.
- Depends on: U2
- Done when: Context round-trips to DynamoDB and is visible to both users.

### U4 — Third-Friend Agent (P0, FR-4, FR-8)
Strands Agents flow (ContextSummarizer → CueCardGenerator → FollowupComposer) on Bedrock. JSON output, JP tone, AI-labeled.
- Depends on: U3
- Done when: One Bedrock call yields ≥ 10 valid cards persisted as `CARD#<seq>`.

### U5 — Topic Card System (P0, FR-4, FR-5, FR-6)
Card list endpoint, "help" pop-next, mark-as-shown / used.
- Depends on: U4
- Done when: Help-tap surfaces a fresh card in < 2s and never repeats within a session.

### U6 — Mock XR Presence (P0, FR-5, US-7)
CSS/SVG ghost overlay + floating card animation. No real AR.
- Depends on: U5
- Done when: Both phones display the ghost over the camera-style background.

### U7 — Notification Simulation + Scheduler (P0/P1, FR-7)
EventBridge Scheduler creates per-session nudges; Lambda flips card to "ready". UI shows toast-style notification.
- Depends on: U5
- Done when: A scheduled nudge fires once during a demo session.

### U8 — Follow-up Generation (P0, FR-8, US-8)
End-session flow → FollowupComposer → display copyable JP message.
- Depends on: U4, U2
- Done when: Ending the session shows a follow-up draft.

### U9 — Cost Control (P0, NFR-1, NFR-3)
Batch generation, idempotent /generate, DDB TTL, polling instead of WebSocket. CloudWatch alarm at $1/mo.
- Depends on: U4, U2
- Done when: Per-outing Bedrock invocations ≤ 3 in instrumented run.

### U10 — Demo Preparation (P0)
Demo scenario, screenshots, submission text, fallback recorded video.
- Depends on: U6, U7, U8
- Done when: 90-second demo runs end-to-end on two browsers.

## Post-MVP

- **U11** — Cognito auth (replace guest mode if used in MVP).
- **U12** — Real push notifications (APNs/FCM).
- **U13** — Long-term memory across outings.
- **U14** — Native AR (ARKit/ARCore).
- **U15** — Realtime sync via WebSocket / IoT Core.

## Dependency Graph

```
U1 → U2 → U3 → U4 → U5 → U6
                    ↘ U7
              U4,U2 → U8
              U4,U2 → U9
            U6,U7,U8 → U10
```
