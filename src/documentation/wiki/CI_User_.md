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

#Describes the special handling of all Users as configuration item.

----
##Introduction
Currently following user objects are supported from MxUpdate:
* [association](CI_User_Association.md)
* [group](CI_User_Group.md)
* [role](CI_User_Role.md)
* [administration person](CI_User_PersonAdmin.md) (without related business object)

Generally for all user also the workspace objects are always handled (exported and updated).

----
##Parameter Definitions
*   **Name:** `UserIgnoreWSO4Users`
    **Parameters:** `‑‑ignoreworkspaceobjectsforuser [USER_MATCH]`, `‑‑ignorewso4user [USER_MATCH]`
    Defines the match of users for which users workspace objects are not handled (wether exported nor updated). Attention! A workspace object defined in the TCL update file are not ignored and will be created!
