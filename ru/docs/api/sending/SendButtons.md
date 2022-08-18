# SendButtons

Метод предназначен для отправки сообщения с кнопками в личный или групповой чат.
Сообщение будет добавлено в очередь на отправку.  Проверка авторизации whatsapp-а на телефоне (т.е. наличие в связанных устройствах) не выполняется. Сообщение на отправку хранится 24 часа в очереди и будет отправлено сразу же после авторизации телефона. 
Скорость отправки сообщений из очереди регулирует параметр [Интервал отправки сообщений](../send-messages-delay.md).

## Запрос {#request}

Для отправки требуется выполнить запрос по адресу:
```
POST https://api.green-api.com/waInstance{{idInstance}}/SendButtons/{{apiTokenInstance}}
```

Для получения параметров запроса `idInstance` и `apiTokenInstance` обратитесь к разделу [Перед началом работы](../../before-start.md#parameters).

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`chatId` | **string** | Да | [Идентификатор чата](../chat-id.md)
`message` | **string** | Да | Текст сообщения. Поддерживаются символы emoji 😃 
`footer` | **string** | Нет | Подвал сообщения. Удобен для визуального выделения текста, который относится к кнопкам
`buttons` | **array** | Да | Кнопки сообщения
`quotedMessageId` | **string** | Нет | Идентификатор цитируемого сообщения,если указан то сообщение отправится с цитированием указанного сообщения чата
`archiveChat` | **boolean** | Нет | Помещает в архив чат, в который отправлено сообщение. Принимает значания: true|false

Поля массива `buttons`

Параметр | Тип | Описание
----- | ----- | -----
`buttonId` | **integer** | Идентификатор кнопки
`buttonText` | **string** | текст на кнопке


> Максимальная длина текстового сообщения составляет 4096 символов

### Пример тела запроса {#request-example-body}

Отправка сообщения в личный чат:
```json
{
    "chatId": "79001234567@c.us",
    "message": "Hello",
    "footer": "Please choose the color:",
    "buttons": [
        {
            "buttonId": "1",
            "buttonText": "green"
        },
        {
            "buttonId": "2",
            "buttonText": "red"
        },
        {
            "buttonId": "3",
            "buttonText": "blue"
        }
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

### Ошибки SendMessage {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](../common-errors.md)

## Пример curl

```
curl --location --request POST 'https://api.green-api.com/waInstance{{idInstance}}/SendButtons/{{apiTokenInstance}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "chatId": "79001234567@c.us",
	"message": "Please choose the color:",
    "buttons": [{"buttonId": "1", "buttonText": "green"}, {"buttonId": "2", "buttonText": "red"}, {"buttonId": "3", "buttonText": "blue"}]
}'
```