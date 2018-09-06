# Teams

## About teams and ID's

Teams is where the real work happens. They are the leaf on the organisation and the place employees are attached. They are the groups used for many types of dialogs and where leader is connected to employees.

### ID fields

Team has a lot of relations, they are returned as ID's. Default is Musskema.dk ID but if you have set [ext_id as key](#unique-id-39-s) that will be returned for all these values.

 * department
 * employees
 * responsible_employee

## About employees in teams

An employee can ONLY be in one team, if you insert the same employee in more teams he will just be moved to the last team you insert him into.
<aside class="warning">
As all dialogs in Musskema.dk is connected between teams and the manager of the team it is important that employee is placed in correct team!
</aside>


## Get all teams

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v2/core/teams'
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "234",
    "department": "12332",
    "name": "ABC",
    "employees": [
      "123",
      "321"
    ],
    "ext_id": "101",
    "responsible_employee": "321"
  },
  {
    "id": "90",
    "name": "ABCD",
    "employees": [
      "321",
      "543"
    ],
    "responsible_employee": "9908",
  }
]
```

This endpoint retrieves all teams - 25 teams at a time.

### HTTP Request

`GET https://api.secure2.musskema.dk/v2/core/teams`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Request more teams


## Get a specific team

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v2/core/teams/234'
``

> The above command returns JSON structured like this:

```json
{
  "id": "234",
  "department": "12332",
  "name": "ABC",
  "employees": [
    "123",
    "321"
  ],
  "ext_id": "203",
  "responsible_employee": "321"
}
```

### HTTP Request

`GET https://api.secure2.musskema.dk/v2/core/teams/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the team - either Musskem.dk ID or your own ID (ext_id)

## Create a team

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"team":{"name":"ABC","department":"12332","employees":["123","321"],"responsible_employee":"321","ext_id":"101"}}'
 -X POST 'https://api.secure2.musskema.dk/v2/core/teams'
```

> Example of JSON data for creating team:

```json
{
  "team": {
    "department": "12332",
    "name": "ABC",
    "employees": [
      "123",
      "321"
    ],
    "ext_id": "101",
    "responsible_employee": "321"
  }
}
```

> Responds with data on newly created team:

```json
{
  "id": "234",
  "department": "12332",
  "name": "ABC",
  "employees": [
    "123",
    "321"
  ],
  "ext_id": "101",
  "responsible_employee": "321"
}
```

### HTTP Request

`POST https://api.secure2.musskema.dk/v2/core/teams`

### Attributes in JSON data

Name | Required | Description
---- | -------- | -----------
department | yes | ID of department where team is to be placed.
name | no | String with full name of team.
ext_id | no | Your ID number for the team.
employees | no | ID of employees to be put into this team. Employees can only be in one team at a time.
responsible_employee | no | ID of leader for this team.

### Response

If everyting works out the response will be with HTTP header 201 - Created, along with a location header pointing to the new team. Full JSON data on newly created team is also present.

## Update a specific team

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"team":{"name":"ABC","department":"12332","employees":["123","321"]}}'
 -X PUT 'https://api.secure2.musskema.dk/v2/core/teams/123'
```

> Example of JSON data for updating team:

```json
{
  "team": {
    "department": "3210",
    "name": "ABCDEF",
  }
}
```

> Responds with new complete data for team:

```json
{
  "id": "234",
  "department": "3210",
  "name": "ABCDEF",
  "employees": [
    "123",
    "321"
  ],
  "ext_id": "101",
  "responsible_employee": "321"
}
```

### HTTP Request

`PUT https://api.secure2.musskema.dk/v2/core/teams<ID>`

### Attributes in JSON data

Name | Required | Description
---- | -------- | -----------
department | yes | ID of department where team is to be placed.
name | no | String with full name of team.
ext_id | no | Your ID number for the team.
employees | no | ID of employees to be put into this team. Employees can only be in one team at a time.
responsible_employee | no | ID of leader for this team.

### Moving a team to a new department

With update you can also change the department to move the team to a new location in organisation. All employees will follow the team to its new location.

### Updating list of employees

The list of employees is a full list - so if you want to add an employee to the team you must supply a full list with both new and old team members. If you wish to remove all members from team you must supply an empty list.

## Delete a team

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X PUT 'https://api.secure2.musskema.dk/v2/core/teams/123'
```

### HTTP Request

`DELETE https://api.secure2.musskema.dk/v2/core/teams<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the team - either Musskem.dk ID or your own ID (ext_id)

<aside class="notice">
There can be no employees in team when deleting it.
</aside>

<aside class="warning">
A deleted team CAN NOT be restored - all dialogs concerning that team is invisible to any leader who were involved!
</aside>

