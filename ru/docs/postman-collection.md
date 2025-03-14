# Коллекция Postman

Для тестирования и отладки запросов к Green API рекомендуется использовать [Green API - Postman Collection](https://github.com/green-api/green-api-postman-collection)

[Postman](https://www.getpostman.com/) - популярный инструмент для тестирования и разработки API. Чтобы упростить разработчикам интеграцию с Green API, мы создали коллекцию Postman с полным набором необходимых API.

1. [Установка](#setup): установка коллекции
2. [Конфигурирование](#configure): настройка переменных среды
3. [Тестирование](#test): использование методов API

## Видеоинструкция

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/MkuiIck5Z4c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</center>

## Установка {#setup}

Чтобы приступить к работе, скачайте указанные ниже компоненты и установите Postman:

- Приложение [Postman](https://www.postman.com/downloads/) 
- Коллекция [Green API - Postman Collection](https://github.com/green-api/green-api-postman-collection) (клонируйте репозиторий или скачайте пакет в виде ZIP-файла)

После установки и запуска Postman, нажмите `Import` и выберите два JSON-файла `collection.json` и `environment.json` из пакета коллекции [Postman на GitHub](https://github.com/green-api/green-api-postman-collection).

<center>![`Пункт 1`](./assets/postman_step1.png)</center>

<center>![`Пункт 2`](./assets/postman_step2.png)</center>

 После импорта вы увидите элемент `Green API` в разделе `Collections` и сможете выбрать пункт `Green API Developer` в качестве `Environment`.

## Конфигурирование {#configure}

Настраиваемая среда Postman фактически представляет собой набор пар "ключ-значение". Вы можете создавать стандартные переменные, которые затем будут использоваться в разных запросах. [Подробнее о переменных среды Postman](https://learning.postman.com/docs/postman/variables-and-environments/managing-environments/).

Заранее настроенная среда `Green API Developer` содержит полный набор переменных, на которые ссылается коллекция. Некоторые из этих переменных следует отредактировать и заменить собственными значениями. Чтобы открыть диалог редактирования, нажмите маленькую кнопку с изображением глаза рядом с раскрывающимся списком среды и выберите `Edit`.

Задайте значения двух переменных `idInstance`и `apiTokenInstance`, которые были получены на этапе [Перед началом работы](before-start.md#parameters).

## Тестирование {#test}

Теперь вы можете выбрать любой метод API в коллекции и приступать к отправке запросов. Все методы для удобства приведены в том же порядке, в каком они рассматриваются в [Документации API](api/index.md). Вы можете вносить в эти методы любые изменения, чтобы упростить их тестирование и обработку ответов.