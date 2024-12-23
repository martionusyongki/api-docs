# BUTTON API SPEC

## Create Button

Endpoint : POST /api/subfeatures/{idSubFeature}/buttons

Request Header :

- X-API-TOKEN : token (Mandatory)

Request Body :

```json
{
  "id" : "save", // alfanumeric, mandatory, max 50
  "subFeatureId" : "purchaseorder", // alfanumeric, mandatory, max 50
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
  "errors" : "id, sub feature id, name, user_login must not be blank, button already exists"
}
```

Response Body (Failed, 401) :

```json
{
  "errors" : "unauthorized"
}
```

## Get Button

Endpoint : GET /api/subfeatures/{idSubFeature}/buttons/{id}

Request Header :

- X-API-TOKEN : token (Mandatory)

Response Body (Success) :

```json
{
  "data" : {
    "id" : "save",
    "subFeatureId" : "purchaseorder",
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
  "errors" : "button not found"
}
```

## Update Button

Endpoint : PATCH /api/subfeatures/{idSubFeature}/buttons/{id}

Request Header :

- X-API-TOKEN : token (Mandatory)

Request Body :

```json
{
  "name" : "save", // alfanumeric, mandatory, max 100
  "isActive" : true, // boolean
  "updatedBy": "current login username" // mandatory, as user login
}
```

Response Body (Success) :

```json
{
  "data" : {
    "id" : "purchase",
    "subFeatureId" : "purchaseorder",
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
  "errors" : "button not found"
}
```

## Search Button

Endpoint : GET /api/subfeatures/buttons

Query Param :

- id : String, button id, using like query, optional
- subFeatureId : String, sub feature id, using like query, optional
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
      "subFeatureId" : "admin",
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