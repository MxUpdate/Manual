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

#Describes how to develop MxUpdate Update Deployment Tool

----
##Create MxUpdate Manual
For the PDF manual of MxUpdate the own sub project "mxupdate-manual" exists.


Two different profiles exists which could be activated:

Name of the Profile | Description
--------------------|----------------
`make-pdf`          | Prepares the manual as PDF file.
`release-profile`   | The PDF document is uploaded to Google Code.

The two profiles exists because the `gcupload` plug-in does currently not work together with the `eFaps Wiki plug-in` (which is used to create the PDF manual).

###Generate PDF File
```
mvn clean wikiutil:convert2pdf -P make-pdf
```

###Upload to Google Code
The (not existing) source code is tried to pack, but ignored for the upload. Only the created PDF file is uploaded.
```
mvn gcupload:gcupload -P release-profile
```
