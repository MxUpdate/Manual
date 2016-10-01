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

#Describes the special handling of IEF Mass Promote Configuration Objects as configuration item.

----
##Introduction

The Mass Promote Configuration Objects are used from the IEF integrations.

----
##Example (Snippet)
```TCL
################################################################################
# IEFMASSPROMOTECONFIG:
# ~~~~~~~~~~~~~~~~~~~~~
# IEF-MassPromoteConfig________________MxUpdateTest________-
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# -
# MxUpdate Test IEF mass promote configuration.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mql escape mod bus "${OBJECTID}" \
    description "MxUpdate Test IEF mass promote configuration." \
    "IEF-MassPromoteValidationRuleJPO" "" \
    "IEF-ValidateObjectPromotion" "TRUE" \
    "IEF-ValidateObjectSelection" "TRUE"
```