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

#Describes the special handling of Formats as configuration item.

----
##Introduction
Formats are used for files check-in on business objects. They are used from
policies. For a deep instruction see the "MQL Guide" or "Business Modeler Guide"
of the "ENOVIAvStudio Modeling Platform".

----
##Handled Properties
This format properties could be handled from MxUpdate:

Property          | Written           | Default Value | Kind
------------------|-------------------|---------------|----
symbolic name     | if defined        | empty list    | list of symbolic name strings
description       | always            | empty string  | multi-line-string
hidden            | always            | ***false***   | flag
version           | always            | empty string  | string
file suffix       | always            | empty string  | string
file type         | always            | empty string  | string
mime type         | always            | empty string  | string
view program      | if supported      | empty string  | string
edit program      | if supported      | empty string  | string
print program     | if supported      | empty string  | string
properties        | if defined        | empty list    | list of values and referenced admin objects

The view, edit and print program are legacy properties and not supported anymore from current MX versions.

----
##Parameter Definitions
*   **Name:** ```DMFormatSupportsPrograms ```
    **Value:** ```true```if the MQL command ```help format```includes the string ```view```
    If the flag is true, format supports view, edit and print programs. The flag is only needed for legacy MX versions.

----
##Syntax
```
mxUpdate format "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | version VERSION_STRING
    | suffix VERSION_STRING
    | type TYPE_STRING
    | mime MIME_STRING
    | (view PROGRAM)
    | (edit PROGRAM)
    | (print PROGRAM)
    | property NAME [to TYPE NAME] [value VALUE_STRING]
```
    
**Hint:** Programs for ```view```, ```edit``` and ```print``` are legacy. Newer MX versions does not support anymore this feature.

----
##Example
```TCL
################################################################################
# FORMAT_TestFormat.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate format "${NAME}" {
    symbolicname "format_TestFormat"
    description "Format for test purposes."
    !hidden
    version "1"
    suffix "txt"
    type "text"
    mime "text/plain"
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "TestFormat"
    ################################################## Info End
}
```