# - Teams

## Create team

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"user":{"name":"The A Team","owner":"78765","id":"A11111"}}'
 -X POST 'https://api.secure2.musskema.dk/v3/core/departments/D9/teams'
```

> HTTP 201 Created - with complete data of new team, including responsible_employee and department:

```json
{
  "name": "The A Team",
  "id": "A11111",
  "responsible_employee": {
    "employment": "Programmer",
    "id": "78765",
    ...
  },
  "employees": [],
  "department": {
    "name": "The Firm",
    "id": "9987",
    ...
  }
}
```

<aside class="success">
<b>POST</b> https://api.secure2.musskema.dk/v3/{core|wpa}/departments/{department_id}/teams
</aside>

Creating a team is on an endpoint under departments as this will always require a department.

Field | Value | Required
------|-------|---------
name | Name of team | Yes
id | Your ID for team | Yes  

## Update team

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"user":{"name":"The A Team","owner":"78765","id":"A1"}}'
 -X PATCH 'https://api.secure2.musskema.dk/v3/core/teams/A11111'
```

> HTTP 200 OK - with complete data of updated team, including responsible_employee, employees and department:

```json
{
  "name": "The A Team",
  "id": "A1",
  "responsible_employee": {
    "employment": "Programmer",
    "id": "78765",
    ...
  },
  "employees": [ 
    {
      "employment": "Geek",
      "id": "4321",
      ...
    }, 
    {
      "employment": "Another Geek",
      "id": "1234",
      ...
    }
  ],
  "department": {
    "name": "The Firm",
    "id": "9987",
    ...
  }
}
```

<aside class="success">
<b>PATCH</b> https://api.secure2.musskema.dk/v3/{core|wpa}/teams/{id}
</aside>

Field | Value | Required
------|-------|---------
name | Name of team | No
id | Your ID for team | No  

## Delete team

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X DELETE 'https://api.secure2.musskema.dk/v3/core/teams/A11111'
```

> HTTP 200 OK

<aside class="success">
<b>DELETE</b> https://api.secure2.musskema.dk/v3/{core|wpa}/teams/{id}
</aside>

<aside class="warning">
Deleting a team is a permanent and very destructive action. Conversational data in Musskema.dk connects leaders and employes through the team - deleting the team makes the data associated with it unavailable to the leader.
</aside>

## Show team

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v3/core/teams/A11111'
```

> HTTP 200 OK - with complete data of team, including responsible_employee, employees and department:

```json
{
  "name": "The A Team",
  "id": "A1",
  "responsible_employee": {
    "employment": "Programmer",
    "id": "78765",
    ...
  },
  "employees": [ 
    {
      "employment": "Geek",
      "id": "4321",
      ...
    }, 
    {
      "employment": "Another Geek",
      "id": "1234",
      ...
    }
  ],
  "department": {
    "name": "The Firm",
    "id": "9987",
    ...
  }
}
```
<aside class="success">
<b>GET</b> https://api.secure2.musskema.dk/v3/{core|wpa}/teams/{id}
</aside>

## Show team list


```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v3/core/teams'
```

> HTTP 200 OK - array with teams:

```json
[{
  "name": "The A Team",
  "id": "A1",
  "responsible_employee": {
    "employment": "Programmer",
    "id": "78765",
    ...
  },
  "employees": [ 
    {
      "employment": "Geek",
      "id": "4321",
      ...
    }, 
    {
      "employment": "Another Geek",
      "id": "1234",
      ...
    }
  ],
  "department": {
    "name": "The Firm",
    "id": "9987",
    ...
  }
}]
```
<aside class="success">
<b>GET</b> https://api.secure2.musskema.dk/v3/{core|wpa}/teams
</aside>

[List is paginated](#pagination)