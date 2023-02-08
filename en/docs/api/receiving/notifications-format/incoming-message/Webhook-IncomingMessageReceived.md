# Incoming messages

This section describes the general format of incoming webhooks with the `incomingMessageReceived` type. Description of all incoming webhooks types is given in [Incoming webhooks types](../type-webhook.md) section.

The system provides for receiving notifications about incoming messages of the below types:

- [Incoming text message](TextMessage.md)
- [Selecting a regular button](/docs/api/receiving/notifications-format/selected-buttons/ButtonsResponseMessage.md)
- [Selecting a template button](/docs/api/receiving/notifications-format/selected-buttons/TemplateButtonsReplyMessage.md)
- [Selecting a List Item](/docs/api/receiving/notifications-format/selected-buttons/ListResponseMessage.md)
- [Incoming text message with URL](ExtendedTextMessage.md)
- [Incoming image, video, audio, document message](ImageMessage.md)
- [Incoming location message](LocationMessage.md)
- [Incoming contact message](ContactMessage.md)
- [Incoming message with an array of contacts](ContactsArrayMessage.md)
- [Incoming quoted message](QuotedMessage.md)
- [Incoming message with sticker](StickerMessage.md)
- [Incoming message-reaction](ReactionMessage.md)
- [Incoming message with an invitation to the group](GroupInviteMessage.md)
- [Incoming poll message](PollMessage.md)

## incomingMessageReceived webhook parameters {#webhook-parameters}

Parameter | Type | Description
----- | ----- | -----
`typeWebhook` | **string** | [Incoming webhook type](../type-webhook.md). For a webhook of this type, the paramaeter takes on the value `incomingMessageReceived`
`instanceData` | **object** | Account data
`timestamp` | **integer** | Event timestamp in UNIX format
`idMessage` | **string** | Incoming message Id
`senderData` | **object** | Message or file sender data
`messageData` | **object** | Received message or file data

`instanceData` object parameters

Parameter | Type | Description
----- | ----- | -----
`idInstance` | **integer** | Account Id
`wid` | **string** | Account Id in WhatsApp format
`typeInstance` | **string** | Account messenger type 

`senderData` object parameters

Parameter | Type | Description
----- | ----- | -----
`chatId` | **string** | [Chat Id](../../../chat-id.md), where a message or file has been received
`sender` | **string** | Message or file sender [Id](../../../chat-id.md#corr) 
`chatName` | **string** | chat name
`senderName` | **string** | Sender name

### `messageData` object parameters

`messageData` object has different parameters depending on incoming message type:

- [Incoming text message](TextMessage.md)
- [Incoming text message with URL](ExtendedTextMessage.md)
- [Incoming image, video, audio, document message](ImageMessage.md)
- [Incoming location message](LocationMessage.md)
- [Incoming contact message](ContactMessage.md)
- [Incoming message with an array of contacts](ContactsArrayMessage.md)
- [Incoming quoed message](QuotedMessage.md)
- [Incoming message with sticker](StickerMessage.md)
- [Incoming message-reaction](ReactionMessage.md)
- [Incoming message with an invitation to the group](GroupInviteMessage.md)
- [Incoming poll message](PollMessage.md)

### Webhook body example {#webhook-example-body}

```json
{
    "typeWebhook": "incomingMessageReceived",
    "instanceData": {
        "idInstance": 1234,
        "wid": "11001234567@c.us",
        "typeInstance": "whatsapp"
    },
    "timestamp": 1588091580,
    "idMessage": "F7AEC1B7086ECDC7E6E45923F5EDB825",
    "senderData": {
        "chatId": "79001234568@c.us",
        "sender": "79001234568@c.us",
        "chatName": "Green API",
        "senderName": "Green API"
    },
    "messageData":{
       // Depending on typeMessage = textMessage || imageMessage || videoMessage || documentMessage || audioMessage || locationMessage || contactMessage || extendedTextMessage || quotedMessage
       ...
       ...
       ...
        }
    }
}
```