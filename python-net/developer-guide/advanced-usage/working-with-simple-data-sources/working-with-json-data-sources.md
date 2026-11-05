---
id: working-with-json-data-sources
url: assembly/python-net/working-with-json-data-sources
title: Working with JSON Data Sources
weight: 2
description: "Working with JSON Data Sources with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: working with json data sources, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
To access JSON data while building a report, the GroupDocs.Assembly API introduces *JsonDataSource* class. You can pass its instance to the assembler as a data source. Using of *JsonDataSource* enables you to work with typed values of JSON elements in template

documents. For more convenience, the set of simple JSON types is extended as follows:

*   Int32?
*   Int64?
*   Double?
*   Boolean?
*   DateTime?
*   String

{{< alert style="info" >}}These are .NET nullable types: in a template, the members of a *JsonDataSource* date need `.Value` (`<<[o.OrderDate.Value.Month]>>`). The same file read with `json.load` and passed as a list of dicts is typed by Python instead: a `datetime` is a date with no `.Value`, a `str` stays a string, and dates are converted in Python first. See [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

### Treating the top level arrays or objects having array

In template documents, if a top-level JSON element is an array or an object having only one property of an array type, a JsonDataSource instance is treated as a collection of rows, like a list of dicts: iterate it with `foreach` (see "[Using data sources]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md#using-data-sources" >}})") .

Suppose we have Json data like:
```
[ 
   { 
      Name:"John Doe",
      Age:30,
      Birth:"1989-04-01 4:00:00 pm"
   },
   { 
      Name:"Jane Doe",
      Age:27,
      Birth:"1992-01-31 07:00:00 am"
   },
   { 
      Name:"John Smith",
      Age:51,
      Birth:"1968-03-08 1:00:00 pm"
   }
]
```

or alternative JSON like:
```
{ 
   Persons:[ 
      { 
         Name:"John Doe",
         Age:30,
         Birth:"1989-04-01 4:00:00 pm"
      },
      { 
         Name:"Jane Doe",
         Age:27,
         Birth:"1992-01-31 07:00:00 am"
      },
      { 
         Name:"John Smith",
         Age:51,
         Birth:"1968-03-08 1:00:00 pm"
      }
   ]
}
```

If we use the template like following:
```
<<foreach \[in persons\]>>Name: <<\[Name\]>>, Age: <<\[Age\]>>, Date of Birth: <<\[Birth\]:"dd.MM.yyyy">>
<</foreach>>
Average age: <<\[persons.Average(p => p.Age)\]>>
```

The results will be produced for both pieces of JSON data like:
```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968
Average age: 36
```

{{< alert style="warning" >}}Using of the custom date-time format becomes possible, because text values of Birth properties are automatically converted to DateTime?.{{< /alert >}}

### Treating the objects at top level

If a top-level JSON element represents an object, a *JsonDataSource* instance is treated in template documents as a single row, like a dict: read its values by name (see "[Using data sources]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md#using-data-sources" >}})"). If a top-level JSON object has a single property that is also an object, then this nested object is accessed by the assembler instead.

Suppose we have Json data like:
```
{ 
   Name:"John Doe",
   Age:30,
   Birth:"1989-04-01 4:00:00 pm",
   Child:[ 
      "Ann Doe",
      "Charles Doe"
   ]
}
```

or alternatively like:
```
{ 
   Person:{ 
      Name:"John Doe",
      Age:30,
      Birth:"1989-04-01 4:00:00 pm",
      Child:[ 
         "Ann Doe",
         "Charles Doe"
      ]
   }
}
```

If we use the template like following:
```
Name: <<\[Name\]>>, Age: <<\[Age\]>>, Date of Birth:
<<\[Birth\]:"dd.MM.yyyy">>
Children:
<<foreach \[in Child\]>><<\[Child\_Text\]>>
<</foreach>>
```

The results will be produced for both pieces of JSON data like:
```
Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Children:
Ann Doe
Charles Doe
```

{{< alert style="warning" >}}To reference a JSON object property that is an array of simple-type values, the name of the property (for example, "Child") should be used in a template document, whereas the same name with the "_Text" suffix (for example, "Child_Text") should be used to reference the value of an item of this array.{{< /alert >}}

### The complete example

The following example sums up typical scenarios involving nested JSON objects and arrays.

#### JSON
```
[ 
   { 
      Name:"John Smith",
      Contract:[ 
         { 
            Client:{ 
               Name:"A Company"
            },
            Price:1200000
         },
         { 
            Client:{ 
               Name:"B Ltd."
            },
            Price:750000
         },
         { 
            Client:{ 
               Name:"C & D"
            },
            Price:350000
         }
      ]
   },
   { 
      Name:"Tony Anderson",
      Contract:[ 
         { 
            Client:{ 
               Name:"E Corp."
            },
            Price:650000
         },
         { 
            Client:{ 
               Name:"F & Partners"
            },
            Price:550000
         }
      ]
   },
   { 
      Name:"July James",
      Contract:[ 
         { 
            Client:{ 
               Name:"G & Co."
            },
            Price:350000
         },
         { 
            Client:{ 
               Name:"H Group"
            },
            Price:250000
         },
         { 
            Client:{ 
               Name:"I & Sons"
            },
            Price:100000
         },
         { 
            Client:{ 
               Name:"J Ent."
            },
            Price:100000
         }
      ]
   }
]
```

#### Template document
```
<<foreach [in managers]>>Manager: <<[Name]>>
Contracts:
<<foreach [in Contract]>>- <<[Client.Name]>> ($<<[Price]>>)
<</foreach>>
<</foreach>>
```

#### Source code

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataSource

assembler = DocumentAssembler()
assembler.assemble_document("data-destination-with-nested-elements.docx", "data-destination-with-nested-elements-report.docx", DataSourceInfo(JsonDataSource("managers.json"), "managers"))
```
{{< /tab >}}
{{< tab "data-destination-with-nested-elements.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [data-destination-with-nested-elements.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-simple-data-sources/working-with-json-data-sources/data-destination-with-nested-elements.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "managers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [managers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-simple-data-sources/working-with-json-data-sources/managers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "data-destination-with-nested-elements-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-simple-data-sources/working-with-json-data-sources/source_code/data-destination-with-nested-elements-report.docx)
{{< /tab >}}
{{< /tabs >}}

#### Result document
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

### Recognition of JSON simple values

For recognition of JSON simple values (null, boolean, number, integer, and string), the engine provides two modes: *loose* and *strict*. In the loose mode, types of JSON simple values are determined upon parsing of their string representations. In the strict mode, types of JSON simple values are determined from JSON notation itself. To see the main difference between the modes, consider the following JSON snippet.

```
{ prop: "123" }
```

In the loose mode, the type of prop is determined as integer, whereas in the strict mode, it is determined as string.

The loose mode is used by the engine by default to support more typed data representation options. However, in some scenarios, it can be more preferable to disable recognition of numbers and other JSON simple values from strings, for example, when you need to keep leading padding zeros in a string value representing a number. In this case, you can switch to the strict mode as shown in following code snippet.

```python
from groupdocs.assembly.data import JsonDataLoadOptions, JsonDataSource, JsonSimpleValueParseMode

options = JsonDataLoadOptions()
options.simple_value_parse_mode = JsonSimpleValueParseMode.STRICT
data_source = JsonDataSource("managers.json", options)
```

**Note –** Parsing of date-time values does not depend on whether the loose or strict mode is used.

Recognition of date-time values is a special case, because [JSON specification](https://www.json.org) does not define a format for their representation. So, by default, while parsing date-time values from strings, the engine tries several formats in the following order:

1. [The ISO-8601 format](https://en.wikipedia.org/wiki/ISO_8601) (for values like "2015-03-02T13:56:04Z")
2. [The Microsoft® JSON date-time format](https://docs.microsoft.com/en-us/previous-versions/dotnet/articles/bb299886(v=msdn.10)#from-javascript-literals-to-json) (for values like "/Date(1224043200000)/")
3. All date-time formats supported for the current culture
4. All date-time formats supported for the English USA culture
5. All date-time formats supported for the English New Zealand culture

Although this approach is quite flexible, in some scenarios, you may need to restrict strings to be recognized as date-time values. You can achieve this by specifying an exact format in the context of the current culture to be used while parsing date-time values from strings as shown in the following example.

```python
from groupdocs.assembly.data import JsonDataLoadOptions, JsonDataSource

options = JsonDataLoadOptions()
options.exact_date_time_parse_format = "MM/dd/yyyy"
data_source = JsonDataSource("managers.json", options)
```

In this example, strings conforming the format "MM/dd/yyyy" are going to be recognized as date-time values while loading JSON, whereas the others are not (but see the following note).

In some scenarios, you may need to disable recognition of date-time values at all, for example, when you deal with strings containing already formatted date-time values, which you do not want to re-format using the engine. You can achieve this by setting the exact date-time parse format to an empty string (but see the following note).

**Note –** Strings conforming the Microsoft® JSON date-time format (for example, "/Date(1224043200000)/") are always recognized as date-time values regardless of the exact date-time parse format.

### Download

#### Data Source Document

*   [data-destination-with-nested-elements.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-simple-data-sources/working-with-json-data-sources/data-destination-with-nested-elements.docx)

#### Template
