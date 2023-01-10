# GetContactInfo

The method is aimed for getting information on a contact.

## Request {#request}

To get contacts list, you have to execute a request at:
```
GET https://api.green-api.com/waInstance{{idInstance}}/getContactInfo/{{apiTokenInstance}}
```

For `idInstance` and `apiTokenInstance` request parameters, refer to [Before you start](../../before-start.md#parameters) section.

### Request parameters {#request-parameters}

Parameter | Type | Mandatory | Description
----- | ----- | ----- | -----
`chatId` | **string** | Yes | [Correspondent id](../chat-id.md)

### Request body example {#request-example-body}

```json
{
    "chatId": "71234567890@c.us"
}
```

## Response {#response}

### Response parameters {#response-parameters}

Parameter | Type |  Description
----- | ----- | ----- 
`avatar` | **string** | Avatar url
`name` | **string** | Contact name
                    ||1) If the account is added to the phone book, then the account name is taken from the phone book
                    ||2) If the account is not added to the phone book, then the name specified in the WhatsApp account profile is used
                    ||3) If the account is not added to the phone book, and if no name is set in the WhatsApp account profile, then an empty string is returned
`email` | **string** | Contact e-mail
`category` | **string** | Business contact category
`description` | **string** | Business contact description
`products` | **object** | Contact products cards



`products` object parameters

| Parameter      | Type       | Description                             |
| ------------- | ---------- | ------------------------------------ |
| `id`    | **string** | Prodict id            |
| `imageUrls` | **object** | Product images urls |
| `availability` | **string** | Product availability            |
| `reviewStatus` | **object** | Product review status |
| `name` | **string** | Product name
| `description` | **string** | Product description
| `price` | **string** | Product price
| `isHidden` | **boolean** | Product condition


### Response body example {#response-example-body}

```json
{
    "avatar": "https://pps.whatsapp.net/v/t61.24694-24/24_1349471992200940_2091838963901201896_n.jpg?ccb=11-4&oh=01_AVzZilQn10nj9M9cfQV4PW5dgdXOkiOuD_jCqP2MCXIpyA",
    "name": "Dealer",
    "email": "24service@tt.tt",
    "category": "Automotive Dealership",
    "description": "Oficial service",
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
            "name": "Replacement",
            "description": "From 1000 RUB",
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
            "name": "Technical maintenance",
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

### GetContactInfo errors {#errors}

For a list of errors common to all methods, refer to [Common errors](../common-errors.md) section

## Python request example  {#request-example-python}

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
