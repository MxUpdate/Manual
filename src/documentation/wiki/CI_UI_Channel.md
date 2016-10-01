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

#Describes the special handling of Channels as configuration item.

----
## Introduction
A channels is a collection of commands. Multiple channels are used to define the content of MX portals. For a deep instruction see the "MQL Guide" or "Business Modeler Guide" of the "ENOVIAvStudio Modeling Platform".

**Hint!** The configuration item 'channel' of the MxUpdate Update tool does not handle channels which are defined as user's workspace item.

----
##Handled Properties
This command properties could be handled from MxUpdate:

Property      | Written    | Default Value | Kind
--------------|------------|---------------|----
uuid          | if defined | empty         | string
symbolic name | if defined | empty list    | list of symbolic name strings
description   | always     | empty string  | multi-line-string
hidden        | always     | ***false***   | flag
label         | always     | empty string  | string
href          | always     | empty string  | string
alt           | always     | empty string  | string
height        | always     | ***0***       | integer
settings      | if defined | empty list    | list of settings
commands      | is defined | empty list    | list of assigned commands
properties    | if defined | empty list    | list of values and referenced admin objects

----
## Syntax
```
mxUpdate channel "${NAME}" { [OPTION] }
```
where ***`OPTION`*** is:
```
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | label LABEL_STRING
    | href HREF_STRING
    | alt ALT_STRING
    | setting SETTING_NAME SETTING_VALUE
    | command COMMAND_STRING
    | property NAME [to TYPE NAME] [value VALUE_STRING]
```

----
##Example
```tcl
################################################################################
# CHANNEL_TestChannel
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate channel "${NAME}" {
    symbolicname "channel_TestChannel"
    description "Channel for test purposes."
    label "Test Label"
    height 100
    setting "Registered Suite" "MxUpdateCentral"
    command "First Test Command"
    command "Second Test Command"
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "TestChannel"
    ################################################## Info End
}
```