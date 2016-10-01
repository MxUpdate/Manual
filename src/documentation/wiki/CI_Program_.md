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

#Describes the special handling of all Programs as configuration item.

----
##Introduction
Currently following program objects are supported from !MxUpdate:
  * [EKL / External / Java / MQL programs](CI_Program_Program.md)
  * [Page objects](CI_Program_Page.md)

----
## Encoding Work-Around for old MX versions
Old MX versions exports two closing square brackets '`]]`' not encoded. This
means that the XML parser used internally from !MxUpdate failed. In this case
following error message appears:

    org.xml.sax.SAXParseException: The content of elements must consist of well-formed character data or markup.

MxUpdate has an implemented work-around that corrects the encoding of the XML
export. To use this work-around parameter *!ProgramUseEncodingWorkAround* must
be activated (see [Program Parameter Definitions](CI_Program.md#Parameter_Definitions)).

----
##Parameter Definitions
*   **Name:** `ProgramUseEncodingWorkAround`
    **Default Value:** `false`
    The encoding work around for old MX versions is used.

The parameters could be changed depending on project needs. For further information see the [Parameter Definition Format](UpdatePropertyFileFormat_ParameterDef.md).
