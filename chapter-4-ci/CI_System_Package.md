#Configuration Item 'Package'

----
##Introduction
Packages are used to package admin objects. For a deep instruction see the MX documentation.

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
custom        | always             | ***false***   | flag
used packages | if defined         | empty list    | list to packages
properties    | if defined         | empty list    | list of values and referenced admin objects

----
## Syntax
```
mxUpdate package "${NAME}" { [OPTION] }
```
where `OPTION` is:
```
    | package PACKAGE_NAME
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | [!]custom
    | usepackage PACKAGE_NAME
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
```
----
##Example
```TCL
################################################################################
# PACKAGE_TestPackage
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate package "${NAME}" {
    description "MxUpdate Test Package with two members."
    !hidden
    !custom
    usepackage "MxUdpateAnotherPackage"
}
```
