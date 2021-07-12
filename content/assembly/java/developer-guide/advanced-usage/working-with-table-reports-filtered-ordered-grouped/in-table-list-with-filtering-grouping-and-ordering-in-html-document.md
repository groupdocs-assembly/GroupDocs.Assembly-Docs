---
id: in-table-list-with-filtering-grouping-and-ordering-in-html-document
url: assembly/java/in-table-list-with-filtering-grouping-and-ordering-in-html-document
title: In-Table List with Filtering Grouping and Ordering in HTML Document
weight: 4
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
# In-Table List with Filtering, Grouping, and Ordering in HTML Document

{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate In-TableList with Filtering, Grouping, and Ordering report in HTML Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Table List with Filtering, Grouping, and Ordering in HTML Document

### Reporting Requirement

As a report developer, you are required to represent managers' contract information with the following key requirements:

*   Report must show each manager along with sum of prices of his contracts.
*   It must represent all the information in tabular form.
*   Report must be generated in the HTML Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="gdassembly">
	<tbody>
		<tr>
			<td colspan="2">&lt;&lt;foreach \[in getContracts() .where(c => c.getDate().getYear() + 1900 == 2015) .groupBy(c => c.getManager()) .orderBy(g => g.key.getName())\]>> &lt;&lt;/foreach>></td>
		</tr>
		<tr>
			<td><b>Manager</b></td>
			<td><b>Contract Price</b></td>
		</tr>
		<tr>
			<td><b>&lt;&lt;[key.getName()]>></b></td>
			<td>&lt;&lt;[sum(c => c.getPrice())]>></td>
		</tr>
	</tbody>
</table>

### Download In-Table List with Filtering, Grouping, and Ordering Template

Please download the sample template we created in this article:

*   [In-Table List with Filtering, Grouping, and Ordering.html](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Html%20Templates/In-Table%20List%20with%20Filtering%2C%20Grouping%2C%20and%20Ordering.html?raw=true)

### Generating The Report

{{< gist GroupDocsGists 4554b48316196d2579cb1cbd679b8bfe >}}


