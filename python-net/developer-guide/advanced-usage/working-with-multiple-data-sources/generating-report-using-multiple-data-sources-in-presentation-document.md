---
id: generating-report-using-multiple-data-sources-in-presentation-document
url: assembly/python-net/generating-report-using-multiple-data-sources-in-presentation-document
title: Generating Report using Multiple Data Sources in Presentation Document
weight: 3
description: "Generating Report using Multiple Data Sources in Presentation Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: generating report using multiple data sources in presentation document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a report. This report will fetch data from multiple data sources.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Generating Report in Microsoft PowerPoint Document

### Creating a Template

1.  Add a new slide
2.  Add a bullet list at the place where you want it
3.  Save your Document

## Reporting Requirement

As a report developer, you are required to generate a report that fetches data from two different data sources (e:g XML, JSON). Report must show following information:

*   Customer name
*   List of products

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

{{< alert style="warning" >}}There is no way to use an image inside a foreach tag in Microsoft PowerPoint.{{< /alert >}}

**NOTE: There is no way to use images inside a foreach tag in PowerPoint.**

<<foreach \[in customers\]>>**<<\[CustomerName\]>>**

<</foreach\>>

```text
We provide support for the following products:
<<foreach [in products]>><<[ProductName]>>
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}){{< /alert >}}

### Download Template

Get the template from here.

*   [multiple-data-source.odp](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-presentation-document/multiple-data-source.odp)

### Generating the Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("multiple-data-source.odp", "multiple-data-source-report.odp", [
    DataSourceInfo(customers, "customers"),
    DataSourceInfo(products, "products"),
])
```
{{< /tab >}}
{{< tab "multiple-data-source.odp" >}}
{{< tab-text >}}
The following sample file is used in this example: [multiple-data-source.odp](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-presentation-document/multiple-data-source.odp)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-presentation-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-presentation-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "multiple-data-source-report.odp" >}}  
```text
Binary file (ODP, 6 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-presentation-document/generating_the_report/multiple-data-source-report.odp)
{{< /tab >}}
{{< /tabs >}}

## Generating Report in OpenOffice Presentation Document

### Creating the Template

OpenDocument Text (ODT) is a word processing document format which can be used as an alternative to Microsoft Word Document (DOC/DOCX) formats. Since ODT is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODT, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we'll not reinvent the wheel to recreate a template for generating a report in ODT format. Instead, we'll save the existing template to ODT format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

1.  Open existing template we created in previous topic.
2.  Click "File" and select "Save As".
3.  Select "OpenDocument Text" from "Save As Type" drop down.
4.  Click "Save".

### Download Template

Get template from here.
