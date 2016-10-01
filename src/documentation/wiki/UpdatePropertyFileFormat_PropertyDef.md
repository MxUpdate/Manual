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

#Description of the Key "PropertyDef" within MxUpdate property file.

---
##Introduction

Properties with key "PropertyDef" defines the mapping to name of the MX properties used for admin administration objects and also the mapping to name of MX attributes used for business administration objects.

---
##Sub Keys of "PropertyDef"

Type          | Description
--------------|-------------
AttributeName | Name of the used attribute for business object administration objects
PropertyName  | Name of the property for admin administration objects


---
##Used MxUpdate Properties

Name          | Description
--------------|-------
Application   | Name of application which has installed the configuration item.
Author        | Name of the author of the configuration item.
FileDate      | Date of the last modified of the file which defines the configuration item.
InstalledDate | Date of the first installation of the configuration item.
Installer     | First installer of the configuration item.
OriginalName  | Original name of the configuration name (e.g. if the configuration name was renamed).
Version       | Version of the configuration item.
