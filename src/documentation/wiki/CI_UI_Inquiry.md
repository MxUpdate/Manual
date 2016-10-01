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

#Describes the special handling of Inquiries as configuration item.

----
##Introduction
An inquiry is used to produce a list of objects which e.g. could be used to select objects which are shown in a web table. For a deep instruction see the "MQL Guide" or "Business Modeler Guide" of the "ENOVIAvStudio Modeling Platform".

----
##Handled Inquiry Properties
This inquiry properties could be handled from MxUpdate:

Property    | Written            | Default Value | Kind
------------|--------------------|---------------|----
description | always             | empty string  | multi-line-string
hidden      | always             | ***false***   | flag
pattern     | always             | empty string  | string
format      | always             | empty string  | string
code        | always             | empty string  | multi-line-string
arguments   | if defined         | empty list    | list of key / value pairs
properties  | if defined         | empty list    | list of values and referenced admin objects


----
## Syntax
```
mxUpdate inquiry "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | description DESCRIPTION_STRING
    | [!]hidden
    | pattern PATTERN_STRING
    | format FORMAT_STRING
    | argument KEY_STRING VALUE_STRING
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
    | code CODE_STRING
```

For better reading, the code **`CODE_STRING `** itself is automatically exported with new line, code content and new line. The import trims all trailing new lines and spaces.

----
##Example

```tcl
################################################################################
# INQUIRY:
# ~~~~~~~~
# MxUpdate_Test
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# inquiry_MxUpdate_Test
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Inquiry for test purposes.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mxUdpate inquiry "${NAME}" {
    description "Inquiry for test purposes."
    pattern "${OID}"
    format "${OID}"
    argument "ID" "objectId"
    code "
print bus ${ID} select id dump \"
\"
"
}
```