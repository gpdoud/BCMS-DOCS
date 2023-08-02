[Back to README.md](/README.md)

# Role Model (class)

The `Role` model defines the privileges that a user be assigned with. A user can be assigned only 1 role.

Unlike other models, the Role has a string for the primary key and the value must be unique.

There are five privileges available for a role. A role can be created with multiple privileges. If a role does have multiple privileges and one privilege has allows access and one does not, the user WILL have the privilege. For example, a role can be created with BOTH `IsAdmin` and `IsStaff`:

* `IsRoot`: no restrictions
* `IsAdmin`: no current restrictions
* `IsStaff`: not used at this time
* `IsInstructor`: can manage a cohort they are teaching, create & modify an assessment, review students assessment and scores, check a student in and out of the cohort.
* `IsStudent`: can check-in & out, take and view assessements

## Properties

The `Code` property is a string and is the primary key. The maximum length is 8 characters and the value most be unique.