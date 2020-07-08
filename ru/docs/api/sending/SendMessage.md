# SendMessage

Метод предназначен для отправки текстового сообщения в личный или групповой чат.
Сообщение будет добавлено в очередь на отправку. 
Скорость отправки сообщений из очереди регулирует параметр [Интервал отправки сообщений](/api/send-messages-delay).

## Запрос {#request}

Для отправки текстового сообщения требуется выполнить запрос по адресу:
```
POST https://api.green-api.com/waInstance{{idInstance}}/SendMessage/{{apiTokenInstance}}
```

Для получения параметров запроса `idInstance` и `apiTokenInstance` обратитесь к разделу [Перед началом работы](/before-start#parameters).

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`chatId` | **string** | Да | [Идентификатор чата](/api/chat-id)
`message ` | **string** | Да | Текст сообщения. Поддерживаются символы emoji 😃 

> Максимальная длина текстового сообщения составляет 4096 символов

### Пример тела запроса {#request-example-body}

Отправка сообщения в личный чат:
```json
{
    "chatId": "79001234567@c.us",
    "message": "I use Green-API to send this message to you!"
}
```

Отправка сообщения в групповой чат:
```json
{
    "chatId": "79001234567-1581234048@g.us",
    "message": "I use Green-API to send this message to you!"
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

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](/api/common-errors)

## Пример кода на Python  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/waInstance{{idInstance}}/sendMessage/{{apiTokenInstance}}"

payload = "{\r\n\t\"chatId\": \"79001234567@c.us\",\r\n\t\"message\": \"I use Green-API to send this message to you!\"\r\n}"
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```