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

Property              | Written    | Default Value | Kind
----------------------|------------|---------------|----
symbolic name         | if defined | empty list    | list of symbolic name strings
description           | always     | empty string  | string
hidden                | always     | ***false***   | flag
from/cardinality      | always     | ***many***    | enumeration of ***one*** and ***many***
from+to/types         | if defined | empty list    | list of types
from+to/relationships | if defined | empty list    | list of relationships
attributes            | if defined | empty list    | list of assigned global attributes
local attributes      | if defined | empty list    | list of assigned local attributes
properties            | if defined | empty list    | list of values and referenced admin objects

----
##Parameter Definitions
*   **Name:** ```DMPathTypeAttrIgnore```
    **Parameter:** ```‑‑ignorePathTypeAttributes [ATTRIBUTE_MATCH]```
    Pattern defining the match of attributes which are ignored if not defined anymore within the delta calculation for attributes of path types.
*   **Name:** ```DMPathTypeAttrRemove```
    **Parameter:** ```‑‑removePathTypeAttributes [ATTRIBUTE_MATCH]```
    Pattern defining the match of attributes which are removed if not defined anymore within the delta calculation for attributes of path types.
    
----
##Explanation of Update Error Codes

Error Code | Description
-----------|------------
12301      | The given global attribute is not defined anymore in the update, but already assigned to the type. The global attribute is not automatically removed because otherwise potentially data could be lost.
12302      | The given local attribute is not defined anymore in the update, but already assigned to the type. The local attribute is not automatically removed because otherwise potentially data could be lost.

----
## Syntax
```
mxUpdate pathtype "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
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
# TYPE_MxUpdateTestPathType.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate pathtype "${NAME}" {
    symbolicname "type_MxUpdateTestPathType"
    description "MxUpdate Test Path Type with two attributes."
    !hidden
    from {
        cardinality one
        relationship "MxUpdate Relationship"
    }
    to {
        type all
    }
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
    property "original name" value "MxUpdateTestPathType"
    ################################################## Info End
}
```
