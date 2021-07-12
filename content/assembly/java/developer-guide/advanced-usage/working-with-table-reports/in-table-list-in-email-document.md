---
id: in-table-list-in-email-document
url: assembly/java/in-table-list-in-email-document
title: In-Table List in Email Document
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-Table List report in Email Document format.{{< /alert >}}

## In-Table List in Email Document

### Reporting Requirement

As a report developer, you are required to represent the information of the managers with the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show managers' name.
*   It must show the sum of contract prices against each manager.
*   It must sum up all the contract prices for all the managers.
*   All the representation must be in tabular form.

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

*   [In-Table List.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist samicheemagroupdocs 0d625560bae96e7e79e4cd275484bc5a >}}


