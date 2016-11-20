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

#Describes the special handling of Commands as configuration item.

----
## Introduction
Commands are used to define buttons with an action for the web user interface.
For a deep instruction see the "MQL Guide" or "Business Modeler Guide"
of the "Program Guide".

----
## Handled Command Properties
This command properties could be handled from MxUpdate:

Property      | Written      | Default Value | Kind
--------------|--------------|---------------|----
package       | if defined   | empty         | string
uuid          | if defined   | empty         | string
symbolic name | if defined   | empty list    | list of symbolic name strings
description   | always       | empty string  | multi-line-string
hidden        | always       | ***false***   | flag
label         | always       | empty string  | string
href          | always       | empty string  | string
alt           | always       | empty string  | string
users         | if defined   | empty list    | list of users
settings      | if defined   | empty list    | list of settings
properties    | if defined   | empty list    | list of values and referenced admin objects
code          | if not empty | empty string  | multi-line-string

----
## Syntax
```
mxUpdate command "${NAME}" { [OPTION] }
```
where ***`OPTION`*** is:
```
    | package PACKAGE_NAME
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | label LABEL_STRING
    | href HREF_STRING
    | alt ALT_STRING
    | user USER_NAME
    | setting SETTING_NAME SETTING_VALUE
    | property NAME [to TYPE NAME] [value VALUE_STRING]
    | code CODE_STRING
```
For better reading, the code **`CODE_STRING `** itself is automatically exported with new line, code content and new line. The import trims all trailing new lines and spaces.

----
## Example
```tcl
################################################################################
# COMMAND_TestCommand
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate command "${NAME}" {
    symbolicname "command_TestCommand"
    description "Command for test purposes."
    label "Test Label"
    href "${COMMON_DIR}/emxTable.jsp?table=TestTable&inquiry=TestInquiry"
    alt ""
    user "Employee"
    setting "Target Location" "content"
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "TestCommand"
    ################################################## Info End
    code "
function test()  {
    console.log(\"test\");
}
"
}
```