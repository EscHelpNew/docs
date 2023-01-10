# GetMessage

The method returns the chat message.

## Request {#request}

To get chat message, you have to execute a request at:
```
POST https://api.green-api.com/waInstance{{idInstance}}/getMessage/{{apiTokenInstance}}
```

For `idInstance` and `apiTokenInstance` request parameters, please refer to [Before you start](../../before-start.md#parameters) section.

### Request parameters {#request-parameters}

| Parameter   | Type       | Mandatory | Description                                                               |
|-------------|------------|-----------|---------------------------------------------------------------------------|
| `chatId`    | **string** | Yes       | [Personal or chat Id](../chat-id.md) the message of which you need to get |
| `idMessage` | **string** | Yes       | Message ID                                                                |

### Request body example {#request-example-body}

message request:
```json
{
  "chatId": "120363043968066561@g.us",
  "idMessage": "BAE5F4886F6F2D05"
}
```

## Response {#response}

The response contains a received or sent message in the chat.

### Response parameters {#response-parameters}

Object with parameters:

| Parameter             | Type                                                       | Description                                                                                                |
|-----------------------|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| `idMessage`           | **string**                                                 | Message Id                                                                                                 |
| `timestamp`           | **integer**                                                | Time when the message has been sent in UNIX format                                                         |
| `typeMessage`         | **string**                                                 | Message type, possible variants:                                                                           |
|                       |                                                            | `textMessage` - text message                                                                               |
|                       |                                                            | `imageMessage` - image message                                                                             |
|                       |                                                            | `videoMessage` - video message                                                                             | 
|                       |                                                            | `documentMessage` - document file message                                                                  |        
|                       |                                                            | `audioMessage` - audio message                                                                             |     
|                       |                                                            | `locationMessage` - location message                                                                   |
|                       |                                                            | `contactMessage` - contact message                                                                         |   
|                       |                                                            | `extendedTextMessage` - link and preview message                                                           |
|                       |                                                            | `quotedMessage` - Quoted message (deprecated)                                                      | 
|                       |                                                            | `buttonsMessage` - buttons message                                                                    |
|                       |                                                            | `templateMessage` - template buttons message                                                        |
|                       |                                                            | `listMessage` - selection list message                                                           |
|                       |                                                            | `buttonsResponseMessage` - simple button selection                                                              |
|                       |                                                            | `templateButtonsReplyMessage` - template button selection                                                 |
|                       |                                                            | `listResponseMessage` - list element selection                                                                  |
| `chatId`              | **string**                                                 | [Chat Id](../chat-id.md)                                                                                   |
| `senderId`            | **string**                                                 | Incoming message sender [Id](../chat-id.md#corr). Present only for `type` = `incoming`                     |
| `senderName`          | **string**                                                 | Incoming message sender name. Present only for `type` = `incoming`                                         |
| `textMessage`         | **string**                                                 | Message text, if `typeMessage`=`textMessage`                                                               |
| `downloadUrl`         | **string**                                                 | Link to download a file, if `typeMessage` = `imageMessage`/`videoMessage`/`documentMessage`/`audioMessage` |
| `caption`             | **string**                                                 | File caption, if `typeMessage` = `imageMessage`/`videoMessage`/`documentMessage`                           |
| `location`            | **object**                                                 | Location structure object, if `typeMessage`=`locationMessage`                                              |
| `contact`             | **object**                                                 | Contact structure object, if `typeMessage`=`contactMessage`                                                |
| `extendedTextMessage` | **object**                                                 | Link data structure object, if `typeMessage`=`extendedTextMessage`                                         |
| `quotedMessage`       | **object**                                                 | Object quoted message            |

Parameters of `location` object:

| Parameter       | Type       | Description                  |
|-----------------|------------|------------------------------|
| `nameLocation`  | **string** | Location name                |
| `address`       | **string** | Location address             |
| `latitude`      | **double** | Location latitude            |
| `longitude`     | **double** | Location longitude           |
| `jpegThumbnail` | **string** | `base64`-coded image preview |

Parameters of `contact` object:

| Parameter     | Type       | Description                          |
|---------------|------------|--------------------------------------|
| `displayName` | **string** | Contact display name                 |
| `vcard`       | **string** | VCard structure (contact visit card) |

Parameters of `extendedTextMessage` object:

| Parameter       | Type       | Description                  |
|-----------------|------------|------------------------------|
| `text`          | **string** | Link text                    |
| `description`   | **string** | Link description             |
| `title`         | **string** | Link title                   |
| `previewType`   | **string** | Link preview type            |
| `jpegThumbnail` | **string** | `base64`-coded image preview |
| `stanzaId`      | **string** | Quoted message ID     |
| `participant`   | **string** | Recipient chat ID         |

### Response body example {#response-example-body}

```json
    {
        "idMessage": "DE8CFFA93B95237B077F8FA08331A0B5",
        "timestamp": 1587129319,
        "typeMessage": "textMessage",
        "chatId": "11001234567@c.us",
        "senderId": "11001234567@c.us",
        "senderName": "John",
        "textMessage": "Hi"
    }
```
```json
    {
        "idMessage": "EA0BD1AE042DC4F3609867126309D67C",
        "timestamp": 1587147598,
        "typeMessage": "imageMessage",
        "chatId": "11001234567@c.us",
        "senderId": "11001234567@c.us",
        "senderName": "John",
        "downloadUrl": "https://api.green-api.com/waInstance1234/downloadFile/EA1BD1AE042DC4F3609867126309D67C",
        "caption": "What do you think?"
    }
```
```json
    {
        "idMessage": "DE8CFFA93B95237B077F8FA08331A0B5",
        "timestamp": 1587129319,
        "typeMessage": "locationMessage",
        "chatId": "71234567891@c.us",
        "senderId": "1234567891@c.us",
        "senderName": "John",
        "location": {
            "nameLocation": "I'm here, come",
    	    "address": "614111, Perm",
            "latitude": 53.9370129,
            "longitude": 54.8728409,
            "jpegThumbnail": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wB=="
        }
    }
```
```json
    {
        "idMessage": "DE8CFFA93B95237B077F8FA08331A0B5",
        "timestamp": 1587129319,
        "typeMessage": "contactMessage",
        "chatId": "1234567891@c.us",
        "senderId": "71234567891@c.us",
        "senderName": "John",
        "contact": {
            "displayName": "Victor Petrov",
            "vcard": "BEGIN:VCARD\nVERSION:3.0\nN:Andreevich;Victor;;;\nFN:Victor Andreevich\nORG:Image\nTITLE:\nitem1.TEL;waid=79099291652:+7 123 456-78-91\nitem1.X-ABLabel:Мобильный\nEND:VCARD"
        }
    }
```
```json
    {
        "idMessage": "DE8CFFA93B95237B077F8FA08331A0B5",
        "timestamp": 1587129319,
        "typeMessage": "extendedTextMessage",
        "chatId": "1234567891@c.us",
        "senderId": "71234567891@c.us",
        "senderName": "John",
        "extendedTextMessage": {
            "text": "https://www.youtube.com/watch?v=9lO06Zxhu8*8*",
    	    "description": "Ролик",
            "title": "Awesome video",
            "previewType": "video",
            "jpegThumbnail": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wB=="
        }
    }
```
```json
    {
        "idMessage": "6195B3523153621DFDFC184D3317E80D",
        "timestamp": 1603182280,
        "typeMessage": "quotedMessage",
        "chatId": "71234567891@c.us",
        "senderId": "71234567891@c.us",
        "senderName": "Мой",
        "textMessage": "Quote test",
        "extendedTextMessage": {
            "stanzaId": "3A6424373F90A939B3C8",
            "participant": "71987654321@c.us"
        }
    }
```

### GetMessage errors {#errors}

For a list of errors common to all methods, refer to [Common errors](../common-errors.md) section

| HTTP code | Error identifier      | Description            |
|-----------|-----------------------|------------------------|
| 400       | `chatId not found`    | chatID is not found    |
| 400       | `ID message notfound` | IDMessage is not found |


## Python request example  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/waInstance{{idInstance}}/getMessage/{{apiTokenInstance}}"

payload = "{\r\n\"chatId\": \"120363043968066561@g.us\, \"idMessage\": \"BAE5F4886F6F2D05\" \"r\n}"
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```
