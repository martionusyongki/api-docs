# ROLE API SPEC

## Create Role

Endpoint : POST /api/roles

Request Header :

- X-API-TOKEN : token (Mandatory)

Request Body :

```json
{
  "id" : "admin", // alfanumeric, mandatory, max 100
  "name" : "admin", // alfanumeric, mandatory, max 100
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
  "errors" : "id, name, user_login must not be blank, role already exists"
}
```

Response Body (Failed, 401) :

```json
{
  "errors" : "unauthorized"
}
```

## Get Role

Endpoint : GET /api/roles/{id}

Request Header :

- X-API-TOKEN : token (Mandatory)

Response Body (Success) :

```json
{
  "data" : {
    "id" : "admin",
    "name" : "admin",
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
  "errors" : "role not found"
}
```

## Update Role

Endpoint : PATCH /api/roles/{id}

Request Header :

- X-API-TOKEN : token (Mandatory)

Request Body :

```json
{
  "name" : "admin", // alfanumeric, mandatory, max 100
  "isActive" : true, // boolean
  "updatedBy": "yongki" // mandatory, as user login
}
```
Response Body (Success) :

```json
{
  "data" : {
    "id" : "admin",
    "name" : "admin",
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
  "errors" : "role not found"
}
```

## Search Role

Endpoint : GET /api/roles

Query Param :

- id : String, role id, using like query, optional
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
      "id" : "admin",
      "name" : "admin",
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