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

#Describes the special handling of Menus as configuration item.

----
##Introduction
Menus are used to define group buttons for the web user interface. In some
cases a menu could also be a button with action. For a deep instruction see the
"MQL Guide" or "Business Modeler Guide" of the "ENOVIAvStudio Modeling
Platform".

----
##Handled Menu Properties
This menu properties could be handled from MxUpdate:

Property           | Written       | Default Value | Kind
-------------------|---------------|---------------|----
package            | if defined    | empty         | string
uuid               | if defined    | empty         | string
symbolic name      | if defined    | empty list    | list of symbolic name strings
description        | always        | empty string  | multi-line-string
hidden             | always        | ***false***   | flag
type tree          | if ***true*** | ***false***   | flag
label              | always        | empty string  | string
href               | always        | empty string  | string
settings           | if defined    | empty list    | list of settings
commands and menus | if defined    | empty list    | list of child commands / menus
properties         | if defined    | empty list    | list of values and referenced admin objects

----
## Syntax
```
mxUpdate menu "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | package PACKAGE_NAME
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | [!]treemenu
    | label LABEL_STRING
    | href HREF_STRING
    | alt ALT_STRING
    | setting SETTING_NAME SETTING_VALUE
    | command COMMAND_NAME
    | menu MENU_NAME
    | property NAME [to TYPE NAME] [value VALUE_STRING]
```

----
##Example
```tcl
################################################################################
# MENU_TestToolbarMenu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate menu "${NAME}" {
    symbolicname "menu_MxUpdateToolbarMenu"
    description "Menu for test purposes."
    label "emxFramework.Common.Actions"
    href ""
    alt ""
    setting "Registered Suite" "Framework"
    command "MxUpdate_Test"
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "MxUpdateToolbarMenu"
    ################################################## Info End
}
```