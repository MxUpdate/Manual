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

#Describes the special handling of IEF EBOM Sync Config Objects as configuration item.

----
##Introduction
The IEF EBOM Sync Configuration objects are used to configure EBOM sync's.

The configuration item itself is stored as business object. The IEF EBOM Sync Configuration depends on the used integration. This means that all configuration items are from a type derived from `IEF-EBOMSyncConfig`. So the type of the EBOM Sync Configuration object is important and must be part of the file name.

The file name is a concatenation of the EBOM Sync Configuration type, the name and revision. As separator 16 underscores are used between the type and name and 8 underscores between name and revision.


----
## Syntax
```
mxUpdate ebomsyncconfig "${NAME}" "${REVISION}" { [OPTION] }
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
# IEFEBOMSYNC_ECAD-EBOMSyncConfig________________MxUpdateEBOMSyncTest________-.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate ebomsyncconfig "${NAME}" "${REVISION}" {
    type "ECAD-EBOMSyncConfig"
    description "The EBOM sync configuration object for MxUpdate integration test."
    current "Exists"
          :
    attribute "IEF-EBOMSync-AssignPartToMajor" "FALSE"
    attribute "IEF-EBOMSync-DrawingRelationInfo" ""
    attribute "IEF-EBOMSync-FailOnNotFindingMatchingPart" "TRUE"
    attribute "IEF-EBOMSync-GenerateCollapsedEBOM" "TRUE"
    attribute "IEF-EBOMSync-NewPartRevision" "1"
    attribute "IEF-EBOMSync-ObjectAttrMapping" ""
          :
}
```
