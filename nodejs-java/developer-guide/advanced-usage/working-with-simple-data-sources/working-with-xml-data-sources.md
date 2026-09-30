---
id: working-with-xml-data-sources
url: assembly/nodejs-java/working-with-xml-data-sources
title: Working with XML Data Sources
weight: 3
description: "Pass XML data to GroupDocs.Assembly for Node.js via Java with XmlDataSource and use typed values in templates without an XML schema."
keywords: xml, XmlDataSource, XmlDataLoadOptions, node.js, report generation
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
To access XML data while building a report, you can read XML into a `DataSet` and pass it to the assembler as a data source. However, if you cannot specify an XML schema while loading XML into a `DataSet`, all attributes and text values of XML elements are loaded as strings. Thus, it becomes impossible, for example, to use arithmetic operations on numbers or to specify custom date-time and numeric formats to output corresponding values, because all of them are treated as strings.

To overcome this limitation, pass an `XmlDataSource` instance to the assembler as a data source instead. Even when an XML schema is not provided, `XmlDataSource` recognizes values of the following types by their string representations:

*   Integer
*   Long
*   Double
*   Boolean
*   Date

{{< alert style="warning" >}}For recognition of data types to work, string representations of corresponding attributes and text values of XML elements must be formed using invariant culture settings.{{< /alert >}}

An `XmlDataSource` can be created from a file path or a Java `InputStream`, optionally together with an XML schema and `XmlDataLoadOptions`.

## Treating a top-level XML element that contains only a sequence of elements of the same type

In template documents, if a top-level XML element contains only a sequence of elements of the same type, an `XmlDataSource` instance should be treated in the same way as if it was a `DataTable` instance (see "[Using Data Sources](/assembly/nodejs-java/template-syntax-part-1-of-2/#using-data-sources)" for more information).

Suppose we have XML data like:
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

And the following template:
```
<<foreach [in persons]>>Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth: <<[Birth]:"dd.MM.yyyy">>
<</foreach>>
Average age: <<[persons.average(p => p.Age)]>>
```

The data source is passed under the name used in the template:

```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

const dataSource = new groupdocs.XmlDataSource("persons.xml");
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

{{< alert style="warning" >}}Using a custom date-time format and an extension method involving arithmetic in the template is possible because text values of the Birth and Age XML elements are automatically converted to a date and an integer respectively, even in the absence of an XML schema.{{< /alert >}}

## Treating a top-level XML element that contains attributes or nested elements of different types

If a top-level XML element contains attributes or nested elements of different types, an `XmlDataSource` instance should be treated in template documents in the same way as if it was a `DataRow` instance (see "[Using Data Sources](/assembly/nodejs-java/template-syntax-part-1-of-2/#using-data-sources)" for more information) as shown in the following example.

Suppose we have XML data like:
```
<Person>
   <Name>John Doe</Name>
   <Age>30</Age>
   <Birth>1989-04-01 4:00:00 pm</Birth>
   <Child>Ann Doe</Child>
   <Child>Charles Doe</Child>
</Person>
```

And the following template:
```
Name: <<[Name]>>, Age: <<[Age]>>, Date of Birth:
<<[Birth]:"dd.MM.yyyy">>
Children:
<<foreach [in Child]>><<[Child_Text]>>
<</foreach>>
```

The members of the element are referenced directly, so the data source can be passed without a name:

```javascript
const dataSource = new groupdocs.XmlDataSource("person.xml");
assembler.assembleDocument("template.txt", "report.txt",
    new groupdocs.DataSourceInfo(dataSource));
```

The result is:
```
Name: John Doe, Age: 30, Date of Birth:
01.04.1989
Children:
Ann Doe
Charles Doe
```

{{< alert style="warning" >}}To reference a sequence of repeated simple-type XML elements with the same name, use the elements' name itself (for example, "Child") in a template document, and the same name with the "_Text" suffix (for example, "Child_Text") to reference the text value of one of these elements.{{< /alert >}}

## The complete example

The following example sums up typical scenarios involving nested complex-type XML elements.

### XML

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

### Template document

```
<<foreach [in managers]>>Manager: <<[Name]>>
Contracts:
<<foreach [in Contract]>>- <<[Client.Name]>> ($<<[Price]>>)
<</foreach>>
<</foreach>>
```

### Source code

{{< tabs "xml-complete-example" >}}
{{< tab "JavaScript" >}}
```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

// Source template and destination report
const templatePath = "SimpleDatasetDemo.docx";
const reportPath = "SimpleXMLDSDemo Out.docx";

// Load the XML data
const dataSource = new groupdocs.XmlDataSource("Managers.xml");
const dataSourceInfo = new groupdocs.DataSourceInfo(dataSource, "managers");

// Assemble the document
const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument(templatePath, reportPath, dataSourceInfo);

process.exit(0);
```
{{< /tab >}}
{{< /tabs >}}

### Result document

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

## Download

### Data source document

*   [Managers.xml](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Data%20Sources/XML%20DataSource/Managers.xml?raw=true)

### Template

*   [SimpleDatasetDemo.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/SimpleDatasetDemo.docx?raw=true)
