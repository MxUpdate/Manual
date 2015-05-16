#Describes the special handling of all Programs as configuration item.

----
##Introduction
Currently following program objects are supported from !MxUpdate:
  * [JPO programs](CI_Program_JPO.md)
  * [MQL programs](CI_Program_MQL.md)
  * [Page objects](CI_Program_Page.md)

----
## Encoding Work-Around for old MX versions
Old MX versions exports two closing square brackets '`]]`' not encoded. This
means that the XML parser used internally from !MxUpdate failed. In this case
following error message appears:

    org.xml.sax.SAXParseException: The content of elements must consist of well-formed character data or markup.

MxUpdate has an implemented work-around that corrects the encoding of the XML
export. To use this work-around parameter *!ProgramUseEncodingWorkAround* must
be activated (see [Program Parameter Definitions](CI_Program.md#Parameter_Definitions)).

----
##Parameter Definitions
*   **Name:** `ProgramUseEncodingWorkAround`
    **Default Value:** `false`
    The encoding work around for old MX versions is used.

The parameters could be changed depending on project needs. For further information see the [Parameter Definition Format](UpdatePropertyFileFormat_ParameterDef.md).
