# Simple button selection

This section describes  `messageData` object incoming webhook format for simple buttons. For a description of the general format of incoming webhooks, refer to [Incoming messages](/../docs/api/receiving/notifications-format/) section. 

## Webhook {#webhook}

### Webhook parameters {#webhook-parameters}

`messageData` object parameters

Parameter | Type | Description
----- | ----- | -----
`typeMessage` | **string** | Received message type. For messages of this type, the parameter takes on the value `buttonsResponseMessage`
`buttonsResponseMessage` | **object** | Data object on the user button selection data

`buttonsResponseMessage` object parameters

Parameter | Type | Description
----- | ----- | -----
`selectedButtonId` | **string** | selected button identifier
`selectedButtonText` | **string** | selected button text
`stanzaId` | **string** | button message ID

### Webhook body example {#webhook-example-body}

```json
{
    "typeWebhook": "incomingMessageReceived",
    "instanceData": {
        "idInstance": 1101000001,
        "wid": "11001234567@c.us",
        "typeInstance": "whatsapp"
    },
    "timestamp": 1656315272,
    "idMessage": "9BB19BB0D568BA7B185EEAD21A33D317",
    "senderData": {
        "chatId": "11001234567@c.us",
        "sender": "11001234567@c.us",
        "senderName": "Green API"
    },
    "messageData": {
        "typeMessage": "buttonsResponseMessage",
        "buttonsResponseMessage": {
            "stanzaId": "BAE53AFDD5F0C137",
            "selectedButtonId": "1",
            "selectedButtonText": "Green"
        }
    }
}
```
