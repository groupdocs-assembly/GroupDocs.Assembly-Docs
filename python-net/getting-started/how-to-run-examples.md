---
id: how-to-run-examples
url: assembly/python-net/how-to-run-examples
title: How to Run Examples
weight: 7
description: "How to clone, set up, and run the GroupDocs.Assembly for Python via .NET example suite - locally, with a license, or in Docker."
keywords: "groupdocs assembly python, examples, run examples, docker, ci"
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
toc: True
structuredData:
  showOrganization: True
  application:
    name: Document Assembly and Report Generation
    description: Build documents and reports from templates and data using Python language and GroupDocs.Assembly for Python via .NET
    productCode: assembly
    productPlatform: python-net
  howTo:
    name: How to run Assembly examples
    description: Learn how to run GroupDocs.Assembly examples using Python
    steps:
      - name: Clone repository
        text: Clone the repository with Assembly examples from GitHub
      - name: Install package
        text: Install the GroupDocs.Assembly package with pip
      - name: Run examples
        text: Execute run_all_examples.py to run the examples
---

The complete project [GroupDocs.Assembly for Python via .NET](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET) with code examples and sample files is hosted on GitHub. Every example of this documentation is there as a script, next to its templates and data files.

## Prerequisites

- [Python 3.5-3.14](https://www.python.org/downloads/), 64-bit.
- On Linux, ICU, `libgdiplus` and fonts (`libicu-dev libgdiplus fontconfig ttf-mscorefonts-installer`). On macOS: `mono-libgdiplus` (via Homebrew). See [System Requirements]({{< ref "assembly/python-net/getting-started/system-requirements.md" >}}) for what each one is needed for.

## Get the code

```bash
git clone https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET.git
cd ./GroupDocs.Assembly-for-Python-via-.NET/Examples
```

## Project structure

```
Examples/
├── run_all_examples.py     # Runs every example and prints a pass/fail summary
├── requirements.txt
├── product-overview/       # The quick example of the product overview
├── licensing/              # Set a license from a file, a stream, or a metered key
├── getting-started/
│   ├── hello-world/        # Fill a Word template with a dict
│   └── quick-start-guide/  # A Word table, a PDF report from JSON, an Excel sheet
└── developer-guide/
    ├── basic-usage/        # Template syntax, data sources, tables, lists, images, email, output formats
    └── advanced-usage/     # Every report type in every format: charts, barcodes, master-detail, data bands
```

The folders follow this documentation: each page's examples are in the folder of that page, with the templates and data files they read.

## Set up

```bash
pip install -r requirements.txt
```

To run the examples with the full feature set, apply a license. The simplest way is the `GROUPDOCS_LIC_PATH` environment variable, which the package applies at the first call into the engine:

{{< tabs "set-license" >}}
{{< tab "Windows" >}}
```batch
set GROUPDOCS_LIC_PATH=C:\path\to\GroupDocs.Assembly.lic
```
{{< /tab >}}
{{< tab "Linux / macOS" >}}
```bash
export GROUPDOCS_LIC_PATH=/path/to/GroupDocs.Assembly.lic
```
{{< /tab >}}
{{< /tabs >}}

Without a license the suite still runs, in evaluation mode: every report carries an evaluation mark, and a report stops after about 200 paragraphs (see [Licensing and evaluation]({{< ref "assembly/python-net/getting-started/licensing-and-subscription.md" >}})).

## Run the examples

Run the full suite, which prints a pass/fail summary at the end:

```bash
python run_all_examples.py
```

You can also run any single example by navigating to its folder and running the script directly. Each example reads its templates and data from its own folder, and writes its reports next to the script:

```bash
cd getting-started/hello-world
python hello_world.py
```

## Run with Docker

The repository ships a `Dockerfile` that builds a Linux image with Python 3.13, the system packages the library needs on Linux (ICU, `libgdiplus` and the Microsoft core fonts), and the package preinstalled from PyPI.

```bash
# Build the image
docker build -t assembly-examples .

# Run unlicensed (evaluation mode)
docker run --rm assembly-examples

# Run with a license mounted from the host
docker run --rm \
    -v /path/to/license:/lic:ro \
    -e GROUPDOCS_LIC_PATH=/lic/your-license.lic \
    assembly-examples
```

## Continuous integration

The `.github/workflows/` directory contains a workflow that runs the full example suite on every push, on `ubuntu-latest` with Python 3.13. The same run is reproducible locally via the `Dockerfile` above.

## Troubleshooting

- **"Couldn't find a valid ICU package"**, with the Python process ending abruptly (Linux) - install ICU (`libicu-dev` on Debian and Ubuntu). Do not set `DOTNET_SYSTEM_GLOBALIZATION_INVARIANT`.
- **"The type initializer for 'Gdip' threw an exception"** for a presentation template (Linux/macOS) - install `libgdiplus` (`sudo apt install libgdiplus`, or `brew install mono-libgdiplus` on macOS).
- **"Evaluation Only" in the reports, or a report that stops early** - the evaluation limits. Apply a license (see above); a free 30-day [temporary license](https://purchase.groupdocs.com/temporary-license) is available.
- **`LicenseError` at the first call** - `GROUPDOCS_LIC_PATH` names a file that is missing, expired or for another product. The message gives the engine's reason.
- **The first example takes 15-30 seconds** (Windows, with a license) - that is the engine's license check, which runs once per process.
- **The output differs from the output tab** - the tabs come from a run on Windows set to US English, and numbers, currencies and dates that a template formats follow the culture of the process: `<<[price]:"C">>` writes `$18.40` there, and another currency sign elsewhere.

## Contribute

If you would like to add or improve an example, we encourage you to contribute to the project. All examples in this repository are open source and can be freely used in your own applications. Fork the repository, edit the source code, and open a pull request.
