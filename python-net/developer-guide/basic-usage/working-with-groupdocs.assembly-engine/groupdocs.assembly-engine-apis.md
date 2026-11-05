---
id: groupdocs-assembly-engine-apis
url: assembly/python-net/groupdocs-assembly-engine-apis
title: GroupDocs.Assembly Engine APIs
weight: 3
description: "The GroupDocs.Assembly for Python via .NET API: DocumentAssembler.assemble_document, DataSourceInfo, Python dicts and lists, XML, JSON and CSV data sources, known types, missing members and spreadsheet data types."
keywords: DocumentAssembler, assemble_document, DataSourceInfo, XmlDataSource, JsonDataSource, CsvDataSource, known_types, dict, Python, GroupDocs.Assembly
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will discuss the behavior of GroupDocs.Assembly APIs.{{< /alert >}}

## Overview of the API

Classes of GroupDocs.Assembly for Python via .NET are located within the `groupdocs.assembly` package, and the data source classes within `groupdocs.assembly.data`. The main of the classes is [`DocumentAssembler`](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/). All the functionality required to build a report from a template is assembled within the class.

### Building Reports

To build a report from a template, you can use the [`DocumentAssembler.assemble_document`](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/assemble_document/) method. The following table describes its parameters.

| Parameter | Description |
| --- | --- |
| `source_path` or `source_stream` | A template document: its path, or a binary file object or `io.BytesIO` to read it from. At runtime, the template is populated with a data from the specified sources and becomes a ready report. |
| `target_path` or `target_stream` | Where to write the report: a path, or a binary file object or `io.BytesIO`. |
| `load_save_options` | Optional. A `LoadSaveOptions` object, for instance to write the report in another format: `LoadSaveOptions(FileFormat.PDF)`. Passed positionally, it goes before the data sources. |
| `data_source_infos` | One [`DataSourceInfo`](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/datasourceinfo/), or a list of them. |

A `DataSourceInfo` pairs a data source with its name:

| Parameter | Description |
| --- | --- |
| `data_source` | An object providing a data to populate the template. It can be one of the following:<ul><li>A `dict`, or a `list` or `tuple` of dicts. The engine reads a dict as an object whose members are its keys (see [Using Data Sources]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md#using-data-sources" >}})).</li><li>A single value: a `str`, a number, a `bool` or a `datetime`, or a list of such values.</li><li>A `JsonDataSource`, `XmlDataSource` or `CsvDataSource`.</li><li>A `DocumentTable` or `DocumentTableSet`.</li></ul> |
| `name` | The identifier of the data source within the template. You can omit this identifier, if the template uses the [contextual object member access]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md#using-contextual-object-member-access" >}}) when dealing with the data source. |

`assemble_document` returns `True` when the report is built. It takes at least one data source.

Given a template to be populated with a data from a list of customers that is identified as "customers" within the template, you can use the following code to build the corresponding report.

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("in-table-list.docx", "in-table-list-report.docx", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "in-table-list.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-table-list.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/in-table-list.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-table-list-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/building_reports/in-table-list-report.docx)
{{< /tab >}}
{{< /tabs >}}

Given a template to be populated with a data about a single customer using the contextual object member access, such as `<<[CustomerName]>>`, you can pass the customer's dict without a name:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("customer-contact.docx", "customer-contact-report.docx", DataSourceInfo(customer))
```
{{< /tab >}}
{{< tab "customer-contact.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-contact.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/customer-contact.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-contact-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/building_reports_2/customer-contact-report.docx)
{{< /tab >}}
{{< /tabs >}}

### Accessing XML Data

To access XML data while building a report, you can pass an `XmlDataSource` instance to the engine as a data source. You can also parse XML yourself, with `xml.etree.ElementTree` for instance, and pass the result as dicts and lists; but then every attribute and text value is a string, unless your code converts it. Thus, it becomes impossible, for example, to use arithmetic operations on numbers or to specify custom date-time and numeric formats to output corresponding values, because all of them are treated as strings.

`XmlDataSource` overcomes this limitation. Even when XML schema is not provided, `XmlDataSource` is capable to recognize values of the following types by their string representations:

- Int64?
- Double?
- Boolean?
- DateTime?

**Note –** For recognition of data types to work, string representations of corresponding attributes and text values of XML elements must be formed using invariant culture settings.

**Note –** The `?` means that the values are .NET nullable types. Operators and format strings work on them directly, but a member of the value is reached through `Value`: `<<[Birth.Value.Year]>>`. A `datetime` in a Python dict needs no `Value`: `<<[Birth.Year]>>`.

While loading data to `XmlDataSource`, the engine performs actions typical for XML deserialization behind the scenes: It maps complex-type XML elements to internal objects and simple-type XML elements to fields of containing objects. So, in template documents, an `XmlDataSource` instance should be treated as an object having corresponding fields and nested objects as shown in the following example.

XML

```xml
<Person>
	<Name>Amara Osei</Name>
	<Age>41</Age>
	<Birth>1984-03-12 9:30:00 am</Birth>
	<Certificate>Food safety level 3</Certificate>
	<Certificate>Forklift operation</Certificate>
</Person>
```

Template document

```text
Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth: <<[Birth]:"dd.MM.yyyy">>

Certificates:

<<foreach [in Certificate]>><<[Certificate_Text]>>
<</foreach>>
```

Source code

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import XmlDataSource

data_source = XmlDataSource("staff-certificates.xml")

assembler = DocumentAssembler()
assembler.assemble_document("staff-certificates.docx", "staff-certificates-report.docx", DataSourceInfo(data_source))
```
{{< /tab >}}
{{< tab "staff-certificates.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-certificates.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-certificates.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-certificates.xml" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-certificates.xml](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-certificates.xml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-certificates-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_xml_data/staff-certificates-report.docx)
{{< /tab >}}
{{< /tabs >}}

Result document

```text
Name: Amara Osei, Age: 41, Date of Birth: 12.03.1984

Certificates:

Food safety level 3
Forklift operation
```

**Note –** To reference a sequence of repeated simple-type XML elements with the same name, the elements' name itself (for example, "Certificate") should be used in a template document, whereas the same name with the "_Text" suffix (for example, "Certificate_Text") should be used to reference the text value of one of these elements.

By default, if a root XML element contains only a sequence of elements of one type, the engine does not generate an internal root object while loading XML data. So, in template documents, such an `XmlDataSource` instance should be treated as a sequence of corresponding nested objects as shown in the following example.

XML

```xml
<Persons>
	<Person>
		<Name>Amara Osei</Name>
		<Age>41</Age>
		<Birth>1984-03-12 9:30:00 am</Birth>
	</Person>
	<Person>
		<Name>Jonas Weber</Name>
		<Age>37</Age>
		<Birth>1988-07-04 2:00:00 pm</Birth>
	</Person>
	<Person>
		<Name>Lena Park</Name>
		<Age>29</Age>
		<Birth>1996-11-21 7:45:00 am</Birth>
	</Person>
</Persons>
```

Template document

```text
<<foreach [in persons]>>Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth: <<[Birth]:"dd.MM.yyyy">>
<</foreach>>

Average age: <<[persons.Average(p => p.Age)]>>
```

Source code

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import XmlDataSource

data_source = XmlDataSource("staff-ages.xml")

assembler = DocumentAssembler()
assembler.assemble_document("staff-ages.docx", "staff-ages-report.docx", DataSourceInfo(data_source, "persons"))
```
{{< /tab >}}
{{< tab "staff-ages.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-ages.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-ages.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-ages.xml" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-ages.xml](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-ages.xml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-ages-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_xml_data_2/staff-ages-report.docx)
{{< /tab >}}
{{< /tabs >}}

Result document

```text
Name: Amara Osei, Age: 41, Date of Birth: 12.03.1984
Name: Jonas Weber, Age: 37, Date of Birth: 04.07.1988
Name: Lena Park, Age: 29, Date of Birth: 21.11.1996

Average age: 35.666666666666664
```

However, if your scenario requires an internal object for a root XML element to be always generated while loading data to `XmlDataSource`, you can force this as shown in the following example. The persons are then a member of the root object, `persons.Person`:

```text
<<foreach [in persons.Person]>>Name: <<[Name]>>, Age: <<[Age]>>
<</foreach>>

Average age: <<[persons.Person.Average(p => p.Age)]>>
```

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import XmlDataLoadOptions, XmlDataSource

options = XmlDataLoadOptions()
options.always_generate_root_object = True
data_source = XmlDataSource("staff-ages.xml", options)

assembler = DocumentAssembler()
assembler.assemble_document("staff-ages-root.docx", "staff-ages-root-report.docx", DataSourceInfo(data_source, "persons"))
```
{{< /tab >}}
{{< tab "staff-ages-root.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-ages-root.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-ages-root.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-ages.xml" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-ages.xml](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-ages.xml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-ages-root-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_xml_data_3/staff-ages-root-report.docx)
{{< /tab >}}
{{< /tabs >}}

The following example sums up typical scenarios involving nested complex-type XML elements. It reads `managers.xml`, Harbor Lane's account managers and their contracts:

XML

```xml
<Managers>
  <Manager>
    <Name>Mei Tanaka</Name>
    <Contract>
      <Client>
        <Name>Harbourview Hotel</Name>
      </Client>
      <Price>120000</Price>
    </Contract>
    <Contract>
      <Client>
        <Name>Quayside Bistro</Name>
      </Client>
      <Price>75000</Price>
    </Contract>
    ...
  </Manager>
  ...
</Managers>
```

Template document

```text
<<foreach [in managers]>>Manager: <<[Name]>>
Contracts:
<<foreach [in Contract]>>- <<[Client.Name]>> ($<<[Price]>>)
<</foreach>>
<</foreach>>
```

Source code

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import XmlDataSource

data_source = XmlDataSource("managers.xml")

assembler = DocumentAssembler()
assembler.assemble_document("manager-contract-list.docx", "manager-contract-list-report.docx", DataSourceInfo(data_source, "managers"))
```
{{< /tab >}}
{{< tab "manager-contract-list.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [manager-contract-list.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/manager-contract-list.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "managers.xml" >}}
{{< tab-text >}}
The following sample file is used in this example: [managers.xml](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/managers.xml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "manager-contract-list-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_xml_data_4/manager-contract-list-report.docx)
{{< /tab >}}
{{< /tabs >}}

Result document

```text
Manager: Mei Tanaka
Contracts:
- Harbourview Hotel ($120000)
- Quayside Bistro ($75000)
- Saltmarsh Deli ($35000)

Manager: Daniel Reyes
Contracts:
- Lantern Street Café ($65000)
- Millbrook Market ($55000)

Manager: Sofia Marino
Contracts:
- Pier Nine Kitchen ($35000)
- The Copper Kettle ($25000)
- Driftwood Grill ($10000)
- Tidewater Tavern ($10000)
```

### Accessing JSON Data

To access JSON data while building a report, you can pass a `JsonDataSource` instance to the engine as a data source. You can also load JSON with `json.load` and pass the resulting dicts and lists, as most examples of this documentation do; then Python's types decide the types of the values, and a date stays a string until your code makes it a `datetime`.

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

```json
{
	"Name": "Amara Osei",
	"Age": 41,
	"Birth": "1984-03-12 9:30:00 am",
	"Certificate": [ "Food safety level 3", "Forklift operation" ]
}
```

Template document

```text
Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth: <<[Birth]:"dd.MM.yyyy">>

Certificates:

<<foreach [in Certificate]>><<[Certificate_Text]>>
<</foreach>>
```

Source code

{{< tabs "example7" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataSource

data_source = JsonDataSource("staff-certificates.json")

assembler = DocumentAssembler()
assembler.assemble_document("staff-certificates.docx", "staff-certificates-from-json.docx", DataSourceInfo(data_source))
```
{{< /tab >}}
{{< tab "staff-certificates.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-certificates.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-certificates.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-certificates.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-certificates.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-certificates.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-certificates-from-json.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_json_data/staff-certificates-from-json.docx)
{{< /tab >}}
{{< /tabs >}}

Result document

```text
Name: Amara Osei, Age: 41, Date of Birth: 12.03.1984

Certificates:

Food safety level 3
Forklift operation
```

**Note –** To reference a JSON object property that is an array of simple-type values, the name of the property (for example, "Certificate") should be used in a template document, whereas the same name with the "_Text" suffix (for example, "Certificate_Text") should be used to reference the value of an item of this array.

If a root JSON element is an array, a `JsonDataSource` instance should be treated as a sequence of items of this array as shown in the following example.

JSON

```json
[
	{
		"Name": "Amara Osei",
		"Age": 41,
		"Birth": "1984-03-12 9:30:00 am"
	},
	{
		"Name": "Jonas Weber",
		"Age": 37,
		"Birth": "1988-07-04 2:00:00 pm"
	},
	{
		"Name": "Lena Park",
		"Age": 29,
		"Birth": "1996-11-21 7:45:00 am"
	}
]
```

Template document

```text
<<foreach [in persons]>>Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth: <<[Birth]:"dd.MM.yyyy">>
<</foreach>>

Average age: <<[persons.Average(p => p.Age)]>>
```

Source code

{{< tabs "example8" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataSource

data_source = JsonDataSource("staff-ages.json")

assembler = DocumentAssembler()
assembler.assemble_document("staff-ages.docx", "staff-ages-from-json.docx", DataSourceInfo(data_source, "persons"))
```
{{< /tab >}}
{{< tab "staff-ages.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-ages.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-ages.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-ages.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-ages.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-ages.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-ages-from-json.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_json_data_2/staff-ages-from-json.docx)
{{< /tab >}}
{{< /tabs >}}

Result document

```text
Name: Amara Osei, Age: 41, Date of Birth: 12.03.1984
Name: Jonas Weber, Age: 37, Date of Birth: 04.07.1988
Name: Lena Park, Age: 29, Date of Birth: 21.11.1996

Average age: 35.666666666666664
```

By default, if a root JSON element is an object having only one property that is an object or array in turn, the engine does not generate an internal root object while loading JSON data. So, in template documents, such a `JsonDataSource` instance should be treated according to what this property represents instead. For instance, the following JSON snippets can be used to produce the same results in previous examples of this section respectively.

JSON 1

```json
{
	"Person":
	{
		"Name": "Amara Osei",
		"Age": 41,
		"Birth": "1984-03-12 9:30:00 am",
		"Certificate": [ "Food safety level 3", "Forklift operation" ]
	}
}
```

JSON 2

```json
{
	"Persons":
	[
		{
			"Name": "Amara Osei",
			"Age": 41,
			"Birth": "1984-03-12 9:30:00 am"
		},
		...
	]
}
```

The second one, with the template of the previous example:

{{< tabs "example9" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataSource

data_source = JsonDataSource("staff-ages-wrapped.json")

assembler = DocumentAssembler()
assembler.assemble_document("staff-ages.docx", "staff-ages-wrapped-report.docx", DataSourceInfo(data_source, "persons"))
```
{{< /tab >}}
{{< tab "staff-ages.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-ages.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-ages.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-ages-wrapped.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-ages-wrapped.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-ages-wrapped.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-ages-wrapped-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_json_data_3/staff-ages-wrapped-report.docx)
{{< /tab >}}
{{< /tabs >}}

However, if your scenario requires an internal object for a root JSON element to be always generated while loading data to `JsonDataSource`, you can force this as shown in the following code snippet.

```python
from groupdocs.assembly.data import JsonDataLoadOptions, JsonDataSource

options = JsonDataLoadOptions()
options.always_generate_root_object = True
data_source = JsonDataSource("staff-ages-wrapped.json", options)
```

The following example sums up typical scenarios involving nested JSON objects and arrays. It reads `managers.json`, the same account managers as `managers.xml` above, with the same template and the same result:

JSON

```json
[
  {
    "Name": "Mei Tanaka",
    "Contract": [
      { "Client": { "Name": "Harbourview Hotel" }, "Price": 120000 },
      { "Client": { "Name": "Quayside Bistro" }, "Price": 75000 },
      { "Client": { "Name": "Saltmarsh Deli" }, "Price": 35000 }
    ]
  },
  ...
]
```

Source code

{{< tabs "example10" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataSource

data_source = JsonDataSource("managers.json")

assembler = DocumentAssembler()
assembler.assemble_document("manager-contract-list.docx", "manager-contract-list-from-json.docx", DataSourceInfo(data_source, "managers"))
```
{{< /tab >}}
{{< tab "manager-contract-list.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [manager-contract-list.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/manager-contract-list.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "managers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [managers.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/managers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "manager-contract-list-from-json.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_json_data_4/manager-contract-list-from-json.docx)
{{< /tab >}}
{{< /tabs >}}

For recognition of JSON simple values (null, boolean, number, integer, and string), the engine provides two modes: *loose* and *strict*. In the loose mode, types of JSON simple values are determined upon parsing of their string representations. In the strict mode, types of JSON simple values are determined from JSON notation itself. To see the main difference between the modes, consider the following JSON snippet.

`{ "prop": "123" }`

In the loose mode, the type of `prop` is determined as integer, whereas in the strict mode, it is determined as string.

The loose mode is used by the engine by default to support more typed data representation options. However, in some scenarios, it can be more preferable to disable recognition of numbers and other JSON simple values from strings, for example, when you need to keep leading padding zeros in a string value representing a number. In this case, you can switch to the strict mode as shown in the following example. It builds the same product list twice: in the loose mode, the code `"00418"` is the number 418; in the strict mode, it stays `00418`.

{{< tabs "example11" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataLoadOptions, JsonDataSource, JsonSimpleValueParseMode

assembler = DocumentAssembler()

# Loose mode (the default): "00418" is read as the number 418
assembler.assemble_document("product-codes.docx", "product-codes-loose.docx",
                            DataSourceInfo(JsonDataSource("product-codes.json"), "products"))

# Strict mode: "00418" stays a string
options = JsonDataLoadOptions()
options.simple_value_parse_mode = JsonSimpleValueParseMode.STRICT
assembler.assemble_document("product-codes.docx", "product-codes-strict.docx",
                            DataSourceInfo(JsonDataSource("product-codes.json", options), "products"))
```
{{< /tab >}}
{{< tab "product-codes.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [product-codes.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/product-codes.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "product-codes.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [product-codes.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/product-codes.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "accessing-json-data-5-outputs.zip" >}}  
```text
product-codes-loose.docx (7 KB)
product-codes-strict.docx (7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_json_data_5/accessing-json-data-5-outputs.zip)
{{< /tab >}}
{{< /tabs >}}

**Note –** Parsing of date-time values does not depend on whether the loose or strict mode is used.

Recognition of date-time values is a special case, because [JSON specification](https://www.json.org) does not define a format for their representation. So, by default, while parsing date-time values from strings, the engine tries several formats in the following order:

1. [The ISO-8601 format](https://en.wikipedia.org/wiki/ISO_8601) (for values like "2015-03-02T13:56:04Z")
2. [The Microsoft® JSON date-time format](https://docs.microsoft.com/en-us/previous-versions/dotnet/articles/bb299886(v=msdn.10)#from-javascript-literals-to-json) (for values like "/Date(1224043200000)/")
3. All date-time formats supported for the current culture
4. All date-time formats supported for the English USA culture
5. All date-time formats supported for the English New Zealand culture

**Note –** An ISO-8601 date without a time, such as "2015-01-14", is read as midnight UTC and converted to the local time: on a computer two hours ahead of UTC, measured with 26.11, it becomes 13 January 2015, 22:00. Write the time, "2015-01-14T00:00:00", to keep the date as it is.

Although this approach is quite flexible, in some scenarios, you may need to restrict strings to be recognized as date-time values. You can achieve this by specifying one or several exact formats in the context of the current culture to be used while parsing date-time values from strings, as a list of strings. In the following example, strings conforming the format "MM/dd/yyyy" (`Ordered`) are recognized as date-time values while loading JSON, whereas the others (`Delivered`, already formatted as the report should show it) are not (but see the following note):

{{< tabs "example12" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataLoadOptions, JsonDataSource

options = JsonDataLoadOptions()
options.exact_date_time_parse_formats = ["MM/dd/yyyy"]
data_source = JsonDataSource("delivery-dates.json", options)

assembler = DocumentAssembler()
assembler.assemble_document("delivery-dates.docx", "delivery-dates-report.docx", DataSourceInfo(data_source, "deliveries"))
```
{{< /tab >}}
{{< tab "delivery-dates.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [delivery-dates.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/delivery-dates.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "delivery-dates.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [delivery-dates.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/delivery-dates.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "delivery-dates-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_json_data_6/delivery-dates-report.docx)
{{< /tab >}}
{{< /tabs >}}

In some scenarios, you may need to disable recognition of date-time values at all, for example, when you deal with strings containing already formatted date-time values, which you do not want to re-format using the engine. You can achieve this by setting the exact date-time parse formats to an empty list, `options.exact_date_time_parse_formats = []` (but see the following note).

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

```text
Amara Osei,41,1984-03-12 9:30:00 am
Jonas Weber,37,1988-07-04 2:00:00 pm
Lena Park,29,1996-11-21 7:45:00 am
```

Template document

```text
<<foreach [in persons]>>Name: <<[Column1]>>, Age: <<[Column2]>>, Date of Birth: <<[Column3]:"dd.MM.yyyy">>
<</foreach>>
Average age: <<[persons.Average(p => p.Column2)]>>
```

Source code

{{< tabs "example13" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import CsvDataSource

data_source = CsvDataSource("staff-ages-no-header.csv")

assembler = DocumentAssembler()
assembler.assemble_document("staff-ages-columns.docx", "staff-ages-columns-report.docx", DataSourceInfo(data_source, "persons"))
```
{{< /tab >}}
{{< tab "staff-ages-columns.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-ages-columns.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-ages-columns.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-ages-no-header.csv" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-ages-no-header.csv](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-ages-no-header.csv)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-ages-columns-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_csv_data/staff-ages-columns-report.docx)
{{< /tab >}}
{{< /tabs >}}

Result document

```text
Name: Amara Osei, Age: 41, Date of Birth: 12.03.1984
Name: Jonas Weber, Age: 37, Date of Birth: 04.07.1988
Name: Lena Park, Age: 29, Date of Birth: 21.11.1996
Average age: 35.666666666666664
```

By default, `CsvDataSource` uses column names such as "Column1", "Column2", and so on, as you can see from the previous example. However, `CsvDataSource` can be configured to read column names from the first line of CSV data as shown in the following example.

CSV

```text
Name,Age,Birth
Amara Osei,41,1984-03-12T09:30:00
Jonas Weber,37,1988-07-04T14:00:00
Lena Park,29,1996-11-21T07:45:00
```

Template document

```text
<<foreach [in persons]>>Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth: <<[Birth]:"dd.MM.yyyy">>
<</foreach>>

Average age: <<[persons.Average(p => p.Age)]>>
```

Source code

{{< tabs "example14" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import CsvDataLoadOptions, CsvDataSource

options = CsvDataLoadOptions(True)
data_source = CsvDataSource("persons.csv", options)

assembler = DocumentAssembler()
assembler.assemble_document("staff-ages.docx", "staff-ages-from-csv.docx", DataSourceInfo(data_source, "persons"))
```
{{< /tab >}}
{{< tab "staff-ages.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-ages.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/staff-ages.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "persons.csv" >}}
{{< tab-text >}}
The following sample file is used in this example: [persons.csv](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/persons.csv)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-ages-from-csv.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_csv_data_2/staff-ages-from-csv.docx)
{{< /tab >}}
{{< /tabs >}}

Result document

```text
Name: Amara Osei, Age: 41, Date of Birth: 12.03.1984
Name: Jonas Weber, Age: 37, Date of Birth: 04.07.1988
Name: Lena Park, Age: 29, Date of Birth: 21.11.1996

Average age: 35.666666666666664
```

Also, you can use `CsvDataLoadOptions` to customize the following characters playing special roles while loading CSV data:

- Value separator, `delimiter` (the default is comma)
- Single-line comment start, `comment_char` (the default is sharp)
- Quotation mark enabling to use other special characters within a value, `quote_char` (the default is double quotes)

```python
from groupdocs.assembly.data import CsvDataLoadOptions, CsvDataSource

options = CsvDataLoadOptions(True)
options.delimiter = ";"
options.comment_char = "%"
options.quote_char = "'"
data_source = CsvDataSource("staff.csv", options)
```

### Setting up Known External Types

GroupDocs.Assembly Engine must be aware of the external types that you reference in your template before the engine processes the template. In Python, these are .NET types: the classes of the .NET runtime, such as `System.Math` or `System.Convert`, whose static members a template can call. You can set up external types known by the engine through the `DocumentAssembler.known_types` property. The property represents an unordered set (that is, a collection of unique items) of types. Add a type by its full .NET name, `known_types.add("System.Math")`, or by a Python type that has a .NET counterpart: `known_types.add(float)` adds `System.Double`. Every type in the set must meet requirements declared at [Using Types]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md#using-types" >}}).

**Note:** Aliases of simple types like `int`, `double`, `string`, and others are known by the engine by default.

Consider the following example. Given a template that rounds the unit price of each order with the static `Math.Round` method, you can use the following code to make the engine be aware of the `System.Math` class before processing the template.

```text
<<foreach [o in customer.Order]>><<[o.OrderNumber]>> | <<[o.Product.ProductName]>> | <<[Math.Round((double)o.Price / o.ProductQuantity, 2)]>><</foreach>>
```

{{< tabs "example15" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.known_types.add("System.Math")
assembler.assemble_document("order-unit-prices.docx", "order-unit-prices-report.docx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "order-unit-prices.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-unit-prices.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/order-unit-prices.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-unit-prices-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/setting_up_known_external_types/order-unit-prices-report.docx)
{{< /tab >}}
{{< /tabs >}}

A Python class or function cannot be a known type: a template calls .NET code only. Compute such values in Python and put them in the data instead.

### Accessing Missing Members of Data Objects

By default, GroupDocs.Assembly forbids access to missing members of data objects used to build a report in template expressions, since such access is forbidden by C# Language Specification 5.0. On attempt to use a missing member of a data object, the assembler throws an exception then, which reaches Python as a `RuntimeError`: "Can not get the value of member 'Email' on type ...".

But in some scenarios, members of data objects are not exactly known while designing a template. For example, if dicts come from a source that leaves a key out when it has no value, some of expected data members can be missing.

**Note –** For Python data, a member is missing only when no dict of its kind has the key. When some dicts of one list have a key and others do not, or hold `None` for it, the member exists and is empty (`null`) where the key is absent.

To support such scenarios, the assembler provides an option to treat missing members of data objects as null literals. You can enable the option as shown in the following example.

```python
assembler = DocumentAssembler()
assembler.options |= DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS
assembler.assemble_document(...)
```

Consider the following example. None of the customers of `customers.json` has an `Email` key, so by default, the template expression `<<[c.Email]>>` causes the assembler to throw an exception while building a report. With `DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS` applied, the assembler treats access to such a member as a null literal, so no exception is thrown and simply no value is written to the report then.

{{< tabs "example16" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler, DocumentAssemblyOptions

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.options |= DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS
assembler.assemble_document("customer-emails.docx", "customer-emails-report.docx", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "customer-emails.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-emails.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/customer-emails.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-emails-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/accessing_missing_members_of_data_objects/customer-emails-report.docx)
{{< /tab >}}
{{< /tabs >}}

### Optimizing Reflection Calls

GroupDocs.Assembly Engine uses reflection calls while accessing members of the objects it reads, Python dicts included: a dict reaches the engine as an object of a .NET type made from its keys. However, reflection calls are much slower than direct calls, which creates a performance overhead.

Due to the performance overhead, the engine provides a strategy minimizing the reflection usage. The strategy is based upon the runtime type generation. That is, the engine generates a proxy type per an external type. The proxy directly calls members of the corresponding external type, the engine to access these members in a uniform way with no reflection involved. The proxy is [lazily initialized](http://en.wikipedia.org/wiki/Lazy_initialization) and reused in further. Thus, the reflection is used only while building the proxy.

Although this strategy can significantly minimize the reflection usage in a long run, it creates a performance overhead of the runtime type generation. So, if you deal with small data collections all the time while building your reports, consider the disabling of the strategy.

You can control the enabling of the strategy through the `DocumentAssembler.use_reflection_optimization` static property. By default, the strategy is enabled.

```python
from groupdocs.assembly import DocumentAssembler

DocumentAssembler.use_reflection_optimization = False
```

### Integrating with Native Spreadsheet Data Types

By default, GroupDocs.Assembly outputs expression results as string values regardless of expression types. In most scenarios, this is the best option, since expression results can be formatted through template syntax depending on expression types. However, for Spreadsheet documents, this may interfere calculation of formulas expecting values of types other than string. To overcome this, GroupDocs.Assembly provides integration with native Spreadsheet data types, which can be enabled as shown in the following code snippet.

```python
assembler = DocumentAssembler()
assembler.options |= DocumentAssemblyOptions.USE_SPREADSHEET_DATA_TYPES
assembler.assemble_document(...)
```

Let us show how it works by using an example. Let `number` be a numeric value. Then, consider the following template for a Spreadsheet cell.

```text
<<[number]>>
```

By default, while assembling a document, GroupDocs.Assembly converts `number` into a string using built-in .NET routines. However, when integration with native Spreadsheet data types is enabled, the cell's value is written as a number, thus enabling to use it in Spreadsheet formulas expecting numbers.

Integration with native Spreadsheet data types also affects formatting of the cell's value: If a numeric format is defined for the cell (for example, using "Format Cells" context menu in Microsoft Excel), then the format is applied; otherwise, a default numeric format for cells is applied.

**Note –** The same applies to other native Spreadsheet data types such as date-time and Boolean.

In the following example, the order numbers, quantities and prices of `orders.json` become numeric cells of the worksheet:

{{< tabs "example17" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler, DocumentAssemblyOptions

with open("orders.json", encoding="utf-8") as f:
    orders = json.load(f)

assembler = DocumentAssembler()
assembler.options |= DocumentAssemblyOptions.USE_SPREADSHEET_DATA_TYPES
assembler.assemble_document("order-prices.xlsx", "order-prices-report.xlsx", DataSourceInfo(orders, "orders"))
```
{{< /tab >}}
{{< tab "order-prices.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-prices.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/order-prices.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-prices-report.xlsx" >}}  
```text
Binary file (XLSX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis/integrating_with_native_spreadsheet_data_types/order-prices-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

The following table describes, in which cases integration with native Spreadsheet data types has no effect even when enabled.

| Cell Template Syntax Example | Explanation |
| --- | --- |
| `<<[number]:ordinal>>` | If an expression result is formatted using template syntax, it is written as a string. |
| `Some text <<[number]>>` | Presence of text other than template syntax makes a result cell value to become a string. |
| `<<[number]>><<[anotherNumber]>>` | Results of multiple expressions in a single cell are converted to strings and concatenated. |

## Technical Considerations

Here, we will reveal some technical aspects and implementation details related to the GroupDocs.Assembly Engine which can be useful for you while making design decisions for your applications.

### Implicit Enumeration Determination

If you do not specify the type of an enumeration item in a `foreach` statement or lambda function signature within your template explicitly, the type is implicitly determined by the engine from the type of the enumeration. For the data a Python application passes, it is as follows:

1.  If the enumeration is a list (or tuple) of dicts, then the item type is the type the engine made from the dicts' keys. All dicts of one list share one type, which has the keys of all of them.
2.  Otherwise, if the enumeration is a list of values of one kind, such as strings or integers, then the item type is that of the values: `String`, `Int64`, `Double`, `DateTime` and so on.
3.  Otherwise, if the enumeration is a list of values of different kinds, then the item type is `Object`: the items can be output, but their members cannot be read.
4.  An empty list has no items to take a type from, so its item type is `Object`, unless the same key holds a non-empty list in another dict of the same kind. A template that reads a member of such an item fails with "Can not get the value of member '...' on type 'System.Object'"; give the data an item, or apply `DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS`.
5.  If the enumeration is a `DocumentTable`, or a table of a `DocumentTableSet`, then the items are its rows. If it is an array of a `JsonDataSource`, a sequence of elements of an `XmlDataSource`, or a `CsvDataSource`, then the items are the objects the engine made from them.

### Support for LINQ Providers

The engine does not cooperate with [LINQ providers](http://msdn.microsoft.com/en-us/library/vstudio/bb882640(v=vs.110).aspx), and the data a Python application passes is already complete in memory: `DataSourceInfo` copies a dict and everything it holds when it is created. So, an expression such as the following one runs over all the persons of the city, whatever source they came from.

```text
city.Persons.Where(p => p.Age > 30).OrderBy(p => p.Name)
```

If you read the data from a database, the query that loaded it is the one that ran; filtering and ordering in the template come after it. In some cases, this can lead to a significant performance overhead. So, if the performance of your application is your primary concern, then consider a preparing of your sequential data outside your templates. That is, pass to the engine a sequential data that is already filtered, ordered, grouped, and so forth: with a `WHERE` and an `ORDER BY` in the SQL query, or with a list comprehension and `sorted` in Python.

### Merging GroupDocs.Assembly

The .NET version of this page describes how to merge the GroupDocs.Assembly assembly into another .NET assembly. GroupDocs.Assembly for Python via .NET ships the engine inside its wheel, so there is nothing to merge.
