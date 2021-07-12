---
id: in-table-list-with-alternate-content-in-email-document
url: assembly/java/in-table-list-with-alternate-content-in-email-document
title: In-Table List With Alternate Content in Email Document
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-Table List With Alternate Content report in Email Document format.{{< /alert >}}

## In-Table List With Alternate Content in Email Document

### Creating a In-Table List With Alternate Content

Practicing the following steps you can create In-Table List With Alternate Content Template in MS Outlook 2013.

1.  Add a new email.
2.  Press "Insert" tab to insert the table.
3.  Insert a 2X3 table.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent your clients and their prices with the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show each client along with its price.
*   It must show sum of all the prices.
*   It must represent all the information in tabular form.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="gd-assembly">
	<tbody>
		<tr>
			<td style="background-color: #5B9BD5"><b>Client</b></td>
			<td style="background-color: #5B9BD5"><b>Contract Price</b></td>
		</tr>
    <tr>
      <td colspan="2" style="background-color: #5B9BD5"><b>&lt;&lt;if [!getContracts().any()]>>No data</td>
		<tr>
			<td style="background-color: #5B9BD5"><b>&lt;&lt;else>>&lt;&lt;foreach [in getContracts()]>>&lt;&lt;[getClient().getName()]>></b></td>
			<td style="background-color: #D2DEEF"><b>&lt;&lt;[getPrice()]>>&lt;&lt;/foreach>></b></td>
		</tr>
    <tr>
			<td style="background-color: #5B9BD5"><b>Total:</b></td>
			<td style="background-color: #D2DEEF"><b>&lt;&lt;[getContracts().sum(c => c.getPrice())]>>&lt;&lt;/if>></b></td>
		</tr>
	</tbody>
</table>

### Download In-Table List With Alternate Content Template

Please download the sample In-Table List With Alternate Content document we created in this article:

*   [In-Table List With Alternate Content.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist samicheemagroupdocs 34eef2196b70162362cba82f22222a6f >}}


