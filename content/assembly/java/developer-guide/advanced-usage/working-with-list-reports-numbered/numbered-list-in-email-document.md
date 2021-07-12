---
id: numbered-list-in-email-document
url: assembly/java/numbered-list-in-email-document
title: Numbered List in Email Document
weight: 6
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Numbered List report in Email Document format.{{< /alert >}}

## Numbered List in Email Document

### Creating a Numbered List

Practicing the following steps you can create Numbered List Template in MS Outlook 2013.

1.  Create a new Email.
2.  Write a sentence like "We provide support for the following clients:".
3.  Start numbered list.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show the client names in a numbered list.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
We provide support for the following clients:
1<<foreach [in getClients()]>><<[numberOf()]>>. <<[getName()]>>
<</foreach>>
```

### Download Numbered List Template

Please download the sample Numbered List document we created in this article:

*   [Numbered List.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist samicheemagroupdocs 598ebf2271841f987e2056918ba0507f >}}



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
<<foreach [in getContracts()]>><<[getClient().getName()]>> (Manager:<<[getManager().getName()]>>)
1.  <<restartNum>><<foreach [service in getServices()]>><<[service.getName()]>>
<</foreach>><</foreach>>
```

 Then, the generated report will look as follows:
```
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

*    [Numbered List\_RestartNum.msg](attachments/49545620/85426184.msg)
