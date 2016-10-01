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

#Describes the special handling of Types as configuration item.

----
##Introduction
Types are used to define the behavior for attributes, triggers etc. of business
objects. For a deep instruction see the "MQL Guide" or "Business Modeler Guide"
of the "ENOVIA Studio Modeling Platform".

----
##Handled Properties
This type properties could be handled from MxUpdate:

Property         | Written            | Default Value | Kind
-----------------|--------------------|---------------|----
symbolic name    | if defined         | empty list    | list of symbolic name strings
description      | always             | empty string  | string
kind             | if not ***basic*** | ***basic***   | enumeration of ***basic** and ***composed***
abstract         | if ***true***      | ***false***   | flag
derived          | if set / not empty | empty string  | is derived from another type
hidden           | always             | ***false***   | flag
triggers         | if defined         | empty list    |
methods          | if defined         | empty list    | list of assigned methods
attributes       | if defined         | empty list    | list of assigned global attributes
local attributes | if defined         | empty list    | list of assigned local attributes
local path types | if defined         | empty list    | list of assigned local path types
properties       | if defined         | empty list    | list of values and referenced admin objects

----
##Parameter Definitions
*   **Name:** ```DMTypeAttrIgnore```
    **Parameter:** ```‑‑ignoreTypeAttributes [ATTRIBUTE_MATCH]```
    Pattern defining the match of attributes which are ignored if not defined anymore within the delta calculation for attributes of types.
*   **Name:** ```DMTypeAttrRemove```
    **Parameter:** ```‑‑removeTypeAttributes [ATTRIBUTE_MATCH]```
    Pattern defining the match of attributes which are removed if not defined anymore within the delta calculation for attributes of types.
    
----
##Explanation of Update Error Codes

Error Code | Description
-----------|------------
11801      | The given global attribute is not defined anymore in the update, but already assigned to the type. The global attribute is not automatically removed because otherwise potentially data could be lost.
11802      | Kind of a type can not be changed if the current kind is not ***basic***.
11803      | Derived of a type can not be changed because potentially some data can be lost.
11804      | The given local attribute is not defined anymore in the update, but already assigned to the type. The local attribute is not automatically removed because otherwise potentially data could be lost.
11805      | The given local path type is not defined anymore in the update, but already assigned to the type. The local path type is not automatically removed because otherwise potentially data could be lost.

----
## Syntax
```
mxUpdate type "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | kind | basic    |
    |      | composed |
    | [!]abstract
    | derived TYPE_NAME
    | [!]hidden
    | trigger EVENT_TYPE | action   | PROGRAM_NAME [input ARG_STRING]
    |                    | check    |
    |                    | override |
    | method PROGRAM_NAME
    | attribute ATTRIBUTE_NAME
    | local attribute ATTRIBUTE_NAME { [LOCAL_ATTRIBUTE] }
    | local pathtype PATH_TYPE_NAME { [LOCAL_PATH_TYPE] }
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
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
where **`LOCAL_PATH_TYPE`** is:
```
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | from { [FROM] }
    | to { [TO] }
    | attribute ATTRIBUTE_NAME
    | local attribute ATTRIBUTE_NAME { [LOCAL_ATTRIBUTE] }
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
```
where **`FROM`** is:
```
    | cardinality | many |
    |             | one  |
    | type | TYPE_NAME |
    |      | all       |
    | relationship | RELATIONSHIP_NAME |
    |              | all               |
```
where **`TO`** is:
```
    | type | TYPE_NAME |
    |      | all       |
    | relationship | RELATIONSHIP_NAME |
    |              | all               |
```

----
##Example
```tcl
################################################################################
# TYPE_MxUpdateTestType.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate type "${NAME}" {
    symbolicname "type_MxUpdateTestType"
    description "MxUpdate Test Type with two attributes."
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
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "MxUpdateTestType"
    ################################################## Info End
}
```
