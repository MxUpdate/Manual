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

#Description of the Key "Mode" within MxUpdate property file.

##Introduction
Properties with key "Mode" defines the allowed parameters for the four different modes (delete, export, help and import).

##Four Different Modes
The MxUpdate deployment tool knows four different modes. The modes are identified by special wording.

Type   | Description
-------|-------------
DELETE | Defines the delete mode
EXPORT | Defines the export mode
HELP   | Defines the help mode
IMPORT | Defines the import / update mode

##Sub Keys of "Mode"
The sub keys are defined after the "Mode" Key. Following sub keys are interpreted by MxUpdate:

Type          | Description
--------------|--------
ParameterDesc | Description used for the help of the MxUpdate deployment tool.
ParameterList | Comma separated list of parameter names (without '-' and '--' prefixes)<p>_If a parameter contains only one single character, one minus '-' is used as prefix. If the parameter name contains more than one character, two minus '--' are used as prefix._</p><p>_If no parameter list is defined, the user could not use the parameter within MxUpdate deployment tool._</p>
