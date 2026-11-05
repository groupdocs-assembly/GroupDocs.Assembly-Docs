---
id: features-overview
url: assembly/python-net/features-overview
title: Features Overview
linkTitle: Features Overview
weight: 1
description: "GroupDocs.Assembly for Python via .NET builds reports from Word, Excel, PowerPoint, OpenDocument, email, HTML, Markdown and text templates, filled with Python dicts and lists, JSON, XML and CSV files, or the tables of other documents: tables, lists, charts, images, barcodes, hyperlinks and more."
keywords: report generation, document assembly, template, data source, python dict, json, xml, csv, document table, table report, list report, chart report, image report, barcode, email report, python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
toc: True
---

GroupDocs.Assembly for Python via .NET generates reports from templates. A template is an ordinary document of one of the [supported formats]({{< ref "assembly/python-net/getting-started/supported-document-formats.md" >}}) whose text holds tags such as `<<[customer.Name]>>` or `<<foreach [o in orders]>>`. Every task follows the same workflow: prepare the data, wrap each data source in a `DataSourceInfo` with the name the template uses, and call `DocumentAssembler.assemble_document()` with the template and the report to write.

## Data sources

Fill a template with:

- **Python data**: dicts, lists, numbers, strings, dates and `Decimal` values, as they are. A dict's keys are read as members (`customer.Name`), a list is a collection to iterate. See [Generate from custom objects]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-from-custom-objects.md" >}}) and [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).
- **JSON, XML and CSV files** through `JsonDataSource`, `XmlDataSource` and `CsvDataSource`, which recognize numbers, booleans and dates in the text. See [Working with simple data sources]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-simple-data-sources/_index.md" >}}).
- **The tables of other documents**: a table of a Word document or a presentation, or a worksheet, as a `DocumentTable`, and several related tables of one document as a `DocumentTableSet`. See [Using documents as data source]({{< ref "assembly/python-net/developer-guide/advanced-usage/using-documents-as-data-source/_index.md" >}}).
- **Database rows**, turned into dicts in Python. See [Generate from a database]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-from-database.md" >}}).
- **Several sources in one report**, each under its own name. See [Working with multiple data sources]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-multiple-data-sources/_index.md" >}}).

## Template syntax

Expressions in tags use a subset of C# syntax that works on any data source: arithmetic, comparisons, string operations, the `Sum`, `Count`, `Average`, `Where`, `OrderBy`, `GroupBy` and other sequence operations, and conditional expressions. Format numbers, dates and text in the tag itself, declare variables, and leave comments in a template. See [Template syntax - part 1]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md" >}}), [part 2]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md" >}}), [Basic template syntax]({{< ref "assembly/python-net/developer-guide/basic-usage/basic-template-syntax.md" >}}) and [Enumeration extension methods]({{< ref "assembly/python-net/developer-guide/advanced-usage/enumeration-extension-methods.md" >}}).

## Reports

- **Tables**: a row per item, with totals, grouping, filtering and ordering, master-detail tables, highlighted rows, alternate content for empty data, merged cells. See [Working with table reports]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-table-reports/_index.md" >}}) and [Generate tables from a collection]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-tables-from-collection.md" >}}).
- **Lists**: bulleted, numbered and multicolored numbered lists, and lists inside a paragraph. See [Generate bullet lists]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-bullet-lists.md" >}}) and [Generate numbered lists]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-numbered-lists.md" >}}).
- **Charts**: pie, bubble, scatter and column charts whose series, points, colors and titles come from the data. See [Working with chart reports: pie]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-reports-pie/_index.md" >}}) and [Working with chart series coloring]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-series-coloring/_index.md" >}}).
- **Images and barcodes**: pictures named by the data, and barcodes generated from it. See [Inserting images dynamically]({{< ref "assembly/python-net/developer-guide/advanced-usage/inserting-images-dynamically.md" >}}) and [Working with barcode image generation]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-barcode-image-generation/_index.md" >}}).
- **Hyperlinks, bookmarks, check boxes and other documents**: links and bookmarks built from data, check box and drop-down values, and whole documents inserted into the report. See [Inserting hyperlinks or bookmarks]({{< ref "assembly/python-net/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/_index.md" >}}), [Set checkbox values dynamically]({{< ref "assembly/python-net/developer-guide/advanced-usage/set-checkbox-values-dynamically.md" >}}) and [Inserting documents dynamically]({{< ref "assembly/python-net/developer-guide/advanced-usage/inserting-documents-dynamically.md" >}}).
- **Email messages**: MSG and EML templates whose sender, recipients, subject and body come from the data. See [Generate email messages]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-email-messages.md" >}}).

## Formats

Templates and reports can be Word processing documents, spreadsheets, presentations, OpenDocument files, emails, HTML, Markdown and plain text. A report is saved in the format of its file extension, or of the format you name with `LoadSaveOptions`, so a Word template can give a PDF or HTML report. See [Supported document formats]({{< ref "assembly/python-net/getting-started/supported-document-formats.md" >}}), [Changing target file format]({{< ref "assembly/python-net/developer-guide/advanced-usage/changing-target-file-format.md" >}}) and [Using Markdown documents]({{< ref "assembly/python-net/developer-guide/advanced-usage/using-markdown-documents.md" >}}).

## Assembly options

- Update fields and recalculate formulas while assembling: see [Updating fields]({{< ref "assembly/python-net/developer-guide/advanced-usage/updating-fields-while-assembling-word-processing-documents.md" >}}) and [Calculate formulas]({{< ref "assembly/python-net/developer-guide/advanced-usage/calculate-formula-while-assembling-spreadsheet-documents.md" >}}).
- Remove the paragraphs that end up empty: see [Removing empty paragraphs]({{< ref "assembly/python-net/developer-guide/advanced-usage/removing-empty-paragraphs.md" >}}).
- Write template errors into the report instead of raising: see [In-line syntax error messages]({{< ref "assembly/python-net/developer-guide/advanced-usage/use-of-in-line-syntax-error-messages-into-templates.md" >}}).
- Allow members the data does not have (`DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS`).

## Loading and saving

Read templates from files or streams and write reports to files or streams, resolve the pictures of an HTML template from a folder of your choice, save an HTML report with its resources in a separate folder, and choose the OOXML compliance level of a Word report. See [Streams vs. file paths]({{< ref "assembly/python-net/developer-guide/basic-usage/streams-vs-file-paths.md" >}}), [Loading and saving with external resource files]({{< ref "assembly/python-net/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/_index.md" >}}) and [Specify OOXML compliance]({{< ref "assembly/python-net/developer-guide/basic-usage/specify-ooxml-compliance.md" >}}).
