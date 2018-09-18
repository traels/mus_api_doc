# Departments, teams and dialogs

## Build your organisation

The organisation in Musskema.dk consists of a tree of departments with team as the leafs. Departments holds nothing but managers, employees are working from the teams.

## Teams are handles to data

As mentioned [employees](#users-and-employees) is the handle to data, so deleting an employee will remove data even though the user is still in Musskema.dk. In the same way the **team** is the handle the leader has to data between him and the employee. If you delete the team all dialog data on that team will be inaccessible to the leader.

## Owner / responsible person on team and departments

On teams and departments it is possible to set an owner, but in the response and when fetching teams and departments you will see a responsible person. The reason for this is quite simple - owner is optional, and if you do not supply one it is the closest owner (going up in the organisation) who will be responsible for the team or department.