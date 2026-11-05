---
id: saving-to-html-with-external-resource-files
url: assembly/python-net/saving-to-html-with-external-resource-files
title: Saving to HTML with External Resource Files
weight: 2
description: "Saving to HTML with External Resource Files with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: saving to html with external resource files, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

Since version 19.5, The GroupDocs.Assembly provides a great feature which is saving of external resource files while an assembled document loaded from a non-HTML format is being saved to HTML.

From now on, when saving an assembled document to an HTML file, by default, external resource files are stored to a folder having the same name as the HTML file without extension plus the "\_files" suffix. This folder is located in the same folder as the HTML file. The following example illustrates the scenario. The following code snippet shows the way of API usage:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# The report's pictures and styles are written next to the report
assembler = DocumentAssembler()
assembler.assemble_document("externalresourcefiles.docx", "externalresourcefiles-report.htm",
                            DataSourceInfo("Harbor Lane Provisions", "value"))
```
{{< /tab >}}
{{< tab "externalresourcefiles.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [externalresourcefiles.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/saving-to-html-with-external-resource-files/externalresourcefiles.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "saving-to-html-with-external-resource-files-outputs.zip" >}}  
```text
externalresourcefiles-report.htm (698 bytes)
externalresourcefiles-report_files/Aspose.Words.165b7697-7df9-499c-92f6-dda9068177f6.001.jpeg (2 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/saving-to-html-with-external-resource-files/saving_to_html_with_external_resource_files/saving-to-html-with-external-resource-files-outputs.zip)
{{< /tab >}}
{{< /tabs >}}

In the following example, the default folder used to store HTML resource files is overridden by an explicitly specified folder.

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import os

from groupdocs.assembly import DataSourceInfo, DocumentAssembler, LoadSaveOptions

# Write the report's pictures and styles to another folder
options = LoadSaveOptions()
options.resource_save_folder = os.path.abspath("resources")

assembler = DocumentAssembler()
assembler.assemble_document("externalresourcefiles.docx", "externalresourcefiles-report.htm", options,
                            DataSourceInfo("Harbor Lane Provisions", "value"))
```
{{< /tab >}}
{{< tab "externalresourcefiles.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [externalresourcefiles.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/saving-to-html-with-external-resource-files/externalresourcefiles.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "saving-to-html-with-external-resource-files-2-outputs.zip" >}}  
```text
externalresourcefiles-report.htm (725 bytes)
resources/Aspose.Words.5ece6732-d711-4035-b268-404c3fb6d420.001.jpeg (2 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/saving-to-html-with-external-resource-files/saving_to_html_with_external_resource_files_2/saving-to-html-with-external-resource-files-2-outputs.zip)
{{< /tab >}}
{{< /tabs >}}
