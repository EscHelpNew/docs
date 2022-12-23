# Входящее сообщение с контактом

В данном разделе описывается формат входящего уведомления объекта `messageData` для входящего сообщения с несколькими контактами. Для получения описания общего формата входящих уведомлений обратитесь к разделу [Входящие сообщения](Webhook-IncomingMessageReceived.md).

Для получения входящих уведомлений данного вида требуется выполнение двух условий:

`typeWebhook` = `incomingMessageReceived`

`messageData.typeMessage` = `contactsArrayMessage`

## Уведомление {#webhook}

### Формат уведомления {#webhook-parameters}

Поля объекта `messageData`

| Параметр             | Тип        | Описание                                                                                        |
| -------------------- | ---------- | ----------------------------------------------------------------------------------------------- |
| `typeMessage`        | **string** | Тип принятого сообщения. Для сообщений данного типа поле принимает значение `contactsArrayMessage` |
| `contacts` | **object** | Объект массива данных о принятых контактах.                                                              |
| `quotedMessage`      | **object** | Объект данных о цитируемом сообщении. Присутствует только, если само сообщение является цитатой |
|`isForwarded` | **boolean** | Является ли сообщение пересланным, принимает значения true/false|
|`forwardingScore` | **integer** | Количество пересылок сообщения|

Поля объекта `contacts`

| Параметр      | Тип        | Описание                                     |
| ------------- | ---------- | -------------------------------------------- |
| `displayName` | **string** | Отображаемое имя контакта                    |
| `vcard`       | **string** | Структура VCard (визитной карточки контакта) |


Поля объекта `quotedMessage`

| Параметр      | Тип        | Описание                             |
| ------------- | ---------- | ------------------------------------ |
| `stanzaId`    | **string** | id цитируемого сообщения             |
| `participant` | **string** | id отправителя цитируемого сообщения |
| `typeMessage` | **string** | Тип цитируемого сообщения            |

Остальные поля заполняются в зависимости от типа цитируемого сообщения и идентичны полям входящих сообщений описаннных в разделе [Входящие сообщения](Webhook-IncomingMessageReceived.md)

### Пример тела уведомления {#webhook-example-body}

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
    "typeMessage": "ContactsArrayMessage",
    "contacts":  [
		{
			"displayName": "Виктор Андреевич",
			"vcard": "BEGIN:VCARD\nVERSION:3.0\nN:Андреевич;Виктор;;;\nFN:Виктор Андреевич\nORG:Image\nTITLE:\nitem1.TEL;waid=79001234569:+7 900 123-45-69\nitem1.X-ABLabel:Мобильный\nEND:VCARD"
		},
		{
			"displayName": "Oleg edrosovich",
			"vcard": "BEGIN:VCARD\nVERSION:3.0\nN:Андреевич;Виктор;;;\nFN:Виктор Андреевич\nORG:Image\nTITLE:\nitem1.TEL;waid=79001234569:+7 900 123-45-69\nitem1.X-ABLabel:Мобильный\nEND:VCARD"
		}
    ],
	"forwardingScore": 4,
    "isForwarded": true
    }
  }
}
```

### Пример тела уведомления входящего сообщения с массивом контактов и цитатой текстового сообщения {#webhook-example-body}

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
    "typeMessage": "ContactsArrayMessage",
    "contacts":  [
		{
			"displayName": "Виктор Андреевич",
			"vcard": "BEGIN:VCARD\nVERSION:3.0\nN:Андреевич;Виктор;;;\nFN:Виктор Андреевич\nORG:Image\nTITLE:\nitem1.TEL;waid=79001234569:+7 900 123-45-69\nitem1.X-ABLabel:Мобильный\nEND:VCARD"
		},
		{
			"displayName": "Oleg edrosovich",
			"vcard": "BEGIN:VCARD\nVERSION:3.0\nN:Андреевич;Виктор;;;\nFN:Виктор Андреевич\nORG:Image\nTITLE:\nitem1.TEL;waid=79001234569:+7 900 123-45-69\nitem1.X-ABLabel:Мобильный\nEND:VCARD"
		}
    ],
	"forwardingScore": 4,
    "isForwarded": true
    },
    "quotedMessage": {
      "stanzaId": "9A73322488DCB7D9689A6112F2528C9D",
      "participant": "79001235696@c.us",
      "typeMessage": "textMessage",
      "textMessage": "Привет"
    }
  }
}
```

### Пример тела уведомления входящего сообщения с массивом контактов и цитатой аудио/видео/документ {#webhook-example-body}

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
    "typeMessage": "ContactsArrayMessage",
    "contacts":  [
		{
			"displayName": "Виктор Андреевич",
			"vcard": "BEGIN:VCARD\nVERSION:3.0\nN:Андреевич;Виктор;;;\nFN:Виктор Андреевич\nORG:Image\nTITLE:\nitem1.TEL;waid=79001234569:+7 900 123-45-69\nitem1.X-ABLabel:Мобильный\nEND:VCARD"
		},
		{
			"displayName": "Oleg edrosovich",
			"vcard": "BEGIN:VCARD\nVERSION:3.0\nN:Андреевич;Виктор;;;\nFN:Виктор Андреевич\nORG:Image\nTITLE:\nitem1.TEL;waid=79001234569:+7 900 123-45-69\nitem1.X-ABLabel:Мобильный\nEND:VCARD"
		}
    ],
	"forwardingScore": 4,
    "isForwarded": true
    },
    "quotedMessage": {
         "stanzaId": "9A73322488DCB7D9689A6112F2528C9D",
         "participant": "79061230000@c.us",
         "typeMessage": "imageMessage",
         "downloadUrl": "",
          "caption": "",
          "jpegThumbnail": ""
    }
  }
```

### Пример тела уведомления входящего сообщения с массивом контактов и цитатой контакта {#webhook-example-body}

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
    "typeMessage": "ContactsArrayMessage",
    "contacts":  [
		{
			"displayName": "Виктор Андреевич",
			"vcard": "BEGIN:VCARD\nVERSION:3.0\nN:Андреевич;Виктор;;;\nFN:Виктор Андреевич\nORG:Image\nTITLE:\nitem1.TEL;waid=79001234569:+7 900 123-45-69\nitem1.X-ABLabel:Мобильный\nEND:VCARD"
		},
		{
			"displayName": "Oleg edrosovich",
			"vcard": "BEGIN:VCARD\nVERSION:3.0\nN:Андреевич;Виктор;;;\nFN:Виктор Андреевич\nORG:Image\nTITLE:\nitem1.TEL;waid=79001234569:+7 900 123-45-69\nitem1.X-ABLabel:Мобильный\nEND:VCARD"
		}
    ],
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
### Пример тела уведомления входящего сообщения с массивом контактов и цитатой геопозиции {#webhook-example-body}

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
    "typeMessage": "ContactsArrayMessage",
    "contacts":  [
		{
			"displayName": "Виктор Андреевич",
			"vcard": "BEGIN:VCARD\nVERSION:3.0\nN:Андреевич;Виктор;;;\nFN:Виктор Андреевич\nORG:Image\nTITLE:\nitem1.TEL;waid=79001234569:+7 900 123-45-69\nitem1.X-ABLabel:Мобильный\nEND:VCARD"
		},
		{
			"displayName": "Oleg edrosovich",
			"vcard": "BEGIN:VCARD\nVERSION:3.0\nN:Андреевич;Виктор;;;\nFN:Виктор Андреевич\nORG:Image\nTITLE:\nitem1.TEL;waid=79001234569:+7 900 123-45-69\nitem1.X-ABLabel:Мобильный\nEND:VCARD"
		}
    ],
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
