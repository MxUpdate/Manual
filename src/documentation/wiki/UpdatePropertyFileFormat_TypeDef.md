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

#Description of the Key "TypeDef" within MxUpdate property file.

---
##Introduction

Properties with key "TypeDef" defines all existing administration types which could be imported and exported with the MxUpdate Deployment Tool.

---
##Sub Keys of "TypeDef"

The sub keys are defined after the "TypeDef" Key. Following sub keys are interpreted by MxUpdate:

Type                    | Description
------------------------|--------------
AdminSuffix             | Suffix for admin administration objects<br/>E.g. for web tables `system` must be defined.
AdminType               | Name of the type for admin administration objects.
BusIgnoreAttributes     | Comma separated list of ignored attributes for business administration objects.
BusPolicy               | Policy for business administration objects. With this policy new business objects are created.
BusRelsBoth             | Comma separated list of to / from relationships for business administration objects
BusRelsFrom             | Comma separated list of from relationships for business administration objects.
BusRelsTo               | Comma separated list of to relationships for business administration objects.
BusType                 | Type for business administration objects.
BusTypeDerived          | If set to `true` business objects are using types which are derived from the defined business type. The default value is `false`.
BusVault                | Vault for business administration objects. Business objects are created in this vault.
FileMatchLast           | Defines that a match must be done at last (after a file does not match any other "TypeDef" definition); value must set to `true`.<br/>E.g. if no file prefix and file suffix is defined, a match must be done as last. Otherwise a file matches always.
FilePath                | File path used to export.
FilePrefix              | Prefix used for file names.
FileSuffix              | Suffix used for file names.
JPO                     | Defines the name of the JPO which implements the export / import.
OrderNo                 | Defines the order number within an update. If no order number is defined, the update is done after all other updates.
ParameterDesc           | Description of the parameter used in the help.
ParameterDescOpposite   | Description of the opposite parameters used in the help.<br/>Opposite parameters are used to define matches file names which must be ignored.
ParameterList           | Comma separated list of parameters. The parameters are not case sensitive. If a parameter contains only one single character, one minus '-' is used as prefix. If the parameter name contains more than one character, two minus '--' are used as prefix.<br/><br/>**Example:**<br/>`TypeDef.Policy.ParameterList = p,pol,policy`<br/>So for policies three parameters are defined:<br/>`-p`<br/>`--pol`<br/>`--policy`</p>
ParameterListOpposite   | Comma separated list of opposite parameters. The parameters are not case sensitive. The list is defined in the same way as the ParameterList sub key.
TextLogging             | Text used as logging entry.
TextTitle               | Title entry in the MxUpdate file.
Icon                    | Path to the icon used from the !MxUpdate Eclipse plug-in.
Wiki                    | Name of the Wiki file used to reference.
