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
##Example
```TCL
################################################################################
# OBJECTGENERATOR:
# ~~~~~~~~~~~~~~~~
# type_MxUpdateTestType
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Object Generator for MxUpdate Test Type Objects to define the prefix.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mql mod bus "${OBJECTID}" \
    description "Object Generator for MxUpdate Test Type Objects to define the prefix." \
    "eService Name Prefix" "TEST-" \
    "eService Name Suffix" "" \
    "eService Processing Time Limit" "60" \
    "eService Retry Count" "5" \
    "eService Retry Delay" "60" \
    "eService Safety Policy" "policy_MxUpdateTestPolicy" \
    "eService Safety Vault" "vault_eServiceProduction"
mql connect bus  "${OBJECTID}" \
    relationship "eService Number Generator" \
    to "eService Number Generator" "type_MxUpdateTestType" ""
```
