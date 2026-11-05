---
id: home
url: assembly/python-net
title: GroupDocs.Assembly for Python via .NET
linkTitle: GroupDocs.Assembly for Python
weight: 1
description: "Native Python library that builds reports and documents from Word, Excel, PowerPoint, email, HTML, Markdown and text templates filled with Python dicts, JSON, XML, CSV or document tables, on Windows, Linux, and macOS. No Microsoft Office required."
keywords: GroupDocs.Assembly, Python via .NET, report generation, document automation, document assembly, template, mail merge, python dict, JSON, XML, CSV, DOCX, XLSX, PPTX, PDF, email, on-premise, Windows, Linux, macOS, python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: true
toc: True
structuredData:
    showOrganization: true
---

<img src="/logo/128x128/groupdocs-assembly-python.png" alt="groupdocs-assembly-python-net-home" align="left" style="width:110px; margin: 0 30px 30px 0"/>

<img src="https://img.shields.io/pypi/v/groupdocs-assembly-net?label=GroupDocs.Assembly%20PyPI" alt="PyPI package">
<img src="https://img.shields.io/pypi/dm/groupdocs-assembly-net?label=pypi%20downloads" alt="PyPI downloads">

{{< button style="primary" link="https://releases.groupdocs.com/assembly/python-net/release-notes/" >}} <svg class="gdoc-icon gdoc-product-doc__btn-icon"><use xlink:href="/img/groupdocs-stack.svg#document"></use></svg> Release notes {{< /button >}}
{{< button style="primary" link="https://pypi.org/project/groupdocs-assembly-net/" >}} {{< icon "gdoc_download" >}} Download from PyPI {{< /button >}}
{{< button style="primary" link="https://products.groupdocs.app/assembly/family" >}} <svg class="gdoc-icon gdoc-product-doc__btn-icon"><use xlink:href="/img/groupdocs-stack.svg#app"></use></svg> Online app {{< /button >}}

[GroupDocs.Assembly for Python via .NET](https://products.groupdocs.com/assembly/python-net/) is a document automation and report generation API: it fills templates - ordinary Word, Excel, PowerPoint, OpenDocument, email, HTML, Markdown and text documents with tags such as `<<[customer.Name]>>` - with your data, and saves the result in the template's format or another, such as PDF. The data can be Python dicts and lists, JSON, XML and CSV files, or the tables of other documents, with no MS Office or OpenOffice installation required.

<div style="clear:left"></div>

## Quick example

```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Fill the tags of hello-world.docx, such as <<[customer.Name]>>, with a dict and save a PDF
customer = {"Name": "Quayside Bistro", "Product": "Harbor Blend whole bean coffee"}
DocumentAssembler().assemble_document("hello-world.docx", "hello-world.pdf", DataSourceInfo(customer, "customer"))
```

## Features

- **Python data as it is**: Dicts and lists, with their numbers, strings, dates and `Decimal` values, are read by the template's tags as objects: `customer.Name`, `o.OrderDate.Month`.
- **Data files and documents**: JSON, XML and CSV files, and the tables of Word, Excel and PowerPoint documents, as data sources.
- **Template syntax**: Expressions, formatting and data bands, with `Sum`, `Where`, `GroupBy`, `OrderBy` and other sequence operations written in the template.
- **Every kind of report**: Tables, lists, charts, images, barcodes, hyperlinks, bookmarks, check boxes and inserted documents.
- **Email**: Messages whose sender, recipients, subject and body come from data.
- **Any output format**: Save a report in the template's format, or a Word template as PDF, HTML, XPS, Markdown and more.
- **Assembly options**: Update fields and formulas, remove empty paragraphs, and write template errors into the report instead of raising.

## Supported File Formats

GroupDocs.Assembly works with more than 40 file formats: it fills templates of 35 of them and saves reports to all of them. For a complete list, see the [full list of supported formats]({{< ref "assembly/python-net/getting-started/supported-document-formats.md" >}}).

- **Word Processing** (DOC, DOCX, DOCM, DOT, DOTX, DOTM, RTF, ODT, OTT, TXT, MD)
- **Spreadsheets** (XLS, XLSX, XLSM, XLSB, XLT, XLTX, XLTM, ODS)
- **Presentations** (PPT, PPTX, PPTM, PPS, PPSX, PPSM, POT, POTX, POTM, ODP, OTP)
- **Email** (MSG, EML, EMLX)
- **Web** (HTML, MHTML)
- **Reports also as** (PDF, XPS, OXPS, TIFF, SVG, PS, PCL, XAML, EPUB)

## Getting Started

To get started, refer to the [System Requirements]({{< ref "assembly/python-net/getting-started/system-requirements.md" >}}), [Supported Document Formats]({{< ref "assembly/python-net/getting-started/supported-document-formats.md" >}}), [Installation]({{< ref "assembly/python-net/getting-started/installation.md" >}}), and [Quick Start Guide]({{< ref "assembly/python-net/getting-started/quick-start-guide.md" >}}) sections for setup instructions.

## Developer Guide

For practical code examples and explanations of the template-and-data workflow, see the [Developer Guide]({{< ref "assembly/python-net/developer-guide/_index.md" >}}) section. It covers the template syntax, every data source, and table, list, chart, image, barcode and email reports in each document format.

## AI Agents and LLM Integration

The package ships an `AGENTS.md` reference for AI coding assistants, and the documentation is available to them through an MCP server and as machine-readable text. See [AI agents and LLM integration]({{< ref "assembly/python-net/agents-and-llm-integration.md" >}}).

## Technical Support

If you experience any issues or have suggestions, please refer to the [Technical Support]({{< ref "assembly/python-net/technical-support.md" >}}) topic. This topic provides multiple support channels tailored to your needs.
