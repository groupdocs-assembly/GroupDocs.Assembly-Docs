---
id: in-table-list-with-filtering-grouping-and-ordering-in-presentation-document
url: assembly/java/in-table-list-with-filtering-grouping-and-ordering-in-presentation-document
title: In-Table List with Filtering Grouping and Ordering in Presentation Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate In-TableList with Filtering, Grouping, and Ordering report in Presentation Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Table List with Filtering, Grouping, and Ordering in Microsoft PowerPoint Document

### Creating a In-Table List with Filtering, Grouping, and Ordering

Practising the following steps you can create In-Table List with Filtering, Grouping, and Ordering Template in MS PowerPoint 2013.

1.  Add a new presentation slide.
2.  Press "Insert" tab to insert the table.
3.  Insert a 2x2 table.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent managers' contract information with the following key requirements:

*   Report must show each manager along with sum of prices of his contracts.
*   It must represent all the information in tabular form.
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="gd-assembly">
	<tbody>
		<tr>
			<td style="background-color: #5B9BD5"><b>Manager/Client</b></td>
			<td style="background-color: #5B9BD5"><b>Contract Price</b></td>
		</tr>
		<tr>
			<td style="background-color: #5B9BD5"><b>&lt;&lt;foreach [in getContracts()<br>   .where(c => c.getDate().getYear() + 1900 == 2015)<br>   .groupBy(c => c.getManager())<br>   .orderBy(g => g.key.getName())]>>&lt;&lt;[key.getName()]>></b></td>
			<td style="background-color: #D2DEEF">&lt;&lt;[sum(c => c.getPrice())]>>&lt;&lt;/foreach>></td>
		</tr>
	</tbody>
</table>

### Download In-Table List with Filtering, Grouping, and Ordering Template

Please download the sample In-Table List with Filtering, Grouping, and Ordering document we created in this article:

*   [In-Table List with Filtering, Grouping, and Ordering.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/In-Table%20List%20with%20Filtering%2C%20Grouping%2C%20and%20Ordering.pptx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 845d7d45c8593f13c7f96a4046f7d0d4 >}}

### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
