[Back to README.md](README.md)

# User Model (class)

The `User` model defines users that can log and use BCMS. The model is also used to identify the 'owner' of some other models.

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

* Role

## Primary Key for

* Enrollment
* Cohort
* Feedback
* Commentary (2x)
* InstructorCohort