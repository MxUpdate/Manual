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

#Describes the special handling of IEF Global Registry Objects as configuration item.

----
##Introduction

In the IEF Global Registry Objects each installed integrations is registered. The integration source itself is done with XML tags. Maximum one object exists (if at minimum one integration is used). The object is identified with name "IEF-GlobalRegistry" and revision "-".

----
## Syntax
```
mxUpdate globalregistry "${NAME}" "${REVISION}" { [OPTION] }
```
where **`OPTION`** is:
```
    | description DESCRIPTION_STRING
    | current CURRENT_STATE
    | attribute ATTR_NAME ATTR_MULTI_LINE_VALUE
```

----
##Example (Snippet)
```TCL
################################################################################
# IEFGLOBALREGISTRY_IEF-GlobalRegistry________-.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate globalregistry "${NAME}" "${REVISION}" {
    description "IEF Global Registry Object"
    current "Exists"
    attribute "IEF-RegistryData" "<?xml version='1.0'?><integrationregistry>....</integrationregistry>"
}
```
