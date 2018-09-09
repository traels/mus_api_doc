# - Delegations

Delegations is the same for both teams and departments, so this chapter covers two endpoints. 
URL varies and reponse shows either team or department that delegation has been created on.

<aside class="notice">
Delegations is also where we break the rule about ID's. This endpoint takes no ID and return our internal ID when showing delegation data.
</aside>

### Responsibilities available on teams

Core/WPA | Responsibility name | Grants access to
---------|---------------------|-----------------
Core | dialog_access_cv | Access to teams CV data
Core | dialog_access_onboarding | Access to onboarding dialog for team
Core | dialog_access_siab | Access to sickness absence dialog for team
Core | dialog_access_edp | Access to employee development dialog for team
WPA | dialog_access_wpa | Access to workplace assessment dialog for team

### Responsibilities available on departments

Core/WPA | Responsibility name | Grants access to
---------|---------------------|-----------------
Core | manage_organisation_department | Access to organisation editor for department
Core | configuration | Access to configuration for this department
Core | department_task_report_siab | Ability to read tasks for employees in department
Core | department_task_report_edp | Ability to read tasks for employees in department
WPA | department_task_report_wpa | Ability to read tasks for employees in department

 - any of these will also give access to statistics for this department.
 - any of these will also give access to organisation editor for department (when you have API enabled that is a read only access)
 - all of these is for the chosen department and all departments below

## Create delegation

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -d '{"delegation":{"responsibility":"dialog_access_edp","employee_id":"78765"}}'
 -X POST 'https://api.secure2.musskema.dk/v3/core/departments/D9/delegations'
```

> HTTP 201 Created - with data for new delegation:

```json
{
  "id": "1234567890",
  "responsibility": "dialog_access_edp",
  "employee": {
    "employment": "Programmer",
    "id": "78765",
    ...
  },
  "department|team": {
    "name": "The Firm",
    "id": "D9",
    ...
  }
}
```

<aside class="success">
<b>POST</b> https://api.secure2.musskema.dk/v3/{core|wpa}/{departments|teams}/{id}/delegations
</aside>

Field | Value | Required
------|-------|---------
responsibility | [A responsibility name valid for either team or department](#delegations) | Yes
employee_id | Your ID for employee to delegate responsibility to | Yes  

## Destroy delegation

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X DELETE 'https://api.secure2.musskema.dk/v3/core/departments/D9/delegations/1234567890'
```

> HTTP 200 OK

<aside class="success">
<b>DELETE</b> https://api.secure2.musskema.dk/v3/{core|wpa}/{departments|teams}/{id}/delegations/{id}
</aside>

## Show delegation list

```shell
curl -v -H 'Content-Type: application/json' -H 'Accept: application/json'
 -H 'company_id: <CID>'
 -H 'access_token: <TOKEN>'
 -X DELETE 'https://api.secure2.musskema.dk/v3/core/departments/D9/delegations/1234567890'
```

> HTTP 200 OK - with array of delegations for team or department:

```json
[{
  "id": "1234567890",
  "responsibility": "dialog_access_edp",
  "employee": {
    "employment": "Programmer",
    "id": "78765",
    ...
  },
  "department|team": {
    "name": "The Firm",
    "id": "D9",
    ...
  }
}]
```

<aside class="success">
<b>GET</b> https://api.secure2.musskema.dk/v3/{core|wpa}/{departments|teams}/{id}/delegations
</aside>
