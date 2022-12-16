# Отправленное сообщение через API

Формат сообщения, отправленного с API, идентичен формату [входящего сообщения](../incoming-message/Webhook-IncomingMessageReceived.md), при этом [тип входящего уведомления](../type-webhook.md) принимает значение `outgoingAPIMessageReceived`.

### Пример тела уведомления {#webhook-example-body}

```json
{
    "typeWebhook": "outgoingAPIMessageReceived",
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
       // В зависимости от typeMessage = textMessage || imageMessage || videoMessage || documentMessage || audioMessage || locationMessage || contactMessage || extendedTextMessage
       ...
       ...
       ...
        }
    }
}
```