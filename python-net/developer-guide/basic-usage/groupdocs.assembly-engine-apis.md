---
id: groupdocs-assembly-engine-apis
url: assembly/python-net/groupdocs-assembly-engine-apis
title: GroupDocs.Assembly Engine APIs
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will discuss the behavior of GroupDocs.Assembly APIs.{{< /alert >}}

## Overview of the API

Classes of GroupDocs.Assembly are located within the GroupDocs.Assembly namespace. The main of the classes is DocumentAssembler. All the functionality required to build a report from a template is assembled within the class.

### Building Reports

To build a report from a template, you can use one of the `DocumentAssembler.AssembleDocument` overloads. The following table describes parameters of these overloads.

| Parameter | Description |
| --- | --- |
| document | A template document. At runtime, this document instance is populated with a data from the specified source and becomes a ready report. |
| dataSource | An object providing a data to populate the specified template. The object must be of one of the following types:<ul><li>`JsonDataSource`</li><li>`XmlDataSource`</li><li>`CsvDataSource`</li><li>`DataSet`</li><li>`DataTable`</li><li>`DataRow`</li><li>`DataView`</li><li>`DataRowView`</li><li>`IDataReader`</li><li>`IDataRecord`</li><li>An object of a custom [visible type](https://docs.groupdocs.com/assembly/python-net/template-syntax-part-1-of-2/#using-types)</li></ul> |
| dataSourceName | The identifier of the specified data source object within the specified template. You can omit this identifier, if the template uses the [contextual object member access](https://docs.groupdocs.com/assembly/python-net/template-syntax-part-1-of-2/#using-contextual-object-member-access) when dealing with the data source. |

Given a template to be populated with a data from a DataSet instance that is identified as "ds" within the template, you can use the following code to build the corresponding report.

```python
//Setting up source document template
strDocumentTemplate = "Template Folder/wordTemplate.docx";
//Setting up destination document report
strDocumentReport = "Report Folder/wordReport.docx";
// Setting up a data set.
DataSourceInfo = ...
array = [DataSourceInfo]

assembler = ga.DocumentAssembler()

assembler.AssembleDocument(strDocumentTemplate, strDocumentReport, array);
```

### Accessing XML Data

To access XML data while building a report, you can use facilities of `DataSet` to read XML into it and then pass it to the engine as a data source. However, if your scenario does not permit to specify XML schema while loading XML into `DataSet`, all attributes and text values of XML elements are loaded as strings then. Thus, it becomes impossible, for example, to use arithmetic operations on numbers or to specify custom date-time and numeric formats to output corresponding values, because all of them are treated as strings.

To overcome this limitation, you can pass an `XmlDataSource` instance to the engine as a data source instead. Even when XML schema is not provided, `XmlDataSource` is capable to recognize values of the following types by their string representations:

- Int64?
- Double?
- Boolean?
- DateTime?

**Note –** For recognition of data types to work, string representations of corresponding attributes and text values of XML elements must be formed using invariant culture settings.

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
Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth:
<<[Birth]:"dd.MM.yyyy">>

Children:

<<foreach [in Child]>><<[Child_Text]>>
<</foreach>>
```

Source code

```
dataSource = ga.data.XmlDataSource(constants.productXmlFile)
DataSourceInfo = ga.DataSourceInfo(dataSource)
    array = [DataSourceInfo]
assembler = ga.DocumentAssembler()
assembler.AssembleDocument(..., array);
```

Result document

```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989

Children:

Ann Doe
Charles Doe
```

**Note –** To reference a sequence of repeated simple-type XML elements with the same name, the elements’ name itself (for example, “Child”) should be used in a template document, whereas the same name with the “_Text” suffix (for example, “Child_Text”) should be used to reference the text value of one of these elements.

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

Average age: <<[persons.Average(p => p.Age)]>>
```

Source code

```
dataSource = ga.data.XmlDataSource(constants.productXmlFile)
DataSourceInfo = ga.DataSourceInfo(dataSource)
    array = [DataSourceInfo]
assembler = ga.DocumentAssembler()
assembler.AssembleDocument(..., array);
```

Result document

```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968

Average age: 36
```

However, if your scenario requires an internal object for a root XML element to be always generated while loading data to `XmlDataSource`, you can force this as shown in the following code snippet.

```
XmlDataLoadOptions options = new XmlDataLoadOptions();
options.AlwaysGenerateRootObject = true;
XmlDataSource dataSource = new XmlDataSource(..., options);
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

```
dataSource = ga.data.XmlDataSource(constants.productXmlFile)
DataSourceInfo = ga.DataSourceInfo(dataSource, "Manager")
    array = [DataSourceInfo]
assembler = ga.DocumentAssembler()
assembler.AssembleDocument(..., array);
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

### Accessing JSON Data

To access JSON data while building a report, you can pass a `JsonDataSource` instance to the engine as a data source.

Using of `JsonDataSource` enables you to work with typed values of JSON elements in template documents. For more convenience, the set of simple JSON types is extended as follows:

- Int64?
- Double?
- Boolean?
- DateTime?
- String

**Note –** Working with complex JSON types (objects and arrays) is also supported.

While loading data to `JsonDataSource`, the engine performs JSON deserialization and generates corresponding internal objects. So, in template documents, a `JsonDataSource` instance should be treated according to what a root JSON element represents.

If a root JSON element is an object, a `JsonDataSource` instance should be treated as an object as well as shown in the following example.

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

```
 dataSource = ga.data.JsonDataSource(constants.customerJsonFile)
DataSourceInfo = ga.DataSourceInfo(dataSource)
    array = [DataSourceInfo]
assembler = ga.DocumentAssembler()
assembler.AssembleDocument(..., array);
```

Result document

```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989

Children:

Ann Doe
Charles Doe
```

**Note –** To reference a JSON object property that is an array of simple-type values, the name of the property (for example, “Child”) should be used in a template document, whereas the same name with the “_Text” suffix (for example, “Child_Text”) should be used to reference the value of an item of this array.

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

Average age: <<[persons.Average(p => p.Age)]>>
```

Source code

```
 dataSource = ga.data.JsonDataSource(constants.customerJsonFile)
DataSourceInfo = ga.DataSourceInfo(dataSource, "person")
    array = [DataSourceInfo]
assembler = ga.DocumentAssembler()
assembler.AssembleDocument(..., array);
```

Result document

```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968

Average age: 36
```

By default, if a root JSON element is an object having only one property that is an object or array in turn, the engine does not generate an internal root object while loading JSON data. So, in template documents, such a `JsonDataSource` instance should be treated according to what this property represents instead. For instance, the following JSON snippets can be used to produce the same results in previous examples of this section respectively.

JSON1

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

```
options = ga.JsonDataLoadOptions();
options.AlwaysGenerateRootObject = true;
dataSource = new JsonDataSource(..., options);
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

```
dataSource = ga.data.JsonDataSource(constants.customerJsonFile)
DataSourceInfo = ga.DataSourceInfo(dataSource, "managers")
    array = [DataSourceInfo]
assembler = ga.DocumentAssembler()
assembler.AssembleDocument(..., array);
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

For recognition of JSON simple values (null, boolean, number, integer, and string), the engine provides two modes: *loose* and *strict*. In the loose mode, types of JSON simple values are determined upon parsing of their string representations. In the strict mode, types of JSON simple values are determined from JSON notation itself. To see the main difference between the modes, consider the following JSON snippet.

`{ prop: "123" }`

In the loose mode, the type of `prop` is determined as integer, whereas in the strict mode, it is determined as string.

The loose mode is used by the engine by default to support more typed data representation options. However, in some scenarios, it can be more preferable to disable recognition of numbers and other JSON simple values from strings, for example, when you need to keep leading padding zeros in a string value representing a number. In this case, you can switch to the strict mode as shown in following code snippet.

```
JsonDataLoadOptions options = new JsonDataLoadOptions();
options.SimpleValueParseMode = JsonSimpleValueParseMode.Strict;
JsonDataSource dataSource = new JsonDataSource(..., options);
```

**Note –** Parsing of date-time values does not depend on whether the loose or strict mode is used.

Recognition of date-time values is a special case, because [JSON specification](https://www.json.org) does not define a format for their representation. So, by default, while parsing date-time values from strings, the engine tries several formats in the following order:

1. [The ISO-8601 format](https://en.wikipedia.org/wiki/ISO_8601) (for values like "2015-03-02T13:56:04Z")
2. [The Microsoft® JSON date-time format](https://docs.microsoft.com/en-us/previous-versions/dotnet/articles/bb299886(v=msdn.10)#from-javascript-literals-to-json) (for values like "/Date(1224043200000)/")
3. All date-time formats supported for the current culture
4. All date-time formats supported for the English USA culture
5. All date-time formats supported for the English New Zealand culture

Although this approach is quite flexible, in some scenarios, you may need to restrict strings to be recognized as date-time values. You can achieve this by specifying one or several exact formats in the context of the current culture to be used while parsing date-time values from strings as shown in the following example.

```
List<String> formats = new List<String>();
formats.Add("MM/dd/yyyy");

JsonDataLoadOptions options = new JsonDataLoadOptions();
options.ExactDateTimeParseFormats = formats;
JsonDataSource dataSource = new JsonDataSource(..., options);
```

In this example, strings conforming the format "MM/dd/yyyy" are going to be recognized as date-time values while loading JSON, whereas the others are not (but see the following note).

In some scenarios, you may need to disable recognition of date-time values at all, for example, when you deal with strings containing already formatted date-time values, which you do not want to re-format using the engine. You can achieve this by setting the exact date-time parse formats to an empty list (but see the following note).

**Note –** Strings conforming the Microsoft® JSON date-time format (for example, "/Date(1224043200000)/") are always recognized as date-time values regardless of the exact date-time parse formats.

### Accessing CSV Data

To access CSV data while building a report, you can pass a `CsvDataSource` instance to the engine as a data source.

Using of `CsvDataSource` enables you to work with typed values rather than just strings in template documents. Although CSV as a format does not define a way to store values of types other than strings, `CsvDataSource` is capable to recognize values of the following types by their string representations:

- Int64?
- Double?
- Boolean?
- DateTime?

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
Average age: <<[persons.Average(p => p.Column2)]>>
```

Source code

```
CsvDataSource dataSource = ... // Loading CSV.

DocumentAssembler assembler = new DocumentAssembler();
assembler.AssembleDocument(..., new DataSourceInfo(dataSource, "persons"));
```

Result document

```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968

Average age: 36
```

By default, `CsvDataSource` uses column names such as “Column1”, “Column2”, and so on, as you can see from the previous example. However, `CsvDataSource` can be configured to read column names from the first line of CSV data as shown in the following example.

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
Average age: <<[persons.Average(p => p.Age)]>>
```

Source code

```
CsvDataLoadOptions options = new CsvDataLoadOptions(true);
CsvDataSource dataSource = new CsvDataSource(..., options); // Loading CSV.

DocumentAssembler assembler = new DocumentAssembler();
assembler.AssembleDocument(..., new DataSourceInfo(dataSource, "persons"));
```

Result document

```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968

Average age: 36
```

Also, you can use `CsvDataLoadOptions` to customize the following characters playing special roles while loading CSV data:

- Value separator (the default is comma)
- Single-line comment start (the default is sharp)
- Quotation mark enabling to use other special characters within a value (the default is double quotes)

### Setting up Known External Types

GroupDocs.Assembly Engine must be aware of custom external types that you reference in your template before the engine processes the template. You can set up external types known by the engine through the DocumentAssembler.KnownTypes property. The property represents an unordered set (that is, a collection of unique items) of [Type](http://msdn.microsoft.com/en-us/library/system.type(v=vs.110).aspx) objects. Every type in the set must meet requirements declared at [Working with Types](https://docs.groupdocs.com/assembly/python-net/template-syntax-part-1-of-2/#using-types).

**Note:** Aliases of simple types like int, string, and others are known by the engine by default.

Consider the following example. Given an ImageUtil class declared at your application and a template accessing a static member of this class, you can use the following code to make the engine be aware of the class before processing the template.

```csharp
DocumentAssembler assembler = new DocumentAssembler;
assembler.KnownTypes.Add(typeof(ImageUtil));
assembler.AssembleDocument(...);
```

### Accessing Missing Members of Data Objects

By default, GroupDocs.Assembly forbids access to missing members of data objects used to build a report in template expressions, since such access is forbidden by C# Language Specification 5.0. On attempt to use a missing member of a data object, the assembler throws an exception then.

But in some scenarios, members of data objects are not exactly known while designing a template. For example, if using a `DataSet` instance loaded from XML without its schema defined, some of expected data members can be missing.

To support such scenarios, the assembler provides an option to treat missing members of data objects as null literals. You can enable the option as shown in the following example.

```csharp
DocumentAssembler assembler = new DocumentAssembler();
assembler.Options |= DocumentAssemblyOptions.AllowMissingMembers;
assembler.AssembleDocument(...);
```

Consider the following example. Given that `r` is a `DataRow` instance that does not have a field `Missing`, by default, the following template expression causes the assembler to throw an exception while building a report.

```csharp
<<[r.Missing]>>
```

However, if `DocumentAssemblyOptions.AllowMissingMembers` is applied, the assembler treats access to such a field as a null literal, so no exception is thrown and simply no value is written to the report then.

### Optimizing Reflection Calls

GroupDocs.Assembly Engine uses reflection calls while accessing members of custom external types. However, reflection calls are much slower than direct calls, which creates a performance overhead.

Due to the performance overhead, the engine provides a strategy minimizing the reflection usage. The strategy is based upon the runtime type generation. That is, the engine generates a proxy type per an external type. The proxy directly calls members of the corresponding external type, the engine to access these members in a uniform way with no reflection involved. The proxy is [lazily initialized](http://en.wikipedia.org/wiki/Lazy_initialization) and reused in further. Thus, the reflection is used only while building the proxy.

Although this strategy can significantly minimize the reflection usage in a long run, it creates a performance overhead of the runtime type generation. So, if you deal with small data collections all the time while building your reports, consider the disabling of the strategy.

You can control the enabling of the strategy through the `DocumentAssembler.UseReflectionOptimization` static property. By default, the strategy is enabled.

### Integrating with Native Spreadsheet Data Types

By default, GroupDocs.Assembly outputs expression results as string values regardless of expression types. In most scenarios, this is the best option, since expression results can be formatted through template syntax depending on expression types. However, for Spreadsheet documents, this may interfere calculation of formulas expecting values of types other than string. To overcome this, GroupDocs.Assembly provides integration with native Spreadsheet data types, which can be enabled as shown in the following code snippet.

```csharp
DocumentAssembler assembler = new DocumentAssembler();
assembler.Options |= DocumentAssemblyOptions.UseSpreadsheetDataTypes;

assembler.AssembleDocument(...);
```

Let us show how it works by using an example. Let `number` be a numeric value. Then, consider the following template for a Spreadsheet cell.

```csharp
<<[number]>>
```

By default, while assembling a document, GroupDocs.Assembly converts `number` into a string using built-in .NET routines. However, when integration with native Spreadsheet data types is enabled, the cell’s value is written as a number, thus enabling to use it in Spreadsheet formulas expecting numbers.

Integration with native Spreadsheet data types also affects formatting of the cell’s value: If a numeric format is defined for the cell (for example, using “Format Cells” context menu in Microsoft Excel), then the format is applied; otherwise, a default numeric format for cells is applied.

**Note –** The same applies to other native Spreadsheet data types such as date-time and Boolean.

The following table describes, in which cases integration with native Spreadsheet data types has no effect even when enabled.

| Cell Template Syntax Example    | Explanation                                              |
| ----------------------------------- | ------------------------------------------------------------ |
| `<<[number]:ordinal>>`            | If an expression result is formatted using template syntax, it is written as a string. |
| `Some text <<[number]>>`          | Presence of text other than template syntax makes a result cell value to become a string. |
| `<<[number]>><<[anotherNumber]>>` | Results of multiple expressions in a single cell are converted to strings and concatenated. |

## Technical Considerations

Here, we will reveal some technical aspects and implementation details related to the GroupDocs.Assembly Engine which can be useful for you while making design decisions for your applications.

### Implicit Enumeration Determination

If you do not specify the type of an enumeration item in a `foreach` statement or lambda function signature within your template explicitly, the type is implicitly determined by the engine from the type of the enumeration as follows:

1.  If the enumeration represents a `DataTable` instance, then the item type is `DataRow`.
2.  Otherwise, if the enumeration represents a `DataView` instance, then the item type is `DataRowView`.
3.  Otherwise, if the enumeration implements `IDataReader`, then the item type is `IDataRecord`.
4.  Otherwise, if the enumeration represents child rows of a `DataRow` instance, then the item type is `DataRow`.
5.  Otherwise, if the enumeration implements generic `IEnumerable<T>`, then the item type is a type argument corresponding to T. Note, that the engine does not support enumerations that implement `IEnumerable<T>` multiple times using different type arguments.
6.  Otherwise, the item type is `Object`.

### Support for LINQ Providers

The engine does not cooperate with [LINQ providers](http://msdn.microsoft.com/en-us/library/vstudio/bb882640(v=vs.110).aspx). To be aware of consequences of this feature, consider the following example.

Assume, that you have the `City` and `Person` classes defined in your application as follows.

```csharp
public class City
{
    public IList<Person> Persons { get { ... } }
    ...
}
public class Person
{
    public String Name { get { ... } }
    public int Age { get { ... } }
    ...
    }
}
```

Given that `city` is an instance of the `City` class, consider the evaluation of the following template expression by the engine.

```csharp
city.Persons.Where(p => p.Age > 30).OrderBy(p => p.Name)
```

If you use an ORM to provide an interaction of your application with an SQL database in conjunction with a LINQ provider for the ORM, then you most likely expect an SQL query like the following one to be performed in the background while evaluating the template expression.

```csharp
SELECT *
    FROM Persons
    WHERE CityId = @CityId AND Age > 30
    ORDER BY Name
```

However, since the engine does not cooperate with LINQ providers, the actual SQL query in this case is as follows.

```csharp
SELECT *
    FROM Persons
    WHERE CityId = @CityId
```

That is, the engine makes an eager call before applying its built-in extension methods. In some cases, this feature can lead to a significant performance overhead. So, if the performance of your application is your primary concern, then consider a preparing of your sequential data outside your templates. That is, pass to the engine a sequential data that is already filtered, ordered, grouped, and so forth.

### Merging GroupDocs.Assembly

You can use a tool like [ILMerge](http://research.microsoft.com/en-us/people/mbarnett/ilmerge.aspx) to merge GroupDocs.Assembly library with another assembly. But in order to use the Engine, please add the following attribute to the target assembly.

```csharp
[assembly: InternalsVisibleTo(
    "TargetAssemblyName" +
    ".ReportingDynamics" +
    ", PublicKey=TargetAssemblyPublicKey")]
```

`TargetAssemblyName` and `TargetAssemblyPublicKey` stand for the name of your target assembly and its public key (not a public key token) respectively.

Despite of the `InternalsVisibleTo` attribute applied, you can normally use obfuscation routines on your target assembly, if needed. An obfuscation does not harm a functionality of GroupDocs.Assembly Engine.
