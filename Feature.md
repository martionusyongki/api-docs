# FEATURE API SPEC

## Create Feature

Endpoint : POST /api/features

Request Header :

- X-API-TOKEN : token (Mandatory)

Request Body :

```json
{
  "id" : "purchase", // alfanumeric, mandatory, max 50
  "name" : "purchase", // alfanumeric, mandatory, max 100
  "createdBy": "current login username" // mandatory, as user login
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
  "errors" : "id, name, user_login must not be blank, feature already exists"
}
```

Response Body (Failed, 401) :

```json
{
  "errors" : "unauthorized"
}
```

## Get Feature

Endpoint : GET /api/features/{id}

Request Header :

- X-API-TOKEN : token (Mandatory)

Response Body (Success) :

```json
{
  "data" : {
    "id" : "purchase",
    "name" : "purchase",
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
  "errors" : "feature not found"
}
```

## Update Feature

Endpoint : PATCH /api/features/{id}

Request Header :

- X-API-TOKEN : token (Mandatory)

Request Body :

```json
{
  "name" : "purchase", // alfanumeric, mandatory, max 100
  "isActive" : true, // boolean
  "updatedBy": "current login username" // mandatory, as user login
}
```

Response Body (Success) :

```json
{
  "data" : {
    "id" : "purchase",
    "name" : "purchase",
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
  "errors" : "feature not found"
}
```

## Search Feature

Endpoint : GET /api/features

Query Param :

- id : String, feature id, using like query, optional
- name : String, name, using like query, optional
- isActive : boolean, active, using like query, optional
- page : Integer, start from 0
- size : Integer, default 10

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
  "errors" : "Unauthorized"
}
```