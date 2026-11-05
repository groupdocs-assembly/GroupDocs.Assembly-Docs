---
id: loading-of-template-documents-from-html-with-resources
url: assembly/python-net/loading-of-template-documents-from-html-with-resources
title: Loading of template documents from HTML with resources
weight: 1
description: "Loading of template documents from HTML with resources with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: loading of template documents from html with resources, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

GroupDocs.Assembly provides a great feature which is loading of HTML template documents referencing external resource files to be assembled and saved to non-HTML formats. 

Since version 19.5, when loading an HTML document from a file, its containing folder is used as a base URI to resolve external resource files' relative URIs to absolute ones by default as shown in the following example. The following code snippet shows the way of API usage:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# The template's pictures are read from the template's own folder
assembler = DocumentAssembler()
assembler.assemble_document("externalresourcefiles.htm", "externalresourcefiles-report.docx",
                            DataSourceInfo("Harbor Lane Provisions", "value"))
```
{{< /tab >}}
{{< tab "externalresourcefiles.htm" >}}
{{< tab-text >}}
The following sample file is used in this example: [externalresourcefiles.htm](/assembly/python-net/_sample_files/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/loading-of-template-documents-from-html-with-resources/externalresourcefiles.htm)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "image001.jpg" >}}
{{< tab-text >}}
The following sample file is used in this example: [image001.jpg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/loading-of-template-documents-from-html-with-resources/image001.jpg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "externalresourcefiles-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/loading-of-template-documents-from-html-with-resources/loading_of_template_documents_from_html_with_resources/externalresourcefiles-report.docx)
{{< /tab >}}
{{< /tabs >}}

The following code snippet shows the default folder used to resolve external resource files' relative URIs are overridden by an explicitly specified folder.

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import os

from groupdocs.assembly import DataSourceInfo, DocumentAssembler, LoadSaveOptions

# Read the template's pictures from another folder
options = LoadSaveOptions()
options.resource_load_base_uri = os.path.abspath("ExternalResourceFiles")

assembler = DocumentAssembler()
assembler.assemble_document("externalresourcefiles.htm", "externalresourcefiles-report.docx", options,
                            DataSourceInfo("Harbor Lane Provisions", "value"))
```
{{< /tab >}}
{{< tab "externalresourcefiles.htm" >}}
{{< tab-text >}}
The following sample file is used in this example: [externalresourcefiles.htm](/assembly/python-net/_sample_files/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/loading-of-template-documents-from-html-with-resources/externalresourcefiles.htm)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "ExternalResourceFiles/image001.jpg" >}}
{{< tab-text >}}
The following sample file is used in this example: [ExternalResourceFiles/image001.jpg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/loading-of-template-documents-from-html-with-resources/ExternalResourceFiles/image001.jpg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "externalresourcefiles-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/loading-of-template-documents-from-html-with-resources/loading_of_template_documents_from_html_with_resources_2/externalresourcefiles-report.docx)
{{< /tab >}}
{{< /tabs >}}
