---
id: pie-chart-in-presentation-document
url: assembly/python-net/pie-chart-in-presentation-document
title: Pie Chart in Presentation Document
weight: 3
description: "Pie Chart in Presentation Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: pie chart in presentation document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Pie Chart report in Presentation Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Pie Chart in Microsoft PowerPoint Document

### Creating a Pie Chart

Please follow below steps to create Pie Chart in MS PowerPoint 2013:

1.  Add a new presentation slide.
2.  Click the "Insert" tab, and then click "Chart" in the illustrations group to open the "Insert Chart" dialog box.
3.  Select "Pie".
4.  Preview "Pie" and press OK to insert the chart and Worksheet template to your document.
5.  Edit the Worksheet with your data to update the chart. See [Chart Data (Excel)]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-presentation-document.md#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine" >}})
6.  Save the template.

### Reporting Requirement

As a report developer, you are required to share your customers' orders details dynamically with the following key requirements:

*   The report must show information on a Pie Chart.
*   It must indicate customer name with value (price of the orders purchased).
*   The report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```text
Total Order Price<<foreach [in customers]>>
<<x [CustomerName]>>
```

#### Chart Data (Excel)

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 219.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">Total Order Price&lt;&lt;y [</span><span style="font-family: Calibri; font-size: 11pt;">Order.Sum</span><span style="font-family: Calibri; font-size: 11pt;">(c =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">c.Price</span><span style="font-family: Calibri; font-size: 11pt;">)]&gt;&gt;</span></p></td></tr><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 219.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt; text-align: right;"><span style="font-family: Calibri; font-size: 11pt;">8.2</span></p></td></tr><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 219.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt; text-align: right;"><span style="font-family: Calibri; font-size: 11pt;">3.2</span></p></td></tr><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 219.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt; text-align: right;"><span style="font-family: Calibri; font-size: 11pt;">1.4</span></p></td></tr><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 219.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt; text-align: right;"><span style="font-family: Calibri; font-size: 11pt;">1.2</span></p></td></tr></tbody></table>
{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Pie Chart Template

Please download the sample Pie Chart document we created in this article:

*   [pie-chart.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-presentation-document/pie-chart.pptx)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("pie-chart.pptx", "pie-chart-report.pptx", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "pie-chart.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [pie-chart.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-presentation-document/pie-chart.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-presentation-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pie-chart-report.pptx" >}}  
```text
Binary file (PPTX, 44 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-presentation-document/generating_the_report/pie-chart-report.pptx)
{{< /tab >}}
{{< /tabs >}}

## Pie Chart in OpenOffice Presentation Document

To be investigated.
