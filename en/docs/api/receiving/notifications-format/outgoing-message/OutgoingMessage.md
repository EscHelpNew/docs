# Message sent from phone

The format of a message sent fromphone is identical to [incoming message](../incoming-message/Webhook-IncomingMessageReceived.md) format, while [incoming webhook type](../type-webhook.md) takes on the value `outgoingMessageReceived`.

### Webhook body example {#webhook-example-body}

```json
{
    "typeWebhook": "outgoingMessageReceived",
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
       // Depending on typeMessage = textMessage || imageMessage || videoMessage || documentMessage || audioMessage || locationMessage || contactMessage || extendedTextMessage
       ...
       ...
       ...
        }
    }
}
```
