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

#Describes the special handling of groups as configuration item.

----
##Parameter Definitions
*   **Name:** `UserIgnoreWSO4Groups`
    **Parameter:** `‑‑ignoreworkspaceobjectsforgroup [GROUP_MATCH]`, `‑‑ignorewso4group [GROUP_MATCH]`
    Defines the match of groups for which workspace objects are not handled (neither exported nor updated).
    Attention! A workspace object defined in the TCL update file are not ignored and will be created!
