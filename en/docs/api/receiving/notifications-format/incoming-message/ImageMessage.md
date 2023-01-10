# Incoming image, video, audio, document message

This section describes `messageData` object incoming webhook format for incoming image, video, audio or document message. For a description of the general format of incoming webhooks, refer to [Incoming messages](Webhook-IncomingMessageReceived.md) section. 

To get incoming webhooks of this type, two conditions must be true:

`typeWebhook` = `incomingMessageReceived`

`messageData.typeMessage` = `imageMessage` || `videoMessage` || `documentMessage` || `audioMessage`

## Webhook {#webhook}

### Webhook parameters {#webhook-parameters}

`messageData` object parameters

Parameter | Type | Description                                                                                                                                               |
| ----------------- | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
`typeMessage` | **string** | Received message type. For messages of this type, the parameter takes on the value: `imageMessage`, `videoMessage`, `documentMessage`, `audioMessage` |
`fileMessageData ` | **object** | Received file data object                                                                                                                 |
| `quotedMessage`   | **object** | Quoted message data object. Present only if the message itself is a quote                                                                 |        

`fileMessageData` object parameters 

Parameter | Type | Description
----- | ----- | -----
`downloadUrl` | **string** | Link to download file
`caption` | **string** | File caption
| `fileName` | **string** | File name |
| `mimeType` | **string** | File type according to the classification [Media Types](https://www.iana.org/assignments/media-types/media-types.xhtml) |


`quotedMessage` object parameters

| Parameter     | Type        | Description            |
| ------------- | ---------- | ------------------- |
| `stanzaId` | **string** | Quoted message id |
| `participant` | **string** | Quoted message sender's id |
| `typeMessage` | **string** | Quoted message type |

The rest of the fields are filled depending on the type of the quoted message and are identical to the fields of incoming messages described in [Incoming messages](Webhook-IncomingMessageReceived.md) section

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
  "messageData": {
    "typeMessage": "imageMessage",
    "fileMessageData": {
      "downloadUrl": "https://api.green-api.com/waInstance1234/downloadFile/19136A974392FA8CF584D70DD0E1AEDF",
      "caption": "Image",
      "jpegThumbnail": "",
      "mimeType": "image/jpeg",
      "forwardingScore": 4,
      "isForwarded": true
    }
  }
}
```

### Audio and text quote incoming message webhook body example {#webhook-example-body}

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
  "messageData": {
    "typeMessage": "audioMessage",
    "fileMessageData": {
      "downloadUrl": "https://sw-media.storage.yandexcloud.net/9901742665/39c20293-eb8d-abdd-5fdd1b83820a.mpga",
      "fileName": "39c20293-eb8d-abdd-5fdd1b83820a.mpga",
      "mimeType": "image/jpeg",
      "forwardingScore": 4,
      "isForwarded": true
    },
    "quotedMessage": {
      "stanzaId": "9A73322488DCB7D9689A6112F2528C9D",
      "participant": "79001234569@c.us",
      "typeMessage": "textMessage",
      "textMessage": "Hello"
    }
  }
}
```

### Audio and audio/video/document quote incoming message webhook body example {#webhook-example-body}

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
  "messageData": {
    "typeMessage": "audioMessage",
    "fileMessageData": {
      "downloadUrl": "https://s/990173687/801078ab-3340-4e4aa5.ogg",
      "caption": "",
      "fileName": "801078ab-3340-4f78-е9978be4aa5.ogg",
      "jpegThumbnail": "",
      "mimeType": "audio/ogg",
      "forwardingScore": 4,
      "isForwarded": true
    },
    "quotedMessage": {
      "stanzaId": "9A73322488DCB7D9689A6112F2528C9D",
      "participant": "79001234568@c.us",
      "typeMessage": "imageMessage",
      "downloadUrl": "",
      "caption": "",
      "jpegThumbnail": ""
    }
  }
}
```

### Image and location quote incoming message webhook body example {#webhook-example-body}

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
  "messageData": {
    "typeMessage": "imageMessage",
    "fileMessageData": {
      "downloadUrl": "https://sw-media.storage.yandexcloud.net/0b-9784-483b-8426-e8d871d6de9f.jpeg",
      "caption": "",
      "fileName": "d417740b483b-8426-e8d871d6de9f.jpeg",
      "jpegThumbnail": "",
      "mimeType": "image/jpeg",
      "forwardingScore": 4,
      "isForwarded": true
    },
    "quotedMessage": {
      "stanzaId": "9A73322488DCB7D9689A6112F2528C9D",
      "participant": "79060002233@c.us",
      "typeMessage": "locationMessage",
      "location": {
        "nameLocation": "",
        "address": "",
        "jpegThumbnail": "",
        "latitude": 72.5922702,
        "longitude": 45.6645388
      }
    }
  }
}
```

### Image and contact quote incoming message webhook body example {#webhook-example-body}

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
  "messageData": {
    "typeMessage": "imageMessage",
    "fileMessageData": {
      "downloadUrl": "https://sw-media.storage.yandexcloud.net/542ad819-166b-40a4-b0e1-279069cd03bb.jpeg",
      "caption": "",
      "fileName": "542ad819-166b-b0e1-279069cd03bb.jpeg",
      "jpegThumbnail": "",
      "mimeType": "image/jpeg",
      "forwardingScore": 4,
      "isForwarded": true
    },
    "quotedMessage": {
      "stanzaId": "9A73322488DCB7D9689A6112F2528C9D",
      "participant": "79061230000@c.us",
      "typeMessage": "contactMessage",
      "contact": {
        "displayName": "Green-Api",
        "vcard": "BEGIN:VCARD\nVERSION:3.0\nN:Green-Api\nitem1.TEL;waid=79001230000\nitem1.X-ABLabel:Мобильный\nEND:VCARD"
      }
    }
  }
}
```
