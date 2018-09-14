# - Employees in team

<aside class="notice">
  A employee can only be in one team, if you add him to a team when he is already in another he will be removed from the other team. 
</aside>

As mentioned both in [here](#employee-is-the-handle-to-data) and [here](#teams-are-handles-to-data) there are som rules about employees and teams and how it all relates to data, so please read that.

## Add employee to team

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X POST 'https://api.secure2.musskema.dk/v3/core/teams/A11111/employees/4711'
```

> HTTP 200 OK - with complete team data:

```json
{
  "name": "The A Team",
  "id": "A11111",
  "responsible_employee": {
    "employment": "Leader",
    "id": "00001",
    ...
  },
  "employees": [
    {
      "employment": "Programmer",
      "id": "4711",
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
  <b>POST</b> https://api.secure2.musskema.dk/v3/{core|wpa}/teams/{team_id}/employees/{employee_id}
</aside>

## Remove employee from team

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X DELETE 'https://api.secure2.musskema.dk/v3/core/teams/A11111/employees/4711'
```

> HTTP 200 OK - with complete team data:

```json
{
  "name": "The A Team",
  "id": "A11111",
  "responsible_employee": {
    "employment": "Leader",
    "id": "00001",
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
  <b>DELETE</b> https://api.secure2.musskema.dk/v3/{core|wpa}/teams/{team_id}/employees/{employee_id}
</aside>
