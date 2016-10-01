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

#Describes the special handling of Policies as configuration item.

----
## Introduction
Policies are used to define lifecycle's for policies. For more information see the MX documentation.

----
##Handled Properties
This policy properties could be handled from MxUpdate:

Property       | Written              | Default Value   | Kind
---------------|----------------------|-----------------|----
uuid           | if defined           | empty           | string
symbolic name  | if defined           | empty list      | list of symbolic name strings
description    | always               | empty string    | multi-line-string
hidden         | always               | ***false***     | flag
types          | if defined           | empty list      | list of types (or ***all***)
formats        | if defined           | empty list      | list of types (or ***all***)
default format | always               | empty string    | string
enforce        | if ***true***        | ***false***     | flag
delimiter      | if major / major     | empty character | character
minor sequence | if major / major     | empty string    | string
major sequence | if major / major     | empty string    | string
sequence       | if not major / minor | empty string    | string
store          | always               | empty string    | string
allstate       | if defined           | empty list      | list of access statements
states         | if defined           | empty           | list of state properties and state access statements
properties     | if defined           | empty list      | list of values and referenced admin objects

----
## Policy File Format
The policy (excluding the properties of a policy) is defined with the TCL
procedure `mxUpdate`.

*Snippet of an Example:*
```TCL
mxUpdate policy "${NAME}" {
  :
}
```

### All State Access Definition
The "all state access" definition is defined within `allstate`.

*Snippet of an example:*
```TCL
mxUpdate policy "${NAME}" {
  :
  allstate  {
    :
    owner {read show modify}
    revoke owner {modify} filter "type==Test"
    public {none}
    user "creator" {all}
    :
  }
  :
}
```

### Owner and Public Access for States
The owner access is defined with the tag `owner`, the access list (in curly braces), the tag `filter` with the filter expression. The `filter` and expression must be only defined if wanted.

The public access uses instead the tag `public`.

For revoke access, the tag `revoke` must be define in front of the access definitions.

*Snippet of an Example:*
```TCL
mxUpdate policy "${NAME}" {
  :
  state "TestState"  {
    :
    owner {read show modify}
    revoke owner {modify} filter "type==Test"
    public {none}
    :
  }
  :
}
```

----
## Parameter Definitions
*   **Name:** `DMPolicyAllowExportAccessSorting`
    **Default Value:** `true`
    **Opposite Parameter (to deactivate):** `--deactivatePolicyExportAccessSort`
    The exported access of policies and policy states are sorted if parameter is `true`.
*   **Name:** `DMPolicySupportsMajorMinor`
    **Value:** `true` (if the MQL command "`help policy`" contains "`majorrevision`")
    Policies supports major / minor definitions if parameter is `true`.
*   **Name:** `DMPolicyStateSupportsEnforceReserveAccess`
    **Value:** `true` (if the MQL command "`help policy`" contains "`enforcereserveaccess`")
    Policy states supports the 'enforce reserve access' flag if parameter  is `true`.
*   **Name:** `DMPolicyStateSupportsPublished`
    **Value:** `true` (if the MQL command "`help policy`" contains "`published`")
    Policy states supports the published flag if parameter is `true`.

----
## Syntax
```
mxUpdate policy "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | type | all       |
    |      | TYPE_NAME |
    | format | all         |
    |        | FORMAT_NAME |
    | defaultformat FORMAT_NAME
    | [!]enforce
    | delimiter DELIMITER
    | minorsequence REVISION_SEQUENCE
    | majorsequence REVISION_SEQUENCE
    | sequence REVISION_SEQUENCE
    | store STORENAME
    | allstate  { ACCESS_ITEM }
    | state STATE_NAME { [STATE_ITEM] }
    | property NAME [to TYPE NAME] [value VALUE_STRING]
```
where **`STATE_ITEM`** is:
```
    | registeredName REGISTERED_NAME_STRING
    | [!]enforcereserveaccess
    | [!]majorrevision
    | [!]minorrevision
    | [!]version
    | [!]promote
    | [!]checkouthistory
    | [!]published
    | ACCESS_ITEM
    | action PROGRAM_NAME input ARG_STRING
    | check PROGRAM_NAME input ARG_STRING
    | trigger EVENT_TYPE | action   | PROGRAMNAME [input ARG_STRING]
    |                    | check    |
    |                    | override |
    | signature SIGNATURE_NAME { [SIGNATURE_ITEM] }
    | property NAME [to TYPE NAME] [value VALUE_STRING]

```
where **`SIGNATURE_ITEM `** is:
```
    | branch STATENAME
    | approve {USER ...}
    | ignore {USER ...}
    | reject {USER ...}
    | filter FILTER_EXPRESSION
```
where **`ACCESS_ITEM`** is:
```
    | [revoke] [login] | public    | [key KEY_STRING] {ACCESS...} [USER_ITEM]
    |                  | owner     | 
    |                  | user NAME | 

```
where **`USER_ITEM `** is:
```
    | [any|single|ancestor|descendant] organization
    | [any|single|ancestor|descendant] project
    | [any|context] owner
    | [any|no|context|inclusive] reserve
    | [any|no|public|protected|private|notprivate|ppp] maturity
    | [any|oem|goldpartner|partner|supplier|customer|contractor] category
    | [filter|localfilter] EXPRESSION
```

----
## Compatibility to Previous Version
For compatibility to previous version, flags can be also set via values after the flag key.

### Types
After the tag `type` the list of types in curly braces are defined. 
*Snippet of an Examples with One Type:*
```
mxUpdate policy "${NAME}" {
  :
  type {"Test Type"}
  :
}
```

### Formats
After the tag `format` the list of formats in curly braces are defined. 
*Snippet of an example with One Format:*
```
mxUpdate policy "${NAME}" {
  :
  format {generic}
  :
}
```

### Policy Flags
```
hidden | "false" |
       | "true"  |        
enforce | "false" |
        | "true"  |        
```

### Policy State Flags
```
enforcereserveaccess | "false" |
                     | "true"  |        
majorrevision | "false" |
              | "true"  |
minorrevision | "false" |
              | "true"  |
version | "false" |
        | "true"  |
promote | "false" |
        | "true"  |
checkouthistory | "false" |
                | "true"  |
published | "false" |
          | "true"  |
```

----
## Example
```tcl
################################################################################
# POLICY_TestPolicy.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate policy "${NAME}" {
    symbolicname "interface_MxUpdateTestInterface"
    description "Policy for test purposes."
    !hidden
    type all
    format "generic"
    defaultformat "generic"
    sequence "1,2,3,..."
    store ""
    allstate  {
        owner {}
        public {read show}
    }
    state "Submitted"  {
        registeredName "state_Submitted"
        revision
        version
        promote
        checkouthistory
        owner {read modify checkout checkin}
        public {}
        signature "Reject" {
            branch "Rejected"
            approve {Employee}
            ignore {Employee}
            reject {Employee}
            filter ""
        }
        signature "Review" {
            branch "Review"
            approve {Employee}
            ignore {Employee}
            reject {Employee}
            filter ""
        }
    }
    state "Review"  {
        registeredName "state_Review"
        revision
        version
        promote
        checkouthistory
        owner {read modify checkout}
        public {}
    }
    state "Approved"  {
        registeredName "state_Approved"
        revision
        version
        promote
        checkouthistory
        owner {read modify checkout checkin}
        public {}
        signature "creator" {
            branch ""
            approve {creator}
            ignore {}
            reject {}
            filter ""
        }
    }
    state "Rejected"  {
        revision
        version
        promote
        checkouthistory
        owner {read modify show}
        public {}
    }
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "TestPolicy"
    ################################################## Info End
}
```

----
## Limitations

### Filter
With Enovia V6R2010 it is not possible to extract filter informations for owner / public / revoke owner / revoke public access with a XML export or with a MQL print select statement. There exists some incidents for this behavior. This means that a MxUpdate export does not include this filter informations. In this case the filters must be added manually to the configuration item file. So this also means e.g. that the standard MQL compare command does not work correctly (because the filter informations are not exported...).
Starting with Enovia V6R2010x the extract filter information works as expected.

### Signatures and new Access Items
MX creates for signatures automatically depending access items. The key of an access item are the name of the signature.
 * Signature filters are defined as public access with access item 'none'.
 * Approve, reject and ignore definitions for user are defined as access for given users with access item 'approve', 'reject' or 'ignore'.




