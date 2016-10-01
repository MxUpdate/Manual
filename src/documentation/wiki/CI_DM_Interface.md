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

#Describes the special handling of Interfaces as configuration item.

----
##Introduction
Interfaces are used to handle multiple classification of business objects and connections. For a deep instruction see the "MQL Guide" or "Business Modeler Guide" of the "ENOVIA Studio Modeling Platform".

----
##Handled Properties
Property         | Written       | Default Value | Kind
-----------------|---------------|---------------|-----------------------
uuid             | if defined    | empty         | string
symbolic name    | if defined    | empty list    | list of symbolic name strings
description      | always        | empty string  | string
hidden flag      | always        | ***false***   | flag
abstract flag    | if ***true*** | ***false***   | flag
derived          | if defined    | empty list    | list of derived interfaces
interfaces       | if defined    | empty list    | defined for interfaces
types            | if defined    | empty list    | defined for types
relationships    | if defined    | empty list    | defined for relationships
attributes       | if defined    | empty list    | list of assigned global attributes
local attributes | if defined    | empty list    | list of assigned local attributes
properties       | if defined    | empty list    | list of values and referenced admin objects

----
##Parameter Definitions
*   **Name:** `DMInterfaceAttrIgnore`
    **Parameter:** `‑‑ignoreInterfaceAttributes [ATTRIBUTE_MATCH]`
    Pattern defining the match of attributes which are ignored if not defined anymore within the delta calculation for attributes of interfaces.
*   **Name:** `DMInterfaceAttrRemove`
    **Parameter:** `‑‑removeInterfaceAttributes [ATTRIBUTE_MATCH]`
    Pattern defining the match of attributes which are removed if not defined anymore within the delta calculation for attributes of interfaces.
*   **Name:** `DMInterfaceParentIgnore`
    **Parameter:** `‑‑ignoreInterfacParents [INTERFACE_MATCH]`
    Pattern defining the match of interfaces which are ignored within the delta calculation of parent interfaces for interfaces.
*   **Name:** `DMInterfaceParentRemove`
    **Parameter:** `‑‑removeInterfaceParents [ATTRIBUTE_MATCH]`
    Pattern defining the match of interfaces which are removed within the delta calculation of parent interfaces for interfaces.

----
##Explanation of Update Error Codes

Error Code | Description
-----------|------------
10901      | The given global attribute is not defined anymore in the update, but already assigned to the interface. The global attribute is not automatically removed because otherwise potentially data could be lost.
10902      | An interface is already derived from another interface, but within the update this derived interface must be removed. This could end in potentially losing data and so this action is not allowed.
10903      | The given local attribute is not defined anymore in the update, but already assigned to the interface. The local attribute is not automatically removed because otherwise potentially data could be lost.

----
## Syntax
```
mxUpdate interface "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]abstract
    | derived INTERFACE_NAME
    | [!]hidden
    | attribute ATTRIBUTENAME
    | local attribute ATTRIBUTE_NAME { [LOCAL_ATTRIBUTE] }
    | for interface    | INTERFACE_NAME |
    |                  | all            |
    | for relationship | RELATIONSHIP_NAME |
    |                  | all               |
    | for type         | TYPE_NAME |
    |                  | all       |
    | property NAME [to TYPE NAME] [value VALUE_STRING]
```
where **`LOCAL_ATTRIBUTE`** is:
```
    | kind | binary  |
    |      | boolean |
    |      | date    |
    |      | integer |
    |      | real    |
    |      | string  |
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | [!]multivalue
    | [!]rangevalue
    | [!]resetonclone
    | [!]resetonrevision
    | [!]multiline
    | maxlength MAXLENGTH
    | dimension DIMENSION_NAME
    | default DEFAULT_STRING
    | range RANGE_ITEM
    | trigger EVENT_TYPE | action   | PROGRAMNAME [input ARG_STRING]
    |                    | check    |
    |                    | override |
    | property NAME [to ADMIN_TYPE NAME] [value VALUE_STRING]
```
where **`RANGE_ITEM`** is:
```
    | =  | VALUE
    | != |
    | <  |
    | >  |
    | <= |
    | >= | 
    | between VALUE | inclusive | VALUE | inclusive |
    |               | exclusive |       | exclusive |
    | program PROGRAM_NAME [input ARG_STRING]
```

----
##Example
```tcl
################################################################################
# INTERFACE_MxUpdateTestInterface.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate interface "${NAME}" {
    symbolicname "interface_MxUpdateTestInterface"
    description "MxUpdate Test Interface with two attributes, assignable to one type and two relationships and one parent interface."
    derived "MxUpdateTestParentInterface"
    !hidden
    attribute "MxUpdateTestAttribute1"
    attribute "MxUpdateTestAttribute2"
    local attribute "MxUpdate Local Attribute"  {
        kind string
        symbolicname "attribute_MxUpdate_Local_Attribute"
        description "A local MxUpdate Test Attribute"
        !multivalue
        !resetonclone
        !resetonrevision
        !multiline
        maxlength 0
        ################################################## Info Start
        property "original name" value "MxUpdate Local Attribute"
        ################################################## Info End
    }
    for relationship "MxUpdateTestRelationship1"
    for relationship "MxUpdateTestRelationship2"
    for type "MxUpdateTestType"
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "MxUpdateTestInterface"
    ################################################## Info End
}
```