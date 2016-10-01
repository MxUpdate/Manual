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
 * view program
 * edit program
 * print program
 * properties

----
##Steps of the Update Flow

###Cleanup
Following steps are done before the TCL update file is executed:
 * set to not hidden
 * reset description, version, suffix, mime type, file type
 * remove view / edit / print program
 * remove all assigned properties

###Update
The TCL update file is executed.

----
##Parameter Definitions
No further parameters are defined.

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

mql escape mod format "${NAME}" \
    description "Format for test purposes." \
    !hidden \
    version "1" \
    suffix "txt" \
    type "text" \
    mime "text/plain" \
    view "View Program" \
    edit "Edit Program" \
    print "Print Program"
}}}
```