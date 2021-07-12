---
id: generating-report-using-multiple-data-sources-in-spreadsheet-document
url: assembly/java/generating-report-using-multiple-data-sources-in-spreadsheet-document
title: Generating Report using Multiple Data Sources in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a report. This report will fetch data from multiple data sources.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Generating Report in Microsoft Excel Document

### Creating a Template

1.  Add a bullet list at the place where you want it to display clients' names.
2.  Insert a table with two columns, that will show managers' and their contact prices.
3.  Save your Document

### Reporting Requirement

As a report developer, you are required to generate a report that fetches data from two different data sources (e:g custom object, excel data table). Report must show following information:

*   Bulleted list of clients
*   A table showing managers' along with their contract prices and sum of contract prices

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**In-cell list**

We provide support for the following clients:
```
<<foreach [in getClients()]>>
-          <<[getName()]>><</foreach>>
```

**Multiple-cell list**

We provide support for the following clients:

```
<<foreach [in getClients()]>>
-          <<[getName()]>> 
```

| Total Contract Prices by Managers                            |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <<foreach [group in contracts<br />     .groupBy(c => c.Manager)<br />     .orderBy(g => g.key)]>><br /><<[group.key]>> | <<[group.sum(<br />     c => c.Contract_Price)]>><br /><</foreach>> |

### Download Template

Get the template from here.

*   [Multiple DS.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Multiple%20DS.xlsx?raw=true)

### Generating the ReportGenerating Report using Custom Objects and Excel Data Source

{{< gist GroupDocsGists b758da2fedf86e75aefafe122a297cad >}}


