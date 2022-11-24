# How to receive a message
### Installation
1. [Download a processing model](https://github.com/green-api/whatsapp-1c-example/releases/download/1.0/GreenAPI.epf) in the epf format
2. Подключиться к сервису через встроенный в обработку помощник или  самостоятельно через сайт [green-api.com](https://green-api.com/). Получить ``API Token`` и ``ID Instance``
3. Запустить в браузере или тонком клиенте и указать параметры подключения (``API Token`` и ``ID Instance``)
4. Сканировать QR код с мобильного телефона WhatsApp (Меню чаты -> Иконка всех функций -> Связанные устройства -> Привязка устройства)
6. В форме обработки нажать кнопку ``Проверить подключение``. Поле формы статус должно изменится на "Подключен"

![`Проверить подключение`](https://github.com/green-api/whatsapp-api-client-1c/blob/master/media/Login.png?raw=true)

### Использование обработки в собственных конфигурациях

Обработка имеет программный интерфейс, оформленный в соответствии со [стандартами разработки 1С](https://its.1c.ru/db/v8std). Вы можете встроить ее в свою конфигурацию и вызывать АПИ на сервере через создание объекта.

### Examples

#### How to receive a message using a processing model

![`Получение сообщения`](https://github.com/green-api/whatsapp-api-client-1c/blob/master/media/Receiving.png?raw=true)

1. Перейти на вкладку ``Получение сообщений``
2. Нажать на кнопку ``Получить сообщенние``. Если сообщение было отправлено, то поле ``Тело сообщения`` заполнится данными в формате JSON. Если нет отправленных сообщенимй - то обработка будет ждать 20 секунд для получения сообщения.

### The full list of examples

Description |  Module
----- | ----- 
1C demo processing model for WhatsApp| [GreenAPI.epf](https://github.com/green-api/whatsapp-1c-example/releases/download/1.0/GreenAPI.epf)
Sources of 1C processing model for WhatsApp| [whatsapp-api-client-1c](https://github.com/green-api/whatsapp-api-client-1c)
