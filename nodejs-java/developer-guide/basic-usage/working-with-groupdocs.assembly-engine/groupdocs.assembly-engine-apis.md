---
id: groupdocs-assembly-engine-apis
url: assembly/nodejs-java/groupdocs-assembly-engine-apis
title: GroupDocs.Assembly Engine APIs
weight: 3
description: "Build reports with DocumentAssembler in Node.js: assembleDocument overloads, XML, JSON and CSV data sources with load options, known types, assembler options and technical details."
keywords: DocumentAssembler, assembleDocument, DataSourceInfo, XmlDataSource, JsonDataSource, CsvDataSource, JsonDataLoadOptions, CsvDataLoadOptions, known types, node.js, groupdocs assembly
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
{{< alert style="info" >}}This article describes the behavior of the GroupDocs.Assembly APIs available in Node.js.{{< /alert >}}

## Overview of the API

GroupDocs.Assembly for Node.js via Java wraps the Java library, so every class you use is a Java class of the `com.groupdocs.assembly` package exposed to JavaScript through the `@groupdocs/groupdocs.assembly` module. Methods have their Java names and are called synchronously, for example `assembler.assembleDocument(...)` or `assembler.getOptions()`.

The main class is `DocumentAssembler`. It contains everything required to build a report from a template.

```javascript
const {
  DocumentAssembler, DataSourceInfo, LoadSaveOptions, FileFormat,
  JsonDataSource, XmlDataSource, CsvDataSource, DataSet
} = require('@groupdocs/groupdocs.assembly');
```

### Building Reports

To build a report from a template, call one of the `DocumentAssembler.assembleDocument` overloads:

| Overload | Description |
| --- | --- |
| `assembleDocument(sourcePath, targetPath, ...dataSourceInfos)` | Reads a template from a file and saves the report to a file. The report format is taken from the target file extension. |
| `assembleDocument(sourcePath, targetPath, loadSaveOptions, ...dataSourceInfos)` | The same, with an explicit save format and other load/save settings passed as `LoadSaveOptions`. |
| `assembleDocument(sourceStream, targetStream, ...dataSourceInfos)` | Reads a template from a Java `InputStream` and writes the report to a Java `OutputStream`. |
| `assembleDocument(sourceStream, targetStream, loadSaveOptions, ...dataSourceInfos)` | The same, with explicit `LoadSaveOptions`. |

Every data source is passed as a `DataSourceInfo` object that has the following properties:

| Parameter | Description |
| --- | --- |
| dataSource | An object providing data to populate the template. In Node.js, this is a `JsonDataSource`, `XmlDataSource`, `CsvDataSource`, `DataSet`, `DataTable` or `DocumentTable` instance. |
| name | The identifier of the data source object within the template. You can omit it if the template uses the [contextual object member access](/assembly/nodejs-java/template-syntax-part-1-of-2/#using-contextual-object-member-access) when dealing with the data source. |

{{< alert style="info" >}}Plain JavaScript objects cannot be passed as data sources, because they are not Java objects. Where the Java documentation uses custom Java classes (for example, a `Person` class) as data, use JSON, XML or CSV data of the same shape, or a `DataSet`.{{< /alert >}}

Given a template to be populated with data from a `DataSet` instance that is identified as "ds" within the template, you can use the following code to build the corresponding report.

```javascript
const { DocumentAssembler, DataSourceInfo, DataSet } = require('@groupdocs/groupdocs.assembly');

// Setting up a data set
const ds = new DataSet();
ds.readXml('persons.xml');

const assembler = new DocumentAssembler();
assembler.assembleDocument('wordTemplate.docx', 'wordReport.docx', new DataSourceInfo(ds, 'ds'));
```

Given a template to be populated with data about a single person using the contextual object member access, you can pass the person as a JSON object.

```javascript
const { DocumentAssembler, DataSourceInfo, JsonDataSource } = require('@groupdocs/groupdocs.assembly');

// person.json: { "Name": "John Doe", "Age": 30 }
const person = new JsonDataSource('person.json');

const assembler = new DocumentAssembler();
assembler.assembleDocument('wordTemplate.docx', 'wordReport.docx', new DataSourceInfo(person));
```

#### Specifying the Output Format

Pass a `LoadSaveOptions` object to save the report in a format that differs from the template format.

```javascript
const { DocumentAssembler, DataSourceInfo, JsonDataSource, LoadSaveOptions, FileFormat } = require('@groupdocs/groupdocs.assembly');

const assembler = new DocumentAssembler();
assembler.assembleDocument('wordTemplate.docx', 'wordReport.pdf',
  new LoadSaveOptions(FileFormat.PDF),
  new DataSourceInfo(new JsonDataSource('person.json')));
```

#### Using Several Data Sources

To pass several data sources, pass several `DataSourceInfo` objects after the other arguments. Each data source must have its own name.

```javascript
const { DocumentAssembler, DataSourceInfo, JsonDataSource, CsvDataSource, CsvDataLoadOptions } = require('@groupdocs/groupdocs.assembly');

const assembler = new DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx',
  new DataSourceInfo(new JsonDataSource('person.json'), 'p'),
  new DataSourceInfo(new CsvDataSource('persons.csv', new CsvDataLoadOptions(true)), 'persons'));
```

If you build the list of data sources dynamically, create a Java array and pass it instead:

```javascript
const java = require('java');

const infos = java.newArray('com.groupdocs.assembly.DataSourceInfo', [
  new DataSourceInfo(new JsonDataSource('person.json'), 'p'),
  new DataSourceInfo(new CsvDataSource('persons.csv', new CsvDataLoadOptions(true)), 'persons')
]);
assembler.assembleDocument('template.docx', 'report.docx', infos);
```

#### Working with Streams

The stream overloads accept Java streams, not Node.js streams. You can create them with the `java` module that the package depends on:

```javascript
const java = require('java');
const { DocumentAssembler, DataSourceInfo, JsonDataSource, LoadSaveOptions, FileFormat } = require('@groupdocs/groupdocs.assembly');

const FileInputStream = java.import('java.io.FileInputStream');
const FileOutputStream = java.import('java.io.FileOutputStream');

const template = new FileInputStream('wordTemplate.docx');
const report = new FileOutputStream('wordReport.docx');
const data = new FileInputStream('person.json');

const assembler = new DocumentAssembler();
assembler.assembleDocument(template, report,
  new LoadSaveOptions(FileFormat.DOCX),
  new DataSourceInfo(new JsonDataSource(data)));

template.close();
report.close();
data.close();
```

To read a template from a Node.js readable stream, use the `readDataFromStream` helper exported by the package. It collects the stream into a Java `InputStream` and passes it to a callback. To get the report as a Node.js `Buffer`, write it to a `java.io.ByteArrayOutputStream`:

```javascript
const fs = require('fs');
const java = require('java');
const groupdocs = require('@groupdocs/groupdocs.assembly');
const { DocumentAssembler, DataSourceInfo, JsonDataSource, LoadSaveOptions, FileFormat } = groupdocs;

groupdocs.readDataFromStream(fs.createReadStream('wordTemplate.docx'), (templateStream) => {
  const ByteArrayOutputStream = java.import('java.io.ByteArrayOutputStream');
  const output = new ByteArrayOutputStream();

  const assembler = new DocumentAssembler();
  assembler.assembleDocument(templateStream, output,
    new LoadSaveOptions(FileFormat.DOCX),
    new DataSourceInfo(new JsonDataSource('person.json')));

  const buffer = Buffer.from(output.toByteArray());
  fs.writeFileSync('wordReport.docx', buffer);
  process.exit(0);
});
```

`readDataFromStream` works for data files as well: pass the resulting `InputStream` to the `JsonDataSource`, `XmlDataSource` or `CsvDataSource` constructor.

### Accessing XML Data

To access XML data while building a report, you can read XML into a `DataSet` and pass it to the engine as a data source. However, if your scenario does not permit to specify an XML schema while loading XML into `DataSet`, all attributes and text values of XML elements are loaded as strings. Thus, it becomes impossible, for example, to use arithmetic operations on numbers or to specify custom date-time and numeric formats to output corresponding values, because all of them are treated as strings.

To overcome this limitation, you can pass an `XmlDataSource` instance to the engine as a data source instead. Even when an XML schema is not provided, `XmlDataSource` is capable to recognize values of the following types by their string representations:

- Long
- Double
- Boolean
- Date

**Note –** For recognition of data types to work, string representations of corresponding attributes and text values of XML elements must be formed using invariant culture settings.

`XmlDataSource` can be created from a file path or a Java `InputStream`, optionally with an XML schema (as a second path or stream) and `XmlDataLoadOptions`.

While loading data to `XmlDataSource`, the engine performs actions typical for XML deserialization behind the scenes: It maps complex-type XML elements to internal objects and simple-type XML elements to fields of containing objects. So, in template documents, an `XmlDataSource` instance should be treated as an object having corresponding fields and nested objects as shown in the following example.

XML

```
<Person>
   <Name>John Doe</Name>
   <Age>30</Age>
   <Birth>1989-04-01 4:00:00 pm</Birth>
   <Child>Ann Doe</Child>
   <Child>Charles Doe</Child>
</Person>
```

Template document

```
Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth: <<[Birth]:"dd.MM.yyyy">>
Children:
<<foreach [in Child]>><<[Child_Text]>>
<</foreach>>
```

Source code

```javascript
const dataSource = new XmlDataSource('person.xml');

const assembler = new DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx', new DataSourceInfo(dataSource));
```

Result document

```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Children:
Ann Doe
Charles Doe
```

**Note –** To reference a sequence of repeated simple-type XML elements with the same name, the elements' name itself (for example, "Child") should be used in a template document, whereas the same name with the "_Text" suffix (for example, "Child_Text") should be used to reference the text value of one of these elements.

By default, if a root XML element contains only a sequence of elements of one type, the engine does not generate an internal root object while loading XML data. So, in template documents, such an `XmlDataSource` instance should be treated as a sequence of corresponding nested objects as shown in the following example.

XML

```
<Persons>
   <Person>
       <Name>John Doe</Name>
       <Age>30</Age>
       <Birth>1989-04-01 4:00:00 pm</Birth>
   </Person>
   <Person>
       <Name>Jane Doe</Name>
       <Age>27</Age>
       <Birth>1992-01-31 07:00:00 am</Birth>
   </Person>
   <Person>
       <Name>John Smith</Name>
       <Age>51</Age>
       <Birth>1968-03-08 1:00:00 pm</Birth>
   </Person>
</Persons>
```

Template document

```
<<foreach [in persons]>>Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth: <<[Birth]:"dd.MM.yyyy">>
<</foreach>>
Average age: <<[persons.average(p => p.Age)]>>
```

Source code

```javascript
const dataSource = new XmlDataSource('persons.xml');

const assembler = new DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx', new DataSourceInfo(dataSource, 'persons'));
```

Result document

```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968

Average age: 36.0
```

However, if your scenario requires an internal object for a root XML element to be always generated while loading data to `XmlDataSource`, you can force this as shown in the following code snippet. The sequence from the previous example is then accessed as `persons.Person`.

```javascript
const { XmlDataSource, XmlDataLoadOptions } = require('@groupdocs/groupdocs.assembly');

const options = new XmlDataLoadOptions();
options.setAlwaysGenerateRootObject(true);
const dataSource = new XmlDataSource('persons.xml', options);
```

The following example sums up typical scenarios involving nested complex-type XML elements.

XML

```
<Managers>
   <Manager>
       <Name>John Smith</Name>
       <Contract>
           <Client>
               <Name>A Company</Name>
           </Client>
           <Price>1200000</Price>
       </Contract>
       <Contract>
           <Client>
               <Name>B Ltd.</Name>
           </Client>
           <Price>750000</Price>
       </Contract>
       <Contract>
           <Client>
               <Name>C &amp; D</Name>
           </Client>
           <Price>350000</Price>
       </Contract>
   </Manager>
   <Manager>
       <Name>Tony Anderson</Name>
       <Contract>
           <Client>
               <Name>E Corp.</Name>
           </Client>
           <Price>650000</Price>
       </Contract>
       <Contract>
           <Client>
               <Name>F &amp; Partners</Name>
           </Client>
           <Price>550000</Price>
       </Contract>
   </Manager>
   <Manager>
       <Name>July James</Name>
       <Contract>
           <Client>
               <Name>G &amp; Co.</Name>
           </Client>
           <Price>350000</Price>
       </Contract>
       <Contract>
           <Client>
               <Name>H Group</Name>
           </Client>
           <Price>250000</Price>
       </Contract>
       <Contract>
           <Client>
               <Name>I &amp; Sons</Name>
           </Client>
           <Price>100000</Price>
       </Contract>
       <Contract>
           <Client>
               <Name>J Ent.</Name>
           </Client>
           <Price>100000</Price>
       </Contract>
   </Manager>
</Managers>
```

Template document

```
<<foreach [in managers]>>Manager: <<[Name]>>
Contracts:
<<foreach [in Contract]>>- <<[Client.Name]>> ($<<[Price]>>)
<</foreach>>
<</foreach>>
```

Source code

```javascript
const dataSource = new XmlDataSource('managers.xml');

const assembler = new DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx', new DataSourceInfo(dataSource, 'managers'));
```

Result document

```
Manager: John Smith
Contracts:
- A Company ($1200000)
- B Ltd. ($750000)
- C & D ($350000)

Manager: Tony Anderson
Contracts:
- E Corp. ($650000)
- F & Partners ($550000)

Manager: July James
Contracts:
- G & Co. ($350000)
- H Group ($250000)
- I & Sons ($100000)
- J Ent. ($100000)
```

For more examples, see [Working with XML Data Sources](/assembly/nodejs-java/working-with-xml-data-sources/).

### Accessing JSON Data

To access JSON data while building a report, you can pass a `JsonDataSource` instance to the engine as a data source. `JsonDataSource` can be created from a file path or a Java `InputStream`, optionally with `JsonDataLoadOptions`.

Using `JsonDataSource` enables you to work with typed values of JSON elements in template documents. For more convenience, the set of simple JSON types is extended as follows:

- Long
- Double
- Boolean
- Date
- String

**Note –** Working with complex JSON types (objects and arrays) is also supported.

While loading data to `JsonDataSource`, the engine performs JSON deserialization and generates corresponding internal objects. So, in template documents, a `JsonDataSource` instance should be treated according to what a root JSON element represents.

If a root JSON element is an object, a `JsonDataSource` instance should be treated as an object as well, as shown in the following example.

JSON

```
{
   Name: "John Doe",
   Age: 30,
   Birth: "1989-04-01 4:00:00 pm",
   Child: [ "Ann Doe", "Charles Doe" ]
}
```

Template document

```
Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth: <<[Birth]:"dd.MM.yyyy">>
Children:
<<foreach [in Child]>><<[Child_Text]>>
<</foreach>>
```

Source code

```javascript
const dataSource = new JsonDataSource('person.json');

const assembler = new DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx', new DataSourceInfo(dataSource));
```

Result document

```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Children:
Ann Doe
Charles Doe
```

**Note –** To reference a JSON object property that is an array of simple-type values, the name of the property (for example, "Child") should be used in a template document, whereas the same name with the "_Text" suffix (for example, "Child_Text") should be used to reference the value of an item of this array.

If a root JSON element is an array, a `JsonDataSource` instance should be treated as a sequence of items of this array as shown in the following example.

JSON

```
[
   {
       Name: "John Doe",
       Age: 30,
       Birth: "1989-04-01 4:00:00 pm"
   },
   {
       Name: "Jane Doe",
       Age: 27,
       Birth: "1992-01-31 07:00:00 am"
   },
   {
       Name: "John Smith",
       Age: 51,
       Birth: "1968-03-08 1:00:00 pm"
   }
]
```

Template document

```
<<foreach [in persons]>>Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth: <<[Birth]:"dd.MM.yyyy">>
<</foreach>>
Average age: <<[persons.average(p => p.Age)]>>
```

Source code

```javascript
const dataSource = new JsonDataSource('persons.json');

const assembler = new DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx', new DataSourceInfo(dataSource, 'persons'));
```

Result document

```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968

Average age: 36.0
```

By default, if a root JSON element is an object having only one property that is an object or array in turn, the engine does not generate an internal root object while loading JSON data. So, in template documents, such a `JsonDataSource` instance should be treated according to what this property represents instead. For instance, the following JSON snippets can be used to produce the same results as the previous examples of this section respectively.

JSON 1

```
{
   Person:
   {
       Name: "John Doe",
       Age: 30,
       Birth: "1989-04-01 4:00:00 pm",
       Child: [ "Ann Doe", "Charles Doe" ]
   }
}
```

JSON 2

```
{
   Persons:
   [
       {
           Name: "John Doe",
           Age: 30,
           Birth: "1989-04-01 4:00:00 pm"
       },
       {
           Name: "Jane Doe",
           Age: 27,
           Birth: "1992-01-31 07:00:00 am"
       },
       {
           Name: "John Smith",
           Age: 51,
           Birth: "1968-03-08 1:00:00 pm"
       }
   ]
}
```

However, if your scenario requires an internal object for a root JSON element to be always generated while loading data to `JsonDataSource`, you can force this as shown in the following code snippet.

```javascript
const { JsonDataSource, JsonDataLoadOptions } = require('@groupdocs/groupdocs.assembly');

const options = new JsonDataLoadOptions();
options.setAlwaysGenerateRootObject(true);
const dataSource = new JsonDataSource('persons.json', options);
```

The following example sums up typical scenarios involving nested JSON objects and arrays.

JSON

```
[
   {
       Name: "John Smith",
       Contract:
       [
           {
               Client:
               {
                   Name: "A Company"
               },
               Price: 1200000
           },
           {
               Client:
               {
                   Name: "B Ltd."
               },
               Price: 750000
           },
           {
               Client:
               {
                   Name: "C & D"
               },
               Price: 350000
           }
       ]
   },
   {
       Name: "Tony Anderson",
       Contract:
       [
           {
               Client:
               {
                   Name: "E Corp."
               },
               Price: 650000
           },
           {
               Client:
               {
                   Name: "F & Partners"
               },
               Price: 550000
           }
       ]
   },
   {
       Name: "July James",
       Contract:
       [
           {
               Client:
               {
                   Name: "G & Co."
               },
               Price: 350000
           },
           {
               Client:
               {
                   Name: "H Group"
               },
               Price: 250000
           },
           {
               Client:
               {
                   Name: "I & Sons"
               },
               Price: 100000
           },
           {
               Client:
               {
                   Name: "J Ent."
               },
               Price: 100000
           }
       ]
   }
]
```

Template document

```
<<foreach [in managers]>>Manager: <<[Name]>>
Contracts:
<<foreach [in Contract]>>- <<[Client.Name]>> ($<<[Price]>>)
<</foreach>>
<</foreach>>
```

Source code

```javascript
const dataSource = new JsonDataSource('managers.json');

const assembler = new DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx', new DataSourceInfo(dataSource, 'managers'));
```

Result document

```
Manager: John Smith
Contracts:
- A Company ($1200000)
- B Ltd. ($750000)
- C & D ($350000)

Manager: Tony Anderson
Contracts:
- E Corp. ($650000)
- F & Partners ($550000)

Manager: July James
Contracts:
- G & Co. ($350000)
- H Group ($250000)
- I & Sons ($100000)
- J Ent. ($100000)
```

#### Simple Value Parse Modes

For recognition of JSON simple values (null, boolean, number, integer, and string), the engine provides two modes: *loose* and *strict*. In the loose mode, types of JSON simple values are determined upon parsing of their string representations. In the strict mode, types of JSON simple values are determined from JSON notation itself. To see the main difference between the modes, consider the following JSON snippet.

```
{ prop: "00123" }
```

In the loose mode, the type of `prop` is determined as integer (so `<<[prop]>>` outputs `123`), whereas in the strict mode, it is determined as string (so `<<[prop]>>` outputs `00123`).

The loose mode (`JsonSimpleValueParseMode.LOOSE`) is used by the engine by default to support more typed data representation options. However, in some scenarios, it can be more preferable to disable recognition of numbers and other JSON simple values from strings, for example, when you need to keep leading padding zeros in a string value representing a number. In this case, you can switch to the strict mode as shown in the following code snippet.

```javascript
const { JsonDataSource, JsonDataLoadOptions, JsonSimpleValueParseMode } = require('@groupdocs/groupdocs.assembly');

const options = new JsonDataLoadOptions();
options.setSimpleValueParseMode(JsonSimpleValueParseMode.STRICT);
const dataSource = new JsonDataSource('data.json', options);
```

**Note –** Parsing of date-time values does not depend on whether the loose or strict mode is used.

#### Date-Time Formats

Recognition of date-time values is a special case, because the [JSON specification](https://www.json.org) does not define a format for their representation. So, by default, while parsing date-time values from strings, the engine tries several formats in the following order:

- [The ISO-8601 format](https://en.wikipedia.org/wiki/ISO_8601) (for values like "2015-03-02T13:56:04Z")
- [The Microsoft® JSON date-time format](https://docs.microsoft.com/en-us/previous-versions/dotnet/articles/bb299886(v=msdn.10)#from-javascript-literals-to-json) (for values like "/Date(1224043200000)/")
- All date-time formats supported for the current culture
- All date-time formats supported for the English USA culture
- All date-time formats supported for the English New Zealand culture

Although this approach is quite flexible, in some scenarios, you may need to restrict strings to be recognized as date-time values. You can achieve this by specifying one or several exact formats in the context of the current culture to be used while parsing date-time values from strings. The formats are passed as a Java collection, which you can create with the `java` module:

```javascript
const java = require('java');
const { JsonDataSource, JsonDataLoadOptions } = require('@groupdocs/groupdocs.assembly');

const formats = java.newInstanceSync('java.util.ArrayList');
formats.add('MM/dd/yyyy');

const options = new JsonDataLoadOptions();
options.setExactDateTimeParseFormats(formats);
const dataSource = new JsonDataSource('data.json', options);
```

In this example, strings conforming to the format "MM/dd/yyyy" are going to be recognized as date-time values while loading JSON, whereas the others are not (but see the following note). To specify a single format, you can also call `options.setExactDateTimeParseFormat('MM/dd/yyyy')`.

{{< alert style="info" >}}Because exact formats are applied in the context of the current culture, the `/` character stands for the date separator of that culture. The JVM culture is taken from the operating system locale. To make parsing independent of the machine settings, set the JVM locale before the package is loaded, for example `const java = require('java'); java.options.push('-Duser.language=en', '-Duser.country=US');` placed before `require('@groupdocs/groupdocs.assembly')`.{{< /alert >}}

In some scenarios, you may need to disable recognition of date-time values at all, for example, when you deal with strings containing already formatted date-time values, which you do not want to re-format using the engine. You can achieve this by setting the exact date-time parse formats to an empty list (but see the following note).

```javascript
options.setExactDateTimeParseFormats(java.newInstanceSync('java.util.ArrayList'));
```

**Note –** Strings conforming to the Microsoft® JSON date-time format (for example, "/Date(1224043200000)/") are always recognized as date-time values regardless of the exact date-time parse formats.

For more examples, see [Working with JSON Data Sources](/assembly/nodejs-java/working-with-json-data-sources/).

### Accessing CSV Data

To access CSV data while building a report, you can pass a `CsvDataSource` instance to the engine as a data source. `CsvDataSource` can be created from a file path or a Java `InputStream`, optionally with `CsvDataLoadOptions`.

Using `CsvDataSource` enables you to work with typed values rather than just strings in template documents. Although CSV as a format does not define a way to store values of types other than strings, `CsvDataSource` is capable to recognize values of the following types by their string representations:

- Long
- Double
- Boolean
- Date

**Note –** For recognition of data types to work, string representations of corresponding values must be formed using invariant culture settings.

In template documents, a `CsvDataSource` instance should be treated as a sequence of objects having corresponding fields as shown in the following example.

CSV

```
John Doe,30,1989-04-01 4:00:00 pm
Jane Doe,27,1992-01-31 07:00:00 am
John Smith,51,1968-03-08 1:00:00 pm
```

Template document

```
<<foreach [in persons]>>Name: <<[Column1]>>, Age: <<[Column2]>>, Date of Birth: <<[Column3]:"dd.MM.yyyy">>
<</foreach>>
Average age: <<[persons.average(p => p.Column2)]>>
```

Source code

```javascript
const dataSource = new CsvDataSource('persons.csv');

const assembler = new DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx', new DataSourceInfo(dataSource, 'persons'));
```

Result document

```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968

Average age: 36.0
```

By default, `CsvDataSource` uses column names such as "Column1", "Column2", and so on, as you can see from the previous example. However, `CsvDataSource` can be configured to read column names from the first line of CSV data as shown in the following example.

CSV

```
Name,Age,Birth
John Doe,30,1989-04-01 4:00:00 pm
Jane Doe,27,1992-01-31 07:00:00 am
John Smith,51,1968-03-08 1:00:00 pm
```

Template document

```
<<foreach [in persons]>>Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth: <<[Birth]:"dd.MM.yyyy">>
<</foreach>>
Average age: <<[persons.average(p => p.Age)]>>
```

Source code

```javascript
const options = new CsvDataLoadOptions(true); // the first line contains column names
const dataSource = new CsvDataSource('persons.csv', options);

const assembler = new DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx', new DataSourceInfo(dataSource, 'persons'));
```

Result document

```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968

Average age: 36.0
```

Also, you can use `CsvDataLoadOptions` to customize the following characters playing special roles while loading CSV data:

- Value separator (the default is comma), set with `setDelimiter`
- Single-line comment start (the default is sharp), set with `setCommentChar`
- Quotation mark enabling to use other special characters within a value (the default is double quotes), set with `setQuoteChar`

These setters take a Java `char`. A JavaScript string is not converted to `char` automatically, so wrap the character with `java.newChar`:

```javascript
const java = require('java');
const { CsvDataSource, CsvDataLoadOptions } = require('@groupdocs/groupdocs.assembly');

// Data like:
// # Exported persons
// Name;Age;Birth
// 'Doe; John';30;1989-04-01 4:00:00 pm
const options = new CsvDataLoadOptions(true);
options.setDelimiter(java.newChar(';'));
options.setQuoteChar(java.newChar("'"));
options.setCommentChar(java.newChar('#'));
const dataSource = new CsvDataSource('persons.csv', options);
```

For more examples, see [Working with CSV Data Sources](/assembly/nodejs-java/working-with-csv-data-sources/).

### Setting up Known External Types

GroupDocs.Assembly Engine must be aware of external types that you reference in your template before the engine processes the template. You can set up external types known by the engine through the collection returned by `DocumentAssembler.getKnownTypes()`. The collection represents an unordered set (that is, a collection of unique items) of Java `Class` objects and provides the `add`, `remove`, `clear` and `getCount` methods. Every type in the set must meet the requirements declared at [Using Types](/assembly/nodejs-java/template-syntax-part-1-of-2/#using-types).

**Note:** Aliases of simple types like int, string, and others are known by the engine by default. Other classes, including `java.lang.Math` and `java.lang.Integer`, must be added explicitly before you access their static members in a template.

In Node.js, the known types are Java classes. Get a `Class` object with `java.findClassSync` and add it to the set. For example, given a template that uses a static member of `java.lang.Math`:

```
<<[Math.abs(-5)]>>
```

you can use the following code to make the engine aware of the class before processing the template:

```javascript
const java = require('java');
const { DocumentAssembler, DataSourceInfo, JsonDataSource } = require('@groupdocs/groupdocs.assembly');

const assembler = new DocumentAssembler();
assembler.getKnownTypes().add(java.findClassSync('java.lang.Math'));
assembler.assembleDocument('template.docx', 'report.docx', new DataSourceInfo(new JsonDataSource('data.json'), 'ds'));
```

Your own helper types must be Java classes as well (for example, compiled into a JAR that you add with `java.classpath.push(...)` before the package is loaded). JavaScript functions and classes cannot be registered as known types.

{{< alert style="warning" >}}On Java 16 and later, accessing static members of known types fails with an error like *Can not resolve method 'abs' on type 'class java.lang.Math'* while the reflection optimization (see [Optimizing Reflection Calls](#optimizing-reflection-calls)) is enabled, because the JVM denies the reflective access the optimization needs. Use one of the following workarounds:

- Open the `java.lang` package to the library before the package is loaded:
  `const java = require('java'); java.options.push('--add-opens=java.base/java.lang=ALL-UNNAMED');`
- Or disable the optimization: `DocumentAssembler.setUseReflectionOptimization(false);`

On Java 8 and 11, no workaround is needed.{{< /alert >}}

### Accessing Missing Members of Data Objects

By default, GroupDocs.Assembly forbids access to missing members of data objects used to build a report in template expressions. On an attempt to use a missing member of a data object, the assembler throws an exception.

But in some scenarios, members of data objects are not exactly known while designing a template. For example, if using a `DataSet` instance loaded from XML without its schema defined, or JSON data where some properties are optional, some of the expected data members can be missing.

To support such scenarios, the assembler provides an option to treat missing members of data objects as null literals. You can enable the option as shown in the following example.

```javascript
const { DocumentAssembler, DocumentAssemblyOptions } = require('@groupdocs/groupdocs.assembly');

const assembler = new DocumentAssembler();
assembler.setOptions(DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS);
assembler.assembleDocument(...);
```

Consider the following example. Given that `r` is a data object (for example, a `DataRow` instance or a JSON object) that does not have a field `Missing`, by default, the following template expression causes the assembler to throw an exception while building a report.

```
<<[r.Missing]>>
```

However, if `DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS` is applied, the assembler treats access to such a field as a null literal, so no exception is thrown and simply no value is written to the report.

`DocumentAssemblyOptions` values are integer flags. To enable several options, combine them with the bitwise OR operator:

```javascript
assembler.setOptions(assembler.getOptions()
  | DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS
  | DocumentAssemblyOptions.REMOVE_EMPTY_PARAGRAPHS);
```

### Optimizing Reflection Calls

GroupDocs.Assembly Engine uses reflection calls while accessing members of Java types. However, reflection calls are much slower than direct calls, which creates a performance overhead.

To reduce the overhead, the engine provides a strategy minimizing the reflection usage. The strategy is based upon runtime type generation. That is, the engine generates a proxy type per an external type. The proxy directly calls members of the corresponding external type, enabling the engine to access these members in a uniform way with no reflection involved. The proxy is [lazily initialized](http://en.wikipedia.org/wiki/Lazy_initialization) and reused further. Thus, reflection is used only while building the proxy.

Although this strategy can significantly minimize the reflection usage in the long run, it creates a performance overhead of the runtime type generation. So, if you deal with small data collections all the time while building your reports, consider disabling the strategy.

You can control the strategy through the static `DocumentAssembler.setUseReflectionOptimization` method. By default, the strategy is enabled.

```javascript
const { DocumentAssembler } = require('@groupdocs/groupdocs.assembly');

DocumentAssembler.setUseReflectionOptimization(false);
console.log(DocumentAssembler.getUseReflectionOptimization()); // false
```

The setting is global: it applies to all `DocumentAssembler` instances in the process.

### Integrating with Native Spreadsheet Data Types

By default, GroupDocs.Assembly outputs expression results as string values regardless of expression types. In most scenarios, this is the best option, since expression results can be formatted through template syntax depending on expression types. However, for Spreadsheet documents, this may interfere with calculation of formulas expecting values of types other than string. To overcome this, GroupDocs.Assembly provides integration with native Spreadsheet data types, which can be enabled as shown in the following code snippet.

```javascript
const { DocumentAssembler, DocumentAssemblyOptions } = require('@groupdocs/groupdocs.assembly');

const assembler = new DocumentAssembler();
assembler.setOptions(DocumentAssemblyOptions.USE_SPREADSHEET_DATA_TYPES);

assembler.assembleDocument(...);
```

Let us show how it works by using an example. Let `number` be a numeric value. Then, consider the following template for a Spreadsheet cell.

```
<<[number]>>
```

By default, while assembling a document, GroupDocs.Assembly converts `number` into a string. However, when integration with native Spreadsheet data types is enabled, the cell's value is written as a number, thus enabling to use it in Spreadsheet formulas expecting numbers.

Integration with native Spreadsheet data types also affects formatting of the cell's value: If a numeric format is defined for the cell (for example, using the "Format Cells" context menu in Microsoft Excel), then the format is applied; otherwise, a default numeric format for cells is applied.

**Note –** The same applies to other native Spreadsheet data types such as date-time and Boolean.

The following table describes in which cases integration with native Spreadsheet data types has no effect even when enabled.

| Cell Template Syntax Example    | Explanation                                                  |
| ------------------------------- | ------------------------------------------------------------ |
| `<<[number]:ordinal>>`            | If an expression result is formatted using template syntax, it is written as a string. |
| `Some text <<[number]>>`          | Presence of text other than template syntax makes a result cell value to become a string. |
| `<<[number]>><<[anotherNumber]>>` | Results of multiple expressions in a single cell are converted to strings and concatenated. |

## Technical Considerations

Here, we reveal some technical aspects and implementation details related to the GroupDocs.Assembly Engine which can be useful for you while making design decisions for your applications.

### Java Semantics

Because the engine runs in a JVM, template expressions follow Java semantics: Java types (`String`, `Long`, `Double`, `Boolean`, `java.util.Date` and so on) and Java methods of these types (for example, `<<[Name.toUpperCase()]>>` or `<<[Name.length()]>>`). Numeric results are printed the way Java prints them, which is why an average of integer values is output as `36.0` in the examples above.

### Implicit Enumeration Determination

If you do not specify the type of an enumeration item in a `foreach` statement or lambda function signature within your template explicitly, the type is implicitly determined by the engine from the type of the enumeration as follows:

1.  If the enumeration represents a `DataTable` instance, then the item represents its row.
2.  Otherwise, if the enumeration represents child rows of a `DataTable` row, then the item represents a child row.
3.  Otherwise, if the enumeration implements generic `Iterable<T>`, then the item type is a type argument corresponding to T. Note that in some cases it is impossible to extract type arguments at runtime due to the Java [Type Erasure](http://docs.oracle.com/javase/tutorial/java/generics/erasure.html) feature. That is why the engine is capable to extract the item type only if one of the following conditions is met:
    *   The enumeration expression represents an invocation of a type member which return type is a parameterized type like `Iterable<String>`, `ArrayList<Integer>`, and so forth.
    *   The type of the enumeration implements or extends a parameterized type like `Iterable<String>`, `ArrayList<Integer>`, and so forth.
4.  Otherwise, the item type is `Object`.

Sequences produced by `JsonDataSource`, `XmlDataSource`, `CsvDataSource` and `DataSet` are handled by the engine automatically, so you do not need to declare item types for them.
