# Application Design

## Architecture Overview

sanpo uses a low-cost serverless AWS architecture.

## Components

### Frontend

- Static web app
- Mock XR overlay
- Session screen
- Topic card screen
- Notification-like UI

Candidate:

- S3 + CloudFront
- Next.js static export or Vite

### Authentication

- Amazon Cognito

### API

- Amazon API Gateway
- AWS Lambda

### Data Store

- Amazon DynamoDB

Stores:

- users
- outing sessions
- relationship context
- generated topic cards
- intervention history

### AI

- Amazon Bedrock
- Strands Agents

Strands Agents manages the behavior of the AI third friend.

### Scheduling

- Amazon EventBridge Scheduler

Used for time-based interventions.

## Data Model

### User

- userId
- displayName
- preferences

### OutingSession

- sessionId
- userIds
- outingPlan
- status
- startedAt
- endedAt

### RelationshipContext

- sessionId
- relationshipSummary
- knownTopics
- avoidTopics
- tone

### TopicCard

- cardId
- sessionId
- timing
- content
- reason
- status

## MVP Flow

1. Create outing session.
2. Join with second user.
3. Input outing plan and relationship context.
4. Generate initial topic cards.
5. Display shared XR-like third friend.
6. Show cue cards based on time or user action.
7. Generate follow-up message.
