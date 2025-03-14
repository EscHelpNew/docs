# Получить QR-код через websocket

Наравне с получением QR-кода методом [QR](QR.md) существует возможность получить QR-код через websocket-соединение. Таймаут ожидания сканирования QR-кода составляет 100 сек. За это время QR-код должен быть отсканирован. Для получения QR-кода аккаунт должен быть в неавторизованном состоянии. Если аккаунт авторизован, то предварительно требуется разлогинить аккаунт методом [Logout](Logout.md).

После успешного сканирования QR-кода и авторизации аккаунта формируется [входящее уведомление](../receiving/index.md) с видом [Статус аккаунта](../receiving/notifications-format/StateInstanceChanged.md).

Для получения QR-кода требуется установить websocket-соединение по адресу: 

```
wss://api.green-api.com/waInstance{{idInstance}}/scanqrcode/{{apiTokenInstance}
```
## Пример получения QR-кода через websocket {#request-example-js}

Пример получения QR-кода через wesocket можно посмотреть в файле [websocketExampleQRcode](https://github.com/green-api/whatsapp-api-client/blob/master/examples/browserExampleQRCodeWebsocket.html) 

## Ответ {#response}

### Поля ответа {#response-parameters}

Поле | Тип |  Описание
----- | ----- | ----- 
`type` | **string** | Тип сообщения, возможные значения `qrCode`, `error`, `accountData`, `alreadyLogged`, `timeoutExpired`
`message` | **string** | Содержание сообщения. Принимает различные значения в зависимости от значения поля `type`


#### Получено изображение QR-кода {#response-type-qrCode}

Поле | Тип |  Описание
----- | ----- | ----- 
`type` | **string** | `qrCode` - получено изображение QR-кода
`message` | **string** | Изображение QR-кода в кодировке `base64`. Для вывода в браузере нужно добавить строку `data:image/png;base64, {message}`


#### Возникла ошибка {#response-type-error}

Поле | Тип |  Описание
----- | ----- | ----- 
`type` | **string** | `error` - возникла ошибка
`message` | **string** | Описание ошибки


#### Аккаунт уже авторизован {#response-type-alreadyLogged}

Поле | Тип |  Описание
----- | ----- | ----- 
`type` | **string** | `alreadyLogged` - аккаунт уже авторизован. Для получения QR-кода требуется предварительно разлогинить аккаунт методом [Logout](Logout.md)
`message` | **string** | Принимает значение `instance account already authorized`


#### Истек таймаут ожидания сканирования QR-кода {#response-type-timeoutExpired}

Поле | Тип |  Описание
----- | ----- | ----- 
`type` | **string** | `timeoutExpired` - истекло время, в течение которого QR-код должен быть отсканирован. Таймаут ожидания сканирования QR-кода составляет 100 сек.
`message` | **string** | Принимает значение `timeoutExpired`

#### Получены данные авторизованного аккаунта {#response-type-accountData}

Поле | Тип |  Описание
----- | ----- | ----- 
`type` | **string** | `accountData` - получены данные аккаунта после успешной авторизации
`wid` | **string** | Идентификатор аккаунта в формате WhatsApp
`pushname` | **string** | Имя аккаунта в WhatsApp
`webhookUrl` | **string** | URL для получения входящих уведомлений
<!-- `proxy` | **string** |  IP-адрес прокси, который назначен аккаунту -->