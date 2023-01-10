# Receive webhooks via Webhook Endpoint

Webhook Endpoint technology allows you to receive incoming webhooks directly to your server. This means that the Green API server will make a call to the method published on your server side. The advantage of this technology is the fastest possible receipt of incoming webhooks and high capacity, limited only by the rate of processing webhooks on your server side. The disadvantages include the implementation complexity. 

> The Green API server makes attempts to deliver webhooks at 1-minute interval. Therefore, set up your server so that it is always available to process incoming webhooks, or use [Receive webhooks via HTTP API](technology-http-api.md) technology. The delivery of incoming webhooks is guaranteed within 24 hours. 

## Server setting

To receive incoming webhooks using Webhook Endpoint technology, you will need to complete the below steps:

- to publish the IP address on the internet
- to implement the logic for processing incoming webhooks to the specified IP address
- if required for the server, then set the Webhook URL Token 

### Public IP address

To receive incoming webhooks, a public IP address (endpoint) is required, which will be accessible from the Internet. Thus, the Green API server will be able to make a call to your server at the specified address and transmit an incoming webhook.

### Our public IP-addresses which we sent webhooks from

You may specify the below IP addresses from which webhooks from us are received, in your server's security settings:

```
51.250.84.44
51.250.94.65
51.250.91.13
51.250.93.251
51.250.76.115
51.250.69.65
51.250.68.181
51.250.69.45
51.250.74.200
51.250.87.205
```
### Incoming webhooks processing

After receiving an incoming call to the IP address of your server, you will need to process the received webhook. You can see the example of incoming webhook processing code on [NodeJS](https://nodejs.org) in [file](https://github.com/green-api/whatsapp-api-client/blob/master/examples/ReceiveWebhook.js)

## Account setup {#webhookUrl}

Before receiving incoming webhooks, you need to set up your account. Account settings can be performed [in software](# SetSettings) using [SetSettings](../account/SetSettings.md) method, or [online](#cabinet) in your profile interface.

### Setting by [SetSettings](../account/SetSettings.md) {#SetSettings} method

To set up receiving incoming webhooks using Webhook Endpoint technology, you need to specify your IP address or your domain name as the `webhookUrl` parameter, and, if necessary,` webhookUrlToken` to access your server. For example:

```
https://84.211.100.201:3000/green-api/webhook/
```

It is also required to specify what types of webhooks you need to receive. To enable incoming webhooks by type, as well as to specify `webhookUrl` and` webhookUrlToken` parameters, use [SetSettings](../account/SetSettings.md) method.

#### Example of [SetSettings](../account/SetSettings.md) method request body

```json
{
    "webhookUrl": "https://84.211.100.201:3000/green-api/webhook/",
    "webhookUrlToken": "dscnsdiuafkascndjhsalbcvatsvcbasn23rfregvfdg54tds",
    "outgoingWebhook": "yes",
    "stateWebhook": "yes",
    "incomingWebhook": "yes",
    "deviceWebhook": "no"
}
```

### Setup in your profile {#cabinet}

You can also set up to receive incoming webhooks online. To do this, go to [My Profile](https://console.green-api.com) and select the required user account. If the account is authorized, the settings for receiving incoming webhooks will be displayed, see fig. Specify the `webhookUrl` parameter, as well as the switches by webhooks types and, if you need authorization on your webhook server, specify Webhook URL Token. If the account is not authorized and the webhooks settings are not displayed, refer to [Before you start](../../before-start.md#qr) section.

![Setup in your profile](../../assets/technology-webhook-endpoint.png)

## Receive incoming webhooks

After setting up the account, you can start receiving webhooks. You can see the example of incoming webhook processing code:

- On [NodeJS](https://nodejs.org) in [file](../../sdk/nodejs/receiveNotificationserver.md#_5).

- On [Python](https://python.org) in [file](../../sdk/python/pythonWebhookServer/index.md).

## Debug incoming webhooks

You can use any free service on the Internet to debug incoming webhooks, for example, [Webhook.Site](https://webhook.site/) service. The service issues a unique address (URL), which is required to [set](# webhookUrl) as the `webhookUrl` parameter.

A detailed description of incoming webhooks format is given in [Incoming webhooks format](notifications-format/index.md) section.

Http request example that send by green-api:

```
curl --request POST 'your-webhook-url-address' \
--header 'Content-Type: application/json; charset=utf-8' \
--data-raw '{"typeWebhook":"statusInstanceChanged","instanceData":{"idInstance":000001,"wid":"7123456789@c.us","typeInstance":"whatsapp"},"timestamp":1654553712,"statusInstance":"online"}'
```
