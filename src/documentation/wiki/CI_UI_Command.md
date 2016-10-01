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
This command properties could be handled from !MxUpdate:
* description
* hidden flag
* "alt" and label text
* hyperlink reference (HRef)
* user references (assigned users)
* settings
* properties

----
## Syntax

    mxUpdate command NAME {
        description DESCRIPTION_STRING
        [!]hidden
        label LABEL_STRING
        href HREF_STRING
        alt ALT_STRING
        user USER_NAME
        setting SETTING_NAME SETTING_VALUE
        property NAME [to TYPE NAME] [value VALUE_STRING]
    }

----
## Example

```tcl
################################################################################
# COMMAND:
# ~~~~~~~~
# TestCommand
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# command_TestCommand
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Command for test purposes.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mxUpdate command "${NAME}" {
    description "Command for test purposes."
    label "Test Label"
    href "\$\{COMMON_DIR\}/emxTable.jsp?table=TestTable&inquiry=TestInquiry"
    alt ""
    user "Employee"
    setting "Target Location" "content"
}
```