# SUB FEATURE API SPEC

## Create Sub Feature

Endpoint : POST /api/features/{featureId}/subfeatures

Request Header :

- X-API-TOKEN : token (Mandatory)

Request Body :

```json
{
  "id" : "purchaseorder", // alfanumeric, mandatory, max 50
  "featureId" : "purchase", // alfanumeric, mandatory, max 50
  "name" : "Purchase Order", // alfanumeric, mandatory, max 100
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
  "errors" : "id, feature id, name, user_login must not be blank, sub feature already exists"
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

## Get Sub Feature

Endpoint : GET /api/features/{featureId}/subfeatures/{id}

Request Header :

- X-API-TOKEN : token (Mandatory)

Response Body (Success) :

```json
{
  "data" : {
    "id" : "purchaseorder",
    "featureId" : "purchase",
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
  "errors" : "sub feature not found"
}
```

## Update Sub Feature

Endpoint : PATCH /api/features/{featureId}/subfeatures/{id}

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
    "id" : "purchaseorder",
    "featureId" : "purchase",
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
  "errors" : "sub feature not found"
}
```

## Search Sub Feature

Endpoint : GET /api/features/subfeatures

Query Param :

- id : String, sub feature id, using like query, optional
- featureId : String, feature id, using like query, optional
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
      "featureId" : "admin",
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