---
id: working-with-template-syntax-formatting
url: assembly/java/working-with-template-syntax-formatting
title: Working with Template Syntax Formatting
weight: 26
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Template Syntax Formats

### Specifying String and Numeric Formats

Learn more about string and numeric formats [here]({{< ref "assembly/java/getting-started/features-overview.md#features-overview-template-syntax-formatsfor-expression-results" >}}).

### Template Syntax

| **Manager**                                                 | **Contract Price**                                           |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| `<<foreach [in getManagers()]>><br /><<[getName()]:upper>>` | `<<[getContracts().sum(<br />  c =><br /> c.getPrice())]:arabicDash>><br /><</foreach>>` |
| **Total:**                                                  | `<<[getManagers().sum(<br />  m => m.getContracts().sum(<br />    c => c.getPrice()))]>>    ` |

### Download Template

Get template from here.

*   [Numeric upper.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Numeric%20upper.docx?raw=true)

### The Code

{{< gist GroupDocsGists e4325ba680fa92b7f2a008f88987d480 >}}


