# (Не используется) SendLink
> Метод устарел и более не используется. Для замены смотрите метод [SendMessage](/../docs/api/sending/SendMessage/).

Метод предназначен для отправки сообщения со ссылкой, по которой будут добавлены превью изображения, заголовок и описание. Проверка авторизации whatsapp-а на телефоне (т.е. наличие в связанных устройствах) не выполняется. Сообщение на отправку хранится 24 часа в очереди и будет отправлено сразу же после авторизации телефона. 
Картинка, заголовок и описание получаются из [Open Graph](https://en.wikipedia.org/wiki/Facebook_Platform#Open_Graph_protocol) разметки страницы, на которую указывает ссылка.
Сообщение будет добавлено в очередь на отправку. Скорость отправки сообщений из очереди регулирует параметр [Интервал отправки сообщений](../send-messages-delay.md).

## Запрос {#request}

Для отправки сообщения со ссылкой требуется выполнить запрос по адресу:
```
POST https://api.green-api.com/waInstance{{idInstance}}/sendLink/{{apiTokenInstance}}
```

Для получения параметров запроса `idInstance` и `apiTokenInstance` обратитесь к разделу [Перед началом работы](../../before-start.md#parameters).

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`chatId` | **string** | Да | [Идентификатор чата](../chat-id.md)
`urlLink` | **string** | Да | Адрес ссылки
`quotedMessageId` | **string** | Нет | Идентификатор цитируемого сообщения,если указан то сообщение отправится с цитированием указанного сообщения чата

> Рекомендуется, чтобы страница, на которую указыает ссылка `urlLink` содержала разметку [Open Graph](https://en.wikipedia.org/wiki/Facebook_Platform#Open_Graph_protocol). В этом случае сообщение будет дополнено картинкой, заголовком и кратким описанием.

### Пример тела запроса {#request-example-body}

Отправка сообщения в личный чат:
```json
{
    "chatId": "11001234567@c.us",
    "urlLink": "https://green-api.com"
}
```

Отправка сообщения в групповой чат:
```json
{
    "chatId": "120363043968066561@g.us",
    "urlLink": "https://green-api.com"
}
```

Отправка сообщения в личный чат:
```json
{
    "chatId": "11001234567@c.us",
    "urlLink": "https://green-api.com",
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

### Ошибки SendLink {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](../common-errors.md)

## Пример кода на Python  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/waInstance{{idInstance}}/sendLink/{{apiTokenInstance}}"

payload = "{\r\n\t\"chatId\": \"11001234567@c.us\",\r\n\t\"urlLink\": \"https://green-api.com\"\r\n}\r\n"
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```
