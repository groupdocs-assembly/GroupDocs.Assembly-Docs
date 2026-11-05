---
id: set-checkbox-values-dynamically
url: assembly/python-net/set-checkbox-values-dynamically
title: Set Checkbox Values Dynamically
weight: 50
description: "Set Checkbox Values Dynamically with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: set checkbox values dynamically, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

You can set checkbox values to either checked or unchecked in your reports dynamically by taking the following steps:

1.  Add a checkbox content control to your template at a place where you want it to appear in a result document.
2.  By editing content control properties, add a check tag to the title of the checkbox content control using the following syntax.

```text
<<check [conditional_expression]>>
```

The code will look like following snippet:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("checkbox.docx", "checkbox-report.docx", DataSourceInfo(True, "conditional_expression"))
```
{{< /tab >}}
{{< tab "checkbox.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [checkbox.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/set-checkbox-values-dynamically/checkbox.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "checkbox-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/set-checkbox-values-dynamically/set_checkbox_values_dynamically/checkbox-report.docx)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("dropdown.docx", "dropdown-report.docx", [
    DataSourceInfo("Harbor Blend whole bean coffee", "choice_one"),
    DataSourceInfo("Coffee", "choice_one_display_name"),
    DataSourceInfo("Cold-pressed olive oil", "choice_two"),
    DataSourceInfo("Olive oil", "choice_two_display_name"),
    DataSourceInfo("Aged harbour cheddar", "choice_three"),
    DataSourceInfo("Cheddar", "choice_three_display_name"),
])
```
{{< /tab >}}
{{< tab "dropdown.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [dropdown.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/set-checkbox-values-dynamically/dropdown.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "dropdown-report.docx" >}}  
```text
Binary file (DOCX, 16 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/set-checkbox-values-dynamically/set_checkbox_values_dynamically_2/dropdown-report.docx)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("combobox.docx", "combobox-report.docx", [
    DataSourceInfo("Harbor Blend whole bean coffee", "choice_one"),
    DataSourceInfo("Coffee", "choice_one_display_name"),
    DataSourceInfo("Cold-pressed olive oil", "choice_two"),
    DataSourceInfo("Olive oil", "choice_two_display_name"),
    DataSourceInfo("Aged harbour cheddar", "choice_three"),
    DataSourceInfo("Cheddar", "choice_three_display_name"),
])
```
{{< /tab >}}
{{< tab "combobox.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [combobox.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/set-checkbox-values-dynamically/combobox.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "combobox-report.docx" >}}  
```text
Binary file (DOCX, 15 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/set-checkbox-values-dynamically/set_checkbox_values_dynamically_3/combobox-report.docx)
{{< /tab >}}
{{< /tabs >}}

Here, conditional\_expression defines a condition upon which the value of the checkbox content control is to be set to checked (or unchecked, if the condition is not met). The conditional expression must return a Boolean value.

While building a report, a conditional expression declared within a check tag is evaluated and the value of its containing checkbox content control is set accordingly. The check tag itself is removed then.

{{< alert style="warning" >}}Dynamic checkbox value setting is available for Word Processing documents only.{{< /alert >}}
