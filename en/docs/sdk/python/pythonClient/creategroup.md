# How to create a group and send a message to it
### Installation
```
pip install whatsapp-api-client-python
```
### Import 
```
from whatsapp_api_client_python import API
```
### Examples
You may see the full example at: [createGroupAndSendMessage.py](https://github.com/green-api/whatsapp-api-client-python/blob/master/examples/createGroupAndSendMessage.py)

#### How to initialize an object

```
restApi = API.RestApi(ID_INSTANCE, API_TOKEN_INSTANCE)
```
Please note that keys can be obtained from environment variables:
```
from os import environ

ID_INSTANCE = environ['ID_INSTANCE']
API_TOKEN_INSTANCE = environ['API_TOKEN_INSTANCE']
```

#### How to create a group and send a message to it

```
chatIds = [
    "11001234567@c.us"
]
resultCreate = restApi.groups.createGroup('GroupName', 
    chatIds)

if resultCreate.code == 200:
    resultSend = restApi.sending.sendMessage(resultCreate.data['chatId'], 
        'Message text')
```

IMPORTANT: If one tries to create a group with a non-existent number, WhatsApp 
may block the sender's number. The number in the example is non-existent.

### The full list of examples

Description |  Module
----- | ----- 
Example of sending text | [sendTextMessage.py](https://github.com/green-api/whatsapp-api-client-python/blob/master/examples/sendTextMessage.py)
Example of sending a picture by URL | [sendPictureByLink.py](https://github.com/green-api/whatsapp-api-client-python/blob/master/examples/sendPictureByLink.py)
Example of sending a picture by uploading from the disk | [sendPictureByUpload.py](https://github.com/green-api/whatsapp-api-client-python/blob/master/examples/sendPictureByUpload.py)
Example of a group creation and sending a message to the group | [createGroupAndSendMessage.py](https://github.com/green-api/whatsapp-api-client-python/blob/master/examples/createGroupAndSendMessage.py)
Example of incoming webhooks receiving | [receiveNotification.py](https://github.com/green-api/whatsapp-api-client-python/blob/master/examples/receiveNotification.py)
