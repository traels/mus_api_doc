# Sickness absense

When an employee is calling in sick you start a sickness absense, which will prompt the leader to talk to the employee. 

Automating this with the API is only really usefull if you already have a system for managing sickness absense.

## Get all sick employees

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v2/siab/dialogs'
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "123",
    "name": "ABC",
    "date": "2018-01-03",

  },
  {
    "id": "123B",
    "name": "DEF",
    "date": "2018-02-03",
  }
]
```

This gives you all sick employees, their employee ID and the date they were reported sick.

### HTTP Request

`GET https://api.secure2.musskema.dk/v2/siab/dialogs`

## Report employee sick

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'company_id: CID'
 -H 'access_token: token'
 -d '{"employee":"708","date":"2016-12-24"}'
 -X POST 'https://api.secure2.musskema.dk/v2/siab/dialogs'
```

### Attributes in JSON data

Name | Required | Description
---- | -------- | -----------
employee | yes | ID of employee to report sick.
date | yes | Date employee is reported sick. **Format:** YYYY-MM-DD.

### Response

HTTP header 201 - Created.

<aside class="notice">
You can not report an employee sick without the employee being in a team. Without a team Musskema.dk does not know who the employees leader is, and can not start a dialog between employee and leader.
</aside>

<aside class="notice">
An employee can not be reported sick, when he or she is already reported sick. Trying to do so will give an error.
</aside>

## Update sick date

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'company_id: CID'
 -H 'access_token: token'
 -d '{"date":"2019-12-24"}'
 -X PATCH 'https://api.secure2.musskema.dk/v2/siab/dialogs/708'
```

> Example of JSON data to update first day of sickleave

```json
{
  "date": "2019-12-24"
}
```

> The above command returns JSON structured like this:

```json
{
  "id": "708",
  "name": "ABC",
  "date": "2019-12-24",
}
```

### HTTP Request

`GET https://api.secure2.musskema.dk/v2/siab/dialogs/<EMPLOYEE_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the employee - either Musskem.dk ID or your own ID (ext_id)


## Report employee fit

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'company_id: CID'
 -H 'access_token: token'
 -d '{"employee":"708","date":"2016-12-24"}'
 -X DELETE 'https://api.secure2.musskema.dk/v2/siab/dialogs'
```

### Attributes in JSON data

Name | Required | Description
---- | -------- | -----------
employee | yes | ID of employee to report fit.
date | yes | Last day of employees sick leave. **Format:** YYYY-MM-DD.
