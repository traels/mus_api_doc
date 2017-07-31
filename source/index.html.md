---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://secure2.musskema.dk/signup'>Sign Up for a Demo Account</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - employees
  - teams
  - departments
  - sickness
  - errors

search: true
---

# Introduction

Welcome to the Musskema.dk API documentation. To access the API you need to have a company on Musskema.dk and have the API access token for that company.

The API allows you to maintain employees, teams, departments and sickness absense data so you can have your ERP, HR or whatever other tool sync its data to Musskema.dk.

## One-way sync

We have simplified the world a bit by only allowing one-way syncronisation. When you enable API sync for a part of Musskema.dk that part will no longer be available to users on the site. If you setup syncronisation of employees then employees will no longer be able to change name, username or other profile data.

## Unique ID's

> Default response for an employee

```json
{
  "name": "Jane Doe",
  "id": "123",
  "email": "jd@mail.tld",
  "ext_id": "ABC1",
  "username": "jd",
  "gender": "f",
  "birthday": "1979-09-11"
}
```

> Response with key_field=ext_id

```json
{
  "name": "Jane Doe",
  "id": "ABC1",
  "email": "jd@mail.tld",
  "username": "jd",
  "gender": "f",
  "birthday": "1979-09-11"
}
```

Everything has a external ID (ext_id) field that is for you to use. This way you can attach your identifier to the data when creating it - making it easier when you need to find it again and update it.

Default data from API includes both Musskema.dk ID and external ID on everything. You can change that by a simple param on the URL.

`http://api.secure2.musskema.dk/v2/teams?key_field=ext_id`

This will remove the ext_id from the data and use the value from ext_id in the returned id field.

<aside class="success">
When the API tells you to give it an ID you can use either Musskema.dk ID value or your own ext_id value!
</aside>

## Authentication

```shell
# With shell, you can just pass the correct header with each request
curl -v -H 'Content-Type: application/json'
 -H 'company_id: 10238497'
 -H 'access_token: 01298347edf923874a'
 -X GET 'https://api.secure2.musskema.dk/v2/core/departments'
```

> Make sure to replace `01298347edf923874a` with your API key and `10238497` with your company id.

Authentication is done by HTTP headers. You must supply both company_id and access_token headers.

<aside class="notice">
The API access token is created by our support team at info@musskema.dk.
</aside>

## Build your organisation

The organisation in Musskema.dk consists of a tree of departments with team as the leafs. Departments holds nothing but managers, employees are working from the teams.

## What the API can do

**You can use the API in 2 ways:**

 * creating and updating employees - this is the minimum
 * create organisation structure and place employees in teams - this is optional, without this organisation is created from within Musskame.dk

**Then there are a few addons:**

 * create and delete sickness absense - if your employees are registred as sick in another system you can have the status transfered to Musskema.dk to start a sickness absense dialog
 * WPA organisation - the workplace assesment is using a organisational structure of its own, it is possible to enable access to this structure from API, to manage departments and teams in WPA