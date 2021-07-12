---
id: in-table-master-detail-in-presentation-document
url: assembly/java/in-table-master-detail-in-presentation-document
title: In-Table Master-Detail in Presentation Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate In-TableMaster-Detail report in Presentation Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Table Master-Detail in Microsoft PowerPoint Document

### Creating a In-Table Master-Detail

Practising the following steps you can create In-Table Master-Detail Template in MS PowerPoint 2013.

1.  Add a new presentation slide.
2.  Click the document where you want to add the table.
3.  Press "Insert" tab to insert the table.
4.  Insert a 2x4 table.
5.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show each manager along with his total contract prices.
*   It must also show each individual client within the contract.
*   It must show sum of the contract prices.
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

*   [In-Table Master-Detail.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/In-Table%20Master-Detail.pptx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 8ecd459de8afc880b7264a56a2476f6e >}}

### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
