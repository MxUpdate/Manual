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

#Describes the special handling of Trigger Groups as configuration item.

----
##Introduction
Trigger Groups could be used to group trigger parameter definitions. So they are
used as documentation.

----
##Parameter Definitions
*   **Name:** `InstallTriggerGroupPolicyDesc`
    **Default Value:** Policy used for the group trigger definitions.
    Defines the description which is used for the policy of trigger groups.
*   **Name:** `InstallTriggerGroupRelationDesc`
    **Default Value:** Relationship used for the group trigger definitions.
    Defines the description which is used for the relationship of trigger groups.
*   **Name:** `InstallTriggerGroupTypeDesc`
    **Default Value:** Type used for the group trigger definitions.
    Defines the description which is used for the type of trigger groups.

----
##Example
```TCL
################################################################################
# TRIGGERGROUP:
# ~~~~~~~~~~~~~
# MxUpdateTestTypeCreateAction________Type
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Type
# Trigger Group for all triggers on type 'MxUpdateTestTypeCreateAction'.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mql mod bus "${OBJECTID}" \
    description "Trigger Group for all triggers on type 'MxUpdateTestTypeCreateAction'."
mql connect bus "${OBJECTID}" \
    relationship "MxUpdate Trigger Group Relationship" \
    to "eService Trigger Program Parameters" "TypeMxUpdateTestTypeCreateAction" "TestTrigger"
```
