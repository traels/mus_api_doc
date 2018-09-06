# Users and employees

## Splitting users and employees

> Data for employee, consisting of an employment and data for user behind employee:

```json
[{
  "id": "1234e",
  "employement": "Programmer",
  "user": {
    "id": "987u",
    "username": "jh987",
    "name": "Jens Hansen",
    "email": "geek@programmer.it",
    "gender": "m",
    "birthday": "1979-09-11"
  }
},{
  "id": "5678e",
  "employement": "Geek",
  "user": {
    "id": "987u",
    "username": "jh987",
    "name": "Jens Hansen",
    "email": "geek@programmer.it",
    "gender": "m",
    "birthday": "1979-09-11"
  }
}]
```

Everybody in a company is an employee - no matter your privileges or permissions you are first and foremost an employee.

Employees are not users! That might sound strange, but some people have multiple employments within the same organisation - each of those is an employee, but all of a persons employments are connected to the same user to only have one username and password.

The employee is the entity that receives permissions to do things in the system, and is also where conversational data is kept. Delete an employee and the person will no longer have access to data.

### Example data -> see right side
Employee Jens Hansen with ID 1234e can be placed in a team. The other employee with ID 5678e is the same physical person - the same user - and can now be placed in another team.