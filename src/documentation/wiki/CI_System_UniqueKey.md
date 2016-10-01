#Configuration Item 'Unique Key'

----
##Introduction
Unique Keys are system configuration items. For a deep instruction see the MX documentation.

----
##Handled Properties
This package properties could be handled from MxUpdate:

Property      | Written            | Default Value | Kind
--------------|--------------------|---------------|-----------------------
package       | if defined         | empty         | string
uuid          | if defined         | empty         | string
symbolic name | if defined         | empty list    | list of symbolic name strings
description   | always             | empty string  | string
hidden flag   | always             | ***false***   | flag
enable flag   | always             | ***false***   | flag
global flag   | if ***true***      | ***false***   | flag
relationship  | if defined         | empty         | relationship name
type          | if defined         | empty         | type name
interface     | if defined         | empty         | interface name
field         | if defined         | empty list    | list of field expression with size
properties    | if defined         | empty list    | list of values and referenced admin objects


----
## Parameter Definitions
*   **Name:** ```SystemUniqueKeyMXSystemUniqueKeys```
    **Type:** String List
    **Default Value:** ```mxTNR```
    List of MX System Unique Keys which must be ignored (because they can not be handled from MxUpdate).

----
##Explanation of Update Error Codes

Error Code | Description
-----------|------------
70201      | The definition for what kind the unique key is defined is changed, but not allowed.

----
## Syntax
```
mxUpdate uniquekey "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | package PACKAGE_NAME
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | [!]enable
    | [!]global
    | for | type TYPE_NAME         | with interface INTERFACE_NAME
    |     | relationship TYPE_NAME |
    | field EXPRESSION [size SIZE]
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
```

----
##Example
```tcl
################################################################################
# UNIQUEKEY_MxUpdateTest.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate uniquekey "${NAME}" {
    description "MxUpdate Test Unique Key for a type with one field."
    !hidden
    !enable
    for type "MxUpdateType"
    field "attribute[AttrExpr]" size 255
}
```
