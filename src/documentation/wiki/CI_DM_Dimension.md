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

#Describes the special handling of Dimensions as configuration item.

----
##Introduction
The MxUpdate update steps for configuration items is typically done by removing all values and add them again. For dimensions this is not possible, because otherwise there is potentially some data lost. So for dimensions a "special" format is defined.

----
## Handled Properties
This dimension properties could be handled from MxUpdate:

Property           | Written                              | Default Value | Kind
-------------------|--------------------------------------|---------------|----
package            | if defined                           | empty         | string
uuid               | if defined                           | empty         | string
symbolic name      | if defined                           | empty list    | list of symbolic name strings
description        | always                               | empty string  | multi-line-string
hidden             | always                               | ***false***   | flag
unit / default     | if ***true***                        | ***false***   | flag
unit / description | always                               | empty string  | string
unit / label       | always                               | empty string  | string
unit / multiplier  | always                               | ***0.0***     | real number
unit / offset      | always                               | ***0.0***     | real number
properties         | if defined                           | empty list    | list of values and referenced admin objects


----
##Updates where Data could be lost

###Update of the Default Unit
Theoretically an unit could be defined as default if the dimension was not used (from business objects). Otherwise this means the default unit could not be changed if already set. A MQL system error will be thrown in this case. Instead a manual conversion must be done.
Because it could be that in a development system no data exists which references a dimension where the default unit must be changed, an exception will be thrown for this case.
The behavior could be overwritten by defining the parameters `‑‑dimensionAllowUpdateDefaultUnit`.

###Update of Multiplier or Offset for an Unit
As default the MxUpdate Update does not allow to update the multiplier or offset of units. If the MxUpdate Update found out that this must be done, an exception is thrown and the update itself is stopped.
This MxUpdate Update makes this, because if a multiplier or offset is changed, the original value from the user input will be changed, because the calculated value depending on the default unit will be same.
The behavior could be overwritten by defining the parameters `‑‑dimensionAllowUpdateUnitMultiplier` or `‑‑dimensionAllowUpdateUnitOffset`.

###Remove of an Unit
If the MxUpdate Update found out that an unit must be removed, an exception is thrown. Otherwise if the MxUpdate Update does not check this, MX itself could potentially throw an exception. Because the unit of a dimension is removed only if the unit itself was not referenced (used) within a business object instance. Otherwise the update failed with a MQL system error. So in this case a manual conversion must be done.
The idea behind is that e.g. a development system does not contain the complete productive data. So the exception will be also thrown in the development (and not the first time when an update of a productive system is tried).
The behavior could be overwritten by defining the parameters `‑‑dimensionAllowRemoveUnit`.

----
##Parameter Definitions
*   **Name:** `DMDimAllowRemoveUnit`
    **Parameter:** `‑‑dimensionAllowRemoveUnit`
    **Default Value:** `false`
    If the parameter is defined, the MxUpdate Update removes undefined units. Otherwise an exception is thrown if an unit must be removed.
*   **Name:** `DMDimAllowUpdateDefUnit`
    **Parameter:** `‑‑dimensionAllowUpdateDefaultUnit`
    **Default Value:** `false`
    If the parameter is defined, the MxUdpate Update allows to change the default unit of a dimension. Otherwise an exception is thrown if the default unit must be changed.
*   **Name:** `DMDimAllowUpdateUnitMult`
    **Parameter:** `‑‑dimensionAllowUpdateUnitMultiplier`
    **Default Value:** `false`
    If the parameter is defined, the MxUpdate Update allows to change the multiplier of units. Otherwise an exception is thrown if the multiplier must be changed.
*   **Name:** `DMDimAllowUpdateUnitOffs`
    **Parameter:** `‑‑dimensionAllowUpdateUnitOffset`
    **Default Value:** `false`
    If the parameter is defined, the MxUpdate Update allows to change the offset of units. Otherwise an exception is thrown if the offset must be changed.

----
##Explanation of Update Error Codes
Error Code | Description
-----------|------------
10601      | The multiplier of a unit of a dimension is tried to update which means that potentially some data could be loosed.
10602      | The offset of a unit of a dimension is tried to update which means that potentially some data could be loosed.
10603      | The default unit of a dimension is tried to update which means that potentially some data could be loosed. FYI: MX itself also tries to prevent this if a default unit is already defined, but it could be that this case does only happens e.g. in non development systems....
10604      | An unit of a dimension is tried to remove which means that potentially some data could be loosed. FYI: MX itself also tries to prevent this if a unit is used, but it could be that this case does only happens e.g. in non development systems....

----
## Syntax
```
mxUpdate dimension "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | package PACKAGE_NAME
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | unit UNIT_NAME { UNIT_OPTION }
```
where **`UNIT_OPTION`** is:
```
    | [!]default
    | description UNIT_DESCRIPTION
    | label UNIT_LABEL
    | multiplier MULTIPLIER
    | offset OFFSET
```

----
##Example
```TCL
################################################################################
# DIMENSION_MxUpdateTestDimension.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate dimension "${NAME}" {
    symbolicname "dimension_MxUpdateTestDimension"
    description "MxUpdate Test Dimension."
    !hidden
    unit "Kilo-Volt" {
        description ""
        label "kV"
        multiplier 1000.0
        offset 0.0
    }
    unit "Volt" {
        default
        description ""
        label "V"
        multiplier 1.0
        offset 0.0
    }
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "MxUpdateTestDimension"
    ################################################## Info End
}
```
