# SendMessage

Метод предназначен для отправки текстового сообщения в личный или групповой чат.
Сообщение будет добавлено в очередь на отправку. Сообщение на отправку хранится 24 часа в очереди и будет отправлено сразу же после авторизации телефона. 
Скорость отправки сообщений из очереди регулирует параметр [Интервал отправки сообщений](../send-messages-delay.md).

## Видеоинструкция

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/tnX1rByc3CI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</center>

## Запрос {#request}
ы
Для отправки текстового сообщения требуется выполнить запрос по адресу:
```
POST https://api.green-api.com/waInstance{{idInstance}}/SendMessage/{{apiTokenInstance}}
```

Для получения параметров запроса `idInstance` и `apiTokenInstance` обратитесь к разделу [Перед началом работы](../../before-start.md#parameters).

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`chatId` | **string** | Да | [Идентификатор чата](../chat-id.md)
`message` | **string** | Да | Текст сообщения. Поддерживаются символы emoji 😃 
`quotedMessageId` | **string** | Нет | Идентификатор цитируемого сообщения,если указан то сообщение отправится с цитированием указанного сообщения чата
`archiveChat` | **boolean** | Нет | Помещает в архив чат, в который отправлено сообщение. Принимает значения: true|false
`linkPreview` | **boolean** | Нет | Параметр включает отображение превью и описание ссылки. По умолчанию включен. Принимает значения: true/false


> Максимальная длина текстового сообщения составляет 10000 символов

### Пример тела запроса {#request-example-body}

Отправка сообщения в личный чат:
```json
{
    "chatId": "11001234567@c.us",
    "message": "I use Green-API to send this message to you!"
}
```

Отправка сообщения в групповой чат:
```json
{
    "chatId": "120363043968066561@g.us",
    "message": "I use Green-API to send this message to you!"
}
```

Отправка сообщения с цитированием:
```json
{
    "chatId": "11001234567@с.us",
    "message": "I use Green-API to send this message to you!",
    "quotedMessageId": "361B0E63F2FDF95903B6A9C9A102F34B"
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

## Пример кода на Python  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/waInstance{{idInstance}}/sendMessage/{{apiTokenInstance}}"

payload = "{\r\n\t\"chatId\": \"11001234567@c.us\",\r\n\t\"message\": \"I use Green-API to send this message to you!\"\r\n}"
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```