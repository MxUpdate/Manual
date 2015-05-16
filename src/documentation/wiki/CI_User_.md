#Describes the special handling of all Users as configuration item.

----
##Introduction
Currently following user objects are supported from MxUpdate:
* [association](CI_User_Association.md)
* [group](CI_User_Group.md)
* [role](CI_User_Role.md)
* [person](CI_User_Person.md) (with related business object)
* [administration person](CI_User_PersonAdmin.md) (without related business object)

Generally for all user also the workspace objects are always handled (exported and updated).

----
##Parameter Definitions
*   **Name:** `UserIgnoreWSO4Users`
    **Parameters:** `‑‑ignoreworkspaceobjectsforuser [USER_MATCH]`, `‑‑ignorewso4user [USER_MATCH]`
    Defines the match of users for which users workspace objects are not handled (wether exported nor updated). Attention! A workspace object defined in the TCL update file are not ignored and will be created!
