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
The source code of programs are handled as configuration item. The name of the
configuration item file is the same name as they are used within MX.

----
##"Standard" Property and Symbolic Name Handling
All non "standard" properties are removed before the program is updated and the
embedded TCL code is execute. At the end all the "standard" properties
"version", "file date", "application" and "author" are updated (depending on the
used parameters). The "standard" properties "installer" and "original name" are
only set if not already defined.

The symbolic name of the program is the automatically calculated string
`program_[PROGRAM_NAME]`. If the `[PROGRAM_NAME]` includes some spaces
or slashes, they are removed.

----
##Embedded TCL Code
Sometimes some further TCL update code is required, e.g. to define a program
user, or some properties for the program. The MxUpdate Update deployment tool
could handle this within the same program source code. Before the code is
updated in MX, the TCL update code itself will be removed (see parameter
`ProgramTclUpdateNeeded`).

Because all non "standard" properties are removed before the embedded TCL code
is execute, project specific properties could be set by using `add`.

###Start and End Markers
To identify the TCL update code some markers must be defined in the source code.
For the beginning of TCL update code the marker
```TCL
################################################################################
# START NEEDED MQL UPDATE FOR THIS PROGRAM                                     #
################################################################################
```
is used. At the end, the marker
```TCL
################################################################################
# END NEEDED MQL UPDATE FOR THIS PROGRAM                                       #
################################################################################
```
must be defined.

###File Extensions
Embedded TCL update code is only executed for programs with the extensions
".xml", ".xsl", ".xslt", ".mql" and ".tcl". If some embedded TCL update code is
identified for files with other extensions a warning message is shown in the
console.

###Line Prefixes for TCL / MQL Programs
Because e.g. for TCL and MQL programs the embedded TCL update code will be
executed, the line prefix `#` is defined. The line prefix depends on the
file extension (".tcl" for TCL programs and ".mql" for MQL programs).

*Attention! The line prefix must be also defined for the start and end markers!*

###TCL Program Example
So for a TCL program the source code could look like this:
```TCL
#################################################################################
## START NEEDED MQL UPDATE FOR THIS PROGRAM                                     #
#################################################################################
#
#mql mod program "MXPROG.TCL"  \
#    add property "Execute" value "true"
#
#################################################################################
## END NEEDED MQL UPDATE FOR THIS PROGRAM                                       #
#################################################################################
tcl;
eval  {
  .... SOME CODE ....
}
```

###XML Program Example
For XML and XSL(T) files the code could be embedded between start
comment `<!‑‑` and end comment `‑‑>`. So the snippet for a XML program
could like this:
```XML
<!--
   Some Comment...

################################################################################
# START NEEDED MQL UPDATE FOR THIS PROGRAM                                     #
################################################################################

mql mod program "MXPROG.XML"  \
    add property "Extension" value "PDF"

################################################################################
# END NEEDED MQL UPDATE FOR THIS PROGRAM                                       #
################################################################################
-->
```

----
###Parameter Definitions
*   **Name:** `ProgramTclUpdateExtension`
    **Default Value:** `.xml=,.xsl=,.xslt=,.mql=#,.tcl=#`
    Defines the list of all file extensions which could embed TCL update code and depending on the extension the related line prefixes.
*   **Name:** `ProgramTclUpdateMarkEnd`
    **Default Value:** _see the end marker_
    Defines the string to mark the end of embedded TCL update code within program source code.
*   **Name:** `ProgramTclUpdateMarkStart`
    **Default Value:** _see the start marker_
    Defines the string to mark the start of embedded TCL update code within program source code.
*   **Name:** `ProgramTclUpdateNeeded`
    **Parameter:** `‑‑noProgramTclUpdateNeeded`
    **Default Value:** `true`
    Embedded TCL update code within a program is not executed. Instead a warning is shown because of existing TCL update code.
    ***Attention!*** The default value is `true`, but if the parameter is defined the flag will be `false`!
*   **Name:** `ProgramTclUpdateRemoveInCode` 
    **Parameter:** `‑‑noProgramTclUpdateCodeRemove`
    **Default Value:** `true`
    Embedded TCL update code within a MQL program is removed from the code. This means that in MX the code does not include the TCL update code.
    ***Attention!*** The default value is `true`, but if the parameter is defined the flag will be `false`!

The parameters could be changed depending on project needs. For further information see the [Parameter Definition Format](UpdatePropertyFileFormat_ParameterDef.md).
