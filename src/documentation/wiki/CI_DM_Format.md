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
This format properties could be handled from !MxUpdate:
 * description
 * hidden flag
 * version
 * file suffix
 * file type
 * mime type
 * view program (legacy, in new MX version not supported anymore)
 * edit program (legacy, in new MX version not supported anymore)
 * print program (legacy, in new MX version not supported anymore)
 * properties

----
##Parameter Definitions
*   **Name:** ```DMFormatSupportsPrograms ```
    **Value:** ```true```if the MQL command ```help format```includes the string ```view```
    If the flag is true, format supports view, edit and print programs. The flag is only needed for legacy MX versions.

----
##Syntax

    mxUpdate format NAME {
        description DESCRIPTION_STRING
        [!]hidden
        version VERSION_STRING
        suffix VERSION_STRING
        type TYPE_STRING
        mime MIME_STRING
        (view PROGRAM)
        (edit PROGRAM)
        (print PROGRAM)
        property NAME [to TYPE NAME] [value VALUE_STRING]
    }
    
**Hint:** Programs for ```view```, ```edit``` and ```print``` are legacy. Newer MX versions does not support anymore this feature.

----
##Example
```TCL
################################################################################
# FORMAT:
# ~~~~~~~
# TestFormat
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# format_TestFormat
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# Format for test purposes.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mxUpdate format "${NAME}" {
    description "Format for test purposes."
    !hidden
    version "1"
    suffix "txt"
    type "text"
    mime "text/plain"
}
```