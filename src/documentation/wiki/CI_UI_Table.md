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

#Describes the special handling of Tables as configuration item.

----
##Introduction
A web table is used to display multiple business objects with related
information. For a deep instruction see the "MQL Guide" or "Business Modeler
Guide" of the "ENOVIAvStudio Modeling Platform".

----
----
##Handled Table Properties
This form properties could be handled from MxUpdate:

Property              | Written            | Default Value | Kind
----------------------|--------------------|---------------|----
description           | always             | empty string  | string
hidden                | if ***true***      | ***false***   | flag
properties            | if defined         | empty list    | list of values and referenced admin objects
column/name           | always             | empty string  | string
column/label          | always             | empty string  | string
column/select         | if defined         | empty string  | string
column/businessobject | if defined         | empty string  | string
column/relationship   | if defined         | empty string  | string
column/range          | if defined         | empty string  | string
column/href           | if defined         | empty string  | string
column/alt            | if defined         | empty string  | string
column/setting        | if defined         | empty list    | list of key/value pair

----
## Syntax
```
mxUpdate table "${NAME}" { [OPTION] }
```
where `OPTION` is:
```
    | description DESCRIPTION_STRING
    | [!]hidden
    | column { [COLUMN_OPTION] }
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
```
where `COLUMN_OPTION` is:
```
    | name NAME_STRING
    | label LABEL_STRING
    | select SELECT_STRING
    | businessobject SELECT_STRING
    | relationship SELECT_STRING
    | range RANGE_HREF_STRING
    | href HREF_STRING
    | alt ALT_STRING
    | setting KEY_STRING VALUE_STRING 
```

----
##Example
```TCL
################################################################################
# TABLE:
# ~~~~~~
# type_MxUpdate_Product
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# table_type_MxUpdate_Product
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Table for test purposes.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mxUpdate table "${NAME}" {
    description "Table for test purposes." 
    column {
        name "type" 
        label "emxFramework.Basic.Type" 
        businessobject "$<type>" 
        range "" 
        href "" 
        alt "" 
        setting "Registered Suite" "Framework" 
        setting "Show Type Icon" "true" 
    }
    column {
        name "name" 
        label "emxFramework.Basic.Name" 
        businessobject "$<name>" 
        range "" 
        href "${COMMON_DIR}/emxTree.jsp?mode=insert" 
        alt "" 
        setting "Registered Suite" "Framework" 
        setting "Target Location" "content"
    } 
    column {
        name "revision" 
        label "emxFramework.Basic.Revision" 
        businessobject "$<revision>" 
        range "" 
        href "" 
        alt "" 
        setting "Registered Suite" "Framework"
    } 
    column {
        name "description" 
        label "emxFramework.Basic.Description" 
        businessobject "$<description>" 
        range "" 
        href "" 
        alt "" 
        setting "Registered Suite" "Framework"
    }
}
```
