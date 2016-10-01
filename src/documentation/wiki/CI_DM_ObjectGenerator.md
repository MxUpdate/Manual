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

#Describes the special handling of Object Generators as configuration item.

----
##Introduction
An object generator is used to create new business object instances depending on a number generator.

----
## Syntax
```
mxUpdate objectgenerator "${NAME}" "${REVISION}" { [OPTION] }
```
where **`OPTION`** is:
```
    | description DESCRIPTION_STRING
    | current CURRENT_STATE
    | attribute ATTR_NAME ATTR_MULTI_LINE_VALUE
    | connection "eService Number Generator" to "eService Number Generator" NUMBER_NAME NUMBER_REVISION
```

----
##Example
```TCL
################################################################################
# OBJECTGENERATOR_ type_MxUpdateTestType.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate objectgenerator "${NAME}" "${REVISION}" {
    description "Object Generator for MxUpdate Test Type Objects to define the prefix."
    current "Exists"
    attribute "eService Name Prefix" "TEST-"
    attribute "eService Name Suffix" ""
    attribute "eService Processing Time Limit" "60"
    attribute "eService Retry Count" "5"
    attribute "eService Retry Delay" "60"
    attribute "eService Safety Policy" "policy_MxUpdateTestPolicy"
    attribute "eService Safety Vault" "vault_eServiceProduction"
    connection "eService Number Generator" to "eService Number Generator" "type_MxUpdateTestType" ""
}
```
