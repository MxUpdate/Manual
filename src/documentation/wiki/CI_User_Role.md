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

#Describes the special handling of roles as configuration item.

----
##Introduction
Roles are used to define for persons specific access depending on there role. The three different kind of roles for standard roles, organizational roles and project roles exists. For a deep instruction see the "MQL Guide" or "Business Modeler Guide" of the "ENOVIA Studio Modeling Platform".

----
##Special Handling of Role Types
This three different kind of roles exists:
* standard roles
* organizational roles
* project roles

If the kind of the role is changed it could not be reseted if some child roles are assigned to this role. So the kind of the roles be always defined with correct MQL keywords.

----
##Handled Properties
This type properties could be handled from MxUpdate:
* description
* hidden flag
* kind of role (role type)
* properties
* parent roles

----
##Steps of the Update Flow
Following steps are done before the CI update file is executed:
* set to not hidden
* reset description
* remove all parent roles

----
##Parameter Definitions
*   **Name:** `UserIgnoreWSO4Roles`
    **Parameter:** `‑‑ignoreworkspaceobjectsforrole [ROLE_MATCH]`, `‑‑ignorewso4role [ROLE_MATCH]`
    Defines the match of roles for which workspace objects are not handled (neither exported nor updated).
    Attention! A workspace object defined in the TCL update file are not ignored and will be created!
*   **Name:** `UserRoleSupportRoleType`
    **Default Value:** `true`
    Are from current MX version role types supported? This is a V6 feature and so as default set to true. If an older MX version is used which does not support role types the value must be set to `false`.

----
##Example
```TCL
################################################################################
# ROLE:
# ~~~~~
# MxUpdate_Role
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# role_MxUpdate_Role
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Role for test purposes.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mql escape mod role "${NAME}" \
    description "Role for test purposes." \
    !hidden \
    asarole
mql escape mod role "Employee" child "${NAME}"
```
