# sendMessage

Метод предназначен для отправки текстового сообщения в личный чат или в группу.
Сообщение будет добавлено в очередь на отправку.

## Параметры запроса

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`chatId` | **string** | Если не указан `phoneNumber` | Идентификатор личного чата в формате `00000000000@c.us` или `00000000000-0000000000@g.us` для сообщений, отправляемых в группу; Пример: `79001234567@c.us` или `79001234567-1581234048@g.us`
`phoneNumber` | **integer** | Если не указан `chatId` | Номер телефона получателя в международном формате: 11 или 12 цифр; Пример: `79001234567` или `380123456789`
`message ` | **string** | Да | Текст сообщения. Поддерживаются символы emoji 😃. Максимальная длина текстового сообщения 4096 символов

## Пример тела запроса

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

## Поля ответа

Поле | Тип |  Описание
----- | ----- | -----
`idMessage ` | **string** | Идентификатор отправленного сообщения 

## Пример тела ответа

```json
{
    "idMessage": "3EB0C767D097B7C7C030"
}
```

## Ошибки sendMessage

Код HTTP | Идентификатор ошибки | Описание
----- | ----- | -----
400 | `instance in starting process try later` | Аккаунт находится в процессе запуска/перезапуска. Попробуйте повторить попытку спустя несколько секунд.
400 | `instance account not authorized` | Аккаунт не авторизован. Для авторизации аккаунта перейдите в [Личный кабинет](https://cabinet.green-api.com) и считайте QR-код из приложения `WhatsApp Business` на телефоне.
400 | `bad request data` | Данные запроса не валидны. Исправьте ошибку в параметрах запроса и повторите попытку.

## Пример кода на Python

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