# Авторизация

Для выполнения большинства запросов к API необходимо передавать access-токен.
Авторизация осуществляется по протоколу OAuth 2.0

## Получение access-токена

Предварительно необходимо [зарегистрировать](https://t.me/TalentForce_Bot) приложение.

**Запрос**

Необходимо отправить POST-запрос на:

`{{talentforce.url}}/Api/access_token`

В теле запроса необходимо передать дополнительные параметры:

```json
{
    "grant_type":"password",
    "client_id":"{{Client_ID}}",
    "client_secret":"{{client_secret}}",
    "username":"{{Username}}",
    "password":"{{Password}}"
}
```
Тело запроса необходимо передавать в стандартном application/x-www-form-urlencoded с указанием соответствующего заголовка Content-Type:

**Пример ответа**

```json
{
    "token_type": "Bearer",
    "expires_in": 3600,
    "access_token": "полученный_access_token",
    "refresh_token": "полученный_refresh_token"
}
```

## Использование access-токена

Приложение должно использовать полученный `access_token` для авторизации,
передавая его в заголовке в формате:

```Authorization: Bearer полученный_access_token```

или используя тип авторизации = OAuth 2.0:

```Available Tokens: полученный_access_token```
