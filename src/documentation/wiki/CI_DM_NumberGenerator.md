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

#Describes the special handling of Number Generators as configuration item.

----
##Introduction
A number generator is used to create new numbers which e.g. could be used for names of business objects.

----
##Example
```TCL
################################################################################
# NUMBERGENERATOR:
# ~~~~~~~~~~~~~~~~
# type_MxUpdateTestType
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Number Generator for MxUpdate Test Type Objects.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mql mod bus "${OBJECTID}" \
    description "Number Generator for MxUpdate Test Type Objects."

# update of the next number attribute only if not already set
set sTmp [mql print bus "${OBJECTID}" select attribute\[eService Next Number\] dump]
if {[string length "${sTmp}"]==0}  {
  mql mod bus "${OBJECTID}" "eService Next Number" "0000001"
}
```
