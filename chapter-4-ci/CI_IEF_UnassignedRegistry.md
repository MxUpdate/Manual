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

#Describes the special handling of IEF Unassigned Registry Objects as configuration item.

----
##Introduction

The Unassigned Registry Objects are used from the IEF integrations.

----
## Syntax
```
mxUpdate unassignedregistry "${NAME}" "${REVISION}" { [OPTION] }
```
where **`OPTION`** is:
```
    | description DESCRIPTION_STRING
    | current CURRENT_STATE
    | attribute ATTR_NAME ATTR_MULTI_LINE_VALUE
```

----
##Example (Snippet)
```TCL
################################################################################
# IEFUNASSIGNEDREGISTRY_IEF-UnassignedIntegRegistry________________MxUpdateTest________-.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate unassignedregistry "${NAME}" "${REVISION}" {
    type "IEF-UnassignedIntegRegistry"
    description "MxUpdate Test IEF unassigned registry."
    current "Exists"
    attribute "DSCAllowedFeatures" "WhereUsed,Lifecycle"
    attribute "IEF-IntegrationToGCOMapping" ""
}
```
