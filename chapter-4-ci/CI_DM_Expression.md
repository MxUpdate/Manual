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

#Describes the special handling of Expressions as configuration item.

----
##Introduction
Expressions are evaluated against business objects or connections. For a deep
instruction see the "MQL Guide" or "Business Modeler Guide" of the
"ENOVIAvStudio Modeling Platform".

----
##Handled Properties
This expression properties could be handled from MxUpdate:

Property      | Written            | Default Value | Kind
--------------|--------------------|---------------|----
package       | if defined         | empty         | string
uuid          | if defined         | empty         | string
symbolic name | if defined         | empty list    | list of symbolic name strings
description   | always             | empty string  | multi-line-string
hidden        | always             | ***false***   | flag
value         | if defined         | empty string  | multi-line-string
properties    | if defined         | empty list    | list of values and referenced admin objects


----
## Parameter Definitions
No further parameters are defined.

----
## Syntax
```
mxUpdate expression "${NAME}" { [OPTION] }
```
where `OPTION` is:
```
    | package PACKAGE_NAME
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | value EXPRESSION_STRING
    | property NAME [to TYPE NAME] [value VALUE_STRING]
```

----
##Example
```TCL
################################################################################
# EXPRESSION_TestExpression.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate expression "TestExpression" {
    symbolicname "expression_TestExpression"
    description "Expression for test purposes."
    !hidden
    value "current"
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "TestExpression"
    ################################################## Info End
}
```
