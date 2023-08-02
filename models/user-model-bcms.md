[Back to README.md](/README.md)

# User Model (class)

## Overview

The `User` model defines users that can log in and use BCMS. Every user is assigned a `Role` that defines what privileges they have. The model is also used to identify the 'owner' of some other models.

## Properties

The `Username` property must be unique for each user.

Users must login to BCMS using their `Username` and `Password`.

`RoleCode` is a foreign key to the `Role` model and defines priveleges for the user (see `Role` model)

When `Active` is false, the user is treated as if it is *logically* deleted.

`Created` and `Updated` are maintained by the system and should not be modified. They exist primarily for debugging purposes.

Most other property are for display purposes only.

