# CoolFeedback API. Авторизация
 
 Используемый способ авторизации настраивается на этапе развёртывания API

# 1. Basic авторизация

Подробности [здесь](https://en.wikipedia.org/wiki/Basic_access_authentication). Для получения учетных данных для доступа необходимо обратиться на поддержку сервиса

В случае непередачи авторизационного заголовка, либо при налчии в нем некорректных данных - возвращается HTTP код ```401 Unauthorized```


# 2. Token Authentication

В данном случае используются два токена access token и refresh token.

## Access token

Время жизни - 12 часов

Выдаётся при вводе логина/пароля пользователя
Пример запроса:
` http://localhost:51649/api/auth/signin `
В теле запроса передаётся JSON объект
```json
{ 
  "Login" : "TestLogin",
  "Password" : "TestPassword"
}
```

В результате успешной проверки логина/пароля выдаётся ответ в виде:
```json
{
    "accessToken": "eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJQYURtaXRyaWV2IiwianRpIjoiODczZTFlMDMtMzEwYy00YWNhLTgyZGQtNmVjMzllYTdiNDEwIiwiaWF0IjoxNTgyMDExNTQ5LCJpZCI6ImU1MWY5NDE5LTkwYWUtNGY3Ni0zYzMzLTA4ZDcxYTUyNDczZCIsImxvZ2luIjoicGFkbWl0cmlldiIsImlzQWRtaW4iOiJUcnVlIiwibmJmIjoxNTgyMDExNTQ4LCJleHAiOjE1ODIwMTE3MjgsImlzcyI6ImNvb2xmZWVkYmFjayIsImF1ZCI6Imh0dHA6Ly9sb2NhbGhvc3Q6NTAwMC8ifQ.jpYqj7mBLaela1Q0IQ-_JkhRYnTCTj-Llmu7Pj8158ybu7YPmidDeTLvRaLJnx38LwLmBRu36niSBDBPbtK-PA",
    "refreshToken": "b5c74ff0-fc41-433d-9a93-d3fb519dcbbf",
    "tokenExpiration": "2020-02-18T10:42:08+03:00"
}
```
В котором мы получаем access и refresh токен, а также время жизни access токена, в формате ГГГГ-ММ-ДДTЧЧ:MM:CCUTC

В дальнейшем, access токен передаётся в Authotization заколовке типа Bearer Token
```json
Key : Authorization
Value : Bearer eyJhbGciOiJIUzUxMiI...
```

## Refresh token

Время жизни - 1 месяц

Refresh token выдаётся при успешной аутентификации. Используется для получения новой пары access/refresh токенов.
Для запроса новой пары токенов:
` http://localhost:51649/api/auth/refresh `

В заголовке refresh_token передаётся значение полученного ранее refresh токена. В том случе, если токен не корректный, будет получен ответ BadRequest. Если время жизни токена истекло - Unauthorized

В случае успешной проверки refresh токена, будет получен ответ, аналогичный ответу, полученному при аутентификации, содержащий новые access и refresh токены, а также время жизни access токена. 

Refresh токен, с помощью которого была получена новая пара access/reshresh токенов, будет отозван и его повторное использование приведёт к ошибке




 
