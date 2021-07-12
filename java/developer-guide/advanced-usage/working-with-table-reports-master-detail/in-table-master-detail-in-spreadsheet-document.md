---
id: in-table-master-detail-in-spreadsheet-document
url: assembly/java/in-table-master-detail-in-spreadsheet-document
title: In-Table Master-Detail in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate In-TableMaster-Detail report in Spreadsheet Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Table Master-Detail in Microsoft Excel Document

### Creating a In-Table Master-Detail

Practising the following steps you can create In-Table Master-Detail Template in MS Excel 2013.

1.  Add a new Workbook.
2.  Select the range of cells that you want to include in the table.
3.  On the Insert tab, in the Tables group, click Table.
4.  Insert a 2x4 table.
5.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show each manager along with his total contract prices.
*   It must also show each individual client within the contract.
*   It must show sum of the contract prices.
*   It must represent all the information in tabular form.
*   Report must be generated in the Spreadsheet document format.

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

*   [In-Table Master-Detail.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/In-Table%20Master-Detail.xlsx?raw=true)

### Generating The Report

{{< gist GroupDocsGists f32bd70cf4ad82c5c1df41d61bd11e63 >}}

### ODS Template and Report in Apache OpenOffice

In order to check compatibility of ODS between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODS template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODS report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
