---
id: common-list-image-in-presentation-document
url: assembly/python-net/common-list-image-in-presentation-document
title: Common List Image in Presentation Document
weight: 3
description: "Common List Image in Presentation Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: common list image in presentation document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common List Image report in Presentation Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Common List in Microsoft PowerPoint Document

### Creating a Common List Image

Please follow below steps to create Common List Template in MS PowerPoint 2013:

1.  Create a new presentation slide.
2.  Add two shapes to hold pictures and name.
3.  Save your Document.

### Reporting Requirement

As a report developer, you are required to represent the information of the customers with the following key requirements:

*   A report must show multiple customers' picture and name.
*   A report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

{{< alert style="warning" >}}There is no way to use an image inside a foreach tag in Microsoft PowerPoint.{{< /alert >}}

```text
<<foreach [in customers]>><<[CustomerName]>>
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Template

Please download the sample Common List document we created in this article:

*   [common-list.odp](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-presentation-document/common-list.odp)
      
  

{{< alert style="warning" >}}Use this template for DB, Dataset, JSON and XML examples also.{{< /alert >}}

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("common-list.odp", "common-list-report.odp", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "common-list.odp" >}}
{{< tab-text >}}
The following sample file is used in this example: [common-list.odp](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-presentation-document/common-list.odp)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-presentation-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "common-list-report.odp" >}}  
```text
Binary file (ODP, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-presentation-document/generating_the_report/common-list-report.odp)
{{< /tab >}}
{{< /tabs >}}

## Common List in OpenOffice Presentation Document

### Creating the Template

OpenDocument Presentation (ODP) is a presentation document format which can be used as an alternative to Microsoft PowerPoint Document (PPT/PPTX) formats. Since ODP is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODP, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we'll not reinvent the wheel to recreate a template for generating a 'Common List' report in ODP format. Instead, we'll save the existing template to ODP format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

1.  Open existing template we created in previous topic.
2.  Click "File" and select "Save As".
3.  Select "OpenDocument Text" from "Save As Type" dropdown.
4.  Click "Save".

### Download Template

### Generating the Report

### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.

*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
