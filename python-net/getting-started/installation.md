---
id: installation
url: assembly/python-net/installation
title: Install GroupDocs.Assembly for Python via .NET
linkTitle: Installation
weight: 1
keywords: install, installation, pip, pypi, wheel, whl, Windows, Linux, macOS, Apple Silicon, manylinux, requirements.txt, GroupDocs.Assembly, python
description: "Install GroupDocs.Assembly for Python via .NET on Windows, Linux, or macOS - from PyPI or from a pre-downloaded wheel, including Intel and Apple Silicon builds."
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
toc: True
structuredData:
  showOrganization: True
  application:
    name: Document Assembly and Report Generation Tool
    description: The product builds documents and reports from templates of Word, Excel, PowerPoint, email, HTML, Markdown and text formats, filled with data from Python objects, JSON, XML, CSV and document tables.
    productCode: assembly
    productPlatform: python-net
  howTo:
    name: How to install Assembly API
    description: Learn how to install GroupDocs.Assembly into Python
    steps:
      - name: Install from PyPI
        text: Install the package with pip from the PyPI repository
      - name: Download from the official website
        text: Download the OS-specific wheel from the GroupDocs releases website and install it with pip
---

GroupDocs.Assembly for Python via .NET is distributed as a pre-built wheel on [PyPI](https://pypi.org/project/groupdocs-assembly-net/). The PyPI index hosts a separate wheel for each supported platform, and `pip` picks the correct one automatically. Each wheel is self-contained: it bundles the embedded .NET runtime and every managed dependency, so no Microsoft Office, OpenOffice, or separate runtime install is required.

{{< alert style="info" >}}
Before you install, review the [System Requirements]({{< ref "assembly/python-net/getting-started/system-requirements.md" >}}). The wheels need 64-bit Python 3.5-3.14 and pip 20.3 or newer, and run on Windows, on Linux with glibc 2.27 or newer, and on macOS 12 or newer. On Linux, install ICU, `libgdiplus` and fonts; on macOS, install `mono-libgdiplus` (see [Platform Prerequisites](#platform-prerequisites)).
{{< /alert >}}

## Install Package from PyPI

Open a terminal and run the install command for your platform:

{{< tabs "install-pypi">}}
{{< tab "Windows" >}}
```ps
py -m pip install groupdocs-assembly-net
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 -m pip install groupdocs-assembly-net
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 -m pip install groupdocs-assembly-net
```
{{< /tab >}}
{{< /tabs >}}

After running the command you should see output similar to:

```bash
Collecting groupdocs-assembly-net
  Downloading groupdocs_assembly_net-26.11.0-py3-none-win_amd64.whl (81.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 81.1/81.1 MB 3.1 MB/s eta 0:00:00
Installing collected packages: groupdocs-assembly-net
Successfully installed groupdocs-assembly-net-26.11.0
```

The wheel file name will include a platform suffix that matches your operating system - for example `manylinux_2_27_x86_64` on Linux, `macosx_12_0_arm64` on Apple Silicon, or `win_amd64` on 64-bit Windows.

## Add the Package to `requirements.txt`

For reproducible environments, pin the package version in your `requirements.txt`:

```txt
groupdocs-assembly-net==26.11.0
```

Then install all dependencies in one step:

```bash
pip install -r requirements.txt
```

## Install from a Pre-Downloaded Wheel

If your build environment cannot reach PyPI, download the appropriate wheel from the [GroupDocs Releases website](https://releases.groupdocs.com/assembly/python-net/) and install it locally. Wheels are published for the following four platforms:

| Platform | Wheel file name ends with | Oldest system |
| --- | --- | --- |
| Windows 64-bit | `py3-none-win_amd64.whl` | Windows 10, Windows Server 2016 |
| Linux x64 (glibc) | `py3-none-manylinux_2_27_x86_64.whl` | glibc 2.27 (Ubuntu 18.04, Debian 10, RHEL 8) |
| macOS Apple Silicon (M-series) | `py3-none-macosx_12_0_arm64.whl` | macOS 12 |
| macOS Intel | `py3-none-macosx_12_0_x86_64.whl` | macOS 12 |

The file names state the oldest system each wheel runs on, so pip 20.3 or newer refuses a wheel the system cannot run. There is no 32-bit wheel.

Place the downloaded wheel into your project folder, then install it:

{{< tabs "install-wheel">}}
{{< tab "Windows (64-bit)" >}}
```ps
py -m pip install .\groupdocs_assembly_net-26.11.0-py3-none-win_amd64.whl
```
{{< /tab >}}
{{< tab "Linux (glibc)" >}}
```bash
python3 -m pip install ./groupdocs_assembly_net-26.11.0-py3-none-manylinux_2_27_x86_64.whl
```
{{< /tab >}}
{{< tab "macOS (Intel)" >}}
```bash
python3 -m pip install ./groupdocs_assembly_net-26.11.0-py3-none-macosx_12_0_x86_64.whl
```
{{< /tab >}}
{{< tab "macOS (Apple Silicon)" >}}
```bash
python3 -m pip install ./groupdocs_assembly_net-26.11.0-py3-none-macosx_12_0_arm64.whl
```
{{< /tab >}}
{{< /tabs >}}

Name the wheel file explicitly: PowerShell does not expand a `*` wildcard for a native command, so `pip install groupdocs_assembly_net-*.whl` fails there.

Expected output (Linux):

```bash
Processing ./groupdocs_assembly_net-26.11.0-py3-none-manylinux_2_27_x86_64.whl
Installing collected packages: groupdocs-assembly-net
Successfully installed groupdocs-assembly-net-26.11.0
```

If pip reports `is not a supported wheel on this platform`, pip is older than 20.3 or the system is older than the wheel needs: run `python -m pip install --upgrade pip` first. Python 3.5 needs pip 20.3.4, the last release for it. On an Intel Mac, a Python built against an old SDK reports macOS 10.16; use pip 24.1 or newer, or `SYSTEM_VERSION_COMPAT=0 pip install ...`.

## Upgrading from 25.5

GroupDocs.Assembly for Python via .NET 25.5 shipped Windows wheels only, for 32-bit and 64-bit Python. 26.11 adds Linux and macOS, supports Python 3.5 to 3.14, and takes Python dicts and lists as data sources; it has no 32-bit Windows wheel. Upgrade in place:

```bash
python -m pip install --upgrade groupdocs-assembly-net
```

## Platform Prerequisites

On Windows no extra steps are required. On Linux, install ICU, `libgdiplus` and the fonts your templates use; on macOS, `mono-libgdiplus`. The [System Requirements]({{< ref "assembly/python-net/getting-started/system-requirements.md" >}}) page explains what each one is for.

{{< tabs "platform-prereqs">}}
{{< tab "Linux" >}}
```bash
sudo apt-get update
sudo apt-get install -y libicu-dev libgdiplus fontconfig ttf-mscorefonts-installer
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
brew install mono-libgdiplus
```
{{< /tab >}}
{{< /tabs >}}

ICU is required: without it the process aborts at the first call into the engine. `libgdiplus` serves presentations: without it, a PowerPoint or OpenDocument presentation template cannot be filled.

## Verify the Installation

Confirm the package imported correctly:

```bash
python -c "import groupdocs.assembly; print('GroupDocs.Assembly is ready')"
```

You can also list the installed package with `pip show groupdocs-assembly-net` to confirm the version and location.

The first call into the engine takes about a second. On Windows, when a license is applied, the first call in a process takes 15-30 seconds: that is the engine's license check, which runs once per process.

## Next Steps

- Follow the [Hello, World!]({{< ref "assembly/python-net/getting-started/hello-world.md" >}}) guide to build your first report.
- Read the [Features Overview]({{< ref "assembly/python-net/getting-started/features-overview.md" >}}) to see everything you can do.
- Clone the [examples repository](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET) and read [How to Run Examples]({{< ref "assembly/python-net/getting-started/how-to-run-examples.md" >}}) to try every documented scenario locally.
