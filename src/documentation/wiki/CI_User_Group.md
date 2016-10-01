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

#Describes the special handling of groups as configuration item.

----
##Handled Properties
This group properties could be handled from MxUpdate:

Property      | Written    | Default Value | Kind
--------------|------------|---------------|----
package       | if defined | empty         | string
uuid          | if defined | empty         | string
symbolic name | if defined | empty list    | list of symbolic name strings
description   | always     | empty string  | multi-line-string
hidden        | always     | ***false***   | flag
parent        | is defined | empty list    | list of parent groups
properties    | if defined | empty list    | list of values and referenced admin objects


----
##Parameter Definitions
*   **Name:** `UserIgnoreWSO4Groups`
    **Parameter:** `‑‑ignoreworkspaceobjectsforgroup [GROUP_MATCH]`, `‑‑ignorewso4group [GROUP_MATCH]`
    Defines the match of groups for which workspace objects are not handled (neither exported nor updated).
    Attention! A workspace object defined in the TCL update file are not ignored and will be created!

----
## Syntax
```
mxUpdate group "${NAME}" { [OPTION] }
```
where `OPTION` is:
```
    | package PACKAGE_NAME
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
# GROUP_MxUpdate_Group
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate group "${NAME}" {
    symbolicname "group_MxUpdate_Group"
    description "Group for test purposes."
    !hidden
    parent "Company"
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "MxUpdate_Group"
    ################################################## Info End
}
```
