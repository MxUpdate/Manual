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
Property      | Written       | Default Value | Kind
--------------|---------------|---------------|-----------------------
description   | always        | empty string  | string
hidden flag   | always        | ***false***   | flag
abstract flag | if ***true*** | ***false***   | flag
derived       | if defined    | empty list    | list of derived interfaces
types         | if defined    | empty list    | defined for types
relationships | if defined    | empty list    | defined for relationships

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
10901      | The given attribute is not defined anymore in the update, but already assigned to the interface. The attribute is not automatically removed because otherwise potentially data could be lost.
10902      | An interface is already derived from another interface, but within the update this derived interface must be removed. This could end in potentially losing data and so this action is not allowed.

----
## Syntax
```
mxUpdate interface "${NAME}" { [OPTION] }
```
where `OPTION` is:
```
    | description DESCRIPTION_STRING
    | [!]abstract
    | derived INTERFACE_NAME
    | [!]hidden
    | attribute ATTRIBUTENAME
    | for relationship | RELATIONSHIP_NAME |
    |                  | all               |
    | for type | TYPE_NAME |
    |          | all       |
    | property NAME [to TYPE NAME] [value VALUE_STRING]
```

----
##Example
```tcl
################################################################################
# INTERFACE:
# ~~~~~~~~~~
# MxUpdateTestInterface
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# interface_MxUpdateTestInterface
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# MxUpdate Test Interface with two attributes, assignable to one type and two
# relationships and one parent interface.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mxUpdate interface "${NAME}" {
    description "MxUpdate Test Interface with two attributes, assignable to one type and two relationships and one parent interface."
    derived "MxUpdateTestParentInterface"
    !hidden
    attribute "MxUpdateTestAttribute1"
    attribute "MxUpdateTestAttribute2"
    for relationship "MxUpdateTestRelationship1"
    for relationship "MxUpdateTestRelationship2"
    for type "MxUpdateTestType"
}
```