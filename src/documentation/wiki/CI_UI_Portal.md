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

#Describes the special handling of Portals as configuration item.

----
##Introduction
A portal is a collection of channels. A portal is used as power view in the
user interface. For a deep instruction see the "MQL Guide" or "Business Modeler
Guide" of the "ENOVIAvStudio Modeling Platform".

The configuration item 'portal' of the !MxUpdate Update tool does not handle
portals which are defined as user's workspace item.

----
##Handled Properties
This portal properties could be handled from MxUpdate:

Property      | Written       | Default Value | Kind
--------------|---------------|---------------|----
package       | if defined    | empty         | string
uuid          | if defined    | empty         | string
symbolic name | if defined    | empty list    | list of symbolic name strings
description   | always        | empty string  | multi-line-string
hidden        | always        | ***false***   | flag
label         | always        | empty string  | string
href          | always        | empty string  | string
alt           | always        | empty string  | string
settings      | if defined    | empty list    | list of settings
channels      | if defined    | empty list    | list of child channels
properties    | if defined    | empty list    | list of values and referenced admin objects

----
## Syntax
```
mxUpdate portal "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | package PACKAGE_NAME
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | label LABEL_STRING
    | href HREF_STRING
    | alt ALT_STRING
    | setting SETTING_NAME SETTING_VALUE
    | channel COMMAND_NAME
    | property NAME [to TYPE NAME] [value VALUE_STRING]
```

----
##Example
```tcl
################################################################################
# PORTAL_TestPortal
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate portal "${NAME}" {
    symbolicname "portal_TestPortal"
    description "Portal for test purposes."
    label ""
    setting "Registered Suite" "MxUpdateCentral"
    channel "TestChannel"
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "TestPortal"
    ################################################## Info End
}
```