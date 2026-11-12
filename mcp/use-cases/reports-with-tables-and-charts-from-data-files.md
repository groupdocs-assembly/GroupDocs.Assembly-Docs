---
id: mcp-uc-reports-with-tables-and-charts-from-data-files
url: assembly/mcp/use-cases/reports-with-tables-and-charts-from-data-files
title: How to build a report with tables and charts from a CSV or spreadsheet with an AI agent
linkTitle: Reports from data files
weight: 3
description: "Build a report with tables, totals and a chart from a CSV or Excel file with an AI agent over MCP, locally: the template defines the layout and the chart, the data file supplies the numbers."
keywords: report from CSV AI agent, generate report with charts from Excel, chart from data template, Word report from spreadsheet MCP, PowerPoint chart from data
productName: GroupDocs.Assembly MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to build a report with tables and charts from a CSV or spreadsheet with an AI agent"
        description: "Build a report with tables, totals and a chart from a CSV or Excel file with an AI agent over MCP, locally: the template defines the layout and the chart, the data file supplies the numbers."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Assembly MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "Build the Q3 sales report from sales.xlsx as a PDF, and the chart slide from the same data."
---

Run the GroupDocs.Assembly MCP server locally, point your agent at a spreadsheet or CSV, and it produces the report your template defines — the rows, the total, the best performer, and a chart — without drawing a single table itself:

```bash
GROUPDOCS_MCP_STORAGE_PATH=$(pwd)/templates dnx GroupDocs.Assembly.Mcp --yes
```

> Build the Q3 sales report from sales.xlsx as a PDF, and the chart slide from the same data.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "assembly/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## Prerequisites

* The server registered in your AI client — [quick start]({{< ref "assembly/mcp/getting-started/_index.md" >}}).
* A report template with a table row that repeats, and — for a chart — a PowerPoint, Word or Excel template whose chart carries the tags. On Linux and macOS with `dnx`, presentation templates (the chart slide here) need `libgdiplus` ([Linux install]({{< ref "assembly/net/mcp/linux-installation.md" >}})); Word and Excel templates do not, and the Docker image has everything.

## Data in, report out

```text
sales.xlsx (table 1: Region, Quarter, Revenue)
     |
     +-- assemble_document  template sales-report.docx  --> table rows,
     |                                                      total, best region
     '-- assemble_document  template sales-chart.pptx   --> column chart

sales-chart.pptx, as designed in PowerPoint:
  chart title   Revenue by region<<foreach [r in sales]>><<x [r.Region]>>
  series name   Revenue<<y [r.Revenue]>>
after assembly:
  categories    North    South    East    West
  Revenue       182000   146500   98250   211900
```

The table template:

```text
row 1 (header):  Region | Quarter | Revenue (EUR)
row 2 (repeats): <<foreach [r in sales]>><<[r.Region]>> | <<[r.Quarter]>>
                 | <<[r.Revenue]>><</foreach>>
Total revenue: <<[sales.Sum(r => r.Revenue)]>> EUR
Best region: <<[sales.OrderByDescending(r => r.Revenue).First().Region]>>
```

## What the agent sees

Captured from server 26.11.0 (the evaluation note that opens each response is trimmed):

```text
-> get_document_info {"file":{"filePath":"sales.xlsx"}}
<- { "dataKind": "table", "data": { "tableCount": 1, "tables": [
     { "number": 1, "columns": [ "Region", "Quarter", "Revenue" ] } ] } }

-> assemble_document {"template":{"filePath":"sales-report.docx"},
     "data":{"filePath":"sales.xlsx"},"format":"pdf"}
<- Assembled 'sales-report.docx' with 'sales.xlsx' (table 1 (3 column(s):
   Region, Quarter, Revenue) as 'sales') as PDF
   Saved to: …/sales-report_assembled.pdf

-> assemble_document {"template":{"filePath":"sales-chart.pptx"},
     "data":{"filePath":"sales.xlsx"}}
<- Assembled 'sales-chart.pptx' with 'sales.xlsx' (table 1 (3 column(s):
   Region, Quarter, Revenue) as 'sales') as PPTX
   Saved to: …/sales-chart_assembled.pptx

-> assemble_document {"template":{"filePath":"sales-report.docx"},
     "data":{"filePath":"sales.csv"},
     "outputName":"sales-report-from-csv.docx"}
<- Assembled 'sales-report.docx' with 'sales.csv' (CSV with a header row
   as 'sales') as DOCX
```

The report lists North, South, East and West with their revenue, **Total revenue: 638650 EUR** and **Best region: West**. The chart came out with the four regions as categories and 182000, 146500, 98250 and 211900 as the series. The same template took the CSV unchanged, and summed its numbers just like the workbook's: the CSV report also reads **Total revenue: 638650 EUR**.

## How the chart tags work

Design the chart with placeholder data, then put the tags **in the chart's text**, not in a table. The chart on this page is a PowerPoint chart:

* the chart **title** opens the loop and names the category: `Revenue by region<<foreach [r in sales]>><<x [r.Region]>>`;
* each **series name** names its value: `Revenue<<y [r.Revenue]>>`.

The engine replaces the placeholder data with one point per record and removes the tags. Word and Excel charts are filled by the same engine; Excel has its own rules for series names. Details and more chart types: the library's [template syntax]({{< ref "assembly/net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md" >}}).

## Expected result

A PDF or Word report and a chart slide whose numbers match the data file, in seconds. Licensed, no evaluation line.

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| The chart still shows the placeholder data | the tags are not in the chart title / series names | move them into the chart's own text |
| A column is not found | the first row is data, not headers | `hasHeaders: false`, and refer to columns by position |

## FAQ

**Can the model draw the chart instead?** It can describe one; it cannot put a native, editable chart in your deck. The template's chart is a real PowerPoint/Word/Excel chart that people can restyle.

**Which table does it read from a workbook with several sheets?** Table 1 by default; `dataTable: 2` picks the second. `get_document_info` lists them.

**Can the output be Excel?** Yes — an XLSX template with tags in its cells. Unlicensed, it gains an evaluation worksheet.

## Add to your CLAUDE.md or AGENTS.md

Agents follow project instructions about *when* to use a tool. Paste this into the instruction file your agent reads (`CLAUDE.md`, `AGENTS.md`, `.github/copilot-instructions.md`, `.cursorrules`):

```text
For reports from ./data/*.xlsx or *.csv, call get_document_info on the data,
then assemble_document with the report template in ./templates and data as a
file. Never compute or retype the numbers yourself; quote totals from the output.
```

## Honest limits

* **Evaluation mode:** every generated document starts with an *Evaluation Only* line, workbooks gain a worksheet, and e-mail templates lose their HTML body. [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}).
* **`<<[name]>>`, not `{{name}}`:** other engines' placeholders stay in the output as text.
* **Templates are trusted input:** image and document tags load the paths and URLs their expressions return.
* **Dates:** write them as `"2026-11-12T00:00:00"` and format them in the template; a date-only string can shift by a day on machines east of UTC.

## Related

* [Generate documents with AI agents]({{< ref "assembly/mcp/use-cases/generate-documents-with-ai-agents.md" >}})
* [One document per record (mail merge)]({{< ref "assembly/mcp/use-cases/one-document-per-record-mail-merge.md" >}})
* [Inspect and fix a template]({{< ref "assembly/mcp/use-cases/inspect-and-fix-a-template.md" >}})
* [From notes or email to a document]({{< ref "assembly/mcp/use-cases/build-a-document-from-data-the-agent-extracted.md" >}})
* [Reports from repository data]({{< ref "assembly/mcp/use-cases/generate-reports-from-repository-data.md" >}})
* [On-premise deployment]({{< ref "assembly/mcp/use-cases/on-premise-document-generation.md" >}})
* [Tools reference]({{< ref "assembly/mcp/tools-reference/_index.md" >}}) · [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}) · [Troubleshooting & FAQ]({{< ref "assembly/mcp/troubleshooting-faq.md" >}})
* Questions: [Assembly forum](https://forum.groupdocs.com/c/assembly/15)

## Read more

* [The chart comes from the template, the numbers come from the data](https://blog.groupdocs.com/assembly/reports-with-tables-and-charts-from-csv-ai-agent-mcp/) — the same scenario on the GroupDocs blog, with worked examples and the trade-offs.

