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

#Describes the special handling of Relationships as configuration item.

----
##Introduction
Relationships are used to define the behavior for attributes, triggers etc. of
connections between business objects. For a deep instruction see the "MQL Guide"
or "Business Modeler Guide" of the "ENOVIA Studio Modeling Platform".

----
##Handled Properties
This relationship properties could be handled from MxUpdate:

Property                       | Written            | Default Value | Kind
-------------------------------|--------------------|---------------|----
uuid                           | if defined         | empty         | string
symbolic name                  | if defined         | empty list    | list of symbolic name strings
description                    | always             | empty string  | string
kind                           | if not ***basic*** | ***basic***   | enumeration of ***basic** and ***compositional***
abstract                       | if ***true***      | ***false***   | flag
derived                        | if set / not empty | empty string  | is derived from another relationship
hidden                         | always             | ***false***   | flag
prevent duplicate              | always             | ***false***   | flag
rule                           | if set / not empty | empty string  | one referenced rule name
triggers                       | if defined         | empty list    |
attributes                     | if defined         | empty list    | list of assigned global attributes
local attributes               | if defined  | empty list         | list of assigned local attributes
local path types               | if defined         | empty list    | list of assigned local path types
properties                     | if defined         | empty list    | list of values and referenced admin objects
from+to/meaning                | always             | empty string  | string
from+to/cardinality            | always             | ***many***    | enumeration of ***one*** and ***many***
from+to/revision action        | always             | ***none***    | enumeration of ***none***, ***float*** and ***replicate***
from+to/clone action           | always             | ***none***    | enumeration of ***none***, ***float*** and ***replicate***
from+to/propagate connection   | always             | ***true***    | flag
from+to/propagate modify       | always             | ***false***   | flag
from+to/types                  | if defined         | empty list    | list of types
from+to/relationships          | if defined         | empty list    | list of relationships

<!-- ************************************************************************ -->
###Derived Relationships
If a relationship is derived from another relationship, only limited amount of relationship properties can be changed (as currently known from MX V62015x). These properties are handled only in the parent relationship.
Therefore for a derived relationship, the following properties are not written nor handled in the delta calculation:
* from+to/meaning
* from+to/cardinality
* from+to/revision action
* from+to/clone action
* from+to/propagate connection
* from+to/propagate modify

For some properties, limited updates are allowed for the derived relationship. If some definitions are changed, the delta calculation tries to update the relationship. In the case that it failed, an exception is thrown. The properties with limited modifications are:
* from+to/types
* from+to/relationships


<!-- ************************************************************************ -->
###'Compositional' Relationships
If a relationship is new created, the relationship has typically the kind ***basic***. The kind of such relationship can by changed once to ***compositional***, but the change is irreversible. Another change to any other kind is not possible anymore.

Prerequisites for compositional relationships are:
* prevent duplicates must be true
* from cardinality must be ***one***
* from propagateconnection must be false
* to clone must be replicate
* to revision must be replicate
* to propagate connection must be false

<!-- ************************************************************************ -->
###'Dynamical' Relationships

----
##Parameter Definitions
*   **Name:** `DMRelationAttrIgnore`
    **Parameter:** `‑‑ignoreRelationshipAttributes [ATTRIBUTE_MATCH]` 
    Pattern defining the match of attributes which are ignored if not defined anymore within the delta calculation for attributes of relationships.
*   **Name:** `DMRelationAttrRemove`
    **Parameter:** `‑‑removeRelationshipAttributes [ATTRIBUTE_MATCH]` 
    Pattern defining the match of attributes which are removed if not defined anymore within the delta calculation for attributes of interfaces.
*   **Name:** `DMRelationSupportRelCons`
    **Default Value:** `true`
    Are from current MX version connections between relationships supported? This is a V6 feature and so as default set to true. If an older MX version is used which does not support connections between relationships the value must be set to false.

----
##Explanation of Update Error Codes

Error Code | Description
-----------|------------
11401      | The given global attribute is not defined anymore in the update, but already assigned to the relationship. The global attribute is not automatically removed because otherwise potentially data could be lost.
11402      | Kind of a relationship can not be changed if the current kind is not ***basic****.
11403      | Derived of a relationship can not be changed because potentially some data can be lost.
11404      | The given local attribute is not defined anymore in the update, but already assigned to the relationship. The local attribute is not automatically removed because otherwise potentially data could be lost.
11405      | The given local path type is not defined anymore in the update, but already assigned to the relationship. The local path type is not automatically removed because otherwise potentially data could be lost.

----
## Syntax
```
mxUpdate relationship "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | kind | basic         |
    |      | compositional |
    | [!]abstract
    | derived RELATIONSHIP_NAME
    | [!]hidden
    | [!]preventduplicates
    | rule RULE_NAME
    | trigger EVENT_TYPE | action   | PROGRAMNAME [input ARG_STRING]
    |                    | check    |
    |                    | override |
    | from { [SIDE_INFO] }
    | to { [SIDE_INFO] }
    | attribute ATTRIBUTENAME
    | local attribute ATTRIBUTE_NAME { [LOCAL_ATTRIBUTE] }
    | local pathtype PATH_TYPE_NAME { [LOCAL_PATH_TYPE] }
    | property NAME [to TYPE NAME] [value VALUE_STRING]
```
where **`SIDE_INFO`** is
```
    | meaning DESCRIPTION_STRING
    | cardinality | many |
    |             | one  |
    | revision | none      |
    |          | float     |
    |          | replicate |
    | clone | none      |
    |       | float     |
    |       | replicate |
    | [!]propagatemodify
    | [!]propagateconnection
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
where **`LOCAL_PATH_TYPE`** is:
```
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | from { [PATH_TYPE_FROM] }
    | to { [PATH_TYPE_TO] }
    | attribute ATTRIBUTE_NAME
    | local attribute ATTRIBUTE_NAME { [LOCAL_ATTRIBUTE] }
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
```
where **`PATH_TYPE_FROM`** is:
```
    | cardinality | many |
    |             | one  |
    | type | TYPE_NAME |
    |      | all       |
    | relationship | RELATIONSHIP_NAME |
    |              | all               |
```
where **`PATH_TYPE_TO`** is:
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
# RELATIONSHIP_MxUpdateTestRelationship.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate relationship "${NAME}" {
    symbolicname "relationship_MxUpdateTestRelationship"
    description "MxUpdate Test Relationship with two attributes and to / from types and relationships." \
    !hidden \
    !preventduplicates \
    from {
        meaning "From Type"
        cardinality many
        revision none
        clone none
        !propagatemodify
        !propagateconnection
        type "MxUpdateTestFromType1"
        type "MxUpdateTestFromType2"
    }
    to {
        meaning "To Relationship"
        cardinality many
        revision none
        clone none
        !propagatemodify \
        !propagateconnection \
        relationship "MxUpdateTestToRelationship"
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
    property "original name" value "MxUpdateTestRelationship"
    ################################################## Info End
}
```
