---
id: generating-report-using-multiple-data-sources-in-word-processing-document
url: assembly/java/generating-report-using-multiple-data-sources-in-word-processing-document
title: Generating Report using Multiple Data Sources in Word Processing Document
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a report. This report will fetch data from multiple data sources.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Generating Report in Microsoft Word Document

### Creating a Template

1.  Add a bullet list at the place where you want it to display clients' names.
2.  Insert a table with two columns, that will show managers' and their contact prices.
3.  Save your Document

### Reporting Requirement

As a report developer, you are required to generate a report that fetches data from two different data sources (e:g custom object, excel data table). Report must show following information:

*   Bulleted list of clients
*   A table showing managers' along with their contract prices and sum of contract prices

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

We provide support for the following clients:
```
- <<foreach [in getClients()]>><<[getName()]>>
<</foreach>>
```

**Total Contract Prices by Managers**

| **Manager**                                                  | **Total Contract Price**                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **<<foreach [group in contracts**<br />    **.groupBy(c => c.Manager)**<br />    **.orderBy(g => g.key)]>>**<br />**<<[group.key]>>** | <<[group.sum(<br />    c => c.Contract_Price)]>><br /><</foreach>> |

### Download Template

Get template from here:

*   [Multiple DS.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Multiple%20DS.docx?raw=true)

### Generating the ReportGenerating Report using Excel Data Source and Custom Objects

{{< gist GroupDocsGists b9d4a5a09feb9868d1da9e07f3496f00 >}}


