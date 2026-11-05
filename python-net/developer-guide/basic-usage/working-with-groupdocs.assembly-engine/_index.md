---
id: working-with-groupdocs-assembly-engine
url: assembly/python-net/working-with-groupdocs-assembly-engine
title: Working with GroupDocs.Assembly Engine
weight: 200
description: "How the GroupDocs.Assembly engine builds a report from a template and Python data: the template syntax, expressions, data sources and the DocumentAssembler API of GroupDocs.Assembly for Python via .NET."
keywords: GroupDocs.Assembly engine, template syntax, expressions, data source, DocumentAssembler, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
## About this section

The articles in this section will be talking about technical concepts to be considered when creating document templates in order to generate your required reports. After going through this section, hopefully you will understand the template syntax and how to compose expressions, which follow the syntax of C# whatever language your application is written in. Additionally, we'll also discuss how the [GroupDocs.Assembly](https://reference.groupdocs.com/assembly/python-net/) engine reads the syntax, evaluates the expressions against the data your Python code passes, and then generates your desired report according to your business needs.

## At a glance

### Steps you follow

In a nutshell, you will follow these steps when using [GroupDocs.Assembly](https://reference.groupdocs.com/assembly/python-net/) Engine:

1.  Create a data source in one of the supported data formats: Python dicts and lists, or a JSON, XML or CSV file, or the tables of a document
2.  Create a template conforming to the supported syntax and expressions
3.  Pass the data source and the template to the Engine with `DocumentAssembler().assemble_document(...)`

#### The actions by GroupDocs.Assembly Engine

As a result of passing template and data source, the Engine will perform following actions:

1.  Sequentially evaluate the expressions against the passed data source object
2.  Process the results of the expressions according to their roles
3.  Replace the corresponding tags with appropriate contents

### Articles in this section
