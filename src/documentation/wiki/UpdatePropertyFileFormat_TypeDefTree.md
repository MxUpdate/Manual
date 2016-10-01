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

#Description of the Key "TypeDefTree" within MxUpdate property file.

----
##Introduction
Properties with key "TypeDefTree" defines the type definition tree for the Eclipse plug-in. The type definition tree "`All`" must exists and defines which type definition trees are shown within the Eclipse plug-in.

----
##Sub Keys of "TypeDefTree"
The sub keys are defined after the "TypeDefTree" Key. Following sub keys are
interpreted by MxUpdate:

Type               | Description*
-------------------|--------------
Label              | Label used from the the Eclipse plug-in.
SubTypeDefTreeList | Comma separated list of child type definition tree names.
TypeDefList        | Comma separated list of "[TypeDef](UpdatePropertyFileFormat_TypeDef.md)" names.

----
##Example
```
TypeDefTree.All.Label                   =
TypeDefTree.All.SubTypeDefTreeList      = DataModel,Integration,Program,User,UserInterface
TypeDefTree.All.TypeDefList             =
    :
TypeDefTree.User.Label                  = User
TypeDefTree.User.SubTypeDefTreeList     = Association,Group,Person,PersonAdmin,Role
TypeDefTree.User.TypeDefList            = Association,Group,Person,PersonAdmin,Role
    :
TypeDefTree.Person.Label                = Person
TypeDefTree.Person.SubTypeDefTreeList   =
TypeDefTree.Person.TypeDefList          = Person
    :
```