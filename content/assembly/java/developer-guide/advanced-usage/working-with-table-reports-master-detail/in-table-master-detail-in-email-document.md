---
id: in-table-master-detail-in-email-document
url: assembly/java/in-table-master-detail-in-email-document
title: In-Table Master-Detail in Email Document
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-Table Master-Detail report in Email Document format.{{< /alert >}}

## In-Table Master-Detail in Email Document

### Creating a In-Table Master-Detail

Practicing the following steps you can create In-Table Master-Detail Template in MS Outlook 2013.

1.  Create a new Email.
2.  Click the email where you want to add the table.
3.  Press "Insert" tab to insert the table.
4.  Insert a 2x4 table.
5.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show each manager along with his total contract prices.
*   It must also show each individual client within the contract.
*   It must show sum of the contract prices.
*   It must represent all the information in tabular form.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="gd-assembly">
	<tbody>
		<tr>
			<td style="background-color: #5B9BD5"><b>Manager/Client</b></td>
			<td style="background-color: #5B9BD5"><b>Contract Price</b></td>
		</tr>
		<tr>
			<td style="background-color: #5B9BD5"><b>&lt;&lt;foreach [in getManagers()]>>&lt;&lt;[getName()]>></b></td>
			<td style="background-color: #D2DEEF">&lt;&lt;[getContracts().sum(c => c.getPrice())]>></td>
		</tr>
    <tr>
			<td style="background-color: #5B9BD5"><i>&lt;&lt;foreach [in getContracts()]>>  &lt;&lt;[getClient().getName()]>></i></td>
			<td style="background-color: #EAEFF7">&lt;&lt;[getPrice()]>>&lt;&lt;/foreach>>&lt;&lt;/foreach>></td>
		</tr>
    <tr>
			<td style="background-color: #5B9BD5"><b>Total:</b></td>
			<td style="background-color: #D2DEEF">&lt;&lt;[getManagers().sum(m => m.getContracts().sum(c => c.getPrice()))]>></td>
		</tr>
	</tbody>
</table>

### Download In-Table Master-Detail Template

Please download the sample In-Table Master-Detail document we created in this article:

*   [In-Table Master-Detail.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist samicheemagroupdocs d25e0d9e9d41a77fb9df43596303ebed >}}
