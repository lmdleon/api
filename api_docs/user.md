# User (Пользователь)

## Создание

`POST /api/user`

```json
{
    "externalId": "externalID1104",
    "login": "TestLogin",
    "lastName": "TestLastName",
    "firstName": "TestFirstName",
    "middleName": "TestMiddleName",
    "email": "test@croc.ru",
    "phoneNumber": "1111",
    "positionExternalId": "2C4F847B-CF28-4821-AAB0-7A4F8FE01980",
    "organizationExternalId": "27BCD90F-AEF8-44AB-ABDF-BB319D986C75",
    "managerExternalId": "FABC3F0F-5CAB-44C2-A6A9-4F246DF2491F",
    "isActive": "true",
    "HireDate": "2020-18-02T00:00:00+03:00",
    "type": "F651709A-3951-4A7B-BE31-DFE6B1F598A7",
    "postfix": "ДРПО"    
}
```

### Описание полей

|Поле|Тип|Ограничения|Описание|
|----|--------|------------|------------|
|externalId|string| Unique |Внешний идентификатор (опциональный)|
|login| string | - | Логин |
|lastName| string | - | Фамилия |
|firstName| string | - | Имя |
|middleName| string | - | Отчество |
|phoneNumber| string | - | Номер телефона |
|positionExternalId| string | - | Позиция |
|organizationExternalId| string | - | Организация |
|managerExternalId| string | - | Руководитель |
|isActive| string | - | Активен |
|HireDate| string | - | Дата приёма на работу |
|type| string | - | Тип |
|postfix| string | - | Постфикс |

### Логика работы

Если при создании возникла ошибка будет возвращён код ```500``` и текст ошибки
В случае, если пользователь уже существует в БД, то его данные будут обновлены в соответствии с переданными значениями. И будет вовращён статус ```200 OK```
В случае успешного создания, возвращается идентификатор пользователя и статус ```201 Created```

## Обновление пользователя

`PUT /api/user`

Сообщение в тело запроса соответствует сообщению для создания сущности. Сущность обновляется целиком (полная замена ресурса), поэтому должным быть заполнены все параметры. Если какой-то из параметров будет отсутствовать в теле запроса, то это будет воспринято как заполнение пустым значением.
</br>

Если при создании возникла ошибка будет возвращён код ```500``` и текст ошибки

## Обновление фотографии

`POST /api/user/photo`

В Body запроса:

```json
{    
    "externalId": "externalID1104",
    "photo" : "bytes"       
}
```
### Логика работы

Если при обновлении фотографии возникла ошибка будет возвращён код ```500``` и текст ошибки. Если пользователь с указанным идентификатором не найден, то будет передан код ```404 NotFound```. В случае успешного обновления фотографии ```200 OK```

## Удаление

`DELETE /api/user/{id}`

где `{id}` - идентификатор пользователя

### Логика работы

Если при удалении возникнет ошибка, то будет возвращен код ```500```. 
В случае успешного удаления ```200 OK```

## Получение 

#### Получение конкретной записи

`GET /api/user/{id}`
где `id` - идентификатор пользователя

#### Получение всех записей

`GET /api/user`

### Логика работы

Если при получении возникнет ошибка, то будет возвращен код ```500``` и текст ошибки 
В случае успешного запроса возвращен статус ```200 OK```, в теле же ответа будут указан пользователь или список пользователей в формате:

```json
{
    "Id": "065D3C46-F3BD-4292-8D5F-002A0DA030C8",
    "externalId": "externalID1104",
    "login": "TestLogin",
    "lastName": "TestLastName",
    "firstName": "TestFirstName",
    "middleName": "TestMiddleName",
    "email": "test@croc.ru",
    "phoneNumber": "1111",
    "positionExternalId": "2C4F847B-CF28-4821-AAB0-7A4F8FE01980",
    "organizationExternalId": "27BCD90F-AEF8-44AB-ABDF-BB319D986C75",
    "managerExternalId": "FABC3F0F-5CAB-44C2-A6A9-4F246DF2491F",
    "isActive": "true",
    "HireDate": "2020-18-02T00:00:00+03:00",
    "type": "F651709A-3951-4A7B-BE31-DFE6B1F598A7",
    "postfix": "ДРПО"    
}
```

### Описание полей

|Поле|Тип|Ограничения|Описание|
|----|--------|------------|------------|
|Id|Guid| Unique | Идентификатор |
|externalId|string| Unique |Внешний идентификатор (опциональный)|
|login| string | - | Логин |
|lastName| string | - | Фамилия |
|firstName| string | - | Имя |
|middleName| string | - | Отчество |
|phoneNumber| string | - | Номер телефона |
|positionExternalId| string | - | Позиция |
|organizationExternalId| string | - | Организация |
|managerExternalId| string | - | Руководитель |
|isActive| string | - | Активен |
|HireDate| string | - | Дата приёма на работу |
|type| string | - | Тип |
|postfix| string | - | Постфикс |
