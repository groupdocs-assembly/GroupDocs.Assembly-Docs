---
id: bulleted-list-in-spreadsheet-document
url: assembly/python-net/bulleted-list-in-spreadsheet-document
title: Bulleted List in Spreadsheet Document
weight: 2
description: "Bulleted List in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: bulleted list in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bulleted List report in Spreadsheet Document based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Bulleted List in Microsoft Excel Document

### Creating a Bulleted List

Practising the following steps you can insert Bulleted List in MS Excel 2013.  
Adding bulleted list in Microsoft Excel is different than Microsoft Word. Moreover, there are two ways to apply bulleted list in Microsoft Excel:

*   In-Cell List
*   Multiple-Cell List

Apply the following steps to build the In-Cell template

1.  Add a new Workbook.
2.  Press Insert Tab (at the top-bar).
3.  Add bullet symbol by clicking on Symbol icon.
4.  Save the Document.

### Reporting Requirement

As a report developer, you are required to share the information of the products with the following key requirements:

*   A report must show all the products in a bulleted list format.
*   A Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**In-Cell List**

```text
We provide support for the following products:
<<foreach [in products]>>
-          <<[ProductName]>><</foreach>>
```

**Multiple-Cell List**

```text
We provide support for the following products:
<<foreach [in products]>>-          <<[ProductName]>>
```

close the foreach loop in next column

```text
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Bulleted List Template

Please download the sample Bulleted List document we created in this article:

*   [bulleted-list.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-spreadsheet-document/bulleted-list.ods)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("bulleted-list.ods", "bulleted-list-report.ods", DataSourceInfo(products, "product"))
```
{{< /tab >}}
{{< tab "bulleted-list.ods" >}}
{{< tab-text >}}
The following sample file is used in this example: [bulleted-list.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-spreadsheet-document/bulleted-list.ods)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-spreadsheet-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "bulleted-list-report.ods" >}}  
```text
Binary file (ODS, 6 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-spreadsheet-document/generating_the_report/bulleted-list-report.ods)
{{< /tab >}}
{{< /tabs >}}

## Bulleted List in OpenOffice Spreadsheet Document

### Creating the Template

OpenDocument Spreadsheet (ODS) is a spreadsheet document format which can be used as an alternative to Microsoft Excel Document (XLS/XLSX) formats. Since ODS is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODS, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we'll not reinvent the wheel to recreate a template for generating a 'Bulleted List' report in ODS format. Instead, we'll save the existing template to ODS format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

1.  Open existing template we created in previous topic.
2.  Click "File" and select "Save As".
3.  Select "OpenDocument Spreadsheet" from "Save As Type" dropdown.
4.  Click "Save".

### Download Template

### Generating the Report

### ODS Template and Report in Apache OpenOffice

In order to check compatibility of ODS between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODS template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODS report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
