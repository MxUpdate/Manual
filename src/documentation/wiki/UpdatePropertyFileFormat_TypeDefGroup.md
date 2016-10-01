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

#Description of the Key "TypeDefGroup" within MxUpdate property file.

----
##Introduction

Properties with key "!TypeDefGroup" defines additional parameters and default values used from the !MxUpdate Deployment Tool.

----
##Sub Keys of "TypeDefGroup"
The sub keys are defined after the "TypeDefGroup" Key. Following sub keys are interpreted by !MxUpdate:

Type          | Description
--------------|-------------------
ParameterDesc | Description used for the help of the !MxUpdate deployment tool.||
ParameterList | Comma separated list of parameter names (without '-' and '--' prefixes). The parameters are not case sensitive.<br/>If a parameter contains only one single character, one minus '-' is used as prefix. If the parameter name contains more than one character, two minus '--' are used as prefix.<br/>If no parameter list is defined, the user could not use the parameter within MxUpdate deployment tool
TypeDefList   | Comma separated list of "[TypeDef](UpdatePropertyFileFormat_TypeDef.md)" names ||

----
##Example
```Properties
    :
TypeDefGroup.UserInterface.ParameterList    = ui,userinterface
TypeDefGroup.UserInterface.ParameterDesc    = Export / Import of user interface administration objects.
TypeDefGroup.UserInterface.TypeDefList      = Channel,Command,Form,Inquiry,Menu,Portal,Table
    :
```
