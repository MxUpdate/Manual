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

#Description of the Key "ParameterDef" within MxUpdate property file.

----
##Introduction

Properties with key "`ParameterDef`" defines additional parameters and default values used from the MxUpdate Deployment Tool.

----
##Sub Keys of "ParameterDef"

The sub keys are defined after the "`ParameterDef`" Key. Following sub keys are interpreted by MxUpdate:

Type                 | Description
---------------------|-------------
CheckMQLCommand      | MQL command to execute which is checked for a containing string.
CheckResultContains  | String which must be contained by the result of the execute MQL command.
Default              | Default value of the parameter.||
ParameterDesc        | Description used for the help of the MxUpdate deployment tool.
ParameterList        | Comma separated list of parameter names (without '-' and '--' prefixes). The parameters are not case sensitive.<p>_If a parameter contains only one single character, one minus '-' is used as prefix. If the parameter name contains more than one character, two minus '--' are used as prefix._</p><p>_If no parameter list is defined, the user could not use the parameter within MxUpdate deployment tool._</p>||
ParameterArgs        | Parameter Argument <p>_Only for parameters from type Integer, List and String could an argument defined._</p>||
Type                 | Defines the type of the parameter. Possible values are <ul><li>Boolean</li> <li>Integer</li> <li>List</li> <li>Map</li> <li>String</li></ul>
Wiki                 | Defines a reference to the description in the Wiki. Multiple references must be separated by a space.

----
##Evaluated Flags
Boolean flags which depends on an existing feature of a MX version could be 
automatically evaluated. To use it a defined MQL command is executed and the 
result is checked if a string is contained.

**Example**: Only if the result of the executed `help attribute` MQL command 
contains the string "resetonrevision", the flag is set to true value.
```
ParameterDef.DMAttrSupportsFlagResetOnRevision.CheckMQLCommand      = help attribute
ParameterDef.DMAttrSupportsFlagResetOnRevision.CheckResultContains  = resetonrevision
```
