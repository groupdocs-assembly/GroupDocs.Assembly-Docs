---
id: use-of-in-line-syntax-error-messages-into-templates
url: assembly/python-net/use-of-in-line-syntax-error-messages-into-templates
title: Use of In-line Syntax Error Messages into Templates
weight: 40
description: "Use of In-line Syntax Error Messages into Templates with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: use of in-line syntax error messages into templates, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

{{< alert style="info" >}}This version provide the ability to display inline template syntax errors in generated, Word Processing, Presentation, Spreadsheets, Emails and Plain Text documents.{{< /alert >}}

By default, Document Assembler throws an exception when encounters a template syntax error. Such an exception provides information on a reason of the error and specifies a tag or expression part where the error is encountered. In most cases, this information is enough to find a place in a template causing the error and fix it.

However, when dealing with complex templates containing a large number of tags, it becomes harder to find an exact place in a template causing an error. To make things easier, the engine supports the [DocumentAssemblyOptions.INLINE_ERROR_MESSAGES](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassemblyoptions/) option that enables in-lining of a syntax error message into a template document at an exact position where the error occurs during run-time.

{{< alert style="warning" >}}A template syntax error message is written using a bold font to make it more apparent.{{< /alert >}}

Consider the following template.

```text
<<var [name]>>
```

By default, such a template causes the engine to throw an exception while building a report. However, when* *DocumentAssemblyOptions.INLINE_ERROR_MESSAGES** is applied, no exception is thrown and the report looks as follows then.

```text
<<var [name] Error! An assignment operator is expected. >>
```

{{< alert style="warning" >}}Only messages describing errors in template syntax can be in-lined, messages describing errors encountered during expression's evaluation cannot be appeared.{{< /alert >}}

When **DocumentAssemblyOptions.INLINE_ERROR_MESSAGES** is applied, a Boolean value returned by a[DocumentAssembler.assemble_document](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) overload indicates whether building of a report was finished successfully or was interrupted because of a template syntax error. This enables you to process reports which building succeeded or failed differently as shown in the following code snippet.

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler, DocumentAssemblyOptions

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.options = DocumentAssemblyOptions.INLINE_ERROR_MESSAGES
assembler.assemble_document("inline-error.docx", "inline-error-report.docx", DataSourceInfo(products, "product"))
```
{{< /tab >}}
{{< tab "inline-error.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [inline-error.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/use-of-in-line-syntax-error-messages-into-templates/inline-error.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/use-of-in-line-syntax-error-messages-into-templates/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "inline-error-report.docx" >}}  
```text
Binary file (DOCX, 11 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/use-of-in-line-syntax-error-messages-into-templates/use_of_in_line_syntax_error_messages_into_templates/inline-error-report.docx)
{{< /tab >}}
{{< /tabs >}}

{{< alert style="warning" >}}In this article the Word Processing document template file has been used. Therefore, the process for the other file formats is same.{{< /alert >}}

### Download Demo File

Please download the sample demo document files:

*   [inline-error.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/use-of-in-line-syntax-error-messages-into-templates/inline-error.docx)
