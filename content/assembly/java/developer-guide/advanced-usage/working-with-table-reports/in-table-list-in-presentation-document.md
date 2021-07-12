---
id: in-table-list-in-presentation-document
url: assembly/java/in-table-list-in-presentation-document
title: In-Table List in Presentation Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-TableList report in Presentation format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Table List in Microsoft PowerPoint Document

### Creating a In-Table List

Practicing the following steps you can create In-Table List Template in MS PowerPoint 2013.

1.  Add a new presentation slide.
2.  Press "Insert" tab.
3.  Add a 2x3 table.
4.  Save your Document.

### Reporting Requirement

As a report developer, you are required to represent the information of the managers with the following key requirements:

*   Report must show managers' name.
*   It must show the sum of contract prices against each manager.
*   It must sum up all the contract prices for all the managers.
*   All the representation must be in tabular form.
*   Report must be generated in the PowerPoint Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="gd-assembly">
	<tbody>
		<tr>
			<td style="background-color: #5B9BD5"><b>Manager</b></td>
			<td style="background-color: #5B9BD5"><b>Contract Price</b></td>
		</tr>
		<tr>
			<td style="background-color: #5B9BD5"><b>&lt;&lt;foreach [in getManagers()]>>&lt;&lt;[getName()]>></b></td>
			<td style="background-color: #D2DEEF"><b>&lt;&lt;[getContracts().sum(c => c.getPrice())]>>&lt;&lt;foreach>></b></td>
		</tr>
    <tr>
			<td style="background-color: #5B9BD5"><b>Total:</b></td>
			<td style="background-color: #D2DEEF"><b>&lt;&lt;[getManagers().sum(m => m.getContracts().sum(c => c.getPrice()))]>></b></td>
		</tr>
	</tbody>
</table>

### Download In-Table List Template

Please download the sample In-Table List document we created in this article:

*   [In-Table List.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/In-Table%20List.pptx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 99fcb5298182b99b02f37b30bb654883 >}}

### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
