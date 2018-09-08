# - Employees

## Create employee

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"employee":{"employment":"Geek","id":"4711"}}'
 -X POST 'https://api.secure2.musskema.dk/v3/core/users/78765/employees'
```

> HTTP 200 OK - with complete data of employee:

```json
{
  "employment": "Geek",
  "id": "4711",
  "user": {
    "name": "Jane Fonda",
    "gender": "f",
    "birthday": "1989-09-13",
    "email": "jane@mail.tld",
    "username": "user_1_name",
    "id": "78765"
  }
}
```

<aside class="notice">
<b>POST</b> https://api.secure2.musskema.dk/v3/core/users/{user_id}/employees
</aside>

Creating an employee is on an endpoint under users as this will always require a user.

### Data in _employee_ JSON structure

Field | Value | Required
------|-------|---------
employment | Title of employment | No
id | Your ID for user | Yes  

## Update employee

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"employee":{"employment":"Programmer"}}'
 -X PATCH 'https://api.secure2.musskema.dk/v3/core/employees/4711'
```

> HTTP 200 OK - with complete data of updated employee:

```json
{
  "employment": "Programmer",
  "id": "4711",
  "user": {
    "name": "Jane Fonda",
    "gender": "f",
    "birthday": "1989-09-13",
    "email": "jane@mail.tld",
    "username": "user_1_name",
    "id": "78765"
  }
}
```

<aside class="notice">
<b>PATCH</b> https://api.secure2.musskema.dk/v3/core/employees/{id}
</aside>

### Data in _employee_ JSON structure

Field | Value | Required
------|-------|---------
employment | Title of employment | No
id | Your ID for user | No  

## Show employee

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v3/core/employees/4711'
```

> HTTP 200 OK - with complete data of employee:

```json
{
  "employment": "Programmer",
  "id": "4711",
  "user": {
    "name": "Jane Fonda",
    "gender": "f",
    "birthday": "1989-09-13",
    "email": "jane@mail.tld",
    "username": "user_1_name",
    "id": "78765"
  }
}
```

<aside class="notice">
<b>GET</b> https://api.secure2.musskema.dk/v3/core/employees/{id}
</aside>

## Show employee list

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v3/core/employees/4711'
```

> HTTP 200 OK - with array of employees:

```json
[{
  "employment": "Programmer",
  "id": "4711",
  "user": {
    "name": "Jane Fonda",
    "gender": "f",
    "birthday": "1989-09-13",
    "email": "jane@mail.tld",
    "username": "user_1_name",
    "id": "78765"
  }
}]
```

<aside class="notice">
<b>GET</b> https://api.secure2.musskema.dk/v3/core/employees
</aside>

[List is paginated](#pagination)

## Delete (fire) employee

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X DELETE 'https://api.secure2.musskema.dk/v3/core/employees/4711'
```

> HTTP 200 OK

<aside class="notice">
<b>DELETE</b> https://api.secure2.musskema.dk/v3/core/employees/{id}
</aside>

As all conversational data is attached to an employee, this will only do a softdelete and mark the employee as fired. This way you will be able to rehire the user, if you have made a mistake.

You can not delete the owner of the topmost department in the organisation.

## Undelete (rehire) employee

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X PATCH 'https://api.secure2.musskema.dk/v3/core/users/78765/employees/4711'
```

> HTTP 200 OK

<aside class="notice">
<b>PATCH</b> https://api.secure2.musskema.dk/v3/core/users/{user_id}/employees/{id}
</aside>

Rehiring an employee is on an endpoint under users as this will always require a user.

 - you can not rehire an employee if you have created a new employee with same ID
 - when you rehire you set the ID of the user you wish to attach the employee to, useful for when you have also deleted the old user employee was attached to