---
id: numbered-list-in-spreadsheet-document
url: assembly/python-net/numbered-list-in-spreadsheet-document
title: Numbered List in Spreadsheet Document
weight: 2
description: "Numbered List in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: numbered list in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Numbered List report in Spreadsheet Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Numbered List in Microsoft Excel Document

### Creating a Numbered List

Practising the following steps you can create Numbered List Template in MS Excel 2013.  
You can create two kinds of Numbered List in Microsoft Excel.

*   In-cell List
*   Multiple-cell List

Apply the following steps to build the In-Cell template

1.  Add a new Workbook.
2.  Write a sentence, for example "We provide support for the following products:" in a single cell and add syntax there.
3.  Save the template.

### Reporting Requirement

As a report developer, you are required to describe the services you are providing with the following key requirements:

*   The report must show the products in numbered list.
*   The report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**In-cell List**

```text
"We provide support for the following products:<<foreach [in products]>>
<<[NumberOf()]>>.         <<[ProductName]>><</foreach>>"
```

**Multiple-cell List**

```text
<<foreach [in products]>><<[NumberOf()]>>.         <<[ProductName]>>
```

and close foreach in next column,

```text
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

Download Numbered List Template

Please download the sample Numbered List document we created in this article:

*   [numbered-list.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-spreadsheet-document/numbered-list.ods)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("numbered-list.ods", "numbered-list-report.ods", DataSourceInfo(products, "products"))
```
{{< /tab >}}
{{< tab "numbered-list.ods" >}}
{{< tab-text >}}
The following sample file is used in this example: [numbered-list.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-spreadsheet-document/numbered-list.ods)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-spreadsheet-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "numbered-list-report.ods" >}}  
```text
Binary file (ODS, 6 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-spreadsheet-document/generating_the_report/numbered-list-report.ods)
{{< /tab >}}
{{< /tabs >}}

## Numbered List in OpenOffice Spreadsheet Document

### Creating the Template

OpenDocument Spreadsheet (ODS) is a spreadsheet document format which can be used as an alternative to Microsoft Excel Document (XLS/XLSX) formats. Since ODS is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODS, please visit [Wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we'll not reinvent the wheel to recreate a template for generating an 'Numbered List' report in ODS format. Instead, we'll save the existing template to ODS format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

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
