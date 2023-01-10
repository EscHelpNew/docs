# Входящее сообщение с геолокацией

В данном разделе описывается формат входящего уведомления объекта `messageData` для входящего сообщения с геолокацией. Для получения описания общего формата входящих уведомлений обратитесь к разделу [Входящие сообщения](Webhook-IncomingMessageReceived.md).

Для получения входящих уведомлений данного вида требуется выполнение двух условий:

`typeWebhook` = `incomingMessageReceived`

`messageData.typeMessage` = `locationMessage`

## Уведомление {#webhook}

### Формат уведомления {#webhook-parameters}

Поля объекта `messageData`

| Параметр              | Тип        | Описание                                                                                        |
| --------------------- | ---------- | ----------------------------------------------------------------------------------------------- |
| `typeMessage`         | **string** | Тип принятого сообщения. Для сообщений данного типа поле принимает значение `locationMessage`   |
| `locationMessageData` | **object** | Объект данных о принятой геолокации                                                             |
| `quotedMessage`       | **object** | Объект данных о цитируемом сообщении. Присутствует только, если само сообщение является цитатой |

Поля объекта `locationMessageData`

| Параметр        | Тип        | Описание                                |
| --------------- | ---------- | --------------------------------------- |
| `latitude`      | **double** | Широта локации                          |
| `longitude`     | **double** | Долгота локации                         |
| `jpegThumbnail` | **string** | Превью изображения в `base64` кодировке |
|`isForwarded` | **boolean** | Является ли сообщение пересланным, принимает значения true/false|
|`forwardingScore` | **integer** | Количество пересылок сообщения|

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
  "messageData": {
    "typeMessage": "locationMessage",
    "locationMessageData": {
      "latitude": 12.345678910111213,
      "longitude": 14.151617181920212,
      "jpegThumbnail": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAYEBQYFBAYGBQYHBwYIChAKCgkJChQODwwQFx=",
		  "forwardingScore": 4,
      "isForwarded": true
    }
  }
}
```

### Пример тела уведомления входящего сообщения с геопозицией и цитатой текстового сообщения {#webhook-example-body}

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
    "typeMessage": "locationMessage",
    "locationMessageData": {
      "nameLocation": "",
      "address": "",
      "jpegThumbnail": "217",
      "latitude": 74.5922641,
      "longitude": 59.6645355,
		  "forwardingScore": 4,
      "isForwarded": true  
    },
    "quotedMessage": {
      "stanzaId": "9A73322488DCB7D9689A6112F2528C9D",
      "participant": "79001230022@c.us",
      "typeMessage": "textMessage",
      "textMessage": "Привет"
    }
  }
}
```
