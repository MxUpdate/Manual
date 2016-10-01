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

Property    | Written            | Default Value | Kind
------------|--------------------|---------------|----
description | always             | empty string  | multi-line-string
hidden      | always             | ***false***   | flag
value       | if defined         | empty string  | multi-line-string
properties  | if defined         | empty list    | list of values and referenced admin objects


----
## Parameter Definitions
No further parameters are defined.

----
## Syntax

    mxUpdate expression NAME {
        description DESCRIPTION_STRING
        [!]hidden
        value EXPRESSION_STRING
        property NAME [to TYPE NAME] [value VALUE_STRING]
    }

----
##Example
```TCL
################################################################################
# EXPRESSION:
# ~~~~~~~~~~~
# TestExpression
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# expression_TestExpression
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Expression for test purposes.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mxUpdate expression "${NAME}" {
    description "Expression for test purposes."
    !hidden
    value "current"
}
```
