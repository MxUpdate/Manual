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

#Describes the special handling of Rules as configuration item.

----
## Introduction
Rules are used to restrict access for attributes, relationships etc. For a deep
instruction see the "MQL Guide" or "Business Modeler Guide" of the "ENOVIA
Studio Modeling Platform".

----
##Handled Properties

This rule properties could be handled from !MxUpdate:
* description
* hidden flag
* enforce reserve access flag
* owner access
* owner revoke
* public access
* public revoke
* user access
* properties

The governed objects are not handled in the rule configuration item file. They must be defined in the related [attribute](CI_DM_Attribute.md), [form](CI_UI_Form.md), [program](CI_Program.md) or [relationship](CI_DM_Relationship.md) configuration item file.

----
##Parameter Definitions
*   **Name:** `DMRuleAllowExportAccessSorting`
    **Default Value:** `true`
    **Opposite Parameter (to deactivate):** `--deactivateRuleExportAccessSort`
    The exported access of rules are sorted if parameter is `true`.
*   **Name:** `DMRuleSupportsEnforceReserveAccess`
    **Value:** `true` if the MX version supports the 'enforce reserve access' flag (tested by calling MQL command `help rule` and testing the result for `enforcereserveaccess`).

----
## Syntax
```
mxUpdate rule NAME {
    description DESCRIPTION_STRING
    [!]hidden
    [!]enforcereserveaccess
    [revoke] [login] | public    | [key KEY_STRING] {ACCESS_ITEM...} [USER_ITEM]
                     | owner     | 
                     | user NAME | 
    property NAME [to TYPE NAME] [value VALUE_STRING]
}
```
where **`USER_ITEM `** is:
```
    [any|single|ancestor|descendant] organization
    [any|single|ancestor|descendant] project
    [any|context] owner
    [any|no|context|inclusive] reserve
    [any|no|public|protected|private|notprivate|ppp] maturity
    [any|oem|goldpartner|partner|supplier|customer|contractor] category
    [filter|localfilter] EXPRESSION
```

----
##Example
```TCL
################################################################################
# RULE:
# ~~~~~
# TestRule
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# rule_TestRule
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Rule for test purposes.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mxUpdate rule "${NAME}" {
    description "Rule for test purposes."
    !hidden
    owner {modify read show}
    revoke owner {modify} filter "type==Part"
    public {none}
    user "Employee" {show} filter ""
}
```
