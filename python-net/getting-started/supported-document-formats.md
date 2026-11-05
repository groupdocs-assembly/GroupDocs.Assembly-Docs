---
id: supported-document-formats
url: assembly/python-net/supported-document-formats
title: Supported Document Formats
weight: 4
description: "GroupDocs.Assembly for Python via .NET fills templates of Word, Excel, PowerPoint, OpenDocument, email, HTML, Markdown and text formats, more than 40 in all, and saves reports to them and to PDF, XPS, TIFF, SVG, EPUB and more."
keywords: DOCX, DOC, RTF, ODT, XLSX, XLS, ODS, PPTX, PPT, ODP, MSG, EML, HTML, MD, TXT, PDF, XPS, supported formats, template formats, report formats, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
toc: True
---
The following tables contain the file formats supported by GroupDocs.Assembly for Python via .NET. A **template** of any of these formats can be loaded and filled with data. The **report** is saved in the format of its file extension, or of the format named by `LoadSaveOptions(FileFormat....)`; which report formats a template can be saved to depends on its family, as the last table shows.

## Platform notes

The package runs the same engine on every platform, so the tables below hold on Windows, Linux and macOS, with these exceptions:

- **Presentations on Linux and macOS need libgdiplus.** Without it no presentation template (PPT, PPTX, ODP and the others) can be filled: the call raises "The type initializer for 'Gdip' threw an exception". Word processing, spreadsheet, email, HTML and text templates do not need it. See [System Requirements]({{< ref "assembly/python-net/getting-started/system-requirements.md" >}}).
- **On Linux, a presentation cannot be saved as TIFF** ("Not implemented"); save it as PDF instead.
- **Text and HTML templates should start with a UTF-8 byte order mark.** A text or HTML template without one, that holds only ASCII characters, is read as an ANSI document, and the report is written in the Windows-1252 code page on every platform: "Café" becomes a single byte that a UTF-8 reader cannot show. With the mark the report is UTF-8. The sample templates of this documentation have it.

{{< table-filter placeholder="Start typing to find file format" forumUrl="https://forum.groupdocs.com/c/assembly/15">}}

## Word Processing

| Format | Description | Template | Report |
| --- | --- | --- | --- |
| [DOC](https://docs.fileformat.com/word-processing/doc/) | Microsoft Word 97-2003 Document | ✔ | ✔ |
| [DOT](https://docs.fileformat.com/word-processing/dot/) | Microsoft Word 97-2003 Template | ✔ | ✔ |
| [DOCX](https://docs.fileformat.com/word-processing/docx/) | Office Open XML Document | ✔ | ✔ |
| [DOCM](https://docs.fileformat.com/word-processing/docm/) | Office Open XML Document, macro-enabled | ✔ | ✔ |
| [DOTX](https://docs.fileformat.com/word-processing/dotx/) | Office Open XML Template | ✔ | ✔ |
| [DOTM](https://docs.fileformat.com/word-processing/dotm/) | Office Open XML Template, macro-enabled | ✔ | ✔ |
| [RTF](https://docs.fileformat.com/word-processing/rtf/) | Rich Text Format | ✔ | ✔ |
| [ODT](https://docs.fileformat.com/word-processing/odt/) | OpenDocument Text | ✔ | ✔ |
| [OTT](https://docs.fileformat.com/word-processing/ott/) | OpenDocument Text Template | ✔ | ✔ |
| [TXT](https://docs.fileformat.com/word-processing/txt/) | Plain text | ✔ | ✔ |
| [MD](https://docs.fileformat.com/word-processing/md/) | Markdown | ✔ | ✔ |

## Spreadsheet

| Format | Description | Template | Report |
| --- | --- | --- | --- |
| [XLS](https://docs.fileformat.com/spreadsheet/xls/) | Microsoft Excel 97-2003 Workbook | ✔ | ✔ |
| [XLT](https://docs.fileformat.com/spreadsheet/xlt/) | Microsoft Excel 97-2003 Template | ✔ | ✔ |
| [XLSX](https://docs.fileformat.com/spreadsheet/xlsx/) | Office Open XML Workbook | ✔ | ✔ |
| [XLSM](https://docs.fileformat.com/spreadsheet/xlsm/) | Office Open XML Workbook, macro-enabled | ✔ | ✔ |
| [XLTX](https://docs.fileformat.com/spreadsheet/xltx/) | Office Open XML Workbook Template | ✔ | ✔ |
| [XLTM](https://docs.fileformat.com/spreadsheet/xltm/) | Office Open XML Workbook Template, macro-enabled | ✔ | ✔ |
| [XLSB](https://docs.fileformat.com/spreadsheet/xlsb/) | Excel Binary Workbook | ✔ | ✔ |
| [ODS](https://docs.fileformat.com/spreadsheet/ods/) | OpenDocument Spreadsheet | ✔ | ✔ |

## Presentation

| Format | Description | Template | Report |
| --- | --- | --- | --- |
| [PPT](https://docs.fileformat.com/presentation/ppt/) | Microsoft PowerPoint 97-2003 Presentation | ✔ | ✔ |
| [PPS](https://docs.fileformat.com/presentation/pps/) | Microsoft PowerPoint 97-2003 Slide Show | ✔ | ✔ |
| [POT](https://docs.fileformat.com/presentation/pot/) | Microsoft PowerPoint 97-2003 Template | ✔ | ✔ |
| [PPTX](https://docs.fileformat.com/presentation/pptx/) | Office Open XML Presentation | ✔ | ✔ |
| [PPTM](https://docs.fileformat.com/presentation/pptm/) | Office Open XML Presentation, macro-enabled | ✔ | ✔ |
| [PPSX](https://docs.fileformat.com/presentation/ppsx/) | Office Open XML Slide Show | ✔ | ✔ |
| [PPSM](https://docs.fileformat.com/presentation/ppsm/) | Office Open XML Slide Show, macro-enabled | ✔ | ✔ |
| [POTX](https://docs.fileformat.com/presentation/potx/) | Office Open XML Presentation Template | ✔ | ✔ |
| [POTM](https://docs.fileformat.com/presentation/potm/) | Office Open XML Presentation Template, macro-enabled | ✔ | ✔ |
| [ODP](https://docs.fileformat.com/presentation/odp/) | OpenDocument Presentation | ✔ | ✔ |
| [OTP](https://docs.fileformat.com/presentation/otp/) | OpenDocument Presentation Template | ✔ | ✔ |

## Email

| Format | Description | Template | Report |
| --- | --- | --- | --- |
| [MSG](https://docs.fileformat.com/email/msg/) | Microsoft Outlook Message | ✔ | ✔ |
| [EML](https://docs.fileformat.com/email/eml/) | E-mail Message (MIME) | ✔ | ✔ |
| [EMLX](https://docs.fileformat.com/email/emlx/) | Apple Mail Message | ✔ | ✔ |

## Web

| Format | Description | Template | Report |
| --- | --- | --- | --- |
| [HTML](https://docs.fileformat.com/web/html/) | HyperText Markup Language | ✔ | ✔ |
| [MHTML](https://docs.fileformat.com/web/mhtml/) | MIME HTML web archive | ✔ | ✔ |

## Report-only formats

| Format | Description | Template | Report |
| --- | --- | --- | --- |
| [PDF](https://docs.fileformat.com/pdf/) | Portable Document Format |   | ✔ |
| [XPS](https://docs.fileformat.com/page-description-language/xps/) | XML Paper Specification |   | ✔ |
| [OXPS](https://docs.fileformat.com/page-description-language/oxps/) | OpenXPS |   | ✔ |
| [TIFF](https://docs.fileformat.com/image/tiff/) | Tagged Image File Format |   | ✔ |
| [SVG](https://docs.fileformat.com/page-description-language/svg/) | Scalable Vector Graphics |   | ✔ |
| [PS](https://docs.fileformat.com/page-description-language/ps/) | PostScript |   | ✔ |
| [PCL](https://docs.fileformat.com/page-description-language/pcl/) | Printer Command Language |   | ✔ |
| [XAML](https://docs.fileformat.com/web/xaml/) | Extensible Application Markup Language |   | ✔ |
| [EPUB](https://docs.fileformat.com/ebook/epub/) | Electronic Publication |   | ✔ |

## Report formats by template family

Each template family can be saved to the formats below. Saving to another format raises an error ("The document cannot be saved to the given format").

| Template family | Report formats |
| --- | --- |
| Word processing (DOC, DOT, DOCX, DOCM, DOTX, DOTM, RTF, ODT, OTT, TXT, MD), HTML, MHTML | Any word-processing format, HTML, MHTML, PDF, XPS, OXPS, TIFF, SVG, PS, PCL, XAML, EPUB |
| Spreadsheet (XLS, XLT, XLSX, XLSM, XLTX, XLTM, XLSB, ODS) | Any spreadsheet format, HTML, MHTML, PDF, XPS, TIFF, PCL |
| Presentation (PPT, PPS, POT, PPTX, PPTM, PPSX, PPSM, POTX, POTM, ODP, OTP) | Any presentation format, HTML, PDF, XPS, TIFF |
| Email (MSG, EML, EMLX) | Any email format, MHTML, PDF, TIFF, SVG, PS, PCL, and from MSG or EMLX also HTML, XPS, OXPS, XAML, EPUB, Markdown, plain text and DOCX |

An MHTML template can also be saved as an email message (MSG, EML). An EML template whose message has only a plain-text body loses that text when it is saved to HTML, Markdown, plain text, XPS, OXPS, XAML, EPUB or DOCX; save it as an email, MHTML or PDF instead. A Markdown template saved as MHTML loses its text too; save it as HTML instead.

{{< alert style="tip" >}}

**Can't find your file format?**
Please post a request on our [Free Support Forum](https://forum.groupdocs.com/c/assembly/15), and our team will assist you.

{{< /alert >}}
