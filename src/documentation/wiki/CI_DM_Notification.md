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

#Describes the special handling of Notifications as configuration item.

----
##Introduction
The notification objects are used from the generic email utility to define the subject, text and recipients of notifications (emails). The generic email utility is described in the "Business Process Services Administrator's Guide" (Live Collaboration Admin).

The notification object itself is internally stored in MX as business object from type "Notification" with policy "Business Rule" in vault "eService Administration".

----
## Syntax
```
mxUpdate notification "${NAME}" "${REVISION}" { [OPTION] }
```
where **`OPTION`** is:
```
    | description DESCRIPTION_STRING
    | current CURRENT_STATE
    | attribute ATTR_NAME ATTR_MULTI_LINE_VALUE
```

----
##Example
```TCL
################################################################################
# NOTIFICATION_TestNotification________TestRevision.mxu
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate notification "${NAME}" "${REVISION}" {
    description "Notification object for test purposes."
    current "Active"
    attribute "Attachments" ""
    attribute "Body HTML" ""
    attribute "Body Text" "Test Body"
    attribute "Dynamic Bcc List" ""
    attribute "Dynamic Cc List" ""
    attribute "Dynamic To List" ""
    attribute "Filter" ""
    attribute "From Agent" "${USER}"
    attribute "Preprocess JPO" ""
    attribute "Registered Suite" "MxUpdate"
    attribute "Reply To" ""
    attribute "Static Bcc List" ""
    attribute "Static Cc List" ""
    attribute "Static To List" ""
    attribute "Subject Text" "Text Subject"
    attribute "URL Suffix" ""
}
```

