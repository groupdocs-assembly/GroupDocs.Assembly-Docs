---
id: assembly-basic-usage-install-license
url: assembly/python-net/basic-usage-install-and-license
linktitle: Install and Apply License
title: Install GroupDocs.Assembly for Python via .NET and Apply License
weight: 1
description: "Learn how to install GroupDocs.Assembly for Python via .NET with pip and apply a license from a file, a stream or the GROUPDOCS_LIC_PATH environment variable."
keywords: install, pip, PyPI, license, setup, configure, GroupDocs.Assembly, Python, set_license, GROUPDOCS_LIC_PATH, metered license
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

Before you can start generating documents with GroupDocs.Assembly for Python via .NET, you need to install the package and apply a license. This guide shows you how to install the package from PyPI and configure licensing to remove evaluation limitations.

The main classes involved are:
- [License](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/license/) - for applying licenses
- [Metered](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/metered/) - for applying metered licenses
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - for assembling documents

Here are the steps to get started:

* Install the `groupdocs-assembly-net` package with pip
* Apply a license from a file or stream using the [set_license](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/license/set_license/) method, or name the license file in the `GROUPDOCS_LIC_PATH` environment variable
* Verify that the license is applied correctly before using DocumentAssembler

{{< alert style="info" >}}
Calling `set_license` multiple times is not harmful but wastes processor time. Call it once, at start-up: in a script, before the first assembly; in a web application, where the application is created (a Flask application factory, Django's `AppConfig.ready`, a FastAPI startup handler).
{{< /alert >}}

## Install from PyPI

The package is published on PyPI and bundles everything it needs, the .NET runtime included. Install it with pip:

```bash
pip install groupdocs-assembly-net
```

Then import it as `groupdocs.assembly`. See [Installation]({{< ref "assembly/python-net/getting-started/installation.md" >}}) and [System Requirements]({{< ref "assembly/python-net/getting-started/system-requirements.md" >}}) for the supported platforms and Python versions.

## Install a Specific Version

To pin a version, for instance in `requirements.txt`, name it:

```bash
pip install groupdocs-assembly-net==26.11.0
```

## Apply License from File

After installation, apply your license file to remove evaluation limitations. The example reads the path from the `GROUPDOCS_LIC_PATH` environment variable and falls back to a `GroupDocs.Assembly.lic` file in the current folder. A relative path is resolved against the current working directory of the process, which may differ from your script's folder (in a service or a web application), so an absolute path is recommended:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import os

from groupdocs.assembly import License

# Path to your license file
license_path = os.environ.get("GROUPDOCS_LIC_PATH", "GroupDocs.Assembly.lic")

# Apply the license
if os.path.exists(license_path):
    license = License()
    license.set_license(license_path)
    print("License applied successfully from file.")
else:
    print("License file not found. Running in evaluation mode.")
```
{{< /tab >}}
{{< tab "apply-license-from-file.txt" >}}  
```text
License applied successfully from file.
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/install-and-apply-license/apply_license_from_file/apply-license-from-file.txt)
{{< /tab >}}
{{< /tabs >}}

## Apply License from Stream

You can also load a license from any readable binary stream, which is handy when the license ships inside your application's package:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import os

from groupdocs.assembly import License

license_path = os.environ.get("GROUPDOCS_LIC_PATH", "GroupDocs.Assembly.lic")

if os.path.exists(license_path):
    # Load license file into a stream
    with open(license_path, "rb") as stream:
        license = License()
        license.set_license(stream)
    print("License applied successfully from stream.")
else:
    print("License file not found. Running in evaluation mode.")
```
{{< /tab >}}
{{< tab "apply-license-from-stream.txt" >}}  
```text
License applied successfully from stream.
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/install-and-apply-license/apply_license_from_stream/apply-license-from-stream.txt)
{{< /tab >}}
{{< /tabs >}}

## Apply License from an Environment Variable

Set `GROUPDOCS_LIC_PATH` to the license file's path, or to a URL that serves it, and the license is applied at the first call into the engine, with no licensing code:

{{< tabs "env-license" >}}
{{< tab "Windows" >}}
```ps
$env:GROUPDOCS_LIC_PATH = "C:\licenses\GroupDocs.Assembly.lic"
```
{{< /tab >}}
{{< tab "Linux / macOS" >}}
```bash
export GROUPDOCS_LIC_PATH="/opt/licenses/GroupDocs.Assembly.lic"
```
{{< /tab >}}
{{< /tabs >}}

A license that cannot be applied this way (a missing file, an expired subscription, a license for another product) raises `LicenseError` from the first call into the engine on, rather than letting the process run in evaluation mode unnoticed. The message names the variable and the reason, for instance "GROUPDOCS_LIC_PATH=missing.lic could not be applied: the file does not exist". Set `GROUPDOCS_LIC_STRICT=0` to get a `LicenseWarning` and evaluation mode instead.

## Verify License Application

The `is_licensed` property tells whether a license is applied. To be sure, generate a document and check that it has no evaluation watermark:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
import os

from groupdocs.assembly import DataSourceInfo, DocumentAssembler, License

license_path = os.environ.get("GROUPDOCS_LIC_PATH", "GroupDocs.Assembly.lic")

license = License()
if os.path.exists(license_path):
    license.set_license(license_path)
print("Licensed:", license.is_licensed)

# Try to assemble a simple document
assembler = DocumentAssembler()
assembler.assemble_document("license-check.docx", "license-check-report.docx",
                            DataSourceInfo("Harbor Lane Provisions", "company"))
# If the license is valid, no evaluation watermark appears
print("License verification: check license-check-report.docx for a watermark.")
```
{{< /tab >}}
{{< tab "license-check.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [license-check.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/install-and-apply-license/license-check.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "license-check-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/install-and-apply-license/verify_license_application/license-check-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Apply a Metered License

A [Metered License](https://purchase.groupdocs.com/faqs/licensing/metered/) bills by usage. Pass your public and private keys to [set_metered_key](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/metered/) before using the API, then read the consumption. This code is not run with the documentation, because it needs your own keys; keys that are not valid raise `RuntimeError` ("Authentication failed."):

```python
import os

from groupdocs.assembly import Metered

public_key = os.environ["GROUPDOCS_METERED_PUBLIC_KEY"]
private_key = os.environ["GROUPDOCS_METERED_PRIVATE_KEY"]

# Apply the metered keys before assembling documents
metered = Metered()
metered.set_metered_key(public_key, private_key)

print("Consumption quantity:", Metered.get_consumption_quantity())
print("Consumption credit:", Metered.get_consumption_credit())
```

{{< alert style="warning" >}}
The license file contains a digital signature. Do not modify the license file, as even adding an extra line break will invalidate it.
{{< /alert >}}

## "Cannot find license" Error

`set_license` with a path that does not exist raises `FileNotFoundError` ("Cannot find license 'GroupDocs.Assembly.lic'."). When you download the license, some web browsers append `.xml` to its name, and Windows hides known extensions by default, so `GroupDocs.Assembly.lic.xml` is shown as `GroupDocs.Assembly.lic`. Rename the file to remove the `.xml` extension. You are not required to keep the name `GroupDocs.Assembly.lic`: rename the file as you like and pass that name.

### Advanced Usage Topics

To learn more about the evaluation limitations and the licensing options, please refer to [Evaluation Limitations and Licensing]({{< ref "assembly/python-net/getting-started/licensing-and-subscription.md" >}}) and the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
