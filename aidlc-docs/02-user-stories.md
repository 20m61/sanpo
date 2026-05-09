# User Stories

Priority: **P0** = MVP must-have, **P1** = MVP nice-to-have, **P2** = post-MVP.

## Personas

- **Aoi** — invites a friend to a casual outing, slightly anxious about silence.
- **Hina** — joins the outing, happy to react but rarely initiates topics.

Both are 20s–30s smartphone users in Japan.

## Stories

### US-1 — Start an outing (P0, FR-1)
As Aoi, I want to start an outing session and get a short join code, so that I can invite Hina without setup friction.
- AC: Tapping "Start" creates a session in < 2s and shows a 6-char code.
- AC: The code can be copied to clipboard with one tap.

### US-2 — Join an outing (P0, FR-2)
As Hina, I want to enter a code from Aoi and land on the same session, so that we share the same sanpo experience.
- AC: Entering a valid code activates the session for both users.
- AC: Invalid codes show a clear error.

### US-3 — Add relationship context (P0, FR-3)
As either user, I want to tell sanpo a couple of facts (we're old friends / we work together / avoid work talk), so that suggestions feel relevant.
- AC: Form accepts plan, relationship summary, knownTopics, avoidTopics, tone.
- AC: Submission triggers initial card generation.

### US-4 — See shared cue cards (P0, FR-4, FR-5)
As either user, I want to see the same conversation cue cards on both phones, so it feels like a shared third friend.
- AC: Cards list returns identical content for both userIds.
- AC: At least 10 cards available at session start.

### US-5 — Tap "help" when silence hits (P0, FR-6)
As Hina, I want a "ちょっと助けて" button, so that sanpo surfaces a fresh light topic instantly.
- AC: Help-tap shows a card within 2s.
- AC: Cards are not repeated in the same session unless the pool is exhausted.

### US-6 — Time-based gentle nudge (P1, FR-7)
As either user, I want sanpo to softly nudge us at sensible intervals, so the third-friend feeling persists without being noisy.
- AC: At least one scheduled nudge fires per outing.
- AC: Nudges can be paused.

### US-7 — XR ghost presence (P1, FR-5)
As either user, I want sanpo to appear as a small ghost-like overlay on the screen, so it feels like a third friend is walking with us.
- AC: Mock XR overlay renders on a phone-sized viewport.
- AC: Idle animation runs without draining battery (CSS-only).

### US-8 — Follow-up message after outing (P0, FR-8)
As Aoi, after the outing I want a draft follow-up message, so I can keep the relationship warm without thinking hard.
- AC: One Bedrock call produces a short JP message.
- AC: Nothing is sent automatically; user copies manually.

### US-9 — Pause / end session (P0, FR-9)
As either user, I want to pause or end the outing, so I stay in control of sanpo's presence.
- AC: Pause stops scheduled nudges within one tick.
- AC: End surfaces follow-up flow.

### US-10 — AI labeling (P0, FR-10, NFR-7)
As either user, I want sanpo to clearly identify as AI, so I'm never deceived.
- AC: "AI" badge visible on cards and ghost UI.
- AC: Copy avoids implying sanpo is a real human.
