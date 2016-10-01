#Configuration Item 'Index'

----
##Introduction
Index's are system configuration items. For a deep instruction see the MX documentation.

----
##Handled Properties
This package properties could be handled from MxUpdate:

Property      | Written            | Default Value | Kind
--------------|--------------------|---------------|-----------------------
uuid          | if defined         | empty         | string
symbolic name | if defined         | empty list    | list of symbolic name strings
description   | always             | empty string  | string
hidden flag   | always             | ***false***   | flag
enable        | always             | ***false***   | flag
unique flag   | if ***true***      | ***false***   | flag
field         | if defined         | empty list    | list of field expression with size
properties    | if defined         | empty list    | list of values and referenced admin objects

----
## Syntax
```
mxUpdate index "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | [!]enable
    | [!]unique
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
```

----
##Example
```tcl
################################################################################
# INDEX_MxUpdateTest.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate index "${NAME}" {
    description "MxUpdate Test Index with two fields."
    !hidden
    !enable
    field "name"
    field "attribute[AttrExpr]" size 255
}
```
