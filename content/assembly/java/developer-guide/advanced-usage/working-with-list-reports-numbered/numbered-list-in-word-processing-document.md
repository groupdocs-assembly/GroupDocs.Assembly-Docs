---
id: numbered-list-in-word-processing-document
url: assembly/java/numbered-list-in-word-processing-document
title: Numbered List in Word Processing Document
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Numbered List report in Word Processing Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Numbered List in Microsoft Word Document

### Creating a Numbered List

Practising the following steps you can create Numbered List Template in MS Word 2013.

1.  In your document, write a sentence like "We provide support for the following clients:".
2.  Start numbered list.
3.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show the client names in a numbered list.
*   Report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
We provide support for the following clients:
1.	<<foreach [in getClients()]>><<[getName()]>>
<</foreach>>
```

### Download Numbered List Template

Please download the sample Numbered List document we created in this article:

*   [Numbered List.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Numbered%20List.docx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 31fe6f6c5e1080d024c0ec2480830933 >}}

### ODT Template and Report in Apache OpenOffice

In order to check compatibility of ODT between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODT template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODT report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.

## Restart Numbering in Nested Numbered List 

{{< alert style="info" >}}This feature is supported by version 19.7 or greater.{{< /alert >}}


The GroupDocs.Assembly engine allows restart list numbering within your documents dynamically using *<<restartNum>>* tags. In particular, this feature is useful when working with a nested numbered list within a data band.

Assume that we are picking *Order* and *Service* classes as defined in the following *Custom Objects* of our business use case.

{{< gist GroupDocsGists ffcdf1d202f0e706b98796c722e438e3 >}}

Given that orders is an enumeration of Order instances, you could try to use the following template to output information on several orders in one document.

```java
<<foreach [in getContracts()]>><<[getClient().getName()]>> (Manager: <<[getManager().getName()]>>)
1.  <<foreach [service in getServices()]>><<[service.getName()]>>
<</foreach>><</foreach>>
```

The generated report will look as follows:

```
A Company (Manager: John Smith)
	1.	Regular Cleaning
	2.	Oven Cleaning
B Ltd. (Manager: John Smith)
	3.	Regular Cleaning
	4.	Oven Cleaning
C & D (Manager: John Smith)
	5.	Regular Cleaning
	6.	Oven Cleaning
E Corp. (Manager: Tony Anderson)
	7.	Regular Cleaning
	8.	Oven Cleaning
	9.	Carpet Cleaning
F & Partners (Manager: Tony Anderson)
	10.	Regular Cleaning
	11.	Oven Cleaning
	12.	Carpet Cleaning
```

However, there would be a single numbered list across all orders, which is not applicable for this scenario. Hence, you can make the list numbering to restart for every order by putting a *<<restartNum>>* tag into your template before a corresponding *<<foreach>>* tag as follows:

```java
<<foreach [in getContracts()]>><<[getClient().getName()]>> (Manager: <<[getManager().getName()]>>)
1.  <<restartNum>><<foreach [service in getServices()]>><<[service.getName()]>>
<</foreach>><</foreach>>
```
```
 Then, the generated report will look as follows:

A Company (Manager: John Smith)
	1.	Regular Cleaning
	2.	Oven Cleaning
B Ltd. (Manager: John Smith)
	1.	Regular Cleaning
	2.	Oven Cleaning
C & D (Manager: John Smith)
	1.	Regular Cleaning
	2.	Oven Cleaning
E Corp. (Manager: Tony Anderson)
	1.	Regular Cleaning
	2.	Oven Cleaning
	3.	Carpet Cleaning
F & Partners (Manager: Tony Anderson)
	1.	Regular Cleaning
	2.	Oven Cleaning
	3.	Carpet Cleaning
```

Download Numbered List Template

Please download the sample Numbered List template we created in this article:

*    [Numbered List\_RestartNum.docx](attachments/29360197/85426183.docx) (Template for DataBase, DataSet and JSON Data examples)
