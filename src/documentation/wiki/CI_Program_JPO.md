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

#Describes the special handling of JPOs as configuration item.

----
##Introduction
The source code of JPOs are handled as configuration item. The name of the configuration item file is the name as used within MX appended by suffix `_mxJPO.java`. If the JPO name includes points ('.'), this points are interpreted as package name and the name of the file is the text after the last point appended `_mxJPO.java`.

###Example without Package
JPO with name `emxPart` has the configuration item file name `emxPart_mxJPO.java`.

###Example with Package
JPO with name `org.mxupdate.Update` has the file name `Update_mxJPO.java` (in sub directory `org/mxupdate`).

----
##Package Handling of JPOs
Package names of JPOs are not handled like normal Java code.

###Update / Insert JPOs
If a JPO is updated or inserted, the name of the package is set in the front of the JPO file name. The package itself in the JPO source code is removed.

###Extract JPOs
If the JPO is extracted, the MX name of the JPO is used to extract the package name and the file name of the JPO. The code for the package is automatically added to the JPO source code (in the beginning of the source code).

----
##"Standard" Property and Symbolic Name Handling
All non "standard" properties are removed before the JPO is updated and the embedded TCL code is execute. At the end all the "standard" properties "version", "file date", "application" and "author" are updated (depending on the used parameters). The "standard" properties "installer" and "original name" are only set if not already defined.

The symbolic name of the JPO is the automatically calculated string `program_[PROGRAM_NAME]`. If the `[PROGRAM_NAME]` includes some spaces or slashes, they are removed.

----
##Embedded TCL Code
Sometimes some further TCL update code is required, e.g. to define a program user, or some properties for the JPO. The MxUpdate Update deployment tool could handle this within the same JPO source code.

###Start and End Markers
To identify the TCL update code some markers must be defined in the JPO source code. For the beginning of TCL update code the marker
```TCL
################################################################################
# START NEEDED MQL UPDATE FOR THIS JPO PROGRAM                                 #
################################################################################
```
is used. At the end, the marker
```TCL
################################################################################
# END NEEDED MQL UPDATE FOR THIS JPO PROGRAM                                   #
################################################################################
```
must be defined.

Each line of the TCL update code and the markers starts with double slashes '`//`'.

###Example
The following TCL update code defines an extra property "Execute" with the value "true". The code could be added e.g. in the Java file header.
```Java
//################################################################################
//# START NEEDED MQL UPDATE FOR THIS JPO PROGRAM                                 #
//################################################################################
//
//mql mod program "${NAME}"  \
//    add property "Execute" value "true"
//
//################################################################################
//# END NEEDED MQL UPDATE FOR THIS JPO PROGRAM                                   #
//################################################################################
```

----
##Parameter Definitions
*   **Name:** `Compile`
    **Parameter:** `‑‑compile`
    **Default Value:** `false`
    Compiles all updated JPO programs.
*   **Name:** `JPOTclUpdateMarkEnd`
    **Default Value:** _see the end marker_ 
    Defines the string to mark the end of embedded TCL update code within JPO source code.
*   **Name:** `JPOTclUpdateMarkStart`
    **Default Value:** _see the start marker_
    Defines the string to mark the start of embedded TCL update code within JPO source code.
*   **Name:** `JPOTclUpdateNeeded`
    **Parameter:** `‑‑noJPOTclUpdateNeeded`
    **Default Value:** `true`
    Embedded TCL update code within a JPO is not executed. Instead a warning is shown because of existing TCL update code.
    ***Attention!*** The default value is `true`, but if the parameter is defined the flag will be `false`!

The parameters could be changed depending on project needs. For further information see the [Parameter Definition Format](UpdatePropertyFileFormat_ParameterDef.md).
