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

#Describes the special handling of Interfaces as configuration item.

----
##Introduction
Interfaces are used to handle multiple classification of business objects and connections. For a deep instruction see the "MQL Guide" or "Business Modeler Guide" of the "ENOVIA Studio Modeling Platform".

----
##Handled Properties
This interface properties could be handled from !MxUpdate:
 * description
 * hidden flag
 * abstract flag
 * types and relationships where interfaces could be assigned
 * parent interfaces

----
##Steps of the Update Flow

###Cleanup
Following steps are done before the CI update file is executed:
 * set to not hidden
 * set to not abstract
 * reset description
 * remove all assigned types and relationships

###Update
The CI update file is executed. If the TCL procedures "testAttributes" and "testParents" are defined, the attributes of the interface and the parent interfaces are updated.

----
##TCL Procecure "testAttributes"
The TCL procedure "testAttributes" is used to test if all attributes are assigned to the interface. If some attributes are missed, these attributes are assigned to the interface.

###Parameters###
*   **Parameter:** `‑attributes [ATTR_LIST]`
    TCL list of attributes which must be defined on the interface
*   **Parameter:** `‑ignoreattr [NAME]`
    name of the attribute which is ignored (the attribute could be defined or not on the interface); the global parameter `DMWithAttrIgnoreIntAttr` also exists
*   **Parameter:** `‑interface [NAME]`
    name of the interface which is tested
*   **Parameter:** `‑removeattr [NAME]`         
    name of the attribute which is removed if currently assigned to the interface; the global parameter `DMWithAttrRemoveIntAttr` also exists

###Example with Two Attributes
The two attributes "Attribute 1" and "Attribute 2" must be defined on an interface. Within an update the name of the interface is defined in the TCL variable `NAME`.
```TCL
testAttributes -interface "${NAME}" -attributes [list \
    "Attribute 1" \
    "Attribute 2" \
]
```

###Example with One Attribute to Remove
The two attributes "Attribute 1" and "Attribute 2" must be defined on a
interface. If attribute "Remove Attr" exists on the interface, this attribute will be automatically removed. Within an update the name of the interface is defined in the TCL variable `NAME`.
```TCL
testAttributes -interface "${NAME}" -removeattr "Remove Attr" -attributes [list \
    "Attribute 1" \
    "Attribute 2" \
]
```

----
##TCL Procedure "testParents"
The TCL procedure "testParents" is used to define the parent interfaces for an
interface.

###Parameters
*   **Parameter:** `‑interface [NAME]`
    name of the interface which is tested
*   **Parameter:** `‑parents [INTERFACE_LIST]`
    TCL list of parent interfaces which must be defined on the interface

###Example
The interface "ParentInterface" is defined as parent interface. Within an update the name of the interface is defined in the TCL variable `NAME`.
```TCL
testParents -interface "${NAME}" -parents [list \
    "ParentInterface" \
]
```

----
##Parameter Definitions
*   **Name:** `DMWithAttrIgnoreIntAttr`
    **Parameter:** `‑‑ignoreinterfaceattributes [ATTRIBUTE_MATCH`
    Pattern defining the match of attributes which are ignored within the test attributes of interfaces.
*   **Name:** `DMWithAttrRemoveIntAttr`
    **Parameter:** `‑‑removeinterfaceattributes [ATTRIBUTE_MATCH]`
    Pattern defining the match of attributes which are removed if not defined anymore within the test attributes of interfaces.

----
##Explanation of Update Error Codes
Error Code | Description
-----------|------------
10901      | A wrong parameter was given the the called TCL procedure `testParents` which defines the derived interfaces.
10902      | The name of the interface which calls the TCL procedure `testParents` and which is defined within the call as parameter is not equal.
10903      | An interface is already derived from another interface, but within the update this derived interface must be removed. This could end in potentially losing data and so this action is not allowed.
12101      | The given attribute is not defined anymore from TCL procedure `testAttributes` but already assigned to the interface. The attribute is not automatically removed because otherwise potentially data could be lost.
12102      | A wrong parameter was given the called TCL procedure `testAttributes` which defines the assigned attributes for an interface.
12103      | The name of the interface is not the same then defined through the name of the CI file from the called TCL procedure `testAttributes`.

----
##Example
```TCL
################################################################################
# INTERFACE:
# ~~~~~~~~~~
# MxUpdateTestInterface
#
# SYMBOLIC NAME:
# ~~~~~~~~~~~~~~
# interface_MxUpdateTestInterface
#
# DESCRIPTION:
# ~~~~~~~~~~~~
# MxUpdate Test Interface with two attributes, assignable to one type and two
# relationships and one parent interface.
#
# AUTHOR:
# ~~~~~~~
# The MxUpdate Team
################################################################################

mql escape mod interface "${NAME}" \
    description "MxUpdate Test Interface with two attributes, assignable to one type and two relationships and one parent interface." \
    abstract "false" \
    add relationship "MxUpdateTestRelationship1" \
    add relationship "MxUpdateTestRelationship2" \
    add type "MxUpdateTestType"

testParents -interface "${NAME}" -parents [list \
    "MxUpdateTestParentInterface" \
]

testAttributes -interface "${NAME}" -attributes [list \
    "MxUpdateTestAttribute1" \
    "MxUpdateTestAttribute2" \
]
```