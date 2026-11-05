---
id: assembly-basic-usage-json-datasource
url: assembly/python-net/basic-usage-json-datasource
linktitle: Generate from JSON
title: Generate Document from JSON Data Source
weight: 8
description: "Build documents from JSON files and JSON text in Python with the JsonDataSource class of GroupDocs.Assembly for Python via .NET."
keywords: JSON data source, JsonDataSource, JSON binding, parse JSON, generate from JSON, Python, io.BytesIO, assemble JSON
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET enables you to generate documents directly from JSON data sources. The `JsonDataSource` class parses JSON and makes it available to your templates, supporting both simple and complex JSON structures.

The main classes involved are:
- [JsonDataSource](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/jsondatasource/) - loads and parses JSON data
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents from templates
- [DataSourceInfo](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/datasourceinfo/) - wraps the data source

Here are the steps to generate documents from JSON:

* Create or obtain JSON data (from a file, an API response, or a string)
* Instantiate JsonDataSource with the JSON file's path, or with a binary stream holding the JSON text
* Create a template document with expression tags referencing JSON properties
* Use DocumentAssembler to assemble the template with JsonDataSource
* Save the assembled document

{{< alert style="info" >}}
JsonDataSource automatically recognizes JSON types (numbers, booleans, dates, strings) and makes them available with proper types in templates, enabling numeric operations and date formatting. You can also read JSON with Python's `json` module and pass the resulting dicts and lists, as shown in [Generate from Custom Objects]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-from-custom-objects.md" >}}); then the JSON's strings stay strings, and a date must be turned into a `datetime` in Python.
{{< /alert >}}

## Generate Document from JSON File

The simplest way to use JSON data is from a file:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataSource

json_data_source = JsonDataSource("staff-member.json")

assembler = DocumentAssembler()
assembler.assemble_document("staff-member-card.docx", "staff-member-card-report.docx",
                            DataSourceInfo(json_data_source, "data"))
```
{{< /tab >}}
{{< tab "staff-member.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-member.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-json-datasource/staff-member.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-member-card.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-member-card.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-json-datasource/staff-member-card.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-member-card-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-json-datasource/generate_document_from_json_file/staff-member-card-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Generate Document from JSON String

`JsonDataSource` reads a file path or a stream, and a `str` is always taken as a path. To use JSON text you already hold in memory, wrap its UTF-8 bytes in `io.BytesIO`:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataSource

json_string = """{
    "name": "Jonas Weber",
    "age": 37,
    "email": "jonas.weber@harborlane.example",
    "active": true
}"""

json_data_source = JsonDataSource(io.BytesIO(json_string.encode("utf-8")))

assembler = DocumentAssembler()
assembler.assemble_document("staff-member-card.docx", "staff-member-card-from-string.docx",
                            DataSourceInfo(json_data_source, "data"))
```
{{< /tab >}}
{{< tab "staff-member-card.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-member-card.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-json-datasource/staff-member-card.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-member-card-from-string.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-json-datasource/generate_document_from_json_string/staff-member-card-from-string.docx)
{{< /tab >}}
{{< /tabs >}}

## Working with JSON Arrays

When your JSON root is an array, JsonDataSource treats it as a collection:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataSource

json_array = """[
    { "name": "Amara Osei", "age": 41 },
    { "name": "Jonas Weber", "age": 37 },
    { "name": "Lena Park", "age": 29 }
]"""

json_data_source = JsonDataSource(io.BytesIO(json_array.encode("utf-8")))

assembler = DocumentAssembler()
assembler.assemble_document("staff-list.docx", "staff-list-report.docx",
                            DataSourceInfo(json_data_source, "people"))
```
{{< /tab >}}
{{< tab "staff-list.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-list.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-json-datasource/staff-list.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-list-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-json-datasource/working_with_json_arrays/staff-list-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Example for JSON Object

For a JSON object like `{"name": "Amara Osei", "age": 41}`, your template can reference properties directly:

```text
Name: <<[data.name]>>
Age: <<[data.age]>>
```

## Template Example for JSON Array

For a JSON array, use a foreach data band to iterate:

```text
<<foreach [in people]>>
Name: <<[name]>>, Age: <<[age]>>
<</foreach>>
```

## Working with Nested JSON Objects

JsonDataSource handles nested JSON structures automatically:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataSource

nested_json = """{
    "company": "Harbor Lane Provisions",
    "address": {
        "street": "18 Quayside Road",
        "city": "Port Ellery",
        "zip": "48210"
    },
    "employees": [
        { "name": "Amara Osei", "position": "Operations Director" },
        { "name": "Mei Tanaka", "position": "Account Manager" }
    ]
}"""

json_data_source = JsonDataSource(io.BytesIO(nested_json.encode("utf-8")))

assembler = DocumentAssembler()
assembler.assemble_document("company-profile.docx", "company-profile-report.docx",
                            DataSourceInfo(json_data_source, "company"))
```
{{< /tab >}}
{{< tab "company-profile.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [company-profile.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-json-datasource/company-profile.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "company-profile-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-json-datasource/working_with_nested_json_objects/company-profile-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template for nested JSON:

```text
Company: <<[company.company]>>
Address: <<[company.address.street]>>, <<[company.address.city]>> <<[company.address.zip]>>

Employees:
<<foreach [in company.employees]>>
- <<[name]>>, <<[position]>>
<</foreach>>
```

## Configure JSON Data Load Options

You can configure how JsonDataSource parses JSON. The file below has one root property, `accounts`, holding an array, and account codes with leading zeros:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataLoadOptions, JsonDataSource, JsonSimpleValueParseMode

options = JsonDataLoadOptions()
options.always_generate_root_object = True  # Always create root object
options.simple_value_parse_mode = JsonSimpleValueParseMode.STRICT  # Strict type parsing

json_data_source = JsonDataSource("trade-accounts.json", options)

assembler = DocumentAssembler()
assembler.assemble_document("trade-account-list.docx", "trade-account-list-report.docx",
                            DataSourceInfo(json_data_source, "data"))
```
{{< /tab >}}
{{< tab "trade-accounts.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [trade-accounts.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-json-datasource/trade-accounts.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "trade-account-list.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [trade-account-list.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-json-datasource/trade-account-list.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "trade-account-list-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-json-datasource/configure_json_data_load_options/trade-account-list-report.docx)
{{< /tab >}}
{{< /tabs >}}

The template reaches the array through the root object:

```text
<<foreach [in data.accounts]>>
<<[name]>> (account <<[code]>>), managed by <<[manager]>>
<</foreach>>
```

With `JsonSimpleValueParseMode.STRICT`, a JSON string stays a string, so the account code `"0142"` is written as `0142`. In the default `LOOSE` mode, a string that looks like a number becomes a number, and the same tag writes `142`.

{{< alert style="warning" >}}
By default, if a root JSON element is an object with only one property that is an object or array, the engine skips the root object. Set `always_generate_root_object` to `True` to always include it. Without it, `data` above is the array itself, and `data.accounts` fails with "Can not get the value of member 'accounts'".
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with complex JSON structures, date-time parsing, and advanced JsonDataSource options, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
