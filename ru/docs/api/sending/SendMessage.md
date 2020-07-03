# SendMessage

Метод предназначен для отправки текстового сообщения в личный чат или группу.
Сообщение будет добавлено в очередь на отправку.

## Запрос {#request}

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`chatId` | **string** | Если не указан `phoneNumber` | Идентификатор личного чата в формате `00000000000@c.us` или идентификатор группы в формате `00000000000-0000000000@g.us`; Пример: `79001234567@c.us` или `79001234567-1581234048@g.us`
`phoneNumber` | **integer** | Если не указан `chatId` | Номер телефона получателя в международном формате: 11 или 12 цифр; Пример: `79001234567` или `380123456789`
`message ` | **string** | Да | Текст сообщения. Поддерживаются символы emoji 😃. Максимальная длина текстового сообщения 4096 символов

### Пример тела запроса {#request-example-body}

Отправка сообщения в личный чат:
```json
{
    "phoneNumber": 79001234567,
    "message": "I use Green-API to send this message to you!"
}
```

Отправка сообщения в группу:
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

payload = "{\r\n\t\"phoneNumber\": 79001234567,\r\n\t\"message\": \"I use Green-API to send this message to you!\"\r\n}"
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```