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

#Describes the special handling of administration persons as configuration item.

----
##Introduction
Administration Persons are persons in MX for which no related business object exists (unlike "standard" persons). Good examples for such persons are the already standard installed "guest" and "creator" account. If the related person business object does not exists an user could not login into the web application. This means that such persons typically used only for administration.

----
##Handled Administration Persons Properties
This Administration Persons properties could be handled from MxUpdate:

Property      | Written    | Default Value | Kind
--------------|------------|---------------|----
uuid          | if defined | empty         | string
symbolic name | if defined | empty list    | list of symbolic name strings
comment       | always     | empty string  | multi-line-string
active        | always     | ***true***    | flag
trusted       | always     | ***false***   | flag
hidden        | always     | ***false***   | flag
access        | always     | ***all***     | ***all***, or list of access items  
admin         | always     | ***all*** if type contains ***business*** or ***system***, otherwise ***none*** | ***all***, or list of admin access items   
email         | always     | ***false***   | flag
icon mail     | always     | ***true***    | flag
address       | always     | empty string  | string
email address | always     | empty string  | string
fax           | always     | empty string  | string
full name     | always     | empty string  | string
phone         | always     | empty string  | string
products      | always     | empty list    | list of products
type          | if defined | ***application*** and ***full*** | type item
vault         | if defined | empty string  | string of vault name
application   | if defined | empty string  | string of application name
site          | if defined | empty string  | string of site name
groups        | if defined | empty list    | list of groups
roles         | if defined | empty list    | list of roles
properties    | if defined | empty list    | list of values and referenced admin objects


----
## Syntax
```
mxUpdate person "${NAME}" { [OPTION] }
```
where **`OPTION`** is:
```
    | uuid UUID_STRING
    | symbolicname SYMBOLICNAME_STRING
    | comment DESCRIPTION_STRING
    | [!]active
    | [!]trusted
    | [!]hidden
    | access | all              |
    |        | {ACCESS_ITEM...} |
    | admin | all                    |
    |       | {ADMIN_ACCESS_ITEM...} |
    | [!]email
    | [!]iconmail
    | address ADDRESS_STRING
    | emailaddress EMAIL_STRING
    | fax FAX_STRING
    | fullname FULLNAME_STRING
    | phone PHONE_STRING
    | vault VAULT_NAME
    | application APPLICATION_NAME
    | site SITE_NAME
    | type  | {TYPE_ITEM...}
    | group GROUP_NAME
    | role ROLE_NAME
    | product {PRODUCT_ITEM...}
    | property NAME [to ADMIN_TYPE ADMIN_NAME] [value VALUE_STRING]
```
where **`TYPE_ITEM`** is:
```
    | application
    | full
    | business
    | system
```

----
##NOT Handled Person Properties
The password and the password expired flag are NOT handled from MxUpdate.

###Password
The password could not be read from the MX database. They are hashed and only the user itself knows the password (for better understanding see the Internet about hashed password).

Also from security point of view the password should not be added in the CI file, because the CI file is handled typically from a repository (and who knows all the persons which could read the repository?).

###Password Expired Flag
The password expired flag is used e.g. if the user must change his password while login. Because this is used only temporary, the flag itself is not supported from MxUpdate.

----
##Parameter Definitions
*   **Name:** `UserIgnoreWSO4Persons`
    **Parameter:** `--ignorePersonWorkspaceObjects [PERSON_MATCH]`, `‑‑ignoreWorkspaceObjectsForPerson [PERSON_MATCH]`, `‑‑ignorewso4person [PERSON_MATCH]`
    Defines the match of persons for which workspace objects are not handled (neither exported nor updated).
    Attention! A workspace object defined in the TCL update file are not ignored and will be created!
*   **Name:** `UserPersonIgnoreProducts`
    **Parameter:** `‑‑ignorePersonProducts [PERSON_MATCH]`
    Defines the match of persons for whom the manage of products is ignored. This means that the products for given matching person not managed anymore from the MxUpdate Update tool and must (could be) managed e.g. in separate MQL update scripts.
*   **Name:** `UserPersonIgnoreWantsEmail`
    **Parameter:** `‑‑ignorePersonWantsEmail [PERSON_MATCH]`
    Defines the match of persons for whom the 'wants email' - flag is not handled from the MxUpdate Update tool. They could be managed then e.g. in separate MQL update scripts.
*   **Name:** `UserPersonIgnoreWantsIconMail`
    **Parameter:** `‑‑ignorePersonWantsIconMail [PERSON_MATCH]`
    Defines the match of persons for whom the 'wants icon mail' - flag is not handled from the MxUpdate Update tool. They could be managed then e.g. in separate MQL update scripts.

----
##Example
```tcl
################################################################################
# PERSONADMIN_MxUpdate_Person
#
#            This file describes the target of a Configuration Item.
################################################################################

mxUpdate person "${NAME}" {
    symbolicname "person_MxUpdate_Person"
    description "Administration person for test purposes." 
    !hidden 
    !neverexpires 
    access all 
    admin {} 
    disable email 
    enable iconmail 
    address "" 
    email "" 
    fax "" 
    fullname "" 
    phone "" 
    vault ""
    type {application full}
    product {CPF}
    ################################################## Info Start
    property "author" value "The MxUpdate Team"
    property "original name" value "MxUpdate_Person"
    ################################################## Info End
}
```
