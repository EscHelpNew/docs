# Как отправить сообщение

### Установка

Не забудьте создать модуль:

```shell
go mod init example
```

Установка:

```shell
go get github.com/green-api/whatsapp-api-client-golang
```

### Импорт

```
import (
	"github.com/green-api/whatsapp-api-client-golang/pkg/api"
)
```

### Примеры

#### Как инициализировать объект

```
GreenAPI := api.GreenAPI{
    IDInstance:       "1101000001",
    APITokenInstance: "d75b3a66374942c5b3c019c698abc2067e151558acbd412345",
}
```

Обратите внимание, что ключи можно получать из переменных среды:

```
IDInstance := os.Getenv("ID_INSTANCE")
APITokenInstance := os.Getenv("API_TOKEN_INSTANCE")
```

#### Как отправить сообщение

Если у метода API есть необязательные параметры, то в метод библиотеки нужно передавать JSON (`map[string]interface{}`).

Ссылка на пример: [sendMessage/main.go](
https://github.com/green-api/whatsapp-api-client-golang/blob/master/examples/sendMessage/main.go
).

```
response, _ := GreenAPI.Methods().Sending().SendMessage(map[string]interface{}{
    "chatId":  "11001234567@c.us",
    "message": "Any message",
})
```

### Запуск приложения

```shell
go run main.go
```

### Список примеров

| Описание                             | Ссылка на пример                                                                                                                  |
|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| Как создать группу                   | [createGroup/main.go](https://github.com/green-api/whatsapp-api-client-golang/blob/master/examples/createGroup/main.go)           |
| Как отправить файл загрузкой с диска | [sendFileByUpload/main.go](https://github.com/green-api/whatsapp-api-client-golang/blob/master/examples/sendFileByUpload/main.go) |
| Как отправить файл по ссылке         | [sendFileByURL/main.go](https://github.com/green-api/whatsapp-api-client-golang/blob/master/examples/sendFileByURL/main.go)       |
| Как отправить сообщение              | [sendMessage/main.go](https://github.com/green-api/whatsapp-api-client-golang/blob/master/examples/sendMessage/main.go)           |
| Как получать входящие уведомления    | [webhook/main.go](https://github.com/green-api/whatsapp-api-client-golang/blob/master/examples/webhook/main.go)                   | 
