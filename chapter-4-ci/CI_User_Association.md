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

#Describes the special handling of associations as configuration item.

----
##Introduction
Associations are a list of persons which could be defined as expression.

----
##Handled Properties
This group properties could be handled from MxUpdate:

Property      | Written    | Default Value | Kind
--------------|------------|---------------|----
package       | if defined | empty         | string
uuid          | if defined | empty         | string
symbolic name | if defined | empty list    | list of symbolic name strings
description   | always     | empty string  | string
hidden        | always     | ***false***   | flag
definition    | always     | empty string  | string of user expression
properties    | if defined | empty list    | list of values and referenced admin objects

----
## Syntax
```
mxUpdate association "${NAME}" { [OPTION] }
```
where `OPTION` is:
```
    | package PACKAGE_NAME
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | definition DEFINITION_STRING
    | property NAME [to TYPE NAME] [value VALUE_STRING]
```

----
##Example
```tcl
################################################################################
# ASSOCIATION_MxUpdate_PublicCheckin.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate association "${NAME}" {
    symbolicname "association_MxUpdate_PublicCheckin"
    description "Used to give rights in a state expression testing if user has check in rights (like OOTB public read)."
    !hidden
    definition "\"!User Agent\""
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "MxUpdate_PublicCheckin"
    ################################################## Info End
}
```
