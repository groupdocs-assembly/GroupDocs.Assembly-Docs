---
id: developers-guide-web-report-generator
url: assembly/net/developers-guide-web-report-generator
title: Developers Guide - Web Report Generator
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for .NET
hideChildren: False
---
## Execution Steps

### Inputs

*   A **Template** created in one of the Supported Document Formats conforming to Supported Template Syntax.
*   A Connection String in order to connect to a **DataBase** that can be accessed through DataSet / DataTable etc
*   Type of Data Source. For example, Table / Views etc
*   Data Source. Select a table / view from the connected DataBase

### System Processing

*   Verifies Template Document Format.
*   Connects to MS SQL Server Database using connection string
*   Tests Connection according to the provided connection string.
*   Populates all Tables from connected database.
*   Populates all Views from connected database.
*   Allows to enter Custom Query.
*   Passes Template and Data Source to the GroupDocs.Assembly - GroupDocs.Assembly generates a report according to the inputs
*   Serves the report back to the browser

### Output

*   A Report generated based on the Template Syntax and the Data Source - This report will be in the same Document Format as that of the source Template Document Format.

Here is a sample report in Microsoft Word Document Format for 'Products' table

![](https://raw.githubusercontent.com/groupdocsassembly/GroupDocs_Assembly_NET/master/Examples/Data/Screenshots/Product%20Template.png)

## Code Walkthrough

#### Default.aspx.cs

{{< gist atirtahirgroupdocs 202a1a7ed0fa355b5fe0 >}}

#### ReportGenerator.cs

{{< gist atirtahirgroupdocs 500c9be730a4fd553344 >}}

## Technical References

### Creating Templates

*   [Template Syntax - Part 1 of 2](https://docs.groupdocs.com/assembly/net/template-syntax-part-1-of-2/)
*   [Template Syntax - Part 2 of 2](https://docs.groupdocs.com/assembly/net/template-syntax-part-2-of-2/)

### An Example Business Case

*   [Business Case of a Shopping Store](https://docs.groupdocs.com/assembly/net/business-case-of-a-shopping-store/)
*   [The Business Layer](https://docs.groupdocs.com/assembly/net/the-business-layer/)

**Note:** This business case covers almost all the [Supported Data Formats](https://docs.groupdocs.com/assembly/net/features-overview/#data-sources)