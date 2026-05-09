# Application Design

## Architecture Overview

sanpo is a low-cost, event-driven, serverless web app on AWS. Two phones talk to a shared backend; the "third friend" is a Strands Agent flow on top of Amazon Bedrock that generates cue cards in batches.

```
[Phone A]          [Phone B]
    \                /
     \              /
      v            v
   CloudFront + S3 (static web, mock XR overlay)
            |
            v
      API Gateway (HTTP API)
            |
            v
         Lambda  ──>  Bedrock  (cue + follow-up generation, via Strands Agents)
            |
            v
        DynamoDB  (single-table)
            ^
            |
   EventBridge Scheduler  (per-session timed nudges)
```

Auth: Amazon Cognito user pool (email + magic-link or simple password) for MVP. A "guest mode" with anonymous sessionId can be added if Cognito is too heavy for demo time.

## Components

### Frontend (`app/`)
- Static web app (Vite + vanilla TS or React; minimal).
- Routes: `/`, `/session/new`, `/session/join`, `/session/:id`, `/session/:id/end`.
- Mock XR overlay = absolutely-positioned ghost SVG with CSS keyframes; cards float up from bottom.
- Polls `GET /sessions/:id/cards?since=` every 10s while session is active.

### API (Lambda + API Gateway HTTP API)
| Method | Path                          | Purpose                                         |
|--------|-------------------------------|-------------------------------------------------|
| POST   | /sessions                     | Create session, return `{sessionId, joinCode}`  |
| POST   | /sessions/{id}/join           | Join with code; mark session active             |
| PUT    | /sessions/{id}/context        | Save plan + relationship context                |
| POST   | /sessions/{id}/cards/generate | Trigger initial batch generation (Strands+Bedrock) |
| GET    | /sessions/{id}/cards          | List cards (with `since` cursor)                |
| POST   | /sessions/{id}/help           | Pop next unused card (no LLM call when warm)    |
| POST   | /sessions/{id}/pause          | Pause scheduler                                 |
| POST   | /sessions/{id}/end            | End session, trigger follow-up generation       |
| GET    | /sessions/{id}/followup       | Fetch generated follow-up draft                 |

All responses JSON. No WebSocket in MVP.

### AI — Strands Agent
A single agent flow:
1. **ContextSummarizer** — collapses user-provided plan + relationship into a compact prompt.
2. **CueCardGenerator** — produces 10–20 cards as JSON: `{timing, content, reason}`.
3. **FollowupComposer** — produces a short JP message after session end.

Strands Agents orchestrates the steps; Bedrock provides the underlying LLM. Default model: a low-cost text model in `ap-northeast-1` (e.g., a Claude Haiku-class model). Safety: rely on Bedrock's content filters + a short system instruction enforcing JP, gentle tone, no PII, no claims of being human.

### Scheduling
Amazon EventBridge Scheduler — one schedule per session (created on activation, deleted on pause/end). Targets a Lambda that flips the next nudge card to "ready" — no LLM call.

### Data Store — DynamoDB single-table

PK / SK layout:

| PK              | SK                  | Item kind          |
|-----------------|---------------------|--------------------|
| `SESSION#<id>`  | `META`              | OutingSession      |
| `SESSION#<id>`  | `CTX`               | RelationshipCtx    |
| `SESSION#<id>`  | `CARD#<seq>`        | TopicCard          |
| `SESSION#<id>`  | `FOLLOWUP`          | FollowupDraft      |
| `JOINCODE#<c>`  | `META`              | JoinCode → session |
| `USER#<uid>`    | `SESSION#<id>`      | User membership    |

GSI-1: `joinCode` → session lookup. TTL on session items at 24h after `endedAt` to auto-evict.

### Data Model

**OutingSession**: `sessionId`, `userIds[]`, `joinCode`, `outingPlan`, `status` (`created`/`active`/`paused`/`ended`), `startedAt`, `endedAt`.

**RelationshipContext**: `sessionId`, `relationshipSummary`, `knownTopics[]`, `avoidTopics[]`, `tone`.

**TopicCard**: `cardId`, `sessionId`, `seq`, `timing` (`start`/`mid`/`help`/`scheduled`), `content`, `reason`, `status` (`pending`/`shown`/`used`).

**FollowupDraft**: `sessionId`, `text`, `generatedAt`.

## MVP Sequence: Two-User Join

```
A: POST /sessions                 -> {sessionId, joinCode=ABC123}
A: PUT  /sessions/:id/context     (plan, relationship)
A: shares "ABC123" via LINE
B: POST /sessions/:id/join {code} -> 200, status=active
A,B: POST /sessions/:id/cards/generate (Strands+Bedrock, 1 call)
A,B: poll GET /sessions/:id/cards
B: POST /sessions/:id/help         -> next card (no LLM)
EventBridge: scheduled nudge       -> mark next scheduled card ready
A: POST /sessions/:id/end          -> Bedrock follow-up (1 call)
A,B: GET /sessions/:id/followup
```

## Security & Privacy
- Cognito-protected API; all writes scoped to the caller's sessions.
- No audio capture. Camera permission optional (mock XR works without).
- Session items auto-expire via DynamoDB TTL.
- "Delete my data" = drop session items by PK.
