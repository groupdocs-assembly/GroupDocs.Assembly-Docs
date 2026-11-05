---
id: system-requirements
url: assembly/python-net/system-requirements
title: System Requirements
linkTitle: System Requirements
weight: 3
description: "System requirements for GroupDocs.Assembly for Python via .NET - 64-bit Python 3.5-3.14 on Windows, Linux (glibc 2.27+) and macOS 12+, with ICU on Linux and libgdiplus for presentations."
keywords: GroupDocs.Assembly for Python via .NET, system requirements, supported operating systems, Python versions, Windows, Linux, macOS, glibc, ICU, libgdiplus, fonts, pip
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
toc: True
---

{{< alert style="info" >}}
GroupDocs.Assembly for Python via .NET ships as a self-contained wheel that bundles the .NET runtime it needs. No Microsoft Office, third-party document software, .NET install or Mono install is required. On Linux and macOS a few system packages are needed; see [Platform Dependencies](#platform-dependencies). To install the library, follow the steps in the [Installation]({{< ref "assembly/python-net/getting-started/installation.md" >}}) guide.
{{< /alert >}}

## Supported Operating Systems

GroupDocs.Assembly for Python via .NET runs on Windows, Linux, and macOS. The package ships as a platform-specific `.whl`, and `pip` picks the correct one automatically.

### Windows

* Microsoft Windows 10 (x64)
* Microsoft Windows 11 (x64)
* Microsoft Windows Server 2016, 2019, 2022 and 2025

The Windows wheel is 64-bit only: use a 64-bit Python.

### Linux

* Any **x86-64** distribution with **glibc 2.27 or newer** - for example Ubuntu 18.04+, Debian 10+, RHEL 8+. The embedded .NET runtime needs glibc 2.27, and the wheel's `manylinux_2_27_x86_64` tag says so, so pip refuses an older system.

### macOS

* macOS 12 (Monterey) and later - Intel and Apple Silicon (M-series). The wheels are tagged `macosx_12_0_*`, the oldest system the bundled .NET runtime starts on. Microsoft supports .NET 10 on macOS 14 and later.

## Python Version

GroupDocs.Assembly for Python via .NET supports **Python 3.5 through 3.14**, 64-bit. The wheel uses the `py3-none-{platform}` tag, meaning it works with any Python 3.x version in that range without per-version rebuilds.

| Python Version | Supported |
| --- | :---: |
| 3.5  | Yes |
| 3.6  | Yes |
| 3.7  | Yes |
| 3.8  | Yes |
| 3.9  | Yes |
| 3.10 | Yes |
| 3.11 | Yes |
| 3.12 | Yes |
| 3.13 | Yes |
| 3.14 | Yes |

## Package Manager

GroupDocs.Assembly for Python via .NET is distributed via [PyPI](https://pypi.org/project/groupdocs-assembly-net/) and the [GroupDocs Releases website](https://releases.groupdocs.com/assembly/python-net/):

```bash
pip install groupdocs-assembly-net
```

pip picks the wheel for your platform. To install without access to PyPI, download it from the releases website, as described on the [Installation]({{< ref "assembly/python-net/getting-started/installation.md" >}}) page. One wheel is published per platform:

| Platform | Wheel suffix |
| --- | --- |
| Windows 64-bit | `py3-none-win_amd64.whl` |
| Linux x64 (glibc) | `py3-none-manylinux_2_27_x86_64.whl` |
| macOS Apple Silicon | `py3-none-macosx_12_0_arm64.whl` |
| macOS Intel | `py3-none-macosx_12_0_x86_64.whl` |

`pip` 20.3 or newer picks the right wheel for your platform; older versions do not recognise these tags, so upgrade with `python -m pip install --upgrade pip` (on Python 3.5, `python -m pip install "pip==20.3.4"`). On an Intel Mac, a Python built against a pre-11 macOS SDK reports its system as macOS 10.16 - there use pip 24.1 or newer, or run `SYSTEM_VERSION_COMPAT=0 pip install groupdocs-assembly-net`.

## Platform Dependencies

### Linux

Install **ICU**, **`libgdiplus`** and the **fonts** your templates use:

```bash
sudo apt-get update
sudo apt-get install -y libicu-dev libgdiplus fontconfig ttf-mscorefonts-installer
```

What each package is for, measured on the 26.7 engine:

- **ICU** (`libicu-dev`, any version your distribution ships) - required. The .NET runtime needs it for text processing: without it, the first call into the engine aborts the Python process with `Couldn't find a valid ICU package`. Do not set `DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=1` to work around it.
- **`libgdiplus`** - presentations. Without it, no presentation template (PPTX, PPT, ODP and the others) can be filled or saved: the call raises `The type initializer for 'Gdip' threw an exception`. Word processing, spreadsheet, email, HTML and text templates are filled without it, and saved to every format listed on the [Supported Document Formats]({{< ref "assembly/python-net/getting-started/supported-document-formats.md" >}}) page.
- **Fonts** - the reports drawn as PDF, XPS or images use the fonts their text is set in, as on Windows. The measurements above used the Microsoft core fonts (`ttf-mscorefonts-installer`, from Debian's `contrib` section) and `fontconfig`; with only the DejaVu fonts that `libgdiplus` installs, every example of this documentation but four runs, PDF reports included. **A QR code needs the template's default font installed under its name**: a Word document's default font (Times New Roman in this documentation's barcode templates) or a workbook's Normal style font (Calibri is the Excel default). Without it the call raises `Value cannot be null. (Parameter 'trueTypeFont')`, and DejaVu, the Liberation fonts and Carlito do not stand in. Code 128, EAN-13 and Codabar barcodes need no particular font. Install the template's font, or set the template in a font the system has: the spreadsheet barcode sample of this documentation is set in Arial for that reason.

### macOS

Install `mono-libgdiplus` using [Homebrew](https://brew.sh/), for presentations, as on Linux:

```bash
brew install mono-libgdiplus
```

### Windows

No extra dependencies - the wheel is self-contained.

## Performance Notes

* The first call into the engine takes about a second.
* On Windows, when a license is applied, the first call in a process takes 15-30 seconds: that is the engine's license check, which runs once per process. Keep one process for many reports.

## Development Environments

Any editor or IDE that runs CPython works, for example Visual Studio Code, PyCharm and Jupyter. Type stubs (`.pyi`) ship in the wheel, so editors complete class and member names.
