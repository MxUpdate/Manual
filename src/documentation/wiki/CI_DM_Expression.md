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
This expression properties could be handled from !MxUpdate:
 * description
 * hidden flag
 * expression value (expression itself)
 * properties

----
##Steps of the Update Flow

###Cleanup
Following steps are done before the TCL update file is executed:
 * set to not hidden
 * reset description
 * remove value (no expression)

###Update
The TCL update file is executed.

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

mql escape mod expression "${NAME}" \
    description "Expression for test purposes." \
    !hidden \
    value "current"
```
