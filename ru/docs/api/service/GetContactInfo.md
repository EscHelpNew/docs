# GetContactInfo

Метод предназначен для получения информации о контакте.

## Запрос {#request}

Для получения списка контактов требуется выполнить запрос по адресу:
```
POST https://api.green-api.com/waInstance{{idInstance}}/getContactInfo/{{apiTokenInstance}}
```

Для получения параметров запроса `idInstance` и `apiTokenInstance` обратитесь к разделу [Перед началом работы](../../before-start.md#parameters).

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`chatId` | **string** | Да | [Идентификатор корреспондента](../chat-id.md)

### Пример тела запроса {#request-example-body}

```json
{
    "chatId": "71234567890@c.us"
}
```

## Ответ {#response}

### Поля ответа {#response-parameters}

Поле | Тип |  Описание
----- | ----- | ----- 
`avatar` | **string** | ссылка на аватар
`name` | **string** | Имя контакта. Возможные значения:
                    ||1) Если аккаунт записан в телефонную книгу, то получаем имя из книги
                    ||2) Если аккаунт не записан в телефонную книгу, то получаем имя из профиля WhatsApp
                    ||3) Если аккаунт не записан в телефонную книгу и не назначено имя профиля в WhatsApp, то получаем пустое поле
`email` | **string** | Электронная почта контакта
`category` | **string** | Категория бизнес контакта
`description` | **string** | Описание бизнес контакта
`products` | **object** | Карточки товаров контакта
`chatId` | **string** | [Идентификатор корреспондента](../chat-id.md)
`lastSeen` | **string** | Время последнего статуса онлайн
`isArchive` | **string** | Статус архивации чата, принимает значения true/false
`isDisappearing` | **string** | Статус исчезающих сообщений чата, принимает значения true/false
`isMute` | **string** | Статус уведомлений чата, принимает значения true/false
`messageExpiration` | **integer** | Время жизни сообщений в чате, в секундах
`muteExpiration` | **integer** | Время, через сколько будут включены уведомления в чате


Поля объекта `products`

| Параметр      | Тип        | Описание                             |
| ------------- | ---------- | ------------------------------------ |
| `id`    | **string** | id товара            |
| `imageUrls` | **object** | Ссылки на изображения товара |
| `availability` | **string** | Доступность товара            |
| `reviewStatus` | **object** | Статус валидации товара |
| `name` | **string** | Название товара
| `description` | **string** | Описание товара
| `price` | **string** | Цена товара
| `isHidden` | **boolean** | Состояние товара


### Пример тела ответа {#response-example-body}

```json
{
    "avatar": "https://pps.whatsapp.net/v/t61.24694-24/24_1349471992200940_2091838963901201896_n.jpg?ccb=11-4&oh=01_AVzZilQn10nj9M9cfQV4PW5dgdXOkiOuD_jCqP2MCXIpyA",
    "name": "Dealer",
    "email": "24service@tt.tt",
    "category": "Automotive Dealership",
    "description": "Официальный сервис",
    "products": [
        {
            "id": "42079728159",
            "imageUrls": {
                "requested": "https://mmg.whatsapp.net/v/t45.5328-4/263329037_6625110154227932_2879714823340281709_n.jpg?stp=dst-jpg_p100x100&ccb=1-7&_nc_sid=c48759&_nc_ohc=NKICbZlqfPMAX9077mo&_nc_ad=z-m&_nc_cid=0&_nc_ht=mmg.whatsapp.net&oh=01_AVwYzx7CckCFf8F8xIIZ5m2AGdeC8YTnLyd29",
                "original": "https://mmg.whatsapp.net/v/t45.5328-4/263329037_6625110154227932_2879714823340281709_n.jpg?ccb=1-7&_nc_sid=c48759&_nc_ohc=NKICbZlqfPMAX9077mo&_nc_ad=z-m&_nc_cid=0&_nc_ht=mmg.whatsapp.net&oh=01_AVzn_O9azpKNRs1iPId0TQkGYk4D7HZFSQMeobvRiR"
            },
            "reviewStatus": {
                "whatsapp": "APPROVED"
            },
            "availability": "in stock",
            "name": "Замена",
            "description": "От 1000 р.",
            "price": null,
            "isHidden": false
        },
        {
            "id": "3545870328871389",
            "imageUrls": {
                "requested": "https://mmg.whatsapp.net/v/t45.5328-4/261250418_4513761695371199_1710541959703469822_n.jpg?stp=dst-jpg_p100x100&ccb=1-7&_nc_sid=c48759&_nc_ohc=eps8lAw2_3MAX_mWW8K&_nc_ad=z-m&_nc_cid=0&_nc_ht=mmg.whatsapp.net&oh=01_AVxT3HnbR04qKZJSOeK4d8p-noZokqly9QbpYFK-c_8kSA&oe",
                "original": "https://mmg.whatsapp.net/v/t45.5328-4/261250418_4513761695371199_1710541959703469822_n.jpg?ccb=1-7&_nc_sid=c48759&_nc_ohc=eps8lAw2_3MAX_mWW8K&_nc_ad=z-m&_nc_cid=0&_nc_ht=mmg.whatsapp.net&oh=01_AVx2wTCmzof0BoZDmIUpD328CtpJmlvEXGdVzew&o"
            },
            "reviewStatus": {
                "whatsapp": "APPROVED"
            },
            "availability": "in stock",
            "name": "Техническое обслуживание",
            "price": null,
            "isHidden": false
        }
    ],
	"chatId": "71234567890@c.us",
    "lastSeen": null,
    "isArchive": false,
    "isDisappearing": false,
    "isMute": false,
    "messageExpiration": 0,
    "muteExpiration": null
}
```

### Ошибки GetContactInfo {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](../common-errors.md)

## Пример кода на Python  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/waInstance{{idInstance}}/getContactInfo/{{apiTokenInstance}}"

payload = "{"chatId": "71234567890@c.us"}"
headers = {
  'Content-Type': 'application/json'
}


response = requests.request("GET", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```