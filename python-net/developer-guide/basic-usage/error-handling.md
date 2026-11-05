---
id: assembly-basic-usage-error-handling
url: assembly/python-net/basic-usage-error-handling
linktitle: Handle Common Errors
title: Handle Common Template and Data Errors
weight: 31
description: "Catch the exceptions GroupDocs.Assembly for Python via .NET raises for template errors, missing members and missing files, and report template errors inside the document."
keywords: error handling, exceptions, template errors, data errors, validation, RuntimeError, FileNotFoundError, inline error messages, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

Error handling is crucial when generating documents from templates and data sources. GroupDocs.Assembly for Python via .NET raises Python exceptions that help you identify and resolve issues with templates, data sources, or assembly operations. Understanding common error scenarios and how to handle them improves the reliability of your document generation code.

The exceptions you meet are:
- `RuntimeError` - template syntax errors, missing members and other assembly errors
- `FileNotFoundError` - a template or data file that does not exist, or an output folder that does not exist
- `PermissionError` - a report path the process may not write
- `TypeError` - a value that cannot be part of a data source, raised before the engine is called

Here are the steps to handle errors:

* Wrap assembly operations in try/except blocks
* Catch specific exception types
* Validate data sources before assembly
* Handle missing members gracefully
* Log errors for debugging

{{< alert style="info" >}}
The message of an exception raised by the engine starts with the engine's explanation, which names the tag that failed ("An error has been encountered at the end of expression 'data.Email]>'"); the .NET exception type and stack trace follow on the next lines. `FileNotFoundError` and `PermissionError` raised by the engine are also `RuntimeError`, so catch them before `RuntimeError`.
{{< /alert >}}

## Basic Error Handling

Wrap assembly operations in try/except blocks:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler


def engine_message(error):
    # The first line holds the engine's message; " ---> " starts the inner .NET exception
    return str(error).splitlines()[0].split(" ---> ")[0]


try:
    data = {"Name": "Amara Osei", "Age": 41}

    assembler = DocumentAssembler()
    assembler.assemble_document("staff-greeting.docx", "staff-greeting-report.docx",
                                DataSourceInfo(data, "data"))

    print("Document assembled successfully.")
except Exception as error:
    print("Error assembling document:", engine_message(error))
    # Handle error appropriately
```
{{< /tab >}}
{{< tab "staff-greeting.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-greeting.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/error-handling/staff-greeting.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-greeting-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/error-handling/basic_error_handling/staff-greeting-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Handle Template Syntax Errors

A template with a malformed tag raises `RuntimeError`. The template of this example has a tag missing its closing bracket, `<<[data.Name]>`:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import os

from groupdocs.assembly import DataSourceInfo, DocumentAssembler


def engine_message(error):
    # The first line holds the engine's message; " ---> " starts the inner .NET exception
    return str(error).splitlines()[0].split(" ---> ")[0]


output_path = "broken-tag-report.docx"
try:
    data = {"Name": "Amara Osei", "Team": "Operations"}

    assembler = DocumentAssembler()
    assembler.assemble_document("broken-tag.docx", output_path, DataSourceInfo(data, "data"))
except RuntimeError as error:
    print("Template error:", engine_message(error))
    # The failed call leaves an empty report file behind
    if os.path.exists(output_path) and os.path.getsize(output_path) == 0:
        os.remove(output_path)
    # Log error, notify user, or use fallback template
except Exception as error:
    print("Unexpected error:", engine_message(error))
```
{{< /tab >}}
{{< tab "broken-tag.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [broken-tag.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/error-handling/broken-tag.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "handle-template-syntax-errors.txt" >}}  
```text
Template error: Expression tag is not well-formed. Character '>' is unexpected.
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/error-handling/handle_template_syntax_errors/handle-template-syntax-errors.txt)
{{< /tab >}}
{{< /tabs >}}

The example prints:

```text
Template error: Expression tag is not well-formed. Character '>' is unexpected.
```

A call that fails on the template or the data has already created the report file, and leaves it empty (0 bytes); delete it, as above, so that nothing downstream mistakes it for a report.

## Handle Missing Data Members

When the template reads a member the data does not have, the call raises `RuntimeError`: for the template below and a dict without an `"Email"` key, the message starts with "An error has been encountered at the end of expression 'data.Email]>'. Can not get the value of member 'Email'". To output nothing for a missing member instead, set `DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS`:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler, DocumentAssemblyOptions


def engine_message(error):
    # The first line holds the engine's message; " ---> " starts the inner .NET exception
    return str(error).splitlines()[0].split(" ---> ")[0]


try:
    # Data doesn't have all members referenced in template:
    # the template also reads data.Email, which doesn't exist
    data = {"Name": "Amara Osei"}

    assembler = DocumentAssembler()

    # Allow missing members (they output nothing)
    assembler.options |= DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS

    assembler.assemble_document("missing-email.docx", "missing-email-report.docx",
                                DataSourceInfo(data, "data"))
except Exception as error:
    print("Error:", engine_message(error))
```
{{< /tab >}}
{{< tab "missing-email.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [missing-email.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/error-handling/missing-email.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "missing-email-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/error-handling/handle_missing_data_members/missing-email-report.docx)
{{< /tab >}}
{{< /tabs >}}

The template reads both members:

```text
Name: <<[data.Name]>>
Email: <<[data.Email]>>
```

## Validate Data Before Assembly

Validate data sources before assembly. In Python this matters more than in .NET: an empty list carries no item type, so a template that reads its items (`<<[p.ProductName]>>`) fails with "Can not get the value of member 'ProductName' on type 'System.Object'" when the list is empty:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler


def engine_message(error):
    # The first line holds the engine's message; " ---> " starts the inner .NET exception
    return str(error).splitlines()[0].split(" ---> ")[0]


def assemble_catalog(products, output_path):
    # products might be empty or None
    if not products:
        print("Warning: No products to process.")
        return

    try:
        assembler = DocumentAssembler()
        assembler.assemble_document("product-catalog.docx", output_path,
                                    DataSourceInfo(products, "products"))

        print("Document assembled successfully.")
    except Exception as error:
        print("Error:", engine_message(error))


assemble_catalog([
    {"ProductName": "Harbor Blend whole bean coffee", "ProductPrice": "$18.40"},
    {"ProductName": "Chestnut honey", "ProductPrice": "$7.80"},
    {"ProductName": "Smoked gouda", "ProductPrice": "$15.20"},
], "product-catalog-report.docx")

assemble_catalog([], "product-catalog-empty.docx")
```
{{< /tab >}}
{{< tab "product-catalog.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [product-catalog.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/error-handling/product-catalog.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "product-catalog-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/error-handling/validate_data_before_assembly/product-catalog-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Handle File Not Found Errors

A template path that does not exist raises `FileNotFoundError`, and so does a report path whose folder does not exist. Check the path with `os.path.exists()` before the call, catch the exception, or both:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler


def assemble_greeting(template_path, output_path):
    try:
        data = {"Name": "Amara Osei", "Age": 41}

        assembler = DocumentAssembler()
        assembler.assemble_document(template_path, output_path, DataSourceInfo(data, "data"))

        print("Document assembled successfully:", output_path)
    except FileNotFoundError:
        print("Template file not found:", template_path)
    except Exception as error:
        print("Error:", str(error).splitlines()[0])


assemble_greeting("staff-greeting.docx", "staff-greeting-checked.docx")
# This template is not among the example's files
assemble_greeting("staff-greeting-2016.docx", "staff-greeting-2016-report.docx")
```
{{< /tab >}}
{{< tab "staff-greeting.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-greeting.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/error-handling/staff-greeting.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-greeting-checked.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/error-handling/handle_file_not_found_errors/staff-greeting-checked.docx)
{{< /tab >}}
{{< /tabs >}}

The exception's message is the engine's ("Could not find file '<full path>'."). A missing template does not leave a report file behind.

## Handle Missing Values

A `None` value is not an error: the tag outputs nothing, whatever its format, and the call succeeds. Here the invoice has no amount yet:

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler


def engine_message(error):
    # The first line holds the engine's message; " ---> " starts the inner .NET exception
    return str(error).splitlines()[0].split(" ---> ")[0]


invoice = {
    "CustomerName": "Quayside Bistro",
    "Amount": None,  # Not invoiced yet
}

try:
    assembler = DocumentAssembler()
    assembler.assemble_document("invoice-amount.docx", "invoice-amount-report.docx",
                                DataSourceInfo(invoice, "invoice"))
except Exception as error:
    print("Data type error:", engine_message(error))
    # Handle None values or provide defaults
```
{{< /tab >}}
{{< tab "invoice-amount.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [invoice-amount.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/error-handling/invoice-amount.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "invoice-amount-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/error-handling/handle_missing_values/invoice-amount-report.docx)
{{< /tab >}}
{{< /tabs >}}

The template line `Amount due: <<[invoice.Amount]:"C">>` becomes `Amount due:`. When the report must show a value, replace `None` in Python before the call.

## Comprehensive Error Handling

Combine multiple error handling strategies. Catch `FileNotFoundError` and `PermissionError` before `RuntimeError`, since the engine's file errors are `RuntimeError` too:

{{< tabs "example7" >}}
{{< tab "Python" >}}
```python
import os
import traceback

from groupdocs.assembly import DataSourceInfo, DocumentAssembler, DocumentAssemblyOptions


def engine_message(error):
    # The first line holds the engine's message; " ---> " starts the inner .NET exception
    return str(error).splitlines()[0].split(" ---> ")[0]


def assemble(template_path, output_path, data):
    # Validate inputs
    if not template_path or not os.path.exists(template_path):
        print("Invalid template path.")
        return

    # Validate data
    if data is None:
        print("Data source is null.")
        return

    try:
        assembler = DocumentAssembler()

        # Configure error handling options
        assembler.options |= DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS

        assembler.assemble_document(template_path, output_path, DataSourceInfo(data, "data"))

        print("Document assembled successfully.")
    except FileNotFoundError as error:
        print("File not found:", engine_message(error))
    except PermissionError as error:
        print("Access denied:", engine_message(error))
    except RuntimeError as error:
        print("Assembly error:", engine_message(error))
        # Log detailed error information: the full message holds the .NET details
    except Exception as error:
        print("Unexpected error:", error)
        traceback.print_exc()


assemble("missing-email.docx", "missing-email-checked.docx", {"Name": "Jonas Weber", "Age": 37})
```
{{< /tab >}}
{{< tab "missing-email.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [missing-email.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/error-handling/missing-email.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "missing-email-checked.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/error-handling/comprehensive_error_handling/missing-email-checked.docx)
{{< /tab >}}
{{< /tabs >}}

## Handle Stream Errors

With streams, the file errors come from Python itself: `open()` raises `FileNotFoundError` or `PermissionError`, both `OSError`, before the engine is called:

{{< tabs "example8" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

try:
    with open("staff-greeting.docx", "rb") as template_stream, io.BytesIO() as output_stream:
        data = {"Name": "Lena Park", "Age": 29}

        assembler = DocumentAssembler()
        assembler.assemble_document(template_stream, output_stream, DataSourceInfo(data, "data"))

        with open("staff-greeting-from-stream.docx", "wb") as f:
            f.write(output_stream.getvalue())
except OSError as error:
    print("IO error:", error)
except Exception as error:
    print("Error:", str(error).splitlines()[0])
```
{{< /tab >}}
{{< tab "staff-greeting.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-greeting.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/error-handling/staff-greeting.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-greeting-from-stream.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/error-handling/handle_stream_errors/staff-greeting-from-stream.docx)
{{< /tab >}}
{{< /tabs >}}

## Report Template Errors Inside the Document

Instead of raising, the engine can write each template error into the report, at the tag that failed. Set `DocumentAssemblyOptions.INLINE_ERROR_MESSAGES`: `assemble_document` then returns `False` when the template has errors and `True` when it has none. The example saves the report as plain text to an `io.BytesIO` and prints the lines that hold an error:

{{< tabs "example9" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import (DataSourceInfo, DocumentAssembler, DocumentAssemblyOptions, FileFormat,
                                LoadSaveOptions)

data = {"Name": "Amara Osei", "Team": "Operations"}

assembler = DocumentAssembler()
assembler.options = DocumentAssemblyOptions.INLINE_ERROR_MESSAGES

with open("broken-tag.docx", "rb") as template_stream, io.BytesIO() as output_stream:
    parsed = assembler.assemble_document(template_stream, output_stream, LoadSaveOptions(FileFormat.TEXT),
                                         DataSourceInfo(data, "data"))
    print("Template parsed without errors:", parsed)

    if not parsed:
        for line in output_stream.getvalue().decode("utf-8-sig").splitlines():
            if "Error!" in line:
                print(line)
```
{{< /tab >}}
{{< tab "broken-tag.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [broken-tag.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/error-handling/broken-tag.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "report-template-errors-inside-the-document.txt" >}}  
```text
Template parsed without errors: False
Name: <<[data.Name]> Error! Character '>' is unexpected.
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/error-handling/report_template_errors_inside_the_document/report-template-errors-inside-the-document.txt)
{{< /tab >}}
{{< /tabs >}}

The example prints:

```text
Template parsed without errors: False
Name: <<[data.Name]> Error! Character '>' is unexpected.
```

The report keeps the template text up to the error and marks it with "Error!"; after a syntax error, the tags that follow are left as they are (`Team: <<[data.Team]>>` above). A missing member is reported the same way: with `INLINE_ERROR_MESSAGES` and the missing-member template above, the call returns `False` and the report reads `Email: <<[data.Email] Error! Can not get the value of member 'Email' ...>>`. Combined with `ALLOW_MISSING_MEMBERS` (`options = INLINE_ERROR_MESSAGES | ALLOW_MISSING_MEMBERS`), a missing member is no error, and the call returns `True`.

## Error Handling Best Practices

1. **Always use try/except blocks** around assembly operations
2. **Validate inputs** before assembly (file existence, `None` and empty lists)
3. **Use specific exception types** when possible, `FileNotFoundError` and `PermissionError` before `RuntimeError`
4. **Enable `ALLOW_MISSING_MEMBERS`** if your data structure is dynamic
5. **Log errors** with sufficient detail for debugging: the full message holds the .NET exception type and stack trace
6. **Provide user-friendly error messages** in production code, and delete the empty report a failed call leaves

{{< alert style="warning" >}}
Some errors only occur during template evaluation, with particular data. Always test templates with sample data before deploying to production; `INLINE_ERROR_MESSAGES` makes a test run list every error of a template at once.
{{< /alert >}}

### Advanced Usage Topics

To learn more about detailed error logging, template validation, custom error handling, and debugging techniques, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
