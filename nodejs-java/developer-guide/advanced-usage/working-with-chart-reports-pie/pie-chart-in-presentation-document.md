---
id: pie-chart-in-presentation-document
url: assembly/nodejs-java/pie-chart-in-presentation-document
title: Pie Chart in Presentation Document
weight: 3
description: "Generate a pie chart report in a PowerPoint presentation from JSON data using GroupDocs.Assembly for Node.js via Java."
keywords: pie chart, powerpoint, pptx, chart, json, node.js, javascript
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
{{< alert style="info" >}}In this article, we use GroupDocs.Assembly for Node.js via Java to generate a pie chart report in a PowerPoint presentation.{{< /alert >}}

## Pie chart in a Microsoft PowerPoint document

### Creating a pie chart

To create a pie chart in PowerPoint:

1.  Add a new slide.
2.  On the **Insert** tab, click **Chart**.
3.  Select **Pie** and click **OK**. PowerPoint inserts the chart and opens a worksheet with its data.
4.  Edit the chart title and the worksheet as described in [Adding syntax](#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine).
5.  Save the template.

### Reporting requirement

As a report developer, you need to show managers' contract prices with the following requirements:

*   The report must show the information on a pie chart.
*   Each slice must show a manager's name and the total price of the manager's contracts.
*   The report must be generated as a presentation.

### Data source

Save the managers and their contracts as `managers.json`:

```json
[
  { "Name": "John Smith", "Contracts": [ { "Price": 1200000 }, { "Price": 750000 }, { "Price": 350000 } ] },
  { "Name": "Tony Anderson", "Contracts": [ { "Price": 650000 }, { "Price": 550000 } ] },
  { "Name": "July James", "Contracts": [ { "Price": 350000 }, { "Price": 250000 } ] }
]
```

### Adding syntax to be evaluated by GroupDocs.Assembly engine

#### Chart title

The `foreach` tag iterates over the managers, and the `x` tag defines the category (slice) name. The tags are removed from the title in the report.

```
Total Contract Price<<foreach [in managers]>><<x [Name]>>
```

#### Chart data (Excel)

In the chart's worksheet, put the `y` tag into the series name. It defines the value of each slice. The category cells (A–D) can contain any placeholder values: the engine replaces them with data.

|   | Total Contract Price`<<y [Contracts.sum(c => c.Price)]>>` |
| --- | --- |
| A | 8.2 |
| B | 3.2 |
| C | 1.4 |
| D | 1.2 |

The template uses [contextual object member access](/assembly/nodejs-java/template-syntax-part-1-of-2/#using-contextual-object-member-access): `Name` and `Contracts` refer to the members of the current manager.

### Download the pie chart template

Download the sample files used in this article:

*   [pie-chart-template.pptx](/assembly/nodejs-java/_sample_files/developer-guide/pie-chart-in-presentation-document/pie-chart-template.pptx)
*   [managers.json](/assembly/nodejs-java/_sample_files/developer-guide/pie-chart-in-presentation-document/managers.json)

### Generating the report

```javascript
'use strict';

const groupdocs = require('@groupdocs/groupdocs.assembly');

// "managers" is the data source name used in the chart title
const dataSource = new groupdocs.JsonDataSource("managers.json");
const dataSourceInfo = new groupdocs.DataSourceInfo(dataSource, "managers");

const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument("pie-chart-template.pptx", "pie-chart-report.pptx", dataSourceInfo);

process.exit(0);
```

{{< alert style="warning" >}}
In evaluation mode, GroupDocs.Assembly truncates text read from presentations, so template tags in PowerPoint templates may break and assembly fails. [Apply a license](/assembly/nodejs-java/evaluation-limitations-and-licensing/) (a free temporary license is enough) to run this example.
{{< /alert >}}

### Result

The generated [pie-chart-report.pptx](/assembly/nodejs-java/_sample_files/developer-guide/pie-chart-in-presentation-document/pie-chart-report.pptx) contains a pie chart titled "Total Contract Price" with three slices:

| Manager | Total contract price |
| --- | --- |
| John Smith | 2300000 |
| Tony Anderson | 1200000 |
| July James | 600000 |
