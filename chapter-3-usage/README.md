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

#Usage of the MxUpdate Update Deployment Tool.

----
##Introduction
After the !MxUpdate Update Deployment Tool is [installed](UpdateInstallation.md), the tool could be used via MQL console. Three different "modes" exists:
* export
* update (import / create)
* delete

The parameter names depends on the configured [properties](UpdatePropertyFileFormat.md) which could be project specific. To get an overview over all parameter call
```
exec prog MxUpdate --help
```
to get all parameters with arguments and short description.

----
##Export Configuration Items
To export configuration items parameter `‑‑export` (short `‑e`) must be defined. The export path must be defined with `‑‑path`. At minimum one path must be defined. Because the export must know where to export the configuration items, only one path at maximum could be defined.
With the other parameters the configuration item types with matching names are defined.

This default configuration could defined project specific (see [Configuration of the Parameter Definitions](UpdatePropertyFileFormat_ParameterDef.md))

###Examples
####Export all Configuration Items
```
exec prog MxUpdate --export --path C:\Temp\DBSchema --all *
```

####Export all JPOs
```
exec prog MxUpdate --export --path C:\Temp\DBSchema --jpo *
```

####Export all JPOs except JPOs starting with org
```
exec prog MxUpdate --export --path C:\Temp\DBSchema --jpo * --ignorejpo org*
```

----
##Update Configuration Items
To export configuration items parameter `‑‑update` (short `-u`) must be defined. Depending on a defined parameter `‑‑path` two cases exists:
* If at minimum one path is defined with parameter `‑‑path` the `<MATCH>` arguments are patterns used to evaluate matching names names without prefix and suffix.
* If no path parameter is defined, the `<MATCH>` arguments are defined as file names. A defined asterisk '`*`' is interpreted as file wild card. 

###'Update is Required' Check
An update of an existing object must not be done always. The default configuration is, that an update is done always.
*   **Name:** `UpdateCheckFileDate`
    **Parameter:** `‑‑checkfiledate`
    Check if an update is required by comparing the last modified date of the file against the value of the file date property.

###Further Configurations
*   **Name:** `DefaultApplication`
    **Parameter:** `‑‑defaultapplication <APPLICATIONAME>`
    Defines the default name of application which is defined as property / attribute on administration objects. The value is only used for the application on the administration objects if no application is in the update script or as parameter defined. (Default 'Unknown')
*   **Name:** `DefaultAuthor`
    **Parameter:** `‑‑defaultauthor <AUTHORNAME>`
    Defines the default name of author which is defined as property / attribute on administration objects. The value is only used for the author on the administration objects if no author is in the update script or as parameter defined. (Default 'The MxUpdate Team')
*   **Name:** `DefaultInstaller`
    **Parameter:** `‑‑defaultinstaller <INSTALLERNAME>`
    Defines the default name of installer which is defined as property / attribute on administration objects. The value is only used for the installer on the administration objects if no installer is in the update script or as parameter defined.
    The default value is 'The MxUpdate Team'.
*   **Name:** `Application`
    **Parameter:** `‑‑application <APPLICATIONAME>`
    Defines the application for administration objects. The default application and application author in the update script is overwritten.
*   **Name:** `Author`
    **Parameter:** `‑‑author <AUTHORNAME>`
    Defines the author for administration objects. The default author and the author in the update script is overwritten.
*   **Parameter:** `‑‑installer <INSTALLERNAME>`
    Defines the installer for administration objects. The default installer name and existing installer names in update scripts are overwritten.

----
##Delete Configuration Items
To export configuration items parameter `‑‑update` (short `‑u`) must be defined. The path of update files which are checked must be defined with parameter `‑‑delete`. All other parameter defines the matching administration objects. 
