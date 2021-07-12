---
id: in-table-list-with-filtering-grouping-and-ordering-in-email-document
url: assembly/java/in-table-list-with-filtering-grouping-and-ordering-in-email-document
title: In-Table List with Filtering Grouping and Ordering in Email Document
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
# In-Table List with Filtering, Grouping, and Ordering in Email Document

{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-Table List with Filtering, Grouping, and Ordering report in Email Document format.{{< /alert >}}

## In-Table List with Filtering, Grouping, and Ordering in Email Document

### Creating a In-Table List with Filtering, Grouping, and Ordering

Practicing the following steps you can create In-Table List with Filtering, Grouping, and Ordering Template in MS Outlook 2013.

1.  Create a new Email.
2.  Press "Insert" tab to insert the table.
3.  Insert a 2x2 table.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent managers' contract information with the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show each manager along with sum of prices of his contracts.
*   It must represent all the information in tabular form.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="gd-assembly">
	<tbody>
		<tr>
			<td style="background-color: #5B9BD5"><b>Manager</b></td>
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

*   [In-Table List with Filtering, Grouping, and Ordering.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist samicheemagroupdocs 75711d4899c2326cf821c70c1574ed0c >}}
