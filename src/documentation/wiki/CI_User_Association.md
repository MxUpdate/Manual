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

#Describes the special handling of associations as configuration item.

----
##Introduction
Associations are a list of persons which could be defined as expression.

----
##Example
```TCL
################################################################################
# ASSOCIATION:
# ~~~~~~~~~~~~
# MxUpdate_PublicCheckin
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# association_MxUpdate_PublicCheckin
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Used to give rights in a state expression testing if user has check in
# rights (like OOTB public read).
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mql escape mod association "${NAME}" \
    description "Used to give rights in a state expression testing if user has check in rights (like OOTB public read)." \
    !hidden \
    definition "\"!User Agent\""
```
