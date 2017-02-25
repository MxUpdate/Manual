<!--
 *
 *  This file is part of MxUpdate <http://www.mxupdate.org>.
 *
 *  MxUpdate is a deployment tool for a PLM platform to handle
 *  administration objects as single update files (configuration item).
 *
 *  Copyright (C) 2008-2017 The MxUpdate Team
 *
 *  The Manual of MxUpdate is licensed under a CC BY-NC-SA 4.0 license
 *  (Creative Commons Attribution-NonCommercial-ShareAlike 4.0 
 *  International 4.0 license).
 *
 *  You should have received a copy of the license along with this
 *  work. If not, see <http://creativecommons.org/licenses/by-nc-sa/4.0/>.
 *
-->

# System Computing Environment
Each MX system has a Computing Environment. For further information see the MX documentation.

## Syntax
```
mxUpdate computingenvironment "${NAME}" "${REVISION}" { [OPTION] }
```
where **`OPTION`** is:
```
    | description DESCRIPTION_STRING
    | current CURRENT_STATE
    | attribute ATTR_NAME ATTR_MULTI_LINE_VALUE
```

## Example
```TCL
################################################################################
# COMPUTINGENVIRONMENT_MxUpdateTest________-.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate trigger "${NAME}" "${REVISION}" {
    description ""
    current "all"
      :
}
```
