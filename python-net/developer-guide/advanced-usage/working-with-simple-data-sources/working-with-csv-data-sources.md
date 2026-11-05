---
id: working-with-csv-data-sources
url: assembly/python-net/working-with-csv-data-sources
title: Working with CSV Data Sources
weight: 1
description: "Working with CSV Data Sources with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: working with csv data sources, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
To access CSV data while building a report, you can pass a [CsvDataSource](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/csvdatasource/) instance to the assembler as a data source. Using of *CsvDataSource* enables you to work with typed values rather than just strings in template documents. Although CSV as a format does not define a way to store values of types other than strings, *CsvDataSource* is capable to recognize values of the following types by their string representations:

*   Int32?
*   Int64?
*   Double?
*   Boolean?
*   DateTime?

{{< alert style="warning" >}}For recognition of data types to work, string representations of corresponding values must be formed using invariant culture settings.{{< /alert >}}

### Treating simple CSV data

In template documents, a [CsvDataSource ](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/csvdatasource/)instance is treated as a collection of rows, like a list of dicts: iterate it with `foreach` (see "[Using data sources]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md#using-data-sources" >}})") as shown in the following example.

Suppose we have CSV data like:
```
John Doe,30,1989-04-01 4:00:00 pm
Jane Doe,27,1992-01-31 07:00:00 am
John Smith,51,1968-03-08 1:00:00 pm
```

By using the template like following:
```
<<foreach \[in persons\]>>Name: <<\[Column1\]>>, Age: <<\[Column2\]>>, Date
of Birth: <<\[Column3\]:"dd.MM.yyyy">>
<</foreach>>
Average age: <<\[persons.Average(p => p.Column2)\]>>
```

The results will be produced like:
```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968
Average age: 36
```

{{< alert style="warning" >}}Using of the custom date-time format and the extension method involving arithmetic in the template document becomes possible, because text values of Column3 and Column2 are automatically converted to DateTime? and Int32? respectively.{{< /alert >}}

### Configure data source to read column names

By default, [CsvDataSource ](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/csvdatasource/)uses column names such as "*Column1*", "*Column2*", and so on, as you can see from the previous example. However, *CsvDataSource* can be configured to read column names from the first line of CSV data as shown in the following example.

Suppose we have CSV data like:
```
Name,Age,Birth
John Doe,30,1989-04-01 4:00:00 pm
Jane Doe,27,1992-01-31 07:00:00 am
John Smith,51,1968-03-08 1:00:00 pm
```

By using the template like following:
```
<<foreach \[in persons\]>>Name: <<\[Name\]>>, Age: <<\[Age\]>>, Date of
Birth: <<\[Birth\]:"dd.MM.yyyy">>
<</foreach>>
Average age: <<\[persons.Average(p => p.Age)\]>>
```

The code should be written like:
{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import CsvDataLoadOptions, CsvDataSource

# The first line of the file holds the column names
persons = CsvDataSource("persons.csv", CsvDataLoadOptions(True))

assembler = DocumentAssembler()
assembler.assemble_document("data-destination-with-nested-elements.txt", "data-destination-with-nested-elements-report.txt", DataSourceInfo(persons, "persons"))
```
{{< /tab >}}
{{< tab "data-destination-with-nested-elements.txt" >}}
{{< tab-text >}}
The following sample file is used in this example: [data-destination-with-nested-elements.txt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-simple-data-sources/working-with-csv-data-sources/data-destination-with-nested-elements.txt)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "persons.csv" >}}
{{< tab-text >}}
The following sample file is used in this example: [persons.csv](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-simple-data-sources/working-with-csv-data-sources/persons.csv)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "data-destination-with-nested-elements-report.txt" >}}  
```text
Name: Amara Osei, Age: 41, Date of
Birth: 12.03.1984
Name: Jonas Weber, Age: 37, Date of
Birth: 04.07.1988
Name: Lena Park, Age: 29, Date of
Birth: 21.11.1996

Average age: 35.666666666666664
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-simple-data-sources/working-with-csv-data-sources/configure_data_source_to_read_column_names/data-destination-with-nested-elements-report.txt)
{{< /tab >}}
{{< /tabs >}}

The results will be produced like:
```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968
Average age: 36
```

Also, you can use *CsvDataLoadOptions* to customize the following characters playing special roles while loading CSV data (its `delimiter`, `comment_char` and `quote_char` properties):

*   Value separator (the default is comma)
*   Single-line comment start (the default is sharp)
*   Quotation mark enabling to use other special characters within a value (the default is double quotes)

###  Download

#### Data Source Document

*   [data-destination-with-nested-elements.txt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-simple-data-sources/working-with-csv-data-sources/data-destination-with-nested-elements.txt)

#### Template
