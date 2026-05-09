# AI-DLC State

Project: sanpo
Phase: Inception → Construction (handoff)
Status: Inception closed; ready to begin Construction unit U1.

## Inception Checklist

- [x] Workspace Detection — greenfield, AI-DLC scaffolding present.
- [x] Requirements Analysis — FR-1..FR-10, NFR-1..NFR-8 with acceptance criteria.
- [x] User Stories — US-1..US-10 with priorities and ACs.
- [x] Workflow Planning — implicit in units-of-work + demo-plan.
- [x] Application Design — APIs, DDB single-table, Strands flow, sequence.
- [x] Units Generation — U1..U10 MVP, U11..U15 post-MVP, dep graph.
- [x] Risk Assessment — privacy, cost, UX, social, technical.
- [x] Cost Control Strategy — batched generation, no WebSocket, TTL eviction.
- [x] Demo Planning — 5-scene story for hackathon judging.
- [x] Audit Log — `audit.md` initialized.

## Extension Configuration

| Extension                | Enabled | Notes                                                              |
|--------------------------|---------|--------------------------------------------------------------------|
| security/baseline        | Yes     | Cognito-protected API, no audio capture, TTL eviction, AI labeling |
| testing/property-based   | No      | Skipped for hackathon scope; out of MVP                            |

## Human Role

The human defines product intent, emotional problem, constraints, review criteria, final direction, and demo narrative.

## AI Role

AI assists with requirements analysis, user story generation, application design, unit decomposition, risk/cost analysis, and review.

## Current Intent

Two-person outings concentrate conversation labor on two people. sanpo introduces a cute AI third friend, surfaced via notifications and mock XR, that suggests topics, eases silence, and helps maintain atmosphere — without recording audio, polling location, or running always-on infrastructure. Demo target: AWS Summit Japan 2026 Hackathon (theme: services that make humans lazy).

## Construction Plan (Next)

Implement units in sequence:

1. **U1** Project Foundation — `app/` skeleton (Vite + TS), README, dev server.
2. **U2** Outing Session — DynamoDB single-table, create/join/pause/end APIs.
3. **U3** Relationship Context — form + persistence.
4. **U4** Third-Friend Agent — Strands Agents on Bedrock (cue + follow-up).
5. **U5** Topic Card System — list + help-pop endpoint.
6. **U6** Mock XR Presence — CSS/SVG ghost overlay.
7. **U7** Notification Simulation + EventBridge Scheduler.
8. **U8** Follow-up Generation.
9. **U9** Cost Control — batching, TTL, alarm.
10. **U10** Demo Preparation — scenario, screenshots, fallback video.

Stop conditions per unit: see "Done when" in `04-units-of-work.md`.
