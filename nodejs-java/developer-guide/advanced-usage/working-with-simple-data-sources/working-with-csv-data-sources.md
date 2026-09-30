---
id: working-with-csv-data-sources
url: assembly/nodejs-java/working-with-csv-data-sources
title: Working with CSV Data Sources
weight: 1
description: "Pass CSV data to GroupDocs.Assembly for Node.js via Java with CsvDataSource and configure headers, separators and quotes with CsvDataLoadOptions."
keywords: csv, CsvDataSource, CsvDataLoadOptions, node.js, report generation
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
To access CSV data while building a report, pass a `CsvDataSource` instance to the assembler as a data source. Using `CsvDataSource` enables you to work with typed values rather than just strings in template documents. Although CSV as a format does not define a way to store values of types other than strings, `CsvDataSource` recognizes values of the following types by their string representations:

*   Integer
*   Long
*   Double
*   Boolean
*   Date

{{< alert style="warning" >}}For recognition of data types to work, string representations of corresponding values must be formed using invariant culture settings.{{< /alert >}}

## Treating simple CSV data

In template documents, a `CsvDataSource` instance should be treated in the same way as if it was a `DataTable` instance (see "[Using Data Sources](/assembly/nodejs-java/template-syntax-part-1-of-2/#using-data-sources)" for more information) as shown in the following example.

Suppose we have CSV data like:
```
John Doe,30,1989-04-01 4:00:00 pm
Jane Doe,27,1992-01-31 07:00:00 am
John Smith,51,1968-03-08 1:00:00 pm
```

And the following template:
```
<<foreach [in persons]>>Name: <<[Column1]>>, Age: <<[Column2]>>, Date of Birth: <<[Column3]:"dd.MM.yyyy">>
<</foreach>>
Average age: <<[persons.average(p => p.Column2)]>>
```

The code looks like this:

```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

const dataSource = new groupdocs.CsvDataSource("persons.csv");
const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument("template.txt", "report.txt",
    new groupdocs.DataSourceInfo(dataSource, "persons"));
```

The result is:
```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968

Average age: 36.0
```

{{< alert style="warning" >}}Using a custom date-time format and an extension method involving arithmetic in the template is possible because text values of Column3 and Column2 are automatically converted to a date and an integer respectively.{{< /alert >}}

## Configure the data source to read column names

By default, `CsvDataSource` uses column names such as "Column1", "Column2", and so on, as you can see from the previous example. However, `CsvDataSource` can be configured to read column names from the first line of CSV data as shown in the following example.

Suppose we have CSV data like:
```
Name,Age,Birth
John Doe,30,1989-04-01 4:00:00 pm
Jane Doe,27,1992-01-31 07:00:00 am
John Smith,51,1968-03-08 1:00:00 pm
```

And the following template:
```
<<foreach [in persons]>>Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth: <<[Birth]:"dd.MM.yyyy">>
<</foreach>>
Average age: <<[persons.average(p => p.Age)]>>
```

Pass `true` to the `CsvDataLoadOptions` constructor to read column names from the first line:

{{< tabs "csv-headers-example" >}}
{{< tab "JavaScript" >}}
```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

// Source template and destination report
const templatePath = "CsvDatasetDemo.txt";
const reportPath = "SimpleCsvDSDemo Out.txt";

// Read column names from the first line of CSV data
const options = new groupdocs.CsvDataLoadOptions(true);
const dataSource = new groupdocs.CsvDataSource("persons-with-headers.csv", options);
const dataSourceInfo = new groupdocs.DataSourceInfo(dataSource, "persons");

// Assemble the document
const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument(templatePath, reportPath, dataSourceInfo);

process.exit(0);
```
{{< /tab >}}
{{< /tabs >}}

The result is:
```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968

Average age: 36.0
```

## Customize special characters

You can also use `CsvDataLoadOptions` to customize the following characters playing special roles while loading CSV data:

*   Value separator (the default is comma), set with `setDelimiter`
*   Single-line comment start (the default is sharp), set with `setCommentChar`
*   Quotation mark enabling to use other special characters within a value (the default is double quotes), set with `setQuoteChar`

These setters take a Java `char`. Create one from a JavaScript string with `java.newChar`:

```javascript
const java = require('java');

const options = new groupdocs.CsvDataLoadOptions();
options.hasHeaders(true);
options.setDelimiter(java.newChar(';'));
options.setCommentChar(java.newChar('/'));
options.setQuoteChar(java.newChar('"'));

const dataSource = new groupdocs.CsvDataSource("persons.csv", options);
```

{{< alert style="info" >}}Passing a JavaScript string directly (for example, `options.setDelimiter(';')`) fails with the error `Could not find method "setDelimiter(java.lang.String)"`.{{< /alert >}}

## Download

### Data source document

The sample file below has the same columns; its dates are written as `M/d/yyyy H:mm`, so how they are recognized depends on the current culture.

*   [Person.csv](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Data%20Sources/Excel%20DataSource/Person.csv?raw=true)

### Template

*   [CsvDatasetDemo.txt](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Text%20Templates/CsvDatasetDemo.txt?raw=true)
