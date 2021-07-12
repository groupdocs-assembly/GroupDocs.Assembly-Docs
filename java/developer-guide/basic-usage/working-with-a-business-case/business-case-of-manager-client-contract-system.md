---
id: business-case-of-manager-client-contract-system
url: assembly/java/business-case-of-manager-client-contract-system
title: Business Case of Manager-Client Contract System
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This business case has been conceived for the demonstration purpose and serves well for a typical manager-client system. There may be simpler or complex scenarios in real life businesses.{{< /alert >}}

## Business Case

1.  There are many managers offering their services.
2.  There are multiple clients in the market.
3.  A manager can sign multiple contracts and start working.
4.  A contract may contain multiple clients.
5.  The data is fetched from custom objects and report is generated.

## Reporting Requirements

1.  A report based on some criteria is to be generated.
2.  The report can be in any of the formats: Documents, Spreadsheets, Presentations.
3.  The report developer must be able to define templates and then generate reports.

## Business Objects

### Custom Objects

Here are our customer objects:

{{< gist GroupDocsGists ffcdf1d202f0e706b98796c722e438e3 >}}



## Templates Location

There is a fixed location of templates somewhere /Date/Source/. The report developer may create any number of templates and can create sub directories under /Data/Source/ in order to organize the templates as per convenience.

## Reports Location

The reports can be placed anywhere under directory /Data/Destination/. The report developer can create sub directories and give name to the output reports as per convenience.
