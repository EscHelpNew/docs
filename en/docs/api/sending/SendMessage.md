# SendMessage

The method is aimed for sending a text message to a personal or a group chat.
The message will be added to the send queue. Linked device not required when sending. Messages will be kept for 24 hours in the queue until account will be authorized 
The rate at which messages are sent from the queue is managed by [Message sending delay](../send-messages-delay.md) parameter.

## Request {#request}

To send a text message, you have to execute a request at:
```
POST https://api.green-api.com/waInstance{{idInstance}}/SendMessage/{{apiTokenInstance}}
```

For `idInstance` and `apiTokenInstance` request parameters, refer to [Before you start](../../before-start.md#parameters) section.

### Request parameters {#request-parameters}

Parameter | Type | Mandatory | Description
----- | ----- | ----- | -----
`chatId` | **string** | Yes | [Chat Id](../chat-id.md)
`message` | **string** | Yes | Message text. Emoji 😃 characters supported 
`quotedMessageId` | **string** | No | Quoted message ID. If present, the message will be sent quoting the specified chat message
`archiveChat` | **boolean** | No | Archives the chat to which the message was sent. Takes value: true|false
`linkPreview` | **boolean** | No | The parameter includes displaying a preview and a description of the link. Enabled by default. Accepts values: true|false


> The maximum length of a text message is 4096 characters

### Request body example {#request-example-body}

Sending a message to a personal chat:
```json
{
    "chatId": "11001234567@c.us",
    "message": "I use Green-API to send this message to you!"
}
```

Sending a message to a group chat:
```json
{
    "chatId": "11001234567-1581234048@g.us",
    "message": "I use Green-API to send this message to you!"
}
```

Sending a quoted message:
```json
{
    "chatId": "11001234567@с.us",
    "message": "I use Green-API to send this message to you!",
    "quotedMessageId": "361B0E63F2FDF95903B6A9C9A102F34B"
}
```
## Response {#response}

### Response parameters {#response-parameters}

Parameter | Type |  Description
----- | ----- | -----
`idMessage ` | **string** | Sent message Id 

### Response body example {#response-example-body}

```json
{
    "idMessage": "3EB0C767D097B7C7C030"
}
```

### SendMessage errors {#errors}

For a list of errors common to all methods, refer to [Common errors](../common-errors.md) section

## Python request example {#request-example-python}

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
