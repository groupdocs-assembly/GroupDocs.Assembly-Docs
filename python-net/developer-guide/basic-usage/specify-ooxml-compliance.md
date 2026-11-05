---
id: assembly-basic-usage-ooxml-compliance
url: assembly/python-net/basic-usage-ooxml-compliance
linktitle: Specify OOXML Compliance
title: Specify OOXML Compliance Level for Word Documents
weight: 19
description: "Control the OOXML compliance level (Ecma, Transitional, or Strict) of Word documents assembled in Python with GroupDocs.Assembly for Python via .NET."
keywords: OOXML compliance, OoxmlCompliance, ooxml_compliance, Ecma, Transitional, Strict, DOCX compliance, Word document compliance, ISO/IEC 29500, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET allows you to control the OOXML compliance level when saving Word documents to OOXML formats (DOCX, DOCM, DOTX, DOTM, FlatOpc, etc.). You can explicitly specify the compliance level or let the report keep the template's compliance level.

The main classes involved are:
- [LoadSaveOptions](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/loadsaveoptions/) - contains the `ooxml_compliance` property
- [OoxmlCompliance](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/ooxmlcompliance/) - enumeration specifying compliance levels
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents with specified compliance

Here are the steps to specify OOXML compliance:

* Create LoadSaveOptions for your output format
* Set the `ooxml_compliance` property to the desired compliance level (or leave it `None` to keep the template's level)
* Pass the LoadSaveOptions to `assemble_document`, before the data sources
* The output document will be saved with the specified compliance level

{{< alert style="info" >}}
The `ooxml_compliance` property only applies to OOXML formats (DOCX, DOCM, DOTX, DOTM, FlatOpc, etc.) and is ignored for other file formats. When it is `None` (the default), the report keeps the compliance level of the template: measured with Ecma, Transitional and Strict templates, each report kept its template's level.
{{< /alert >}}

## Available OOXML Compliance Levels

The `OoxmlCompliance` enumeration provides three compliance levels:

- **ECMA**: Specifies ECMA-376 compliance level
- **TRANSITIONAL**: Specifies ISO/IEC 29500:2008 Transitional compliance level (commonly used for compatibility)
- **STRICT**: Specifies ISO/IEC 29500:2008 Strict compliance level (fully compliant with the standard)

## Specify Explicit OOXML Compliance Level

You can explicitly set the OOXML compliance level when assembling a document:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler, FileFormat, LoadSaveOptions, OoxmlCompliance

assembler = DocumentAssembler()

# Create LoadSaveOptions with explicit OOXML compliance
options = LoadSaveOptions(FileFormat.DOCX)
options.ooxml_compliance = OoxmlCompliance.STRICT  # or ECMA, TRANSITIONAL

data = {"CompanyName": "Harbor Lane Provisions", "Year": 2015}

assembler.assemble_document("annual-summary.docx", "annual-summary-report.docx", options,
                            DataSourceInfo(data, "company"))
```
{{< /tab >}}
{{< tab "annual-summary.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [annual-summary.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/specify-ooxml-compliance/annual-summary.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "annual-summary-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/specify-ooxml-compliance/specify_explicit_ooxml_compliance_level/annual-summary-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Use Transitional Compliance

For maximum compatibility with older Office versions, use Transitional compliance:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler, FileFormat, LoadSaveOptions, OoxmlCompliance

assembler = DocumentAssembler()

options = LoadSaveOptions(FileFormat.DOCX)
options.ooxml_compliance = OoxmlCompliance.TRANSITIONAL

data = {"CustomerName": "Quayside Bistro", "OrderNumber": "HLP-10001"}

assembler.assemble_document("order-acknowledgement.docx", "order-acknowledgement-report.docx", options,
                            DataSourceInfo(data, "order"))
```
{{< /tab >}}
{{< tab "order-acknowledgement.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-acknowledgement.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/specify-ooxml-compliance/order-acknowledgement.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-acknowledgement-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/specify-ooxml-compliance/use_transitional_compliance/order-acknowledgement-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Use Ecma Compliance

For ECMA-376 standard compliance:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler, FileFormat, LoadSaveOptions, OoxmlCompliance

assembler = DocumentAssembler()

options = LoadSaveOptions(FileFormat.DOCX)
options.ooxml_compliance = OoxmlCompliance.ECMA

data = {"ReportTitle": "Monthly Bulletin", "Month": "January 2015"}

assembler.assemble_document("monthly-bulletin.docx", "monthly-bulletin-report.docx", options,
                            DataSourceInfo(data, "report"))
```
{{< /tab >}}
{{< tab "monthly-bulletin.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [monthly-bulletin.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/specify-ooxml-compliance/monthly-bulletin.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "monthly-bulletin-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/specify-ooxml-compliance/use_ecma_compliance/monthly-bulletin-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Keep the Template's Compliance Level

When `ooxml_compliance` is not set (default `None`), the report keeps the compliance level of the template:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler, FileFormat, LoadSaveOptions

assembler = DocumentAssembler()

# ooxml_compliance is None by default - the template's compliance is kept
options = LoadSaveOptions(FileFormat.DOCX)

data = {"Title": "Delivery Schedule", "Content": "Deliveries to Port Ellery run on Tuesdays and Fridays."}

# The report keeps the compliance level of status-notice.docx
assembler.assemble_document("status-notice.docx", "status-notice-report.docx", options,
                            DataSourceInfo(data, "document"))
```
{{< /tab >}}
{{< tab "status-notice.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [status-notice.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/specify-ooxml-compliance/status-notice.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "status-notice-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/specify-ooxml-compliance/keep_the_template_s_compliance_level/status-notice-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Using with Different OOXML Formats

The `ooxml_compliance` property works with all OOXML formats. The template below is a DOCX; `LoadSaveOptions` saves the report as DOCX, as macro-enabled DOCM and as a DOTX template:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler, FileFormat, LoadSaveOptions, OoxmlCompliance

assembler = DocumentAssembler()
data = {"Name": "Cold-pressed olive oil", "Value": 320}

# DOCX format
docx_options = LoadSaveOptions(FileFormat.DOCX)
docx_options.ooxml_compliance = OoxmlCompliance.STRICT
assembler.assemble_document("stock-card.docx", "stock-card-report.docx", docx_options,
                            DataSourceInfo(data, "item"))

# DOCM format (macro-enabled)
docm_options = LoadSaveOptions(FileFormat.DOCM)
docm_options.ooxml_compliance = OoxmlCompliance.TRANSITIONAL
assembler.assemble_document("stock-card.docx", "stock-card-report.docm", docm_options,
                            DataSourceInfo(data, "item"))

# DOTX format (template)
dotx_options = LoadSaveOptions(FileFormat.DOTX)
dotx_options.ooxml_compliance = OoxmlCompliance.STRICT
assembler.assemble_document("stock-card.docx", "stock-card-report.dotx", dotx_options,
                            DataSourceInfo(data, "item"))
```
{{< /tab >}}
{{< tab "stock-card.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [stock-card.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/specify-ooxml-compliance/stock-card.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "using-with-different-ooxml-formats-outputs.zip" >}}  
```text
stock-card-report.docm (8 KB)
stock-card-report.docx (8 KB)
stock-card-report.dotx (8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/specify-ooxml-compliance/using_with_different_ooxml_formats/using-with-different-ooxml-formats-outputs.zip)
{{< /tab >}}
{{< /tabs >}}

## Using with Streams

You can also specify OOXML compliance when working with streams:

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler, FileFormat, LoadSaveOptions, OoxmlCompliance

assembler = DocumentAssembler()

options = LoadSaveOptions(FileFormat.DOCX)
options.ooxml_compliance = OoxmlCompliance.STRICT

data = {"CompanyName": "Harbor Lane Provisions", "Year": 2015}

with open("annual-summary.docx", "rb") as template_stream, io.BytesIO() as output_stream:
    assembler.assemble_document(template_stream, output_stream, options,
                                DataSourceInfo(data, "company"))

    with open("annual-summary-from-stream.docx", "wb") as f:
        f.write(output_stream.getvalue())
```
{{< /tab >}}
{{< tab "annual-summary.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [annual-summary.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/specify-ooxml-compliance/annual-summary.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "annual-summary-from-stream.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/specify-ooxml-compliance/using_with_streams/annual-summary-from-stream.docx)
{{< /tab >}}
{{< /tabs >}}

## Compliance Level Behavior

Understanding how compliance levels work:

- **When explicitly set**: The specified compliance level is used when saving to OOXML formats
- **When `None` (default)**: The report keeps the template's compliance level (Ecma, Transitional or Strict)
- **For non-OOXML formats**: The property is ignored (e.g., PDF, HTML, RTF)

{{< tabs "example7" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler, FileFormat, LoadSaveOptions, OoxmlCompliance

assembler = DocumentAssembler()
data = {"Title": "Price List", "Content": "Smoked gouda is 15.20 and Smoked sea salt is 3.95."}

# Explicit Strict compliance
strict_options = LoadSaveOptions(FileFormat.DOCX)
strict_options.ooxml_compliance = OoxmlCompliance.STRICT
assembler.assemble_document("compliance-demo.docx", "compliance-demo-strict.docx", strict_options,
                            DataSourceInfo(data, "doc"))

# Automatic preservation (None)
auto_options = LoadSaveOptions(FileFormat.DOCX)
# auto_options.ooxml_compliance is None - the template's level is kept
assembler.assemble_document("compliance-demo.docx", "compliance-demo-auto.docx", auto_options,
                            DataSourceInfo(data, "doc"))

# Note: For PDF output, ooxml_compliance is ignored
pdf_options = LoadSaveOptions(FileFormat.PDF)
pdf_options.ooxml_compliance = OoxmlCompliance.STRICT  # Ignored for PDF
assembler.assemble_document("compliance-demo.docx", "compliance-demo.pdf", pdf_options,
                            DataSourceInfo(data, "doc"))
```
{{< /tab >}}
{{< tab "compliance-demo.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [compliance-demo.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/specify-ooxml-compliance/compliance-demo.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "compliance-level-behavior-outputs.zip" >}}  
```text
compliance-demo-auto.docx (7 KB)
compliance-demo-strict.docx (8 KB)
compliance-demo.pdf (19 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/specify-ooxml-compliance/compliance_level_behavior/compliance-level-behavior-outputs.zip)
{{< /tab >}}
{{< /tabs >}}

{{< alert style="warning" >}}
The `ooxml_compliance` property only affects OOXML formats. When saving to other formats like PDF, HTML, or RTF, this property is ignored. The compliance level is determined by the output format, not the template format.
{{< /alert >}}

### Advanced Usage Topics

To learn more about format-specific options, document conversion settings, and advanced compliance handling, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
