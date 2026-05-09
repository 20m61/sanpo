# sanpo

**2人でも、さんぽ。**

sanpo is an XR + notification service that brings a cute ghost-like third friend into outings between two people.

During an outing, sanpo runs on both users' smartphones, understands the outing plan, time, location, relationship context, and prior memories, then gently speaks through notifications and XR presence to reduce awkward silence and help the two people enjoy the outing as if a third friend were walking with them.

## 日本語サマリー

sanpoは、2人でのお出かけに「3人目」を連れていく、XR＋通知型のサービスです。

2人で出かけると、会話を続ける責任が2人だけに集中し、沈黙や話題切れが気まずさにつながることがあります。sanpoは、お出かけプラン、時間、位置、関係性、これまでの文脈をもとに、通知やXR上の存在としてやさしく会話を仕掛けます。

これにより、利用者は「何を話すか」「いつ話題を変えるか」「気まずい沈黙をどう埋めるか」を自分で考え続ける必要がなくなります。会話の話題生成、空気読み、沈黙処理、雰囲気づくりといった社会的労働を、AIの3人目に外部化します。

## Hackathon Entry Status

AI-DLC Inception phase has been completed for hackathon entry.

The repository currently includes:

- project vision
- requirements analysis
- user stories
- application design
- units of work
- risk assessment
- cost control strategy
- demo plan
- audit log

Construction will start from U1: Project Foundation, followed by the minimal MVP for a two-user outing session, mock XR presence, shared cue cards, and simulated notifications.

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
