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

### Example data -> see right side
Employee Jens Hansen with ID 1234e can be placed in a team. The other employee with ID 5678e is the same physical person - the same user - and can now be placed in another team.

## Employee is the handle to data

The employee is the entity that receives permissions to do things in the system, and is also where conversational data is kept. **Delete an employee and the person will no longer have access to data!**

Some organisations will remove an employee and create him again when moving the employee to a new department. **That is a bit dangerous** if you just copy that procedure to Musskema.dk. Doing so will remove all data from the employee. If you are going to move an employee, and at the same time give him a new ID, you should do exactly that in Musskema.dk. Then the employee will still have access to his data.

Some people ask about confidentiality between leader and employee when moving employees between teams, or changing leader on a team. We'll handle that for you! So you can safely move employees without risk of someone seing things they should not.
