[Back to README.md](README.md)

# Role Model (class)

The `Role` model defines the privileges that a user be assigned with. A user can be assigned only 1 role.

Unlike other models, the Role has a string for the primary key.

There are five privileges available for a role. A role can be created with multiple privileges. If a role does have multiple privileges and one privilege has a privilege and one does not, the user WILL have the privilege. For example, a role can be created with BOTH `IsAdmin` and `IsStaff`:

* `IsRoot`: no restrictions
* `IsAdmin`: no current restrictions
* `IsStaff`: may not maintain users or roles
* `IsInstructor`: can manage a cohort they are teaching, create & modify an assessment, review students assessment and scores, check a student in and out of the cohort.
* `IsStudent`: can check-in & out, take and view assessements

## Properties

Legend
    Types: (B)oolean, (D)ateTime, (I)nt, (S)tring, 

| Name                | Type | Null | Notes |
| ---                 | ---  | ---  | ---   |
| Id (PK)             |  I   |  N   |       |
| Username            |  S   |  N   | Value must be unique      |
| Password            |  S   |  N   |       |
| Firstname           |  S   |  N   |       |
| Lastname            |  S   |  N   |       |
| Email               |  S   |  Y   |       |
| Cellphone           |  S   |  Y   |       |
| Workphone           |  S   |  Y   |       |
| RoleCode (FK)       |  I   |  Y   |       |
| SecurityKey         |  S   |  Y   | For future use |
| PinCode             |  S   |  Y   | Obsolete |
| Active              |  B   |  N   |       |
| Created             |  D   |  N   |       |
| Updated             |  D   |  Y   |       |

Users must login to BCMS using their `Username` and `Password`.

`RoleCode` defines priveleges for the user (see Role model)

When `Active` is false, the user is treated as if it is *logically* deleted.

`Created` and `Updated` are maintained by the system and should not be modified. They exist primarily for debugging purposes.

Most other property are for display purposes only.

## Foreign Keys to

NONE

## Primary Key for

* User
