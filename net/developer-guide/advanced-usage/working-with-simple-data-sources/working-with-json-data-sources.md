---
id: working-with-json-data-sources
url: assembly/net/working-with-json-data-sources
title: Working with JSON Data Sources
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for .NET
hideChildren: False
---
{{< alert style="info" >}}This feature is only compatible with GroupDocs.Assembly for .NET 19.10 or later releases.{{< /alert >}}

To access JSON data while building a report, the GroupDocs.Assembly API introduces *JsonDataSource* class. You can pass its instance to the assembler as a data source. Using of *JsonDataSource* enables you to work with typed values of JSON elements in template

documents. For more convenience, the set of simple JSON types is extended as follows:

*   Int32?
*   Int64?
*   Double?
*   Boolean?
*   DateTime?
*   String

### Treating the top level arrays or objects having array

In template documents, if a top-level JSON element is an array or an object having only one property of an array type, a JsonDataSource instance should be treated in the same way as if it was a DataTable instance (see "[Working with DataTable and DataView Objects](https://docs.groupdocs.com/assembly/net/template-syntax-part-1-of-2/#using-data-sources)" for more information) .

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

### Using nullable values like values of typed objects

{{< alert style="info" >}}This feature is supported by version 26.11 or greater.{{< /alert >}}

A JSON value may be `null` or missing, so simple values reach a template as `Nullable<T>`: `Int32?`, `Int64?`, `Double?`, `Boolean?` and `DateTime?`. A template uses them the same way as values of typed objects, without `.Value` or `== true`:

*   members of dates and numbers: `<<[o.Date.Month]>>`, `<<[o.Total.ToString("F2")]>>`;
*   Booleans as conditions: `<<if [o.Paid]>>`, `<<[o.Paid ? "paid" : "due"]>>`, `o.Paid && o.Date.Year == 2026`;
*   Booleans in predicates of extension methods: `orders.Where(x => x.Paid)`, `orders.Count(x => x.Paid)`, `orders.Any(x => x.Paid)`.

For a missing value, a member gives an empty value and a condition is false. `Value`, `HasValue` and other members of `Nullable<T>` keep their meaning, so existing templates give the same result.

Suppose we have JSON data like:
```json
[
  { "Number": 1, "Paid": true,  "Date": "2026-03-05", "Total": 12.5 },
  { "Number": 2, "Paid": false, "Date": "2026-04-10", "Total": 7 },
  { "Number": 3, "Paid": null,  "Date": null,         "Total": null }
]
```

If we use the template like following:
```
<<foreach [o in orders]>>#<<[o.Number]>>: <<[o.Date.Month]>>/<<[o.Date.Year]>>, <<[o.Total.ToString("F2")]>>, <<[o.Paid ? "paid" : "due"]>>
<</foreach>>Paid orders: <<[orders.Count(x => x.Paid)]>>
<<if [orders.Any(x => x.Paid && x.Date.Year == 2026)]>>Payments received in 2026.<</if>>
```

The result will be like:
```
#1: 3/2026, 12.50, paid
#2: 4/2026, 7.00, due
#3: /, , due
Paid orders: 1
Payments received in 2026.
```

The same template works with the same data loaded from XML or CSV. Example: [UseFileDataLikeTypedObjects.cs](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/GroupDocs.Assembly.Examples.CSharp/AdvancedUsage/UseFileDataLikeTypedObjects.cs).

### Treating the objects at top level

If a top-level JSON element represents an object, a *JsonDataSource* instance should be treated in template documents in the same way as if it was a *DataRow* instance (see "[Working with *DataRow* and *DataRowView* Objects](https://docs.groupdocs.com/assembly/net/template-syntax-part-1-of-2/#using-data-sources)" for more information). If a top-level JSON object has a single property that is also an object, then this nested object is accessed by the assembler instead.

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

{{< gist GroupDocsGists 330892e76bb1958b9199e3d223962e27 >}}

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

### Comparing nested objects in GroupBy and Distinct

{{< alert style="info" >}}This feature is supported by version 26.11 or greater.{{< /alert >}}

Nested JSON objects are compared by value, including their own nested objects. For example, `GroupBy(o => o.Customer)` puts orders whose `Customer` objects hold equal values into one group, and `Select(o => o.Customer).Distinct()` returns each such customer once. See [Enumeration Extension Methods]({{< ref "assembly/net/developer-guide/advanced-usage/enumeration-extension-methods.md" >}}) for an example.

### References between objects ($id and $ref)

{{< alert style="info" >}}This feature is supported by version 26.11 or greater.{{< /alert >}}

JSON written by Json.NET with preserved references holds an object once, marked with `$id`, and refers to it from other places with `$ref`:

```json
{ "Orders": [ { "Customer": { "$id": "1", "Name": "A" } }, { "Customer": { "$ref": "1" } } ] }
```

*JsonDataSource* resolves such references: `$ref` gives a copy of the object it names, so `<<[o.Customer.Name]>>`, `OrderBy` and `GroupBy` work on it.

*   Objects with different `$id` values are different objects, even if their values are equal.
*   An object may refer to an object holding it, such as an order that refers to the customer holding the order. The simple values of that object are available, and its member that would repeat the path (`Order.Customer.Order`) gives the parent object.
*   A `$ref` without a matching `$id` is ignored.
*   Data that would grow over one million nodes because of references fails with an exception.

In [Customers.json](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/DataSources/Customers.json), every order refers to its customer with `$ref`. If we use the template like following:
```
<<foreach [c in customers]>>Customer: <<[c.CustomerName.Trim()]>>
<<foreach [o in c.Order.OrderBy(x => x.OrderDate)]>><<[o.OrderDate.Month]>>/<<[o.OrderDate.Year]>>: <<[o.Product.ProductName]>> for <<[o.Customer.CustomerName.Trim()]>>, <<[o.Customer.ShippingAddress]>>
<</foreach>><</foreach>>
```

```csharp
DocumentAssembler assembler = new DocumentAssembler();
assembler.AssembleDocument("Customer orders.docx", "output.docx",
    new DataSourceInfo(new JsonDataSource("Customers.json"), "customers"));
```

The result will be like (excerpt):
```
Customer: Ali Ahmed
2/2015: Lenovo G50 for Ali Ahmed, Quette House, Park Road, ISB
6/2015: Nexus 5 for Ali Ahmed, Quette House, Park Road, ISB
10/2015: Pavilion G6 for Ali Ahmed, Quette House, Park Road, ISB
```

Example: [UseFileDataLikeTypedObjects.cs](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/GroupDocs.Assembly.Examples.CSharp/AdvancedUsage/UseFileDataLikeTypedObjects.cs).

### Using a JSON Schema

{{< alert style="info" >}}This feature is supported by version 26.11 or greater.{{< /alert >}}

A template is checked against the structure of its data before any `<<if>>` is evaluated. Without a schema, that structure is taken from the JSON data itself, so a reference inside a branch that is never rendered fails when the data behind it is `null`, an empty array or missing. For example, with `"Cards": []` or `"Cards": null`, the following template fails with "Can not get the value of member 'Type'" even though the condition is false:

```
<<if [customer.Cards.Count() > 0]>>Payment card: <<[customer.Cards.First().Type]>><</if>>
```

*JsonDataSource* accepts a JSON Schema, the same way *XmlDataSource* accepts an XML Schema. The template is then checked against the schema rather than the data:

*   members declared in the schema can be referenced even if they are `null`, empty or absent in the data;
*   members not declared in the schema still fail, so misspelled names are detected as before;
*   value types come from the schema, so a `boolean` is a Boolean and a `string` holding digits stays a string.

The schema is passed with one of these constructors:

*   `JsonDataSource(string jsonPath, string jsonSchemaPath)`
*   `JsonDataSource(string jsonPath, string jsonSchemaPath, JsonDataLoadOptions options)`
*   `JsonDataSource(Stream jsonStream, Stream jsonSchemaStream)`
*   `JsonDataSource(Stream jsonStream, Stream jsonSchemaStream, JsonDataLoadOptions options)`

The customer below has no payment cards and no loyalty data, and its account number is a string of digits.

#### JSON (Customer.json)
```json
{ "Name": "Quayside Bistro", "Account": "00042", "Cards": [], "Loyalty": null }
```

#### JSON Schema (Customer.schema.json)
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "Name": { "type": "string" },
    "Account": { "type": "string" },
    "Cards": {
      "type": "array",
      "items": { "type": "object", "properties": { "Type": { "type": "string" }, "Last4": { "type": "string" } } }
    },
    "Loyalty": { "type": ["object", "null"], "properties": { "Level": { "type": "string" } } }
  }
}
```

#### Template document
```
Customer: <<[customer.Name]>>
Account number: <<[customer.Account]>>
<<if [customer.Cards.Count() > 0]>>Payment card: <<[customer.Cards.First().Type]>> ending in <<[customer.Cards.First().Last4]>><<else>>No payment card on file.<</if>>
Loyalty program: <<[customer.Loyalty?.Level]>>
```

#### Source code
```csharp
using GroupDocs.Assembly;
using GroupDocs.Assembly.Data;

JsonDataSource dataSource = new JsonDataSource("Customer.json", "Customer.schema.json");

DocumentAssembler assembler = new DocumentAssembler();
assembler.AssembleDocument("Json schema.docx", "output.docx", new DataSourceInfo(dataSource, "customer"));
```

#### Result document
```
Customer: Quayside Bistro
Account number: 00042
No payment card on file.
Loyalty program:
```

Without the schema, the same template fails on `customer.Cards.First().Type`, and the account number is read as the number `42`. Example: [AssembleFromJsonWithSchema.cs](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/GroupDocs.Assembly.Examples.CSharp/AdvancedUsage/AssembleFromJsonWithSchema.cs).

Supported JSON Schema keywords: `type` (including nullable types such as `["string", "null"]`), `properties`, `items`, `format` (`date-time` and `date` give date values), `enum`, `const`, `allOf`, and local `$ref` pointers (`#/$defs/...`, `#/definitions/...`).

{{< alert style="warning" >}}`oneOf`, `anyOf`, `not`, remote or recursive `$ref`, tuple-form `items` and arrays of arrays are not supported and cause an exception. With a schema, `JsonDataLoadOptions.SimpleValueParseMode` and `ExactDateTimeParseFormats` are not applied (date values must follow ISO 8601), and data members not declared in the schema are ignored.{{< /alert >}}

{{< alert style="info" >}}A call such as `new JsonDataSource(path, null)` with a literal `null` second argument is ambiguous at compile time since version 26.11. Cast the argument: `new JsonDataSource(path, (JsonDataLoadOptions)null)`.{{< /alert >}}

### Recognition of JSON simple values

For recognition of JSON simple values (null, boolean, number, integer, and string), the engine provides two modes: *loose* and *strict*. In the loose mode, types of JSON simple values are determined upon parsing of their string representations. In the strict mode, types of JSON simple values are determined from JSON notation itself. To see the main difference between the modes, consider the following JSON snippet.

```
{ prop: "123" }
```

In the loose mode, the type of prop is determined as integer, whereas in the strict mode, it is determined as string.

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

A date-only value, such as "2020-01-01", keeps its date regardless of the time zone of the server: `<<[date]:"dd.MM.yyyy">>` prints `01.01.2020` on any server. A value with `Z` or a UTC offset, such as "2024-11-03T23:00:00Z" or "2024-11-03T23:00:00+02:00", keeps its exact instant, and the result does not depend on the server time zone either. Date-only values are handled this way since version 26.11.

Although this approach is quite flexible, in some scenarios, you may need to restrict strings to be recognized as date-time values. You can achieve this by specifying an exact format in the context of the current culture to be used while parsing date-time values from strings as shown in the following example.

```
JsonDataLoadOptions options = new JsonDataLoadOptions();
options.ExactDateTimeParseFormat = "MM/dd/yyyy";
JsonDataSource dataSource = new JsonDataSource(..., options);
```

In this example, strings conforming the format "MM/dd/yyyy" are going to be recognized as date-time values while loading JSON, whereas the others are not (but see the following note).

In some scenarios, you may need to disable recognition of date-time values at all, for example, when you deal with strings containing already formatted date-time values, which you do not want to re-format using the engine. You can achieve this by setting the exact date-time parse format to an empty string (but see the following note).

**Note –** Strings conforming the Microsoft® JSON date-time format (for example, "/Date(1224043200000)/") are always recognized as date-time values regardless of the exact date-time parse format.

### Download

#### Data Source Document

*   [ManagerData.json](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Data%20Sources/JSON%20DataSource/ManagerData.json?raw=true)

#### Template

*   [Demo Template.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Source/Word%20Templates/Using%20Spreadsheet%20as%20Table%20of%20Data.docx?raw=true)

A complete scenario built on a JSON data source and a JSON Schema: [Generate Word documents from LLM output]({{< ref "/assembly/net/use-cases/generate-documents-from-llm-output.md" >}}).
