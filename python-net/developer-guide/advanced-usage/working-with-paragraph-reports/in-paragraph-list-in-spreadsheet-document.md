---
id: in-paragraph-list-in-spreadsheet-document
url: assembly/python-net/in-paragraph-list-in-spreadsheet-document
title: In-Paragraph List in Spreadsheet Document
weight: 2
description: "In-Paragraph List in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-paragraph list in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-Paragraph List report in Spreadsheet Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}

## In-Paragraph List in Microsoft Excel Document

### Creating a In-Paragraph List

Practicing the following steps you can create In-Paragraph List Template in MS Excel 2013.

1.  Add a new Workbook.
2.  Write a sentence, for example "We provide support for the following products:" in a single column.
3.  Save the template.

### Reporting Requirement

As a report developer, you are required to describe about the services you are providing with the following key requirements:

*   A descriptive or informative line like "We provide support for the following products:".
*   Show all the products along with the above sentence.
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
We provide support for the following products:
<<foreach [in products]>><<[IndexOf() != 0 ? ", " : ""]>>
<<[ProductName]>>
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax,expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download In-Paragraph List Template

Please download the sample In-Paragraph List document we created in this article:

*   [in-paragraph-list.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-spreadsheet-document/in-paragraph-list.ods)

### Generating The Report

{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("in-paragraph-list.ods", "in-paragraph-list-report.ods", DataSourceInfo(products, "products"))
```
{{< /tab >}}
{{< tab "in-paragraph-list.ods" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-paragraph-list.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-spreadsheet-document/in-paragraph-list.ods)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-spreadsheet-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-paragraph-list-report.ods" >}}  
```text
Binary file (ODS, 5 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-spreadsheet-document/generating_the_report/in-paragraph-list-report.ods)
{{< /tab >}}
{{< /tabs >}}

## In-Paragraph List in OpenOffice Spreadsheet Document

### Creating the Template

OpenDocument Spreadsheet (ODS) is a spreadsheet document format which can be used as an alternative to Microsoft Excel Document (XLS/XLSX) formats. Since ODS is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODS, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we'll not reinvent the wheel to recreate a template for generating an 'In-Paragraph List' report in ODS format. Instead, we'll save the existing template to ODS format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

1.  Open existing template we created in previous topic.
2.  Click "File" and select "Save As".
3.  Select "OpenDocument Spreadsheet" from "Save As Type" drop down.
4.  Click "Save".

### Download Template

### Generating the Report

### ODS Template and Report in Apache OpenOffice

In order to check compatibility of ODS between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODS template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODS report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
