# sanpo

**2人でも、3人さんぽ。**

sanpo is an XR + notification service that brings a cute ghost-like third friend into outings between two people.

During an outing, sanpo runs on both users' smartphones, understands the outing plan, time, location, relationship context, and prior memories, then gently speaks through notifications and XR presence to reduce awkward silence and help the two people enjoy the outing as if a third friend were walking with them.

## Human-degrading impact

People no longer need to work hard to:

- think of conversation topics
- read awkward social cues
- fill silence
- decide when to change topics
- create a comfortable atmosphere

sanpo externalizes the social labor of maintaining a two-person conversation.

## AI-DLC

This project follows AI-DLC.

The human defines intent, constraints, and review decisions.  
AI assists with requirements analysis, application design, unit decomposition, implementation planning, and quality review.

## AWS Architecture

The MVP is designed with:

- Amazon Bedrock
- Strands Agents
- Amazon Cognito
- Amazon API Gateway
- AWS Lambda
- Amazon DynamoDB
- Amazon S3
- Amazon CloudFront
- Amazon EventBridge

## MVP Scope

The initial MVP focuses on:

- two-person outing session
- cute AI third friend concept
- mock XR presence
- shared conversation cue cards
- simulated notifications
- low-cost event-driven architecture

## Cost Strategy

sanpo avoids:

- always-on audio recording
- constant GPS polling
- constant LLM calls
- always-on WebSocket infrastructure
- expensive full AR implementation

Instead, it uses event-triggered generation, cached topic cards, and lightweight mock XR UI.
