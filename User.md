# USER API SPEC

## Create User

Endpoint : POST /api/users

Request Header :

- X-API-TOKEN : token (Mandatory)

Request Body :

```json
{
  "id": "test", // alfanumeric, mandatory, min 5, max 20
  "password": "test", // alfanumeric, mandatory, min 5, max 20
  "name": "yongki", // alfanumeric, mandatory, max 100
  "roleId": "admin", // mandatory
  "createdBy": "yongki" // mandatory, as user login
}
```

Response Body (Success) :

```json
{
  "data" : "successfully registered"
}
```

Response Body (Failed, 400) :

```json
{
  "errors" : "id, password, name, user_login must not be blank, id already exists"
}
```

Response Body (Failed, 401) :

```json
{
  "errors" : "unauthorized"
}
```

## Get User

Endpoint : GET /api/users/{id}

Request Header :

- X-API-TOKEN : token (Mandatory)

Response Body (Success) :

```json
{
  "data" : {
    "id" : "test",
    "name" : "test",
    "roleId" : "admin",
    "isActive" : true
  }
}
```

Response Body (Failed, 401) :

```json
{
  "errors" : "unauthorized"
}
```

Response Body (Failed, 404) :

```json
{
  "errors" : "id not found"
}
```

## Update User

Endpoint : PATCH /api/users/{id}

Request Header :

- X-API-TOKEN : token (Mandatory)

Request Body :

```json
{
  "password": "test", // alfanumeric, mandatory, min 5, max 20
  "name": "yongki", // alfanumeric, mandatory, max 100
  "roleId": "admin",
  "isActive" : true // boolean
  "updatedBy": "yongki" // mandatory, as user login
}
```

Response Body (Success) :

```json
{
  "data" : {
    "id" : "test",
    "name" : "yongki update",
    "roleId" : "admin",
    "isActive" : true
  }
}
```

Response Body (Failed, 401) :

```json
{
  "errors" : "unauthorized"
}
```

Response Body (Failed, 404) :

```json
{
  "errors" : "id not found"
}
```

## Search User

Endpoint : GET /api/users

Query Param :

- id : String, username, using like query, optional
- name : String, name, using like query, optional
- isActive : boolean, active, using like query, optional
- page : Integer, start from 0, mandatory
- size : Integer, default 10, mandatory

Request Header :

- X-API-TOKEN : token (Mandatory)

Response Body (Success) :

```json
{
  "data" : [
    {
      "id" : "test",
      "name" : "yongki",
      "roleId" : "admin",
      "isActive" : true
    }
  ],
  "paging" : {
    "currentPage" : 0,
    "totalPage" : 10,
    "size" : 10
  }
}
```

Response Body (Failed, 401) :

```json
{
  "errors" : "unauthorized"
}
```

## Login User

Endpoint : POST /api/auth/login

Request Body :

```json
{
  "id" : "test", // alfanumeric, mandatory, min 5, max 20
  "password" : "test" // alfanumeric, mandatory, min 5, max 20
}
```

Response Body (Success) :

```json
{
  "data" : {
    "id" : "test",
    "roleId" : "admin",
    "token" : "token",
    "expiredAt" : 123456 // milliseconds
  }
}
```

Response Body (Failed, 401) :

```json
{
  "errors" : "incorrect id or password"
}
```

## Logout User

Endpoint : DELETE /api/auth/logout

Request Header :

- X-API-TOKEN : token (Mandatory)

Response Body (Success) :

```json
{
  "data" : "successfully logged out"
}