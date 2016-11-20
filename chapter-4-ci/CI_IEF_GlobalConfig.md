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

#Describes the special handling of IEF Global Config Objects as configuration item.

----
##Introduction
The IEF Global Configuration objects are used to configure integrations and the related mapping between the CAD application and MX.

The configuration item itself is stored as business object. The IEF Global Configuration depends on the used integration. This means that all configuration items are from a type derived from `MCADInteg-GlobalConfig`. So the type of the configuration object is important and must be part of the
file name.

The file name is a concatenation of the global configuration type, the name and revision. As separator 16 underscores are used between the type and name and 8 underscores between name and revision.

If no global configuration type is defined in the file name (e.g. if an upgrade from `emxGerLibUpdate` is done), the default global configuration type `MCADInteg-GlobalConfig` is used.


----
## Syntax
```
mxUpdate globalconfig "${NAME}" "${REVISION}" { [OPTION] }
```
where **`OPTION`** is:
```
    | description DESCRIPTION_STRING
    | current CURRENT_STATE
    | attribute ATTR_NAME ATTR_MULTI_LINE_VALUE
```

----
##Example (Snippet)
```TCL
################################################################################
# IEFGLOBALCONFIG_ECADInteg-GlobalConfig________________MxUpdateIntegrationTest________1.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate globalconfig "${NAME}" "${REVISION}" {
    type "ECADInteg-GlobalConfig"
    description "The global configuration object for MxUpdate integration test."
    current "Exists"
          :
    attribute "IEF-CSELaunchBinaryDetails" ""
    attribute "IEF-CheckObsoleteAcrossRevisions" "false"
    attribute "IEF-CheckUUIDConflict" "FALSE"
    attribute "IEF-CreateVersionObjects" "TRUE"
    attribute "IEF-DerivedOutputParameterObjTypeMapping" ""
    attribute "IEF-DerivedOutputTypeDefaultParameterObjectMapping" ""
          :
}
```
