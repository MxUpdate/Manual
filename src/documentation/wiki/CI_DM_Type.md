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

Property    | Written            | Default Value | Kind
------------|--------------------|---------------|----
description | always             | empty string  | string
abstract    | if ***true***      | ***false***   | flag
derived     | if set / not empty | empty string  | is derived from another type
hidden      | always             | ***false***   | flag
triggers    | if defined         | empty list    |
methods     | if defined         | empty list    | list of assigned methods
attributes  | if defined         | empty list    | list of assigned attributes
properties  | if defined         | empty list    | list of values and referenced admin objects

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
11801      | The given attribute is not defined anymore in the update, but already assigned to the type. The attribute is not automatically removed because otherwise potentially data could be lost.
11802      | Derived of a type can not be changed because potentially some data can be lost.

----
## Syntax
```
mxUpdate type "${NAME}" { [OPTION] }
```
where `OPTION` is:
```
    | description DESCRIPTION_STRING
    | [!]abstract
    | derived TYPE_NAME
    | [!]hidden
    | trigger EVENT_TYPE | action   | PROGRAM_NAME [input ARG_STRING]
    |                    | check    |
    |                    | override |
    | method PROGRAM_NAME
    | attribute ATTRIBUTE_NAME
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
```

----
##Example
```TCL
################################################################################
# TYPE:
# ~~~~~
# MxUpdateTestType
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# type_MxUpdateTestType
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# MxUpdate Test Type with two attributes.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mxUpdate type "${NAME}" {
    description "MxUpdate Test Type with two attributes."
    !hidden
    attribute "MxUpdateTestAttribute1"
    attribute "MxUpdateTestAttribute2"
}
```
