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

#Describes the special handling of Pages as configuration item.

----
##Introduction
Pages are typically not used from MX. For a page a mime type typ could be defined. A page is handled like an [inquiry](CI_UI_Inquiry.md).

----
##Handled Page Properties
This page properties could be handled from MxUpdate:

Property    | Written            | Default Value | Kind
------------|--------------------|---------------|----
uuid        | if defined         | empty         | string
description | always             | empty string  | multi-line-string
hidden      | if ***true***      | ***false***   | flag
mime type   | always             | empty string  | string
content     | if defined         | empty string  | multi-line-string
properties  | if defined         | empty list    | list of values and referenced admin objects

----
## Syntax
```
mxUpdate page "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | description DESCRIPTION_STRING
    | [!]hidden
    | mime MIME_STRING
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
    | content CONTENT_STRING
```

For better reading, the code **`CONTENT_STRING `** itself is automatically exported with new line, code content and new line. The import trims all trailing new lines and spaces.

----
##Example
```tcl
################################################################################
# PAGE:
# ~~~~~
# MxUpdate_Test.html
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mxUpdate page "${NAME}" {
    description "MxUpdate test page."
    mime "text/html"
    content "
<html>
    <head><title>Title</title></head>
    <body>
        <h1>Test</h1>
    </body>
</html>
"
}
```