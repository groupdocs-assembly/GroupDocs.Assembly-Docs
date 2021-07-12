---
id: working-with-spreadsheet-documents
url: assembly/java/working-with-spreadsheet-documents
title: Working with Spreadsheet Documents
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 18.2 or greater.{{< /alert >}}

## Working with Spreadsheet Documents

GroupDocs.Assembly allows you to use data bands in table rows in **Spreadsheet Documents**. A table-row data band is a data band whose body occupies single or multiple rows of a single document table. The body of such a band starts at the beginning of the first occupied row and ends at the end of the last occupied row as follows. The syntax for using data bands in spreadsheet document is as follows:

| **Client**                               | **Manager**         | **Contract Price**                           |
| ---------------------------------------- | ------------------- | -------------------------------------------- |
| **<<foreach [c in ds]>> <<[c.Client]>>** | **<<[c.Manager]>>** | **<<[c.Contact_Price]>> &lt;&lt;/foreach>>** |

### Working with Table-Row Conditional Blocks

You can also use a table-row conditional block whose body occupies single or multiple rows of a single document table. The body of such a block (as well as the body of its every template option) starts at the beginning of the first occupied row and ends at the end of the last occupied row as follows:

<table class="confluenceTable"><tbody><tr><td class="confluenceTd"><p><strong>&nbsp;</strong></p></td><td class="confluenceTd"><p><strong>&nbsp;</strong></p></td><td class="confluenceTd"><p><strong>&nbsp;</strong></p></td></tr><tr><td class="confluenceTd"><p><strong>&lt;&lt;if ...&gt;&gt; ...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td></tr><tr><td class="confluenceTd"><p><strong>...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td></tr><tr><td class="confluenceTd"><p><strong>&lt;&lt;elseif ...&gt;&gt; ...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td></tr><tr><td class="confluenceTd"><p><strong>...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td></tr><tr><td class="confluenceTd"><p><strong>&lt;&lt;else&gt;&gt; ...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td></tr><tr><td class="confluenceTd"><p><strong>...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td></tr><tr><td class="confluenceTd"><p><strong>...</strong></p></td><td class="confluenceTd"><p><strong>...</strong></p></td><td class="confluenceTd"><p><strong>... &lt;&lt;/if&gt;&gt;</strong></p></td></tr><tr><td class="confluenceTd"><p><strong>&nbsp;</strong></p></td><td class="confluenceTd"><p><strong>&nbsp;</strong></p></td><td class="confluenceTd"><p><strong>&nbsp;</strong></p><div><strong><br></strong></div></td></tr></tbody></table>
{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

### Download

#### Data Source Document

*   [Managers Data.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Data%20Sources/Excel%20DataSource/Contracts%20Data.xlsx)

#### Template

*   [Working with Table Row Data Bands.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Working%20With%20Table%20Row%20Data%20Bands.xlsx)

### The Code

{{< gist GroupDocsGists 59eba4d682fd53447e774dae5a3cceb8 >}}


