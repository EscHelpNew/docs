# Входящие сообщения

В данном разделе приводится описание общего формата входящих уведомлений с типом `incomingMessageReceived`. Описание всех типов входящих уведолмений представлено в разделе [Типы входящих уведомлений](../type-webhook.md).

Система предусматривает получение уведомлений о входящих сообщениях следующих видов:

- [Входящее текстовое сообщение](TextMessage.md)
- [Выбор обычной кнопки](/docs/api/receiving/notifications-format/selected-buttons/ButtonsResponseMessage.md)
- [Выбор шаблонной кнопки](/docs/api/receiving/notifications-format/selected-buttons/TemplateButtonsReplyMessage.md)
- [Выбор элемента списка](/docs/api/receiving/notifications-format/selected-buttons/ListResponseMessage.md)
- [Входящее текстовое сообщение с URL](ExtendedTextMessage.md)
- [Входящее сообщение с изображением, видео, аудио, документом](ImageMessage.md)
- [Входящее сообщение с геолокацией](LocationMessage.md)
- [Входящее сообщение с контактом](ContactMessage.md)
- [Входящее сообщение с цитированием](QuotedMessage.md)
- [Входящее сообщение со стикером](StickerMessage.md)
- [Входящее сообщение-реакция](ReactionMessage.md)
- [Входящее сообщение с приглашением в группу](GroupInviteMessage.md)

## Поля уведомления incomingMessageReceived {#webhook-parameters}

Параметр | Тип | Описание
----- | ----- | -----
`typeWebhook` | **string** | [Тип входящего уведомления](../type-webhook.md). Для уведомления данного типа поле принимает значение `incomingMessageReceived`
`instanceData` | **object** | Данные об аккаунте
`timestamp` | **integer** | Время наступления события в UNIX-формате
`idMessage` | **string** | Идентификатор входящего сообщения
`senderData` | **object** | Данные об отправителе сообщения или файла
`messageData` | **object** | Данные о принятом сообщении или файле

Поля объекта `instanceData`

Параметр | Тип | Описание
----- | ----- | -----
`idInstance` | **integer** | Идентификатор аккаунта
`wid` | **string** | Идентификатор аккаунта в формате WhatsApp
`typeInstance` | **string** | Тип мессенджера для аккаунта

Поля объекта `senderData`

Параметр | Тип | Описание
----- | ----- | -----
`chatId` | **string** | [Идентификатор чата](../../../chat-id.md), в котором получено сообщение или файл
`sender` | **string** | [Идентификатор](../../../chat-id.md#corr) отправителя сообщения или файла
`chatName` | **string** | Имя чата
`senderName` | **string** | Имя отправителя

### Поля объекта `messageData`

Объект `messageData` имеет разные поля в зависимости от типа входящего сообщения:

- [Входящее текстовое сообщение](TextMessage.md)
- [Входящее текстовое сообщение с URL](ExtendedTextMessage.md)
- [Входящее сообщение с изображением, видео, аудио, документом](ImageMessage.md)
- [Входящее сообщение с геолокацией](LocationMessage.md)
- [Входящее сообщение с контактом](ContactMessage.md)
- [Входящее сообщение с цитированием](QuotedMessage.md)
- [Входящее сообщение со стикером](StickerMessage.md)
- [Входящее сообщение-реакция](ReactionMessage.md)
- [Входящее сообщение с приглашением в группу](GroupInviteMessage.md)

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
    "messageData":{
       // В зависимости от typeMessage = textMessage || imageMessage || videoMessage || documentMessage || audioMessage || locationMessage || contactMessage || extendedTextMessage || quotedMessage
       ...
       ...
       ...
        }
    }
}
```