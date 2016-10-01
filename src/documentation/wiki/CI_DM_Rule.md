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

#Describes the special handling of Rules as configuration item.

----
## Introduction
Rules are used to restrict access for attributes, relationships etc. For a deep
instruction see the "MQL Guide" or "Business Modeler Guide" of the "ENOVIA
Studio Modeling Platform".

----
##Handled Properties

This rule properties could be handled from !MxUpdate:
 * description
 * hidden flag
 * owner access
 * owner revoke
 * public access
 * public revoke
 * user access
 * properties
The governed objects are not handled in the rule configuration item file. They must be defined in the related [attribute](CI_DM_Attribute.md), [form](CI_UI_Form.md), [program](CI_Program.md) or [relationship](CI_DM_Relationship.md) configuration item file.

----
##Steps of the Update Flow

###Cleanup
Following steps are done before the TCL update file is executed:
 * set to not hidden
 * no owner and public access
 * no public or owner revoke definition (only if not defined or if not ```none```)
 * remove all users
 * remove all assigned properties

###Update
Within the update the owner / public is defined and further user access added.
The governed objects are not changed or modified.

----
##Parameter Definitions
No further parameters are defined.

----
##Example
```TCL
################################################################################
# RULE:
# ~~~~~
# TestRule
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# rule_TestRule
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Rule for test purposes.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mql escape mod rule "${NAME}" \
    description "Rule for test purposes." \
    !hidden \
    add owner "modify,read,show" \
    add revoke owner "modify" filter "type==Part" \
    add public "none" \
    add user "Employee" "show" filter ""
```