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

#Describes the special handling of Triggers as configuration item.

----
##Introduction
Trigger objects are used from the "emxTriggerManager" to define called JPOs with defined arguments.

----
## Syntax
```
mxUpdate trigger "${NAME}" "${REVISION}" { [OPTION] }
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
# TRIGGER_TypeMxUpdateTestTypeCreateAction________TestTrigger.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate trigger "${NAME}" "${REVISION}" {
    description "Test Trigger to call JPO 'MxUpdateTestProgram' with action create."
    current "Active"
    attribute "eService Constructor Arguments" ""
    attribute "eService Error Type" "Error"
    attribute "eService Method Name" "mxMain"
    attribute "eService Program Argument 1" "${OBJECTID}"
    attribute "eService Program Argument 2" ""
    attribute "eService Program Argument 3" ""
    attribute "eService Program Argument 4" ""
    attribute "eService Program Argument 5" ""
    attribute "eService Program Argument 6" ""
    attribute "eService Program Argument 7" ""
    attribute "eService Program Argument 8" ""
    attribute "eService Program Argument 9" ""
    attribute "eService Program Argument 10" ""
    attribute "eService Program Argument 11" ""
    attribute "eService Program Argument 12" ""
    attribute "eService Program Argument 13" ""
    attribute "eService Program Argument 14" ""
    attribute "eService Program Argument 15" ""
    attribute "eService Program Argument Desc 1" "id of the MxUpdate Test Type object"
    attribute "eService Program Argument Desc 2" ""
    attribute "eService Program Argument Desc 3" ""
    attribute "eService Program Argument Desc 4" ""
    attribute "eService Program Argument Desc 5" ""
    attribute "eService Program Argument Desc 6" ""
    attribute "eService Program Argument Desc 7" ""
    attribute "eService Program Argument Desc 8" ""
    attribute "eService Program Argument Desc 9" ""
    attribute "eService Program Argument Desc 10" ""
    attribute "eService Program Argument Desc 11" ""
    attribute "eService Program Argument Desc 12" ""
    attribute "eService Program Argument Desc 13" ""
    attribute "eService Program Argument Desc 14" ""
    attribute "eService Program Argument Desc 15" ""
    attribute "eService Program Name" "MxUpdateTestProgram"
    attribute "eService Sequence Number" "1"
    attribute "eService Target States" ""
}
```
