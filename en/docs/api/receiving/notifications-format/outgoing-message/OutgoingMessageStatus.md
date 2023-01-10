# Outgoing message status

Incoming webhook of this type contains the status of a previously sent message: sent, delivered, read, etc.

## Webhook {#webhook}

### Webhook parameters {#webhook-parameters}

Parameter | Type | Description
----- | ----- | -----
`typeWebhook` | **string** | [Incoming webhook type](../type-webhook.md). For webhooks of this type the parameter takes on the value `outgoingMessageStatus`
`instanceData` | **object** | Account data 
`timestamp` | **integer** | Event timestamp in UNIX format
`idMessage` | **string** | Outgoing message or file Id. Outgoing message Id is returned by methods: [SendMessage](../../../../api/sending/SendMessage.md), [SendFileByUrl](../../../../api/sending/SendFileByUrl.md), [SendFileByUpload](../../../../api/sending/SendFileByUpload.md), [SendLocation](../../../../api/sending/SendLocation.md), [SendContact](../../../../api/sending/SendContact.md), [SendLink](../../../../api/sending/SendLink.md)
`status` | **string** | Outgoing message or file status. Status takes on the values:
| | `sent` - message sent
| | `delivered` - message delivered to the recipient
| | `read` - message read/viewed/heard by the recipient
| | `failed` - an error occurred while sending a message to WhatsApp server
| | `noAccount` - the recipient's phone number does not have a WhatsApp account 
| | `notInGroup` - the sender is not a participant of a group chat where the message is being sent to
`sendByApi` | **boolean** | Is the message sent through API: true , false

`instanceData` object parameters

Parameter | Type | Description
----- | ----- | -----
`idInstance` | **integer** | Account Id
`wid` | **string** | Account Id in WhatsApp format
`typeInstance` | **string** | Account messenger type

### Webhook body example {#webhook-example-body}

```json
{
    "typeWebhook": "outgoingMessageStatus",
    "timestamp": 1586700802,
    "instanceData": {
        "idInstance": 1234,
        "wid": "11001234567@c.us",
        "typeInstance": "whatsapp"
    },
    "timestamp": 1586700802,
    "idMessage": "3EB0608D6A2901063D63",
    "status": "noAccount",
    "sendByApi": true
}
```
