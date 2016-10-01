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

#Describes the special handling of Web Forms as configuration item.

----
##Introduction
A form is used to display information related to an object. For a deep
instruction see the "MQL Guide" or "Business Modeler Guide" of the
"ENOVIAvStudio Modeling Platform".

----
##Handled Form Properties
This form properties could be handled from MxUpdate:

Property              | Written            | Default Value | Kind
----------------------|--------------------|---------------|----
description           | always             | empty string  | string
hidden                | if ***true***      | ***false***   | flag
properties            | if defined         | empty list    | list of values and referenced admin objects
field/name            | always             | empty string  | string
field/label           | always             | empty string  | string
field/select          | if defined         | empty string  | string
field/businessobject  | if defined         | empty string  | string
field/relationship    | if defined         | empty string  | string
field/range           | if defined         | empty string  | string
field/href            | if defined         | empty string  | string
field/alt             | if defined         | empty string  | string
field/user            | if defined         | empty list    | list of users
field/setting         | if defined         | empty list    | list of key/value pair


----
## Syntax
```
mxUpdate form "${NAME}" { [OPTION] }
```
where `OPTION` is:
```
    | description DESCRIPTION_STRING
    | [!]hidden
    | field { [FIELD_OPTION] }
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
```
where `FIELD_OPTION` is:
```
    | name NAME_STRING
    | label LABEL_STRING
    | select SELECT_STRING
    | businessobject SELECT_STRING
    | relationship SELECT_STRING
    | range RANGE_HREF_STRING
    | href HREF_STRING
    | alt ALT_STRING
    | user USER_STRING
    | setting KEY_STRING VALUE_STRING 
```

	
----
##Example

```TCL
################################################################################
# FORM:
# ~~~~~
# type_MxUpdate_Product
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# form_type_MxUpdate_Product
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Form for test purposes.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mxUpdate form "${NAME}" {
    description "Form for test purposes." 
    field {
        name "type" 
        label "emxFramework.Basic.Type" 
        businessobject "$<type>" 
        range "${SUITE_DIR}/range.jsp" 
        href "${SUITE_DIR}/execute.jsp" 
        setting "Admin Type" "Type" 
        setting "Editable" "false" 
        setting "Field Type" "basic" 
        setting "Registered Suite" "Framework" 
        setting "Show Type Icon" "true"
    }
    field {
        name "name" 
        label "emxFramework.Basic.Name" 
        businessobject "$<name>" 
        setting "Admin Type" "Name" 
        setting "Editable" "true" 
        setting "Field Type" "basic" 
        setting "Input Type" "textbox" 
        setting "Registered Suite" "Framework" 
        setting "Required" "true" 
    }
    field {
        name "revision" 
        label "emxFramework.Basic.Revision" 
        businessobject "$<revision>" 
        setting "Admin Type" "Revision" 
        setting "Editable" "true" 
        setting "Field Type" "basic" 
        setting "Input Type" "textbox" 
        setting "Registered Suite" "Framework" 
        setting "Required" "true" 
    }
}
```
