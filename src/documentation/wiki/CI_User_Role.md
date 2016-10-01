<!--
 *
 *  This file is part of MxUpdate <http://www.mxupdate.org>.
 *
 *  MxUpdate is a deployment tool for a PLM platform to handle
 *  administration objects as single update files (configuration item).
 *
 *  Copyright (C) 2008-2016 The MxUpdate Team
 *
 *  The Manual of MxUpdate is licensed under a CC BY-NC-SA 4.0 license
 *  (Creative Commons Attribution-NonCommercial-ShareAlike 4.0 
 *  International 4.0 license).
 *
 *  You should have received a copy of the license along with this
 *  work. If not, see <http://creativecommons.org/licenses/by-nc-sa/4.0/>.
 *
-->

#Describes the special handling of roles as configuration item.

----
##Introduction
Roles are used to define for persons specific access depending on there role. The three different kind of roles for standard roles, organizational roles and project roles exists. For a deep instruction see the "MQL Guide" or "Business Modeler Guide" of the "ENOVIA Studio Modeling Platform".

----
##Handled Properties
This role properties could be handled from MxUpdate:

Property      | Written           | Default Value | Kind
--------------|-------------------|---------------|----
package       | if defined        | empty         | string
uuid          | if defined        | empty         | string
symbolic name | if defined        | empty list    | list of symbolic name strings
description   | always            | empty string  | multi-line-string
kind          | if not ***role*** | ***role***    | enumeration of ***organization***, ***project*** and ***role***
hidden        | always            | ***false***   | flag
parent        | is defined        | empty list    | list of parent role
properties    | if defined        | empty list    | list of values and referenced admin objects

----
##Special Handling of Role Types
This three different kind of roles exists:
* standard roles
* organizational roles
* project roles

If the kind of the role is changed it could not be reseted if some child roles are assigned to this role.
----
##Parameter Definitions
*   **Name:** `UserIgnoreWSO4Roles`
    **Parameter:** `‑‑ignoreworkspaceobjectsforrole [ROLE_MATCH]`, `‑‑ignorewso4role [ROLE_MATCH]`
    Defines the match of roles for which workspace objects are not handled (neither exported nor updated).
    Attention! A workspace object defined in the TCL update file are not ignored and will be created!
*   **Name:** `UserRoleSupportRoleType`
    **Default Value:** `true`
    Are from current MX version role types supported? This is a V6 feature and so as default set to true. If an older MX version is used which does not support role types the value must be set to `false`.

----
##Explanation of Update Error Codes

Error Code | Description
-----------|------------
31201      | Kind of a role can not be changed if the current kind is not ***role***.

----
## Syntax
```
mxUpdate role "${NAME}" { [OPTION] }
```
where `OPTION` is:
```
    | package PACKAGE_NAME
    | kind | organization |
    |      | project      |
    |      | role         |
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | side SIDE_NAME
    | parent GROUP_NAME
    | property NAME [to TYPE NAME] [value VALUE_STRING]
```

----
##Example
```tcl
################################################################################
# ROLE_MxUpdate_Role
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate mod role "${NAME}" {
    kind role 
    symbolicname "role_MxUpdate_Role"
    description "Role for test purposes."
    !hidden
    parent "Employee"
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "MxUpdate_Role"
    ################################################## Info End
}
```
