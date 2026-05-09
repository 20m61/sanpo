# Cost Control Strategy

## Principle

sanpo should feel always present, but should not compute constantly.

## Avoid

- Always-on audio recording
- Constant GPS polling
- Constant LLM calls
- Always-on WebSocket
- Full native AR implementation in MVP

## Use Instead

- Event-driven AI generation
- Batch topic generation
- DynamoDB caching
- Mock XR overlay
- Time-based intervention
- User-triggered "help" button

## Bedrock Usage

Generate 10-20 topic cards at outing start.

Only call Bedrock again when:

- users request help
- outing context changes significantly
- follow-up message is needed

## Synchronization

MVP can use:

- shared session state
- polling
- simple API updates

Real-time WebSocket is optional for later phases.

## MVP Cost Goal

The MVP should remain near free-tier or very low monthly cost during prototype usage.
