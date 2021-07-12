---
id: introducing-groupdocs-assembly-for-java
url: assembly/java/introducing-groupdocs-assembly-for-java
title: Introducing GroupDocs.Assembly for Java
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
## Introduction to GroupDocs.Assembly for Java

GroupDocs.Assembly for Java is a Java API engine designed to generate documents based on templates. In essence, the engine accepts a template document and some data, assembles data with the template document as per syntax defined by the template document and then, generates the output document in the template's format or in the specified output format. Since GroupDocs.Assembly for Java can generate documents based on a data source, essentially it serves two purposes: Document Automation and Report Generation.

### Document Automation Concept

As per wikipedia, Document Automation can be described as:

> **Document automation** (also known as **document assembly**) is the design of systems and [workflows](https://en.wikipedia.org/wiki/Workflow) that assist in the creation of [electronic documents](https://en.wikipedia.org/wiki/Electronic_document). These include logic-based systems that use segments of pre-existing text and/or data to assemble a new document. This process is increasingly used within certain industries to assemble legal documents, contracts and letters. Document automation systems can also be used to automate all conditional text, variable text, and data contained within a set of documents.
> 
> Automation systems allow companies to minimize data entry, reduce the time spent proof-reading, and reduce the risks associated with human error. Additional benefits include: time and financial savings due to decreased paper handling, document loading, storage, distribution, postage/shipping, faxes, telephone, labor and waste.

For more information, please visit: [https://en.wikipedia.org/wiki/Document\_automation](https://en.wikipedia.org/wiki/Document_automation)

### Report Generation Concept

As per wikipedia, Report Generation can be described as:

> A **report generator** is a computer program whose purpose is to take data from a source such as a database, XML stream or a spreadsheet, and use it to produce a document in a format which satisfies a particular human readership.
> 
> Report generation functionality is almost always\[[citation needed](https://en.wikipedia.org/wiki/Wikipedia:Citation_needed)\] present in [database systems](https://en.wikipedia.org/wiki/Database_systems), where the source of the data is the database itself. It can also be argued that report generation is part of the purpose of a [spreadsheet](https://en.wikipedia.org/wiki/Spreadsheet). Standalone report generators may work with multiple data sources and export reports to different document formats.

For more information, please visit: [https://en.wikipedia.org/wiki/Report\_generator](https://en.wikipedia.org/wiki/Report_generator)

## Supported Document Formats

GroupDocs.Assembly for Java is capable to recognize and load multiple document formats in memory and populate these templates with the assigned data source. Therefore, you can create your templates in any of the supported document formats. The initial version of GroupDocs.Assembly supports word processing documents including Microsoft Word documents, spreadsheet documents including Microsoft Excel Workbooks and presentation documents including Microsoft PowerPoint Presentations. The future releases of GroupDocs.Assembly will be supporting more document formats and the [supported document formats]({{< ref "assembly/java/getting-started/supported-document-formats.md" >}}) section will be updated periodically whenever more document formats are supported in the future releases.

## Supported Output File Formats Depending on Input File Formats

The following table shows which output file formats are supported by GroupDocs.Assembly depending on input file formats:

| Input File Formats (from left to right) and Output File Formats (top down) | Word Processing (DOC, DOCX, DOCM, DOT, DOTX, DOTM, WordprocessingML, RTF, ODT, OTT) | Spreadsheet (XLS, XLSX, XLSM, XLTX, XLTM, XLSB, SpreadsheetML, ODS) | Presentation (PPT, PPTX, PPTM, PPS, PPSX, PPSM, POTX, POTM, ODP) | Email (EML, EMLX, MSG) | HTML and Plain Text |
| --- | --- | --- | --- | --- | --- |
| Word Processing (DOC, DOCX, DOCM, DOT, DOTX, DOTM, WordprocessingML, RTF, ODT, OTT) | Supported | Not Supported | Not Supported | Supported | Supported |
| Spreadsheet (XLS, XLSX, XLSM, XLTX, XLTM, XLSB, SpreadsheetML, ODS) | Not Supported | Supported | Not Supported | Not Supported | Not Supported |
| Presentation (PPT, PPTX, PPTM, PPS, PPSX, PPSM, POTX, POTM, ODP) | Not Supported | Not Supported | Supported | Not Supported | Not Supported |
| Email (EML, EMLX, MSG) | Not Supported | Not Supported | Not Supported | Supported | Not Supported |
| HTML, PDF, XPS, TIFF | Supported | Supported | Supported | Supported | Supported |
| MHTML | Supported | Supported | Not Supported | Supported | Supported |
| Plain Text, XAML, OpenXPS, EPUB, SVG, PS, PCL | Supported | Not Supported | Not Supported | Supported | Supported |

## Supported Template Syntax

Essentially, the GroupDocs.Assembly for Java engine supports LINQ but it does not support the actual LINQ syntax (LINQ extension method analogues are named using lower camel case). Developers can enjoy many benefits including short and concise reporting syntax and binding to any type of supported data source including business objects. For more information about the supported LINQ based syntax, please visit [Template Syntax](/pages/createpage.action?spaceKey=GDDR&title=Template+Syntax+-+Part+1+of+2). In future, [Mustache](https://mustache.github.io/mustache.5.html) template support is also planned.

## Supported Data Sources

GroupDocs.Assembly for Java supports the following data sources:

*   Database
*   XML
*   OData
*   JSON
*   Custom Java Objects

Furthermore, GroupDocs.Assembly for Java support various Data Manipulation features. For more information, please visit [Data Sources]({{< ref "assembly/java/getting-started/features-overview.md#data-sources" >}}).

## Technical Support Channels

### Product Support Forums

The main channel of the Technical Support is [Product Support Forums](http://groupdocs.com/Community/Forums/Default.aspx). Post your question in the Forum and it will be answered within a few hours. Please try to report one issue per thread with all details required to reproduce the issue.

### Sales and License Related Technical Queries

For sales and License related technical queries please visit the [GroupDocs.Purcahse Froum](http://groupdocs.com/Community/forums/groupdocs.purchase/10/showforum.aspx). Please note that GroupDocs.Purchase is a private forum and will require you to sign up with [groupdocs.com](http://www.groupdocs.com) before you can view this forum.
