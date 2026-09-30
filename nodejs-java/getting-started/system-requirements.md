---
id: system-requirements
url: assembly/nodejs-java/system-requirements
title: System Requirements
weight: 3
description: "System requirements for GroupDocs.Assembly for Node.js via Java: supported operating systems, Node.js and Java versions, and native build tools."
keywords: system requirements, supported operating systems, node.js, java, jdk, node-gyp
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---

GroupDocs.Assembly for Node.js via Java does not require Microsoft Office or any other third-party software. It needs Node.js, Java and, at installation time, a native build toolchain for the [java](https://www.npmjs.com/package/java) bridge package.

## Supported operating systems

GroupDocs.Assembly for Node.js via Java runs on any 64-bit operating system where Node.js and Java are available, including:

### Windows

*   Windows 10, Windows 11
*   Windows Server 2016, 2019, 2022, 2025
*   Microsoft Azure

### Linux

*   Ubuntu, Debian, CentOS, RHEL, AlmaLinux, Rocky Linux, Amazon Linux, OpenSUSE and other modern distributions

### macOS

*   macOS 12 Monterey and later (Intel and Apple Silicon)

## Node.js

Use a current LTS version of [Node.js](https://nodejs.org/en/about/previous-releases): Node.js 20 LTS or later is recommended.

## Java

GroupDocs.Assembly for Node.js via Java requires Java 8 (1.8) or later. Java 11, 17 and 21 LTS are supported; Java 17 LTS is recommended.

Install a **JDK**, not only a JRE, on the machine where you run `npm install`: the `java` bridge package compiles a native module against the JDK's JNI headers. A JRE is enough at runtime if the application is deployed with already built `node_modules`.

{{< alert style="info" >}}
On Java 16 and later, templates that call methods of JDK classes (for example, `name.toUpperCase()` or `Math.max(a, b)`) fail with `Can not resolve method` unless you open the `java.lang` package to the library. Run `require('java').options.push('--add-opens=java.base/java.lang=ALL-UNNAMED')` **before** you require `@groupdocs/groupdocs.assembly`. See [Setting up Known External Types](/assembly/nodejs-java/groupdocs-assembly-engine-apis/#setting-up-known-external-types).
{{< /alert >}}

Make sure Java can be found:

- Set `JAVA_HOME` to the JDK root folder.
- Add `JAVA_HOME/bin` to `PATH`.

Windows (PowerShell):

```powershell
$env:JAVA_HOME = "C:\Program Files\Java\jdk-17"
$env:Path = "$env:JAVA_HOME\bin;$env:Path"
```

Linux/macOS (Bash):

```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
export PATH="$JAVA_HOME/bin:$PATH"
```

## Build tools

The `java` package is built with [node-gyp](https://www.npmjs.com/package/node-gyp) during installation. Depending on your operating system, install the following tools (see the `Installation` section of node-gyp for full details).

### Linux

*   Python 3
*   `make`
*   A C/C++ compiler toolchain, such as GCC

On Debian/Ubuntu:

```bash
sudo apt-get update
sudo apt-get install -y build-essential python3
```

### macOS

*   Python 3
*   Xcode Command Line Tools (`xcode-select --install`)

### Windows

*   Python 3
*   Visual Studio Build Tools with the **Desktop development with C++** workload

With [Chocolatey](https://chocolatey.org/):

```powershell
choco install python visualstudio2022-workload-vctools -y
```

## Network access

`npm install` downloads the GroupDocs.Assembly JAR file from `releases.groupdocs.com` in the package's `postinstall` step, using `curl`. Make sure `curl` is available and the machine can reach that host, or see [Installation](/assembly/nodejs-java/installation/) for a manual download.

At runtime no network access is required, except when you use a [metered license](/assembly/nodejs-java/evaluation-limitations-and-licensing/).

## Fonts

To render Word, Excel and PowerPoint documents to fixed-layout formats such as PDF, XPS or images correctly, install the fonts used in your templates on the machine. On Linux servers and in containers, install a comprehensive font set (for example, DejaVu or Noto fonts) and any corporate fonts you use.

## Containers

Example for a Debian/Ubuntu-based image:

```bash
apt-get update \
  && apt-get install -y --no-install-recommends \
     curl ca-certificates build-essential python3 openjdk-17-jdk-headless fonts-dejavu \
  && rm -rf /var/lib/apt/lists/*
```

Then install the package in your application:

```bash
npm install @groupdocs/groupdocs.assembly
```
