# Departments

## Structure of the organisation and ID's to related data

Departments are the building blocks for your companys organisation in Musskema.dk. Managers are set as responsible for departments, gaining access to configuration and reports for that branch of the organisation tree.

Everytime you create or update a department you set its parent department - building the organisation from top to bottom.

### ID fields

Department has relations to other departments and to managers, they are returned as ID's. Default is Musskema.dk ID but if you have set [ext_id as key](#unique-id-39-s) that will be returned for all these values.

## Get all departments

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v2/core/departments'
```

> The above command returns JSON structured like this:

[
  {
    "id": "123",
    "name": "ABC"
    "ext_id": "007",
    "parent_department": "99875",
    "responsible_employee": "1231"
  },
  {
    "id": "123B",
    "name": "DEF"
    "ext_id": "008",
    "parent_department": "123",
    "responsible_employee": "1231"
  }
]

This endpoint retrieves all departments - 25 departments at a time.

### HTTP Request

`GET https://api.secure2.musskema.dk/v2/core/departments`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Request more departments

## Get a specific department

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v2/core/departments/123789'
```

> The above command returns JSON structured like this:

```json
{
  "name": "Department name",
  "id": "123789",
  "ext_id": "007",
  "parent_department": "99875",
  "responsible_employee": "1231"
}
```

### HTTP Request

`GET https://api.secure2.musskema.dk/v2/core/departments/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the department - either Musskem.dk ID or your own ID (ext_id)


## Create a department

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"department":{"name":"New department","parent_department":"1234G43Z","ext_id":"007"}}'
 -X GET 'https://api.secure2.musskema.dk/v2/core/departments'
```

> Example of JSON data for creating department:

```json
{
  "department": {
    "parent_department": "12332",
    "name": "ABC",
    "ext_id": "101",
    "responsible_employee": "321"
  }
}
```

> Responds with data on newly created department:

```json
{
  "id": "234",
  "name": "ABC",
  "ext_id": "101",
  "parent_department": "12332",
  "responsible_employee": "321"
}
```

### HTTP Request

`POST https://api.secure2.musskema.dk/v2/core/departments`

### Attributes in JSON data

Name | Required | Description
---- | -------- | -----------
name | no | String with full name of department.
parent_department | yes | ID of department where department is to be placed.
responsible_employee | no | ID of manager for this department.
ext_id | no | Your ID number for the department.

### Response

If everyting works out the response will be with HTTP header 201 - Created, along with a location header pointing to the new department. Full JSON data on newly created department is also present.

## Update a department

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'company_id: CID'
 -H 'access_token: token'
 -d '{"department":{"name":"Updated department"}}'
 -X PUT 'https://api.secure2.musskema.dk/v2/core/departments/123789'```

> Example of JSON data for updating department:

```json
{
  "department": {
    "name": "ABCDEF",
  }
}
```

> Responds with new complete data for department:

```json
{
  "id": "234",
  "name": "ABCDEF",
  "ext_id": "101",
  "parent_department": "12332",
  "responsible_employee": "321"
}
```

### HTTP Request

`PUT https://api.secure2.musskema.dk/v2/core/departments<ID>`

### Attributes in JSON data

Name | Required | Description
---- | -------- | -----------
name | no | String with full name of department.
parent_department | yes | ID of department where department is to be placed.
responsible_employee | no | ID of manager for this department.
ext_id | no | Your ID number for the department.

<aside class="success">
Moving a department - and the organisation branch below it - is as simple as just setting a new parent department.
</aside>

## Delete a department

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X PUT 'https://api.secure2.musskema.dk/v2/core/departments/123'
```

### HTTP Request

`DELETE https://api.secure2.musskema.dk/v2/core/departments<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the department - either Musskem.dk ID or your own ID (ext_id)

<aside class="notice">
There can be nothing below a department when you delete it. You will have to remove teams and departments below it first.
</aside>
