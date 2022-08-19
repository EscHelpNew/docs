# SendTemplateButtons

>Временно не работает. Не отображаются в телефоне получателя.

Метод предназначен для отправки сообщения с интерактивными кнопками из перечня шаблонов в личный или групповой чат.
Сообщение будет добавлено в очередь на отправку.  Проверка авторизации whatsapp-а на телефоне (т.е. наличие в связанных устройствах) не выполняется. Сообщение на отправку хранится 24 часа в очереди и будет отправлено сразу же после авторизации телефона. 
Скорость отправки сообщений из очереди регулирует параметр [Интервал отправки сообщений](../send-messages-delay.md).

## Запрос {#request}

Для отправки требуется выполнить запрос по адресу:
```
POST https://api.green-api.com/waInstance{{idInstance}}/SendTemplateButtons/{{apiTokenInstance}}
```

Для получения параметров запроса `idInstance` и `apiTokenInstance` обратитесь к разделу [Перед началом работы](../../before-start.md#parameters).

### Особенности при работе с кнопками {#features}

- кнопки-ссылки совместимы с кнопками номерами, но не совместимы с кнопками-ответами;
- кнопки с телефонным номером совместимы с кнопками ссылками, но не совместимы с кнопками-ответами;
- кнопки с быстрыми ответами не совместимы с кнопками номерами и кнопками ссылками..

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`chatId` | **string** | Да | [Идентификатор чата](../chat-id.md)
`message` | **string** | Да | Текст сообщения. Поддерживаются символы emoji 😃 
`footer` | **string** | Нет | Подвал сообщения. Удобен для визуального выделения текста, который относится к кнопкам
`templateButtons` | **array** | Да | Интерактивные кнопки сообщения
`quotedMessageId` | **string** | Нет | Идентификатор цитируемого сообщения,если указан то сообщение отправится с цитированием указанного сообщения чата
`archiveChat` | **boolean** | Нет | Помещает в архив чат, в который отправлено сообщение. Принимает значания: true|false

Поля массива `templateButtons`

Параметр | Тип | Описание
----- | ----- | -----
`index` | **integer** | Идентификатор кнопки
`urlButton` | **object** | кнопка с ссылкой
`callButton` | **object** | кнопка вызова
`quickReplyButton` | **object** | обычная кнопка 

Поля объекта `urlButton`

Параметр | Тип | Описание
----- | ----- | -----
`displayText` | **string** | Текст ссылки
`url` | **string** | веб ссылка

Поля объекта `callButton`

Параметр | Тип | Описание
----- | ----- | -----
`displayText` | **string** | Текст ссылки
`phoneNumber` | **string** | номер телефона

Поля объекта `quickReplyButton`

Параметр | Тип | Описание
----- | ----- | -----
`displayText` | **string** | Текст на кнопке
`id` | **string** | идентификатор кнопки

> Максимальная длина текстового сообщения составляет 4096 символов

### Пример тела запроса {#request-example-body}

Отправка сообщения в личный чат:
```json
{
	"chatId": "79001234567@c.us",
	"message": "Hello",
    "footer": "What kind of action will you choose?",
    "templateButtons": [
            {"index": 1, "urlButton": {"displayText": "⭐ Star us on GitHub!", "url": "https://github.com/green-api/docs"}},
            {"index": 2, "callButton": {"displayText": "Call us", "phoneNumber": "+1 (234) 5678-901"}},
            {"index": 3, "quickReplyButton": {"displayText": "Plain button", "id": "plainButtonId"}}
        ]
}
```

## Ответ {#response}

### Поля ответа {#response-parameters}

Поле | Тип |  Описание
----- | ----- | -----
`idMessage ` | **string** | Идентификатор отправленного сообщения 

### Пример тела ответа {#response-example-body}

```json
{
    "idMessage": "3EB0C767D097B7C7C030"
}
```

### Ошибки SendTemplateButtons {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](../common-errors.md)

## Пример curl

```
curl --location --request POST 'https://api.green-api.com/waInstance{{idInstance}}/SendTemplateButtons/{{apiTokenInstance}}' \
--header 'Content-Type: application/json' \
--data-raw '{
	"chatId": "79001234567@c.us",
	"message": "Hello",
    "footer": "What kind of action will you choose?",
    "templateButtons": [
            {"index": 1, "urlButton": {"displayText": "⭐ Star us on GitHub!", "url": "https://github.com/green-api/docs"}},
            {"index": 2, "callButton": {"displayText": "Call us", "phoneNumber": "+1 (234) 5678-901"}},
            {"index": 3, "quickReplyButton": {"displayText": "Plain button", "id": "plainButtonId"}}
        ]
}'
```