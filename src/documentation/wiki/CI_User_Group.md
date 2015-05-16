#Describes the special handling of groups as configuration item.

----
##Parameter Definitions
*   **Name:** `UserIgnoreWSO4Groups`
    **Parameter:** `‑‑ignoreworkspaceobjectsforgroup [GROUP_MATCH]`, `‑‑ignorewso4group [GROUP_MATCH]`
    Defines the match of groups for which workspace objects are not handled (neither exported nor updated).
    Attention! A workspace object defined in the TCL update file are not ignored and will be created!
