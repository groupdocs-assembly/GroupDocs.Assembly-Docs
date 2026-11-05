---
id: pie-chart-in-word-processing-document
url: assembly/python-net/pie-chart-in-word-processing-document
title: Pie Chart in Word Processing Document
weight: 1
description: "Pie Chart in Word Processing Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: pie chart in word processing document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Pie Chart report in Word Processing Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Pie Chart in Microsoft Word Document

### Creating a Pie Chart

Please follow below steps to can create Pie Chart in MS Word 2013.

1.  Click in the document where you want to insert the chart, click the "Insert" tab, and then click "Chart" in the illustrations group to open the "Insert Chart" dialog box.
2.  Select "Pie".
3.  Preview "Pie" and press OK to insert the chart and Worksheet template to your document.
4.  Edit the Worksheet with your data to update the chart. See [Chart Data (Excel)]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-word-processing-document.md#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine" >}})
5.  Save the template.

### Reporting Requirement

As a report developer, you are required to share your customers' orders details dynamically with the following key requirements:

*   The report must show information on a Pie Chart.
*   It must indicate customer name with value (price of the orders purchased).
*   The report must be generated in the Word Processing Document.
      
  

{{< alert style="info" >}}See the video demonstration of Pie Chart in MS Word [here](https://www.youtube.com/watch?v=boKpFtW_TGE&list=PL25CTxMCj5vOzsaE9Rwjwd4-OwvdaWmJ8&index=13).{{< /alert >}}

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```text
Total Order Price<<foreach [in customers]>>
<<x [CustomerName]>>
```

#### Chart Data (Excel)

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 219.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">Total Order Price&lt;&lt;y [</span><span style="font-family: Calibri; font-size: 11pt;">Order.Sum</span><span style="font-family: Calibri; font-size: 11pt;">(c =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">c.Price</span><span style="font-family: Calibri; font-size: 11pt;">)]&gt;&gt;</span></p></td></tr><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 219.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt; text-align: right;"><span style="font-family: Calibri; font-size: 11pt;">8.2</span></p></td></tr><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 219.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt; text-align: right;"><span style="font-family: Calibri; font-size: 11pt;">3.2</span></p></td></tr><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 219.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt; text-align: right;"><span style="font-family: Calibri; font-size: 11pt;">1.4</span></p></td></tr><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 219.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt; text-align: right;"><span style="font-family: Calibri; font-size: 11pt;">1.2</span></p></td></tr></tbody></table>
{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: Working with GroupDocs.Assembly Engine.{{< /alert >}}

Download Pie Chart Template

Please download the sample Pie Chart document we created in this article:

*   [pie-chart.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-word-processing-document/pie-chart.docx)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("pie-chart.docx", "pie-chart-report.docx", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "pie-chart.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [pie-chart.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-word-processing-document/pie-chart.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-word-processing-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pie-chart-report.docx" >}}  
```text
Binary file (DOCX, 12 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-word-processing-document/generating_the_report/pie-chart-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Pie Chart in OpenOffice Document

To be investigated.
