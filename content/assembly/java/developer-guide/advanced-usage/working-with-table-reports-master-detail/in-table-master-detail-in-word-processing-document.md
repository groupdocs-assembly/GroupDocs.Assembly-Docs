---
id: in-table-master-detail-in-word-processing-document
url: assembly/java/in-table-master-detail-in-word-processing-document
title: In-Table Master-Detail in Word Processing Document
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate In-TableMaster-Detail report in Word Processing Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Table Master-Detail in Microsoft Word Document

### Creating a In-Table Master-Detail

Practising the following steps you can create In-Table Master-Detail Template in MS Word 2013.

1.  Click the document where you want to add the table.
2.  Press "Insert" tab to insert the table.
3.  Insert a 2x4 table.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show each manager along with his total contract prices.
*   It must also show each individual client within the contract.
*   It must show sum of the contract prices.
*   It must represent all the information in tabular form.
*   Report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="iksweb">
	<tbody>
		<tr>
      <td><b>Manager/Client</b></td>
      <td><b>Contract Price</b></td>
		</tr>
		<tr>
      <td><b>&lt;&lt;foreach [in getManagers()]>>&lt;&lt;[getName()]>></b></td>
			<td>&lt;&lt;[getContracts().sum(c => c.getPrice())]>></td>
		</tr>
		<tr>
      <td><i>&lt;&lt;foreach [in getContracts()]>><br\>&lt;&lt;[getClient().getName()]>></i></td>
			<td>&lt;&lt;[getPrice()]>>&lt;&lt;/foreach>>&lt;&lt;/foreach>></td>
		</tr>
		<tr>
      <td><b>Total:</b></td>
			<td>&lt;&lt;[getManagers().sum(<br\>  m => m.getContracts().sum(<br\>    c => c.getPrice()))]>></td>
		</tr>
	</tbody>
</table>

### Download In-Table Master-Detail Template

Please download the sample In-Table Master-Detail document we created in this article:

*   [In-Table Master-Detail.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/In-Table%20Master-Detail.docx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 0a3ab37eccadc39a30691c4a2bc4de4f >}}

### ODT Template and Report in Apache OpenOffice

In order to check compatibility of ODT between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODT template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODT report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
