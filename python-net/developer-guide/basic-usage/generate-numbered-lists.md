---
id: assembly-basic-usage-generate-numbered-lists
url: assembly/python-net/basic-usage-generate-numbered-lists
linktitle: Generate Numbered Lists
title: Generate Numbered Lists from Data Source
weight: 17
description: "Create numbered lists in Word, Excel and email documents from Python lists and CSV files by iterating over them with foreach data bands and NumberOf()."
keywords: numbered lists, numbered items, foreach data band, list numbering, ordered lists, NumberOf, generate numbered, CSV, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

Numbered lists provide a sequential, ordered way to display collections of items in documents. GroupDocs.Assembly for Python via .NET enables you to generate numbered lists by iterating over data collections using foreach data bands within numbered list structures.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate numbered lists:

* Create a numbered list in your template document
* Add a foreach data band within the list to iterate over your collection
* Reference collection item properties in list items
* Optionally use NumberOf() to display item numbers
* Close the foreach data band
* Assemble the document with your collection data

{{< alert style="info" >}}
The foreach data band automatically repeats numbered list items for each element in the collection, maintaining proper numbering sequence.
{{< /alert >}}

## Generate Numbered List from a Python List

Create a numbered list from a list of dicts:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Create sample data
tasks = [
    {"Title": "Receive", "Description": "Check the morning delivery against the purchase order"},
    {"Title": "Pack", "Description": "Pack the orders for Quayside Bistro and Saltmarsh Deli"},
    {"Title": "Ship", "Description": "Load the van for the Port Ellery round"},
]

# Assemble document
assembler = DocumentAssembler()
assembler.assemble_document("numbered-tasks.docx", "numbered-tasks-report.docx",
                            DataSourceInfo(tasks, "tasks"))

print("Numbered list generated successfully.")
```
{{< /tab >}}
{{< tab "numbered-tasks.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [numbered-tasks.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-numbered-lists/numbered-tasks.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "numbered-tasks-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-numbered-lists/generate_numbered_list_from_a_python_list/numbered-tasks-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Structure for Numbered Lists

In your template document (numbered-tasks.docx), create a numbered list. The data band opens inside the first numbered paragraph and closes at the start of the next one, so each task repeats the whole list paragraph:

```text
Tasks to complete:

1. <<foreach [in tasks]>><<[Title]>> - <<[Description]>>
<</foreach>>
```

After assembly, you'll get:

```text
Tasks to complete:

1. Receive - Check the morning delivery against the purchase order
2. Pack - Pack the orders for Quayside Bistro and Saltmarsh Deli
3. Ship - Load the van for the Port Ellery round
```

## Using NumberOf() Function

You can explicitly display item numbers using the NumberOf() function:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

items = [
    "Harbor Blend whole bean coffee",
    "Lighthouse Espresso beans",
    "Chestnut honey",
]

assembler = DocumentAssembler()
assembler.assemble_document("numbered-items.docx", "numbered-items-report.docx",
                            DataSourceInfo(items, "items"))

print("Numbered list with explicit numbers generated successfully.")
```
{{< /tab >}}
{{< tab "numbered-items.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [numbered-items.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-numbered-lists/numbered-items.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "numbered-items-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-numbered-lists/using_numberof_function/numbered-items-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with NumberOf():

```text
Items:
<<foreach [item in items]>><<[item.NumberOf()]>>. <<[item]>>
<</foreach>>
```

The items are strings, so the data band names its iteration variable and calls `NumberOf()` on it. When the items are dicts, `<<[NumberOf()]>>` alone works inside the band, as the spreadsheet and email examples below show.

## Generate Numbered List from a CSV File

ADO.NET's `DataTable` has no Python counterpart. Tabular data kept in a CSV file can be passed as it is with [CsvDataSource](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/csvdatasource/): each line is an item and the header names its members.

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import CsvDataLoadOptions, CsvDataSource

# The first line of the file holds the column names
tasks = CsvDataSource("delivery-tasks.csv", CsvDataLoadOptions(True))

assembler = DocumentAssembler()
assembler.assemble_document("numbered-tasks.docx", "numbered-tasks-from-csv.docx",
                            DataSourceInfo(tasks, "tasks"))

print("Numbered list generated from CSV file successfully.")
```
{{< /tab >}}
{{< tab "numbered-tasks.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [numbered-tasks.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-numbered-lists/numbered-tasks.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "delivery-tasks.csv" >}}
{{< tab-text >}}
The following sample file is used in this example: [delivery-tasks.csv](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-numbered-lists/delivery-tasks.csv)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "numbered-tasks-from-csv.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-numbered-lists/generate_numbered_list_from_a_csv_file/numbered-tasks-from-csv.docx)
{{< /tab >}}
{{< /tabs >}}

## Numbered List in Spreadsheet

For spreadsheet templates, you can create numbered lists in cells:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

tasks = [
    {"Title": "Receive", "Description": "Check the morning delivery against the purchase order"},
    {"Title": "Pack", "Description": "Pack the orders for Quayside Bistro and Saltmarsh Deli"},
]

assembler = DocumentAssembler()
assembler.assemble_document("numbered-tasks.xlsx", "numbered-tasks-report.xlsx",
                            DataSourceInfo(tasks, "tasks"))

print("Numbered list generated in spreadsheet successfully.")
```
{{< /tab >}}
{{< tab "numbered-tasks.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [numbered-tasks.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-numbered-lists/numbered-tasks.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "numbered-tasks-report.xlsx" >}}  
```text
Binary file (XLSX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-numbered-lists/numbered_list_in_spreadsheet/numbered-tasks-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

Template for spreadsheet (in-cell, the whole band in cell A1):

```text
Tasks to complete:<<foreach [in tasks]>> <<[NumberOf()]>>. <<[Title]>>;<</foreach>>
```

## Numbered List in Email

Generate numbered lists in email messages. This template is an EML file whose plain-text body holds the data band:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

tasks = [
    {"Title": "Receive", "Description": "Check the morning delivery against the purchase order"},
    {"Title": "Pack", "Description": "Pack the orders for Quayside Bistro and Saltmarsh Deli"},
]

assembler = DocumentAssembler()
assembler.assemble_document("numbered-tasks.eml", "numbered-tasks-report.eml",
                            DataSourceInfo(tasks, "tasks"))

print("Numbered list generated in email successfully.")
```
{{< /tab >}}
{{< tab "numbered-tasks.eml" >}}
{{< tab-text >}}
The following sample file is used in this example: [numbered-tasks.eml](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-numbered-lists/numbered-tasks.eml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "numbered-tasks-report.eml" >}}  
```text
Binary file (EML, 875 bytes)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-numbered-lists/numbered_list_in_email/numbered-tasks-report.eml)
{{< /tab >}}
{{< /tabs >}}

The message body:

```text
Tasks to complete:

<<foreach [in tasks]>><<[NumberOf()]>>. <<[Title]>> - <<[Description]>>
<</foreach>>
Harbor Lane Provisions
```

{{< alert style="warning" >}}
In Word documents, ensure the numbered list formatting is applied in the template. The foreach data band will repeat the list item format and maintain proper numbering for each collection element.
{{< /alert >}}

### Advanced Usage Topics

To learn more about custom numbering formats, nested numbered lists, and advanced list formatting options, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
