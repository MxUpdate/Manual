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

#Describes the special handling of EKL / External / Java / MQL Programs as configuration item.

----
##Introduction
The source code of programs are handled as part of the configuration item as property.

----
##Handled Page Properties
This page properties could be handled from MxUpdate:

Property      | Written           | Default Value   | Kind
--------------|-------------------|-----------------|----
package       | if defined        | empty           | string
kind          | always            |                 | enumeration of ***ekl***, ***external***, ***java*** and ***mql***
symbolic name | if defined        | empty list      | list of symbolic name strings
description   | always            | empty string    | multi-line-string
hidden        | if ***true***     | ***false***     | flag
rule          | if defined        | empty string    | string
execution     | if ***deferred*** | ***immediate*** | enumeration of ***deferred*** and ***immediate***
properties    | if defined        | empty list      | list of values and referenced admin objects
code          | if defined        | empty string    | multi-line-string

----
##Parameter Definitions
*   **Name:** ```Compile```
    **Parameter:** `‑‑compile`
    **Default Value:** `false`
    Compiles all updated JPO programs.

----
## Update

### EKL / External / MQL Programs
If a `FILE_PATH` for the file parameter is defined, the content of the file defines directly the program code.

### Java Programs (so called Java Program Objects, JPO's)
The `FILE_PATH` references the a Java class definition. If the `CONTENT_STRING` is defined, the code must be already converted JPO code (with `${CLASSNAME}`, `${CLASS:...}` etc.).

----
## Export

### EKL / External / MQL Programs
For better reading, the code **`CONTENT_STRING `** itself is automatically exported with new line, code content and new line. The import trims all trailing new lines and spaces.

### Java Programs (so called Java Program Objects, JPO's)
If a Java program is extracted, the MX name of the JPO is used to extract the package name and the file name of the JPO. The code for the package is automatically added to the JPO source code (in the beginning of the source code). The properties are exported in the mxu-file, the Java source code directly in the depending package sub folder and class name with ```_mxJPO```.

####Example without Package
JPO with name `Part` has the Java file name `Part_mxJPO.java` and the configuration file `Part_mxJPO.java.mxu`.

####Example with Package
JPO with name `org.mxupdate.Update` has the Java class file name `Update_mxJPO.java` (in sub directory `org/mxupdate`) and the configuration file `org.mxupdate.Update_mxJPO.java.mxu'.

----
## Syntax
```
mxUpdate program "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | package PACKAGE_NAME
    | symbolicname SYMBOLICNAME_STRING
    | kind | ekl      |
    |      | external |
    |      | java     |
    |      | mql      |
    | description DESCRIPTION_STRING
    | [!]hidden
    | [!]needsbusinessobject
    | [!]downloadable
    | [!]pipe
    | [!]pooled
    | rule RULE_STRING
    | execute | immediate      |
    |         | deferred       |
    |         | user USER_NAME |
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
    | file FILE_PATH
    | code CONTENT_STRING
```

----
##Example
```tcl
################################################################################
# PROGRAM_MxUpdateTestProgram.mql.mxu
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
}
```