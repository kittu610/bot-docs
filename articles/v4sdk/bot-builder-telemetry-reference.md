---
title: Events generated by the Bot Framework Service telemetry | Microsoft Docs
description: Learn what events are triggered with the new telemetry features.
keywords: telemetry, appinsights, monitor bot
author: ivorb
ms.author: kamrani
manager: kamrani
ms.topic: article
ms.service: bot-service
ms.date: 05/23/2019
monikerRange: 'azure-bot-service-4.0'
---

# Events generated by the Bot Framework Service telemetry

## Channel service events

In addition to `WaterfallDialog`, which was discussed in the [telemetry topic](bot-builder-telemetry.md) and which generates events from your bot code, the Bot Framework Channel service also logs events.  This helps you diagnose issues with Channels or overall bot failures.

### CustomEvent: "Activity"
**Logged From:** Channel Service
Logged by the Channel Service when a message received.

### Exception: "Bot Errors"
**Logged From:** Channel Service
Logged by the channel when a call to the Bot returns a non-2XX Http Response.

## CustomEvent: "WaterfallStart" 

When a WaterfallDialog begins, a `WaterfallStart` event is logged.

- `user_id`  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `session_id` ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.activityId`  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.activityType`  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.channelId` ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.DialogId` (This is the dialogId (string) passed into your Waterfall.  You can consider this the "waterfall type")
- `customDimensions.InstanceID` (unique per instance of the dialog)

## CustomEvent: "WaterfallStep" 

Logs individual steps from a Waterfall Dialog.

- `user_id`  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `session_id` ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.activityId`  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.activityType`  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.channelId` ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.DialogId` (This is the dialogId (string) passed into your Waterfall.  You can consider this the "waterfall type")
- `customDimensions.StepName` (either method name or `StepXofY` if lambda)
- `customDimensions.InstanceID` (unique per instance of the dialog)

## CustomEvent: "WaterfallDialogComplete"

Logs when a Waterfall Dialog completes.

- `user_id`  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `session_id` ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.activityId`  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.activityType`  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.channelId` ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.DialogId` (This is the dialogId (string) passed into your Waterfall.  You can consider this the "waterfall type")
- `customDimensions.InstanceID` (unique per instance of the dialog)

## CustomEvent: "WaterfallDialogCancel" 

Logs when a Waterfall Dialog is canceled.

- `user_id`  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `session_id` ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.activityId`  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.activityType`  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.channelId` ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- `customDimensions.DialogId` (This is the dialogId (string) passed into your Waterfall.  You can consider this the "waterfall type")
- `customDimensions.StepName` (either method name or `StepXofY` if lambda)
- `customDimensions.InstanceID` (unique per instance of the dialog)

## CustomEvent: BotMessageReceived 
Logged when bot receives new message from a user.

When not overridden, this event is logged from `Microsoft.Bot.Builder.TelemetryLoggerMiddleware` using the `Microsoft.Bot.Builder.IBotTelemetry.TrackEvent()` method.

- Session Identifier  
  - When using Application Insights, this is logged from the `TelemetryBotIdInitializer`  as the  **session** identifier (*Temeletry.Context.Session.Id*) used within Application Insights.  
  - Corresponds to the [Conversation ID](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#conversation) as defined by Bot Framework protocol..
  - The property name logged is `session_id`.

- User Identifier
  - When using Application Insights, this is logged from the `TelemetryBotIdInitializer`  as the  **user**  identifier (*Telemetry.Context.User.Id*) used within Application Insights.  
  - The value of this property is a combination of the [Channel Identifier](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#channel-id) and the [User ID](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#from) (concatenated together) properties as defined by the Bot Framework protocol.
  - The property name logged is `user_id`.

- ActivityID 
  - When using Application Insights, this is logged from the `TelemetryBotIdInitializer` as a Property to the event.
  - Corresponds to the [Activity ID](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#Id) as defined by Bot Framework protocol..
  - The property name is `activityId`.

- Channel Identifier
  - When using Application Insights, this is logged from the `TelemetryBotIdInitializer` as a Property to the event.  
  - Corresponds to the [Channel Identifier](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#id) of the Bot Framework protocol.
  - The property name logged is `channelId`.

- ActivityType 
  - When using Application Insights, this is logged from the `TelemetryBotIdInitializer` as a Property to the event.  
  - Corresponds to the [Activity Type](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#type) of the Bot Framework protocol.
  - The property name logged is `activityType`.

- Text
  - **Optionally** logged when the `logPersonalInformation` property is set to `true`.
  - Corresponds to the [Activity Text](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#text) field of the Bot Framework protocol.
  - The property name logged is `text`.

- Speak

  - **Optionally** logged when the `logPersonalInformation` property is set to `true`.
  - Corresponds to the [Activity Speak](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#speak) field of the Bot Framework protocol.
  - The property name logged is `speak`.

  - 

- FromId
  - Corresponds to the [From Identifier](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#from) field of the Bot Framework protocol.
  - The property name logged is `fromId`.

- FromName
  - **Optionally** logged when the `logPersonalInformation` property is set to `true`.
  - Corresponds to the [From Name](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#from) field of the Bot Framework protocol.
  - The property name logged is `fromName`.

- RecipientId
  - Corresponds to the [From Name](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#from) field of the Bot Framework protocol.
  - The property name logged is `fromName`.

- RecipientName
  - Corresponds to the [From Name](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#from) field of the Bot Framework protocol.
  - The property name logged is `fromName`.

- ConversationId
  - Corresponds to the [From Name](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#from) field of the Bot Framework protocol.
  - The property name logged is `fromName`.

- ConversationName
  - Corresponds to the [From Name](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#from) field of the Bot Framework protocol.
  - The property name logged is `fromName`.

- Locale
  - Corresponds to the [From Name](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md#from) field of the Bot Framework protocol.
  - The property name logged is `fromName`.

## CustomEvent: BotMessageSend 
**Logged From:** TelemetryLoggerMiddleware 

Logged when bot sends a message.

- UserID  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- SessionID ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- ActivityID  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- Channel  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- ActivityType  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- ReplyToID
- RecipientId
- ConversationName
- Locale
- RecipientName (Optional for PII)
- Text (Optional for PII)
- Speak (Optional for PII)


## CustomEvent: BotMessageUpdate
**Logged From:** TelemetryLoggerMiddleware
Logged when a message is updated by the bot (rare case)
- UserID  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- SessionID ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- ActivityID ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- Channel  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- ActivityType  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- RecipientId
- ConversationId
- ConversationName
- Locale
- Text (Optional for PII)


## CustomEvent: BotMessageDelete
**Logged From:** TelemetryLoggerMiddleware
Logged when a message is deleted by the bot (rare case)
- UserID  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- SessionID ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- ActivityID  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- Channel  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- ActivityType  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- RecipientId
- ConversationId
- ConversationName

## CustomEvent: LuisEvent
**Logged From:** LuisRecognizer

Logs results from LUIS service.

- UserID  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- SessionID ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- ActivityID ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- Channel ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- ActivityType ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- ApplicationId
- Intent
- IntentScore
- Intent2 
- IntentScore2 
- FromId
- SentimentLabel
- SentimentScore
- Entities (as json)
- Question (Optional for PII)

## CustomEvent: QnAMessage
**Logged From:** QnAMaker

Logs results from QnA Maker service.

- UserID ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- SessionID ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- ActivityID ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- Channel ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- ActivityType  ([From Telemetry Initializer](https://aka.ms/telemetry-initializer))
- Username (Optional for PII)
- Question (Optional for PII)
- MatchedQuestion
- QuestionId
- Answer
- Score
- ArticleFound
