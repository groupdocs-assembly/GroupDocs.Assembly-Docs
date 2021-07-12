---

id: generating-report-using-multiple-data-sources-in-presentation-document
url: assembly/java/generating-report-using-multiple-data-sources-in-presentation-document
title: Generating Report using Multiple Data Sources in Presentation Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a report. This report will fetch data from multiple data sources.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Generating Report in Microsoft PowerPoint Document

### Creating a Template

1.  Add a bullet list at the place where you want it to display clients' names.
2.  Insert a table with two columns, that will show managers' and their contact prices.
3.  Save your Document

### Reporting Requirement

As a report developer, you are required to generate a report that fetches data from two different data sources (e:g custom object, excel data table). Report must show following information:

*   Bulleted list of clients
*   A table showing managers' along with their contract prices and sum of contract prices

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**We provide support for the following clients:**

   • **<<foreach \[in getClients()\]>><<\[getName()\]>>**

**Total Contract Prices by Managers**

<table class="gd-assembly">
	<tbody>
		<tr>
			<td style="background-color: #5B9BD5"><b>Manager</b></td>
			<td style="background-color: #5B9BD5"><b>Total Contract Price</b></td>
		</tr>
		<tr>
			<td style="background-color: #5B9BD5"><b>&lt;&lt;foreach [group in contracts<br />    .groupBy(c => c.Manager)<br />    .orderBy(g => g.key)]>><br />&lt;&lt;[group.key]>></b></td>
			<td style="background-color: #D2DEEF"><b>&lt;&lt;[group.sum(<br />    c => c.Contract_Price)]>><br />&lt;&lt;/foreach>></b></td>
		</tr>
	</tbody>
</table>

### Download Template

Get the template from here:

*   [Multiple DS.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Multiple%20DS.pptx?raw=true)

### Generating the Report

{{< gist GroupDocsGists 3ab9d5c532752f52d597b6cb5fb39ed9 >}}


