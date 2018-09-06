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

It might be a bit confusing with both users and employees - but there is a reason for it. In many larger organisations there are users with multiple employments, one physical person is employeed in multiple different departments.

Employee Jens Hansen with ID 1234e can be placed in a team. The other employee with ID 5678e is the same physical person - the same user - and can now be placed in another team. (See data in right side of page.)

In Musskema.dk the user is just the person logging in. The employee is the entity placed in teams where all conversation data is attached to. Users with multiple employees will be asked to select employee when logging in.
