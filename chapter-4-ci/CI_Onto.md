<!--
 *
 *  This file is part of MxUpdate <http://www.mxupdate.org>.
 *
 *  MxUpdate is a deployment tool for a PLM platform to handle
 *  administration objects as single update files (configuration item).
 *
 *  Copyright (C) 2008-2017 The MxUpdate Team
 *
 *  The Manual of MxUpdate is licensed under a CC BY-NC-SA 4.0 license
 *  (Creative Commons Attribution-NonCommercial-ShareAlike 4.0 
 *  International 4.0 license).
 *
 *  You should have received a copy of the license along with this
 *  work. If not, see <http://creativecommons.org/licenses/by-nc-sa/4.0/>.
 *
-->

# Onto
MX uses for index searches specific onto-tags configurations. For further information see the MX documentation.

## Syntax Onto Concept
```
mxUpdate ontoconcept "${NAME}" "${REVISION}" { [OPTION] }
```
where **`OPTION`** is:
```
    | type TYPE_NAME
    | description DESCRIPTION_STRING
    | current CURRENT_STATE
    | attribute ATTR_NAME ATTR_MULTI_LINE_VALUE
    | connection ONTO_OWNS_RELATIONSHIP_NAME from TYPE NAME REVISION
```

## Syntax Onto Literal
```
mxUpdate ontoliteral "${NAME}" "${REVISION}" { [OPTION] }
```
where **`OPTION`** is:
```
    | type TYPE_NAME
    | description DESCRIPTION_STRING
    | current CURRENT_STATE
    | attribute ATTR_NAME ATTR_MULTI_LINE_VALUE
    | connection ONTO_OWNS_RELATIONSHIP_NAME from TYPE NAME REVISION
```

## Syntax Onto Ontology
```
mxUpdate ontoontology "${NAME}" "${REVISION}" { [OPTION] }
```
where **`OPTION`** is:
```
    | type TYPE_NAME
    | description DESCRIPTION_STRING
    | current CURRENT_STATE
    | attribute ATTR_NAME ATTR_MULTI_LINE_VALUE
```

## Syntax Onto Property
```
mxUpdate ontoproperty "${NAME}" "${REVISION}" { [OPTION] }
```
where **`OPTION`** is:
```
    | type TYPE_NAME
    | description DESCRIPTION_STRING
    | current CURRENT_STATE
    | attribute ATTR_NAME ATTR_MULTI_LINE_VALUE
    | connection ONTO_OWNS_RELATIONSHIP_NAME from TYPE NAME REVISION
    | connection ONTO_SUB_PROPERTY_RELATIONSHIP_NAME to TYPE NAME REVISION
```

## Example
For example see MX.