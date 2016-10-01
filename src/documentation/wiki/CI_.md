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

#Describes the methodic how configuration items could be used within MX

----
##Introduction
Currently within a lot of MX projects the existing configuration (attributes, types, also commands etc.) are handled via MQL update scripts. One good example for that are the installation scripts which are delivered with the installation packages of the different centrals.

----
##Configuration Items
As describes in [Wikipedia](http://www.wikipedia.org) the term [Configuration Items](http://en.wikipedia.org/wiki/Configuration_item) refers to the fundamental structural unit of a configuration management system. In MX the fundamental structure unit are e.g. for the data model attributes, types, policies..., for the user interface e.g. commands, menus, web forms and web tables. So the basic idea behind the "Configuration Item" methodic is to store a complete description of a fundamental structure unit in one single file. This means that each file could be handled easily within a source code repository (like [Subversion](http://subversion.tigris.org/) etc.).

Instead of described each versions and a delta (like in the XML update files delivered from MX) the idea behind the method is to describe the target of an administration object. E.g. for a command the HRef, all settings and all properties are described in this file. If the command must be changed a developer could see the complete command description. A modification of the command is for the developer than very easy. If then the command is deployed the existing command in MX is updated to the new target description in the file.

----
##File Names
Each file name of a configuration item has a prefix and a suffix. The suffix itself is always `.mxu`. The prefix depends on the configuration item type (e.g. for a command the prefix `COMMAND_` is used). As an exception from this rule are the [program configuration items](CI_Program_Program.md).

###Encoding Rules
Within MX a configuration item could use some special characters which are not handled from the file system. Therefore this special characters are encoded.
This characters are not encoded:
* numbers
* alphabetic characters (lower and upper case)
* left or right parenthesis
* plus '`+`' or minus '`-`'
* commas '`,`' or points '`.`'
* spaces '` `'
* equals signs '`=`'
* underscores '`_`'

All other characters are converted with the algorithm:
* the "at symbol" '@' will be converted to double at symbol '@@'
* if a character is in the range of 0 and 254 (ASCII character), then the character is converted to a two characters long hexa-decimal code with '@' as prefix (e.g. double quotes '=' is converted to '@22')
* characters greater than 254 are converted to a four characters long hexa-decimal code with '@u' as prefix (e.g. the euro sign '€' is converted to '@u20AC')

----
##Common TCL Procedures
###Logging Procedures
For logging purposes special TCL procedures are defined which maps directly to
them defined in the MxUpdate Update tool. So the logged text is only printed
depending on the used logging level. The TCL procedures are
* `logError TEXT`
* `logWarning TEXT`
* `logInfo TEXT`
* `logDebug TEXT`
* `logTrace TEXT`

###TCL Procedure "puts"
The TCL procedure `puts` is mapped to the above defined TCL procedure
`logDebug`.

----
##Common Parameter Definitions
A lot of parameters for the MxUpdate Update tool could be defined. Some parameters could as default only defined within the property file.

###Symbolic Names
The parameters are used to control the behavior related to symbolic names. Symbolic names are used within MX for referencing administration objects so that the real name could be changed without changing the code where the administration object is referenced.
*   **Name:** `RegisterSymbolicNames`
    **Default Value:** `eServiceSchemaVariableMapping.tcl`
    Defines the name of the program where all administration objects are registered with symbolic names (except that the `Installer` property is set).

###File Header
A file header is written for all CI files. The parameter `{0}` is automatically replaced by the file name.
*   **Name:** `ExportFileHeader`
    **Default Value:**   `################################################################################`
`# {0}`
`#`
`#            This file describes the target of a Configuration Item.`
`################################################################################`
    Header used for each exported CI file.

###Properties for Admin Objects
For admin object following specific properties exists:

* `MxUpdate File Date` stores the date of the CI file. It is used to check if the file is changed since last call. It helps to improve the performance (see also the MxUpdate usage).
* `MxUpdate Sub Path` stores the path between the 'root' CI path and the CI file. The property is from the import always updated and used from the export to write the file in the correct sub directory.
* `installer` is defined at the first installation of the CI object. The value is not changed afterwards anymore.
* `installed date` is defined at the first installation of the CI object. The value is not changed afterwards anymore.

To handle the installer, the following properties are defined:

*   **Name:** `DefaultInstaller`
    **Parameter:** `--defaultinstaller INSTALLERNAME`
    **Type:** String
    **Default Value:** `The MxUpdate Team`
    Defines the default name of installer which is defined as property / attribute on administration objects. The value is only used for the installer on the administration objects if no installer is in the update script or as parameter defined.
*   **Name:** `Installer`
    **Parameter:** `--installer INSTALLERNAME`
    **Type:** String
    Defines the installer for administration objects. The default installer name and existing installer names in update scripts are overwritten.


####Info Properties
Some properties for admin object are more for information similar e.g. to the @author header property for Java. This properties can be written together inside a specific area in front of all other properties. They are surrounded with comments.

To use this feature, the info properties are configured with parameters.

*   **Name:** `ExportInfoPropsList`
    **Type:** List
    **Default Value:** `author,original name,application,version`
    Defines the name of properties which are used for information. They are written between two comment lines in front of all other properties.
*   **Name:** `ExportInfoPropsTextEnd`
    **Type:** String
    **Default Value:** `################################################## Info Start`
    Comment of the start line after which all information properties are listed.
*   **Name:** `ExportInfoPropsTextStart`
    **Type:** String
    **Default Value:** `################################################## Info End`
    Comment of the end line after the last information property is listed.

####Example
```tcl
mxUpdate type "${NAME}" {
    description ""
    !hidden
    ################################################## Info Start
    property "original name" value "MXUPDATE_Test_ype"
    property "version" value "R15"
    ################################################## Info End
    property "Write Acess" value "FALSE"
}
```

----
##Explanation of Common Update Error Codes
Error Code | Description
-----------|------------
60301      | The JPO caller program `org.mxupdate.update.util.JPOCaller` is called without any required arguments.
60302      | The JPO caller program `org.mxupdate.update.util.JPOCaller` is called with no correct argument defining the case.
90602      | The file name is not correct defined and could not be converted back to a configuration item name. The exception could occur within updates.
