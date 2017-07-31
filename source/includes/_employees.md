
# Employees

## A few notes about employees, users and usernames

Everybody in a company is an employee - no matter your privileges or permissions you are first and foremost an employee.

Employees are not users! That might sound strange, but some people have multiple employments within the same organisation - each of those is an employee, but all of a persons employments are connected to the same user to only have one username and password.

Even when an employee is deleted the username is reserved for that employee. 14 days after the employee has been deleted he can no longer be rehired and his username is released.

## Get all employees

```shell
curl -v -H 'Content-Type: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v2/core/employees'
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "123",
    "name": "ABC",
    "email": "e@mail.tld",
    "ext_id": "ABC1",
    "gender": null,
    "birthday": null,
    "employment": null
  },
  {
    "id": "123B",
    "name": "DEF",
    "email": "e@post.tld",
    "ext_id": "ZXC32",
    "gender": "m",
    "birthday": "1979-09-11",
    "employment": null
  }
]
```

This endpoint retrieves all employees - 25 employees at a time

### HTTP Request

`GET https://api.secure2.musskema.dk/v2/core/employees`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Request more employees

## Get a specific employee

```shell
curl -v -H 'Content-Type: application/json' -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v2/core/employees/123B'
```

> The above command returns JSON structured like this:

```json
{
  "id": "123B",
  "name": "DEF",
  "email": "e@post.tld",
  "ext_id": "ZXC32",
  "gender": "m",
  "birthday": "1979-09-11"
}
```

This endpoint retrieves a specific employee

### HTTP Request

`GET https://api.secure2.musskema.dk/v2/core/employees/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the employee - either Musskem.dk ID or your own ID (ext_id)

## Create an employee

```shell
curl -v -H 'Content-Type: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"employee":{"email":"e@mail.tld","username":"agent","name":"James Bond","ext_id":"123"}}'
 -X POST 'https://api.secure2.musskema.dk/v2/core/employees'
```

> Example of JSON data to create an employee

```json
{
  "employee": {
    "email":"e@mail.tld",
    "username":"agent",
    "name":"James Bond",
    "ext_id":"123"
  }
}
```

> Example of reponse from creating employee:

```json
{
  "id": "123645AB321",
  "email":"e@mail.tld",
  "username":"agent",
  "name":"James Bond",
  "ext_id":"123",
  "gender": null,
  "birthday": null,
  "employment": null
}
```

This endpoint will create a new employee, but also has the ability to create a second employment for a person or rehire a sacked employee.

### HTTP Request

`POST https://api.secure2.musskema.dk/v2/core/employees`

### Attributes in JSON data

Name | Required | Description
---- | -------- | -----------
email | yes | String with valid e-mail.
username | yes | String with username - will default to e-mail if not supplied.
name | yes | String with full name of employee.
gender | no | String with one letter: (m)ale or (f)emale.
birthday | no | String with date in format YYYY-MM-DD.
ext_id | no | Your ID number for the employee.
employment | no | String with title/name of employment. Required when adding a second employment!

### Rehiring a sacked employee

If you've fired an employee by mistake and need to rehire him again you simply create the employee once more, with exactly the same name, e-mail, username and ext_id.

<aside class="notice">
This will ONLY work within 14 days from firing the employee, after that a new employee is created.
</aside>

### Adding a second employment

> Add second employment to employee created above:

```json
{
  "employee": {
    "email":"e@mail.tld",
    "username":"agent",
    "name":"James Bond",
    "employment":"Secret identity",
    "ext_id":"234"
  }
}
```

Sometimes a person has multiple employments in the same organisation. This is handle by having multiple employees in Musskema.dk.

To help simplify the life of persons with multiple employments all employments are connected to the same user. Creating a second employment requires you to create employee with exactly the same name, e-mail and username AND supplying an employment name for this.

### Response

If everyting is good we will respond with 201 - Created and set a location header pointing to the newly created employee.
Alongside that will be a JSON response with the newly created employees data.

## Update an employee

```shell
curl -v -H 'Content-Type: application/json' -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"employee":{"username":"agent","name":"James Bond","ext_id":"1234987"}}'
 -X POST 'https://api.secure2.musskema.dk/v2/core/employees/321'
```

> Example of JSON data to update an employee

```json
{
  "employee": {
    "email":"new@mail.tld"
  }
}
```

> Example of reponse from updating employee:

```json
{
  "id": "123645AB321",
  "email":"new@mail.tld"
  "username":"agent",
  "name":"James Bond",
  "ext_id":"123",
  "gender": null,
  "birthday": null,
  "employment": null
}
```

### HTTP Request

`PUT https://api.secure2.musskema.dk/v2/core/employees/<ID>`

### Attributes in JSON data

Name | Required | Description
---- | -------- | -----------
email | no | String with valid e-mail.
username | no | String with username - will default to e-mail if not supplied.
name | no | String with full name of employee.
gender | no | String with one letter: (m)ale or (f)emale.
birthday | no | String with date in format YYYY-MM-DD.
ext_id | no | Your ID number for the employee.
employment | no | String with title/name of employment.

## Delete an employee

```shell
curl -v -H 'Content-Type: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X DELETE 'https://api.secure2.musskema.dk/v2/core/employees/321'
```

If this employee has multiple employments he will still be able to log in to the other employment. If it was the only one the person does no longer have access to Musskema.dk.

Did you fire the employee by mistake you can [rehire him](#rehiring-a-sacked-employee).

<aside class="warning">
After 14 days it is no longer possible to rehire the employee!
</aside>

### HTTP Request

`https://api.secure2.musskema.dk/v2/core/employees/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the employee - either Musskem.dk ID or your own ID (ext_id)
