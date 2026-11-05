---
id: assembly-basic-usage-xml-datasource
url: assembly/python-net/basic-usage-xml-datasource
linktitle: Generate from XML
title: Generate Document from XML Data Source
weight: 7
description: "Create reports in Python from XML files and XML text with the XmlDataSource class of GroupDocs.Assembly for Python via .NET."
keywords: XML data source, XmlDataSource, XML binding, parse XML, generate from XML, Python, io.BytesIO, assemble XML
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET provides the `XmlDataSource` class to work with XML data directly in templates. XmlDataSource automatically recognizes data types (numbers, dates, booleans) from XML, making it easier to perform calculations and formatting.

The main classes involved are:
- [XmlDataSource](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/xmldatasource/) - loads and parses XML data
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents
- [XmlDataLoadOptions](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/xmldataloadoptions/) - configures XML loading behavior

Here are the steps to generate documents from XML:

* Create or obtain XML data (from a file, a string, or a stream)
* Instantiate XmlDataSource with the XML file's path, or with a binary stream holding the XML text
* Create a template document with expression tags referencing XML elements
* Use DocumentAssembler to assemble the template with XmlDataSource
* Save the assembled document

{{< alert style="info" >}}
XmlDataSource automatically recognizes Int64, Double, Boolean, and DateTime values from XML strings, enabling numeric operations and date formatting in templates without explicit type conversion. The values reach the template as nullable .NET values: a format such as `<<[data.Birth]:"dd.MM.yyyy">>` works as it is, while a member of the value needs `.Value` first (`<<[data.Birth.Value.Year]>>`).
{{< /alert >}}

## Generate Document from XML File

The simplest way to use XML data is from a file:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import XmlDataSource

xml_data_source = XmlDataSource("staff-profile.xml")

assembler = DocumentAssembler()
assembler.assemble_document("staff-profile.docx", "staff-profile-report.docx",
                            DataSourceInfo(xml_data_source, "data"))
```
{{< /tab >}}
{{< tab "staff-profile.xml" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-profile.xml](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-xml-datasource/staff-profile.xml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-profile.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-profile.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-xml-datasource/staff-profile.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-profile-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-xml-datasource/generate_document_from_xml_file/staff-profile-report.docx)
{{< /tab >}}
{{< /tabs >}}

## XML File Example

Your XML file (staff-profile.xml) might look like this:

```xml
<Person>
    <Name>Amara Osei</Name>
    <Age>41</Age>
    <Birth>1984-03-12 9:30:00 am</Birth>
    <Email>amara.osei@harborlane.example</Email>
</Person>
```

## Template Example for XML Object

For the XML above, your template can reference elements directly:

```text
Name: <<[data.Name]>>
Age: <<[data.Age]>>
Date of Birth: <<[data.Birth]:"dd.MM.yyyy">>
Email: <<[data.Email]>>
```

## Generate Document from XML String

`XmlDataSource` reads a file path or a stream, and a `str` is always taken as a path. To use XML text you already hold in memory, wrap its UTF-8 bytes in `io.BytesIO`:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import XmlDataSource

xml_string = """<Person>
    <Name>Jonas Weber</Name>
    <Age>37</Age>
    <Birth>1988-07-04 2:00:00 pm</Birth>
    <Email>jonas.weber@harborlane.example</Email>
</Person>"""

xml_data_source = XmlDataSource(io.BytesIO(xml_string.encode("utf-8")))

assembler = DocumentAssembler()
assembler.assemble_document("staff-profile.docx", "staff-profile-from-string.docx",
                            DataSourceInfo(xml_data_source, "data"))
```
{{< /tab >}}
{{< tab "staff-profile.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-profile.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-xml-datasource/staff-profile.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-profile-from-string.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-xml-datasource/generate_document_from_xml_string/staff-profile-from-string.docx)
{{< /tab >}}
{{< /tabs >}}

## Working with XML Arrays

When your XML root contains a sequence of elements, XmlDataSource treats it as a collection:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import XmlDataSource

xml_array = """<Persons>
    <Person>
        <Name>Amara Osei</Name>
        <Age>41</Age>
    </Person>
    <Person>
        <Name>Jonas Weber</Name>
        <Age>37</Age>
    </Person>
    <Person>
        <Name>Lena Park</Name>
        <Age>29</Age>
    </Person>
</Persons>"""

xml_data_source = XmlDataSource(io.BytesIO(xml_array.encode("utf-8")))

assembler = DocumentAssembler()
assembler.assemble_document("staff-roster.docx", "staff-roster-report.docx",
                            DataSourceInfo(xml_data_source, "persons"))
```
{{< /tab >}}
{{< tab "staff-roster.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-roster.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-xml-datasource/staff-roster.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-roster-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-xml-datasource/working_with_xml_arrays/staff-roster-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Example for XML Array

For XML arrays, use a foreach data band:

```text
<<foreach [in persons]>>
Name: <<[Name]>>, Age: <<[Age]>>
<</foreach>>

Average age: <<[persons.Average(p => p.Age)]:"0.0">>
```

## Working with Nested XML Elements

XmlDataSource handles nested XML structures automatically:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import XmlDataSource

nested_xml = """<Company>
    <Name>Harbor Lane Provisions</Name>
    <Address>
        <Street>18 Quayside Road</Street>
        <City>Port Ellery</City>
        <Zip>48210</Zip>
    </Address>
    <Employees>
        <Employee>
            <Name>Amara Osei</Name>
            <Position>Operations Director</Position>
        </Employee>
        <Employee>
            <Name>Mei Tanaka</Name>
            <Position>Account Manager</Position>
        </Employee>
    </Employees>
</Company>"""

xml_data_source = XmlDataSource(io.BytesIO(nested_xml.encode("utf-8")))

assembler = DocumentAssembler()
assembler.assemble_document("company-overview.docx", "company-overview-report.docx",
                            DataSourceInfo(xml_data_source, "company"))
```
{{< /tab >}}
{{< tab "company-overview.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [company-overview.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-xml-datasource/company-overview.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "company-overview-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-xml-datasource/working_with_nested_xml_elements/company-overview-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template for nested XML:

```text
Company: <<[company.Name]>>
Address: <<[company.Address.Street]>>, <<[company.Address.City]>> <<[company.Address.Zip]>>

Employees:
<<foreach [in company.Employees.Employee]>>
- <<[Name]>>, <<[Position]>>
<</foreach>>
```

The `Employees` element is one object holding the `Employee` elements, so the data band iterates `company.Employees.Employee`. A band over `company.Employees` visits that single object, and `<<[Name]>>` then fails with "Can not get the value of member 'Name' on type 'System.Data.DataRow'".

## Configure XML Data Load Options

You can configure how XmlDataSource parses XML. The roster file below has a root element holding only a sequence of `Person` elements:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import XmlDataLoadOptions, XmlDataSource

options = XmlDataLoadOptions()
options.always_generate_root_object = True  # Always create root object

xml_data_source = XmlDataSource("staff-roster.xml", options)

assembler = DocumentAssembler()
assembler.assemble_document("staff-roster-root.docx", "staff-roster-root-report.docx",
                            DataSourceInfo(xml_data_source, "data"))
```
{{< /tab >}}
{{< tab "staff-roster.xml" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-roster.xml](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-xml-datasource/staff-roster.xml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-roster-root.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-roster-root.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-xml-datasource/staff-roster-root.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-roster-root-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-xml-datasource/configure_xml_data_load_options/staff-roster-root-report.docx)
{{< /tab >}}
{{< /tabs >}}

With the root object generated, the template reaches the people through it:

```text
<<foreach [in data.Person]>>
Name: <<[Name]>>, Age: <<[Age]>>
<</foreach>>
```

{{< alert style="warning" >}}
By default, if a root XML element contains only a sequence of elements of one type, the engine skips the root object. Set `always_generate_root_object` to `True` to always include it. Without it, `data` above is the sequence itself, and `data.Person` fails with "Can not get the value of member 'Person'".
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with XML schemas, complex XML structures, XML attributes, and advanced XmlDataSource options, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
