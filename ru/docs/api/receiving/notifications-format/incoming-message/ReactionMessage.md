# Входящее сообщение-реакция

В данном разделе описывается формат входящего уведомления объекта `messageData` для входящего сообщения реакции. Для получения описания общего формата входящих уведомлений обратитесь к разделу [Входящие сообщения](Webhook-IncomingMessageReceived.md).

Для получения входящих уведомлений данного вида требуется выполнение двух условий:

`typeWebhook` = `incomingMessageReceived`

`messageData.typeMessage` = `reactionMessage`

## Уведомление {#webhook}

### Формат уведомления {#webhook-parameters}

Поля объекта `messageData`

| Параметр          | Тип        | Описание                                                                                                                                       |
| ----------------- | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `typeMessage`     | **string** | Тип принятого сообщения. Для сообщений данного типа поле принимает значение: `reactionMessage`|
|`extendedTextMessageData` | **object** | Объект данных о принятом сообщении-реакции  |                                                                                                            |
| `quotedMessage`   | **object** | Объект данных о цитируемом сообщении. Сообщение на которое отреагировал собеседник   |

Поля объекта `extendedTextMessageData`

Параметр | Тип | Описание
----- | ----- | -----
`text` | **string** | Реакция (эмоджи) на сообщение


Поля объекта `quotedMessage`

| Параметр      | Тип        | Описание            |
| ------------- | ---------- | ------------------- |
| `stanzaId` | **string** | id цитируемого сообщения |
| `participant` | **string** | id отправителя цитируемого сообщения |
| `typeMessage` | **string** | Тип цитируемого сообщения |

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
    "chatName": "Грин",
    "sender": "79001234568@c.us",
    "senderName": "Грин"
  },
  "messageData": {
    "typeMessage": "reactionMessage",
    "extendedTextMessageData": {
      "text": "👍"
    },
    "quotedMessage": {
      "stanzaId": "A16014FAC9F5382E7B9CEEFEF1FFEB6F",
      "participant": "79001234568@c.us"
    }
  }
}
```
