---
id: in-table-list-with-alternate-content-in-presentation-document
url: assembly/java/in-table-list-with-alternate-content-in-presentation-document
title: In-Table List With Alternate Content in Presentation Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate In-TableList WithAlternateContent report in Presentation Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Table List With Alternate Content in Microsoft PowerPoint Document

### Creating a In-Table List With Alternate Content

Practicing the following steps you can create In-Table List With Alternate Content Template in MS PowerPoint 2013.

1.  Add a new presentation slide.
2.  Press "Insert" tab to insert the table.
3.  Insert a 2X3 table.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent your clients and their prices with the following key requirements:

*   Report must show each client along with its price.
*   It must show sum of all the prices.
*   It must represent all the information in tabular form.
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="MsoNormalTable" border="0" cellspacing="0" cellpadding="0" width="608" style="width: 456pt; border-collapse: collapse;"><tbody><tr><td width="371" valign="top" style="width: 278pt; border-top-color: white; border-top-style: solid; border-top-width: 1pt; border-right-color: white; border-right-style: solid; border-right-width: 1pt; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 3pt; border-left-color: white; border-left-style: solid; border-left-width: 1pt; background-color: rgb(91, 155, 213); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal"><b><span style="color: black;">Client</span></b></p></td><td width="237" valign="top" style="width: 178pt; border-top-color: white; border-top-style: solid; border-top-width: 1pt; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 3pt; border-right-color: white; border-right-style: solid; border-right-width: 1pt; background-color: rgb(91, 155, 213); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal"><b><span style="color: black;">Contract Price</span></b></p></td></tr><tr><td width="608" colspan="2" valign="top" style="width: 456pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: white; border-right-style: solid; border-right-width: 1pt; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: white; border-left-style: solid; border-left-width: 1pt; background-color: rgb(91, 155, 213); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal"><b><span style="color: black;">&lt;&lt;if [!getContracts().any()]&gt;&gt;No data</span></b></p></td></tr><tr><td width="371" valign="top" style="width: 278pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: white; border-right-style: solid; border-right-width: 1pt; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: white; border-left-style: solid; border-left-width: 1pt; background-color: rgb(91, 155, 213); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal"><b><span style="color: black;">&lt;&lt;else&gt;&gt;&lt;&lt;foreach [in getContracts()]&gt;&gt;&lt;&lt;[getClient().getName()]&gt;&gt;</span></b></p></td><td width="237" valign="top" style="width: 178pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: white; border-right-style: solid; border-right-width: 1pt; background-color: rgb(234, 239, 247); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal"><b><span style="color: black;">&lt;&lt;[getPrice()]&gt;&gt;&lt;&lt;/foreach&gt;&gt;</span></b></p></td></tr><tr><td width="371" valign="top" style="width: 278pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: white; border-right-style: solid; border-right-width: 1pt; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: white; border-left-style: solid; border-left-width: 1pt; background-color: rgb(91, 155, 213); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal"><b><span style="color: black;">Total:</span></b></p></td><td width="237" valign="top" style="width: 178pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: white; border-right-style: solid; border-right-width: 1pt; background-color: rgb(210, 222, 239); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal"><b><span style="color: black;">&lt;&lt;[getContracts().sum(</span></b></p><p class="MsoNormal"><b><span style="color: black;">&nbsp; c =&gt; c.getPrice())]&gt;&gt;&lt;&lt;/if&gt;&gt;</span></b></p></td></tr></tbody></table>
### Download In-Table List With Alternate Content Template

Please download the sample In-Table List With Alternate Content document we created in this article:

*   [In-Table List With Alternate Content.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/In-Table%20List%20with%20Alternate%20Content.pptx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 1a951e09c816e7a8053e88b25cdb5a4a >}}

### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
