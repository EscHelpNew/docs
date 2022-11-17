# Статус отправленного сообщения

Входящее уведомление данного типа содержит статус ранее отправленного сообщения: отправлено, доставлено, прочитано и др.

## Уведомление {#webhook}

### Формат уведомления {#webhook-parameters}

Параметр | Тип | Описание
----- | ----- | -----
`typeWebhook` | **string** | [Тип входящего уведомления](../type-webhook.md). Для уведомлений данного типа поле принимает значение `outgoingMessageStatus`
`instanceData` | **object** | Данные об аккаунте
`timestamp` | **integer** | Время наступления события в UNIX-формате
`idMessage` | **string** | Идентификатор отправленного сообщения или файла. Идентификатор отправленного сообщения возвращается методами: [SendMessage](../../../../api/sending/SendMessage.md), [SendFileByUrl](../../../../api/sending/SendFileByUrl.md), [SendFileByUpload](../../../../api/sending/SendFileByUpload.md), [SendLocation](../../../../api/sending/SendLocation.md), [SendContact](../../../../api/sending/SendContact.md), [SendLink](../../../../api/sending/SendLink.md)
`status` | **string** | Статус отправленного сообщения или файла. Статус принимает значения:
| | `sent` - сообщение отправлено
| | `delivered` - сообщение доставлено до получателя
| | `read` - сообщение прочитано/просмотрено/прослушано получателем
| | `failed` - произошла ошибка при отправке сообщения на сервер WhatsApp
| | `noAccount` - на номере телефона получателя не зарегистрирован аккаунт WhatsApp
| | `notInGroup` - отправитель не является участником группового чата, в который выполняется отправка сообщения
`sendByApi` | **boolean** | Флаг указывает отправлено сообщение из API или нет, принимает значения: true , false

Поля объекта `instanceData`

Параметр | Тип | Описание
----- | ----- | -----
`idInstance` | **integer** | Идентификатор аккаунта
`wid` | **string** | Идентификатор аккаунта в формате WhatsApp
`typeInstance` | **string** | Тип мессенджера для аккаунта

### Пример тела уведомления {#webhook-example-body}

```json
{
    "typeWebhook": "outgoingMessageStatus",
    "chatId": "11001234567890@c.us",
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
