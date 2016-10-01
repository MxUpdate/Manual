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

#Describes the special handling of Attributes as configuration item.

----
## Introduction
Attributes are used to handle values for business objects and connections. They
are assigned to [types](CI_DM_Type.md), [relationships](CI_DM_Relationship.md) and [interfaces](CI_DM_Interface.md).

----
## Handled Properties
This format properties could be handled from MxUpdate:
 * description
 * hidden flag
 * rules
 * default value
 * dimension (only for real and integer attributes)
 * flag to define that the attribute has multiple values
 * maximum length (only for string attributes)
 * multiline flag (only for string attributes)
 * flag to define that the value is reseted on clone of business object
 * flag to define that the value is reseted on revision of business object
 * flag to define that the value contains range values (only for real, integer and date attributes)
 * triggers
 * ranges
 * properties

----
## Steps of the Update Flow

### Update
The attribute CI file is defined with the so called *update format*. So an update of an attribute is done by calculating the delta between the target and the current existing definition.
This calculating delta means also that the history of an attribute contains only the changes between the different milestone of an attribute definition.

### Special Handling of *Loosing Data* Properties
Some properties / flags can not be changed in some cases without loosing data information. In this cases the changes must be done manually from pre-update migration scripts.
The idea behind is that e.g. a development system does not contain the complete productive data. So the exception will be also thrown in the development (and not the first time when an update of a productive system is tried).

#### *Multi Value* flag
All attributes can be defined as multi-value attribute. To define an attribute as multi-value attribute can be done without any lost data. In the case that the multi-value flag is reset to non-multi-value with potentially losing of data, the change is rejected.

#### *Range Value* flag
Integer, real or date attributes can be defined to contain range values (e.g. 20% range). The definition of an attribute with range values can be done without loosing data. Otherwise removing range values can mean that data is lost. So this change is rejected.

### *Dimension* property
A Dimension can be defined for real and integer attributes. With change of the dimension existing data can be lost. So only a new definition of the Dimension is allowed and a change of a Dimension is rejected. For more information how to update a new dimension including automatically conversion see the Enovia MQL manual.

----
## Format
The *update format* is used to define all attribute properties and flags. The *update format* is similar to the syntax to create new attributes. Only the type of the attribute (integer, real, string, date, boolean) is not define in the file itself, because the name of the attribute file contains itself the attribute type.

### File Names
The file name of an attribute CI file contains prefixed attribute type, the escaped attribute name and as extension ".tcl".

File Name Prefix | Attribute Type
-----------------|----------------------
```BOOLEAN_```   | Boolean attributes
```DATE_```      | Date/Time attributes
```INTEGER_```   | Integer attributes
```REAL_```      | Real attributes
```STRING_```    | String attributes


----
## Parameter Definitions
*   **Name:** ```DMAttrSupportsDimension```
    **Value:** ```true``` if the MX version supports real or integer attributes with dimensions (tested by calling MQL command "```help attribute```" and testing the result for "```dimension```").
    If the flag is set to true attributes supports dimensions.
*   **Name:** ```DMAttrSupportsFlagMultiValue```
    **Value:** ```true``` if the MX version supports attributes with multiple values (tested by calling MQL command "```help attribute```" and testing the result for "```multivalue```").
    If the flag is set to true attributes supports the "multiple value" flag.
*   **Name:** ```DMAttrSupportsFlagRangeValue```
    **Value:** ```true``` if the MX version supports real, integer or date time attributes with range value flag (tested by calling MQL command "```help attribute```" and testing the result for "```rangevalue```").
    If the flag is set to true attributes supports the "rangevalue" flag.
*   **Name:** ```DMAttrSupportsFlagResetOnClone```
    **Value:** ```true``` if the MQL command "```help attribute```" includes the string "```resetonclone```".
    If the flag is set to true attributes supports the "resetonclone" flag.
*   **Name:** ```DMAttrSupportsFlagResetOnRevision```
    **Value:** ```true``` if the MQL command "```help attribute```" includes the string "```resetonrevision```".
    If the flag is set to true attributes supports the "resetonrevision" flag.
*   **Name:** ```DMAttrSupportsPropMaxLength```
    **Value:** ```true``` if the MQL command "```help attribute```" includes the string "```maxlength```".
    If the flag is set to true string attributes supports the "maxlength" property.


----

## Explanation of Update Error Codes

Error Code | Description
-----------|------------
12001      | The given dimension of the attribute should be changed to new dimension, but potentially data could be lost.
12002      | The attribute contains defined range value flag which must be removed, but potentially data could be lost.
12003      | The attribute contains defined multiple value flag which must be removed, but potentially data could be lost.

----

## Syntax
```
mxUpdate attribute NAME {
    description DESCRIPTION_STRING
    [!]hidden
    [!]multivalue
    [!]rangevalue
    [!]multiline
    [!]resetonclone
    [!]resetonrevision
    maxlength MAXLENGTH
    dimension DIMENSION_NAME
    default DEFAULT_STRING
    range RANGE_ITEM
    trigger EVENT_TYPE | action   | PROGRAMNAME [input ARG_STRING]
                       | check    |
                       | override |
    property NAME [to TYPE NAME] [value VALUE_STRING]
}
```
where **RANGE_ITEM** is:
```
    | =  | VALUE
    | != |
    | <  |
    | >  |
    | <= |
    | >= | 
    between VALUE | inclusive | VALUE | inclusive |
                  | exclusive |       | exclusive |
    program PROGRAM_NAME [input ARG_STRING]
```

----

## Example
```tcl
################################################################################
# ATTRIBUTE:
# ~~~~~~~~~~
# MxUpdateTestAttribute
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# attribute_MxUpdateTestAttribute
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# MxUpdate Test String Attribute.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mxUpdate attribute "${NAME}" {
    description "MxUpdate Test String Attribute."
    !hidden
    !multivalue
    !resetonclone
    !resetonrevision
    multiline
    maxlength "100"
    default ""
}
```
