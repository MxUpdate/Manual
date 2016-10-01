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

#Describes the special handling of MQL Programs as configuration item.

----
##Introduction
The source code of programs are handled as part of the configuration item as property.

----
##Handled Page Properties
This page properties could be handled from MxUpdate:

Property      | Written           | Default Value   | Kind
--------------|-------------------|-----------------|----
package       | if defined        | empty           | string
kind          | always            | ***mql***       | is always ***mql***
symbolic name | if defined        | empty list      | list of symbolic name strings
description   | always            | empty string    | multi-line-string
hidden        | if ***true***     | ***false***     | flag
rule          | if defined        | empty string    | string
execution     | if ***deferred*** | ***immediate*** | enumeration of ***deferred*** and ***immediate***
properties    | if defined        | empty list      | list of values and referenced admin objects
code          | if defined        | empty string    | multi-line-string

----
## Syntax
```
mxUpdate program "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | package PACKAGE_NAME
    | symbolicname SYMBOLICNAME_STRING
    | kind mql 
    | description DESCRIPTION_STRING
    | [!]hidden
    | [!]needsbusinessobject
    | [!]downloadable
    | [!]pipe
    | [!]pooled
    | rule RULE_STRING
    | execute | immediate      |
    |         | deferred       |
    | execute user USER_NAME 
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
    | code CONTENT_STRING
```

For better reading, the code **`CONTENT_STRING `** itself is automatically exported with new line, code content and new line. The import trims all trailing new lines and spaces.

----
##Example
```tcl
################################################################################
# PROGRAM_MxUpdateTestProgram.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate program "${NAME}" {
    kind mql
    symbolicname "attribute_MxUpdateTestAttribute"
    description "MxUpdate test program."
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "MxUpdateTestProgram"
    ################################################## Info End
    code "
<html>
    <head><title>Title</title></head>
    <body>
        <h1>Test</h1>
    </body>
</html>
"
```