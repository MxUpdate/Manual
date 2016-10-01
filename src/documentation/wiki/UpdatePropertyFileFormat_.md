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

#Overview over the Property File Format.

##Introduction
With the property file the "behavior" of MxUpdate Update is described. With the property file the allowed parameters, descriptions, administration types etc. are defined. In a project a specific property file could be used (see [Installation](UpdateInstallation.md)).


##Format
In the property file an entry is a concatenation of a key, a name and a sub key with the following format:
```
<KEY>.<NAME>.<SUBKEY>
```
The keys and their related sub keys are described in:
* [Key "Mode"](UpdatePropertyFileFormat_Mode.md)
* [Key "ParameterDef"](UpdatePropertyFileFormat_ParameterDef.md)
* [Key "PropertyDef"](UpdatePropertyFileFormat_PropertyDef.md)
* [Key "TypeDef"](UpdatePropertyFileFormat_TypeDef.md)
* [Key "TypeDefGroup"](UpdatePropertyFileFormat_TypeDefGroup.md)
