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

#Describes the special handling of Number Generators as configuration item.

----
##Introduction
A number generator is used to create new numbers which e.g. could be used for names of business objects.

----
## Syntax
```
mxUpdate numbergenerator "${NAME}" "${REVISION}" { [OPTION] }
```
where **`OPTION`** is:
```
    | description DESCRIPTION_STRING
    | current CURRENT_STATE
    | attribute ATTR_NAME ATTR_MULTI_LINE_VALUE
```

----
##Example
```TCL
################################################################################
# NUMBERGENERATOR_ type_MxUpdateTestType.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate numbergenerator "${NAME}" "${REVISION}" {
    description "Number Generator for MxUpdate Test Type Objects."
    current "Exists"
    # update of next attribute only if not already set
    attribute "eService Next Number" "0000001"
}
```
