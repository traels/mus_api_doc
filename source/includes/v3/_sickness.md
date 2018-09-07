# Sickness absense

This is a bit of a special endpoint. There are a lot of logic in Musskema.dk around sickness absence, so to help you we have made just one endpoint for registering sickness absence. You will not need to worry about keeping track of periods in you end, we will detect overlapping periods and decide if you data should update existing or create new absence period.

### Not everything can be handled, so a few rules to start with:

 - employee **must** be in team to be reported sick
 - if you supply a date range that overlaps multiple existing periods you will get an error 

## Report employee sick and fit

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"employee_id":"708","start_date":"2016-12-24"}'
 -X POST 'https://api.secure2.musskema.dk/v3/siab/dialogs'
```
> If there are no errors data for absence will be returned.

> HTTP header tells if you have created a new absence (201) or just updated an existing (200)

```json
{
  "id": "9876",
  "start_date": "2016-12-24",
  "end_date": "9999-12-31",
  "employee": {
    "id": "708",
    "employment": null,
    "user": {
      "name": "Jane Doe",
      "gender": null,
      "birthday": null,
      "email": "jane@mail.tld",
      "username": "user_1_name",
      "id": "78765"
    }
  }
}
```
<aside class="notice">
You can not report an employee sick without the employee being in a team. Without a team Musskema.dk does not know who the employees leader is, and can not start a dialog between employee and leader.
</aside>


### Attributes in JSON data

Name | Required | Description
---- | -------- | -----------
employee_id | yes | ID of employee to report sick.
start_date | yes | Date employee is reported sick. **Format:** YYYY-MM-DD.
end_date | no | Last day employee is sick. **Format:** YYYY-MM-DD.

**End date** is optional, if you leave out end date the employee is considered sick from start date and **for ever after**.

### Start and end dates and all the rules

> Reporting same employee sick with new dates

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"employee_id":"708","start_date":"2016-12-21","end_date":"2017-01-01"}'
 -X POST 'https://api.secure2.musskema.dk/v3/siab/dialogs'
```

> Results in simply updating the existing absence (HTTP 200 OK)

```json
{
  "id": "9876",
  "start_date": "2016-12-21",
  "end_date": "2017-01-01",
  "employee": {
    "id": "708",
    "employment": null,
    "user": {
      "name": "Jane Doe",
      "gender": null,
      "birthday": null,
      "email": "jane@mail.tld",
      "username": "user_1_name",
      "id": "78765"
    }
  }
}
```

* If you create a new absence period that overlaps a period on the employee
 * end date will be updated if you have supplied one
 * start date will be updated if (either A or B below)
 * **A:** it is before the start date on absence that it overlaps (expanding the period)
 * **B:** you have supplied the exact same end date as the absence it overlaps (then contracting the period)
* If you create a new absence period on the day after employee has been reported fit this is also considered an overlap, and will simply just extend that absence period.
* If you create a new absence in the past (determined by either the employee having been sick after that period, or it is more than 2 month ago) - the absence will be silenced and no conversation will take place in Musskema.dk.
* If you create a absence that overlaps a period where end date is in the past, then the dates will be updated but since the absence is in the past it will be silenced and no notifications and conversations will be generated in Musskema.dk.


<aside class="warning">
  Creating a period that overlaps 2 existing absences will result in an error!
</aside>

<!--
## Get all currently sick employees

This gives you all sick employees with the day they are reported sick, and the ID of the absence.

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X GET 'https://api.secure2.musskema.dk/v3/siab/dialogs'
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "123",
    "start_date": "2018-01-03",
    "end_date": "2018-12-31",
    "employee": {
      "id": "747",
      "name": "Jane Doe",
      "email": "jane@mail.tld",
      "gender": null,
      "birthday": null,
      "employment": null
    }
  },
  {
    "id": "2345",
    "start_date": "2018-02-03",
    "end_date": "9999-12-31",
    "employee": {
      "id": "112",
      "name": "John Doe",
      "email": "john@mail.tld",
      "gender": null,
      "birthday": null,
      "employment": null
    }
  }
]
```

### HTTP Request

`GET https://api.secure2.musskema.dk/v3/siab/dialogs`
-->