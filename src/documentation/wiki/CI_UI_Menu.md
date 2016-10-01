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
This menu properties could be handled from !MxUpdate:
  * description
  * hidden flag
  * flag to indicate that the menu is a type tree menu
  * "alt" and label text
  * hyperlink reference (HRef)
  * settings
  * assigned sub commands and menus
  * properties

----
##Steps of the Update Flow
The menu CI file is defined with the so called *update format*. So an update of an menu is done by calculating the delta between the target and the current existing definition.
This calculating delta means also that the history of a menu contains only the changes between the different milestone of a menu definition.

----
##Parameter Definitions
No further parameters are defined.

----
## Syntax
    mxUpdate menu NAME {
        description DESCRIPTION_STRING
        [!]hidden
        [!]treemenu
        label LABEL_STRING
        href HREF_STRING
        alt ALT_STRING
        setting SETTING_NAME SETTING_VALUE
        command COMMAND
        menu MENU
        property NAME [to TYPE NAME] [value VALUE_STRING]
    }

----
##Example
```TCL
################################################################################
# MENU:
# ~~~~~
# MxUpdateToolbarMenu
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# menu_MxUpdateToolbarMenu
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Menu for test purposes.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mxUpdate menu "${NAME}" {
    description "Menu for test purposes."
    label "emxFramework.Common.Actions"
    href ""
    alt ""
    setting "Registered Suite" "Framework"
    command "MxUpdate_Test"
}
```