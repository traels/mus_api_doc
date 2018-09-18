# - Departments

## Create department

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"department":{"name":"Basement crew","owner":"4711","id":"D987"}}'
 -X POST 'https://api.secure2.musskema.dk/v3/core/departments/D9/departments'
```

> HTTP 201 Created - with complete data of new department, including responsible_employee:

```json
{
  "name": "Basement crew",
  "id": "D987",
  "responsible_employee": {
    "employment": "Programmer",
    "id": "4711",
    ...
  },
  "parent_id": "D9"
}
```

<aside class="success">
<b>POST</b> https://api.secure2.musskema.dk/v3/{core|wpa}/departments/{department_id}/departments
</aside>

Creating a department is on an endpoint under another department as this will always require a parent department.

Field | Value | Required
------|-------|---------
name | Name of department | Yes
owner | ID for employee who owns department | No
id | Your ID for department | Yes

[Read about owner and responsible employee](#owner-responsible-person-on-team-and-departments)

## Update department

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"department":{"name":"Basement department"}}'
 -X PATCH 'https://api.secure2.musskema.dk/v3/core/departments/D987'
```

> HTTP 200 OK - with complete data of updated department, including responsible_employee:

```json
{
  "name": "Basement department",
  "id": "D987",
  "responsible_employee": {
    "employment": "Programmer",
    "id": "4711",
    ...
  },
  "parent_id": "D9"
}
```

<aside class="success">
<b>PATCH</b> https://api.secure2.musskema.dk/v3/{core|wpa}/departments/{id}
</aside>

Field | Value | Required
------|-------|---------
name | Name of department | No
owner | ID for employee who owns department | No
id | Your ID for department | No  

[Read about owner and responsible employee](#owner-responsible-person-on-team-and-departments)

## Delete department

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X DELETE 'https://api.secure2.musskema.dk/v3/core/departments/D987'
```

> HTTP 200 OK

<aside class="success">
<b>DELETE</b> https://api.secure2.musskema.dk/v3/{core|wpa}/departments/{id}
</aside>

<aside class="notice">
In order to prevent accidential deletes a department can only be deleted when there are no departments or teams attached to it.
</aside>

## Move department

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X PATCH 'https://api.secure2.musskema.dk/v3/core/departments/D11/departments/D987'
```

> HTTP 200 OK

<aside class="success">
<b>PATCH</b> https://api.secure2.musskema.dk/v3/{core|wpa}/departments/{department_id}/departments/{id}
</aside>

Moves department {id} below department {department_id}. You can not move a department below it self.

## Show department

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v3/core/departments/D987'
```

> HTTP 200 OK - with complete data of department, including responsible_employee:

```json
{
  "name": "Basement department",
  "id": "D987",
  "responsible_employee": {
    "employment": "Programmer",
    "id": "4711",
    ...
  },
  "parent_id": "D9"
}
```

<aside class="success">
<b>GET</b> https://api.secure2.musskema.dk/v3/{core|wpa}/departments/{id}
</aside>

## Show department list

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v3/core/departments'
```

> HTTP 200 OK - with array of departments:

```json
[{
  "name": "Basement department",
  "id": "D987",
  "responsible_employee": {
    "employment": "Programmer",
    "id": "4711",
    ...
  },
  "parent_id": "D9"
}]
```

<aside class="success">
<b>GET</b> https://api.secure2.musskema.dk/v3/{core|wpa}/departments
</aside>

[List is paginated](#pagination)