# UnarchiveChat
The method unarchives a chat.
## Request {#request}

To unarchive a chat, you have to execute a request at:
```
POST https://api.green-api.com/waInstance{{idInstance}}/unarchiveChat/{{apiTokenInstance}}
```

For `idInstance` and `apiTokenInstance` request parameters, refer to [Before you start](../../before-start.md#parameters) section.

### Request parameters {#request-parameters}

Parameter | Type | Mandatory | Description
----- | ----- | ----- | -----
`chatId` | **string** | Yes | [User or group chat Id](../chat-id.md)

### Request body example {#request-example-body}

```json
{
    "chatId": "120363043968066561@g.us"
}
```

## Response {#response}

### Response parameters {#response-parameters}

The response body is empty. If successful, the server response is 200.

### UnarchiveChat errors {#errors}

For a list of errors common to all methods, refer to [Common errors](../common-errors.md) section

HTTP code | Error identifier | Description
----- | ----- | -----
400 | `"ArchiveChatError: cannot archive chat cause last message not found in chat"` | chatID is false or there is no message in the chat

## Python request example  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/waInstance{{idInstance}}/unarchiveChat/{{apiTokenInstance}}"

payload = "{\r\n    \"chatId\": \"120363043968066561@g.us\"r\n}"
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```
