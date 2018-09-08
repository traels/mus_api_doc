# - Users

## Create user

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"user":{"name":"Jane Doe","gender":"f","birthday":"1989-09-13","email":"jane@mail.tld","username":"user_1_name","id":"78765"}}'
 -X POST 'https://api.secure2.musskema.dk/v3/core/users'
```

> HTTP 201 Created - with complete data of new user:

```json
{
  "name": "Jane Doe",
  "gender": "f",
  "birthday": "1989-09-13",
  "email": "jane@mail.tld",
  "username": "user_1_name",
  "id": "78765"
}
```

<aside class="notice">
<b>POST</b> https://api.secure2.musskema.dk/v3/core/users
</aside>

### Data in _user_ JSON structure

Field | Value | Required
------|-------|---------
name | Name of user | Yes
gender | f/m (female/male) | No
birthday | YYYY-MM-DD | No
email | Valid e-mail address | Yes
username | Unique username | Yes
id | Your ID for user | Yes  

## Update user

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"user":{"name":"Jane Fonda"}}'
 -X PATCH 'https://api.secure2.musskema.dk/v3/core/users/78765'
```

> HTTP 200 OK - with complete data of updated user:

```json
{
  "name": "Jane Fonda",
  "gender": "f",
  "birthday": "1989-09-13",
  "email": "jane@mail.tld",
  "username": "user_1_name",
  "id": "78765"
}
```

<aside class="notice">
<b>PATCH</b> https://api.secure2.musskema.dk/v3/core/users/{id}
</aside>

### Data in _user_ JSON structure
You only need to supply the values you wish to update.

Field | Value | Required
------|-------|---------
name | Name of user | No
gender | f/m (female/male) | No
birthday | YYYY-MM-DD | No
email | Valid e-mail address | No
username | Unique username | No
id | Your ID for user | No  

## Delete user

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X DELETE 'https://api.secure2.musskema.dk/v3/core/users/78765'
```

> HTTP 200 OK

<aside class="notice">
<b>DELETE</b> https://api.secure2.musskema.dk/v3/core/users/{id}
</aside>

 - It is not possible to delete a user that still has active employees attached
 - Deleting a user is permanent, there is no undo. If you change you mind you need to recreate the user.

## Show user

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v3/core/users/78765'
```

> HTTP 200 OK - with complete data of the user:

```json
{
  "name": "Jane Fonda",
  "gender": "f",
  "birthday": "1989-09-13",
  "email": "jane@mail.tld",
  "username": "user_1_name",
  "id": "78765"
}
```

<aside class="notice">
<b>GET</b> https://api.secure2.musskema.dk/v3/core/users/{id}
</aside>

## Show user list

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v3/core/users'
```

> HTTP 200 OK - with array of users:

```json
[{
  "name": "Jane Fonda",
  "gender": "f",
  "birthday": "1989-09-13",
  "email": "jane@mail.tld",
  "username": "user_1_name",
  "id": "78765"
}]
```

<aside class="notice">
<b>GET</b> https://api.secure2.musskema.dk/v3/core/users
</aside>

[List is paginated](#pagination)
