---
id: system-requirements
url: assembly/net/system-requirements
title: System Requirements
weight: 4
description: "GroupDocs.Assembly for .NET system requirements: supported Windows, Linux and macOS releases, the .NET and Mono frameworks, and the development environments it runs in."
keywords: 
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

GroupDocs.Assembly for .NET does not require any external software or third party tool to be installed. Just follow one of the way as described in [Development Environment, Installation and Configuration]({{< ref "assembly/net/getting-started/development-environment-installation-and-configuration.md" >}}).

## Supported Operating Systems

GroupDocs.Assembly for .NET supports any 32-bit or 64-bit operating system where .NET or Mono framework is installed including, but not limited to:

### Windows

*   Microsoft Windows 2003 Server ( x64, x86)
*   Microsoft Windows 2008 Server ( x64, x86)
*   Microsoft Windows 2012 Server ( x64, x86)
*   Microsoft Windows 2012 R2 Server ( x64, x86)
*   Microsoft Windows 2016 Server ( x64, x86)
*   Microsoft Windows 2019 Server ( x64, x86)
*   Microsoft Windows Vista ( x64, x86)
*   Microsoft Windows XP ( x64, x86)
*   Microsoft Windows 7 ( x64, x86)
*   Microsoft Windows 8, 8.1 ( x64, x86)
*   Microsoft Windows 10 ( x64, x86)
*   Microsoft Azure

### Linux

*   Linux (Ubuntu, OpenSUSE, CentOS and others)

### Mac

*   Mac OS X

## Supported Frameworks

GroupDocs.Assembly for .NET  supports .NET and Mono frameworks as follows:

### .NET Frameworks

*   .NET Framework 2.0
*   .NET Framework 3.5
*   .NET Framework 4.0
*   .NET Framework 4.0\_ClientProfile
*   .NET Framework 4.5.0
*   .NET Framework 4.5.1
*   .NET Framework 4.5.2
*   .NET Framework 4.6.0
*   .NET Framework 4.6.2
*   .NET Framework 4.5.0
*   .NET Framework 4.5.1
*   .NET Framework 4.6.0
*   .NET Framework 4.6.2
*   .NET Framework 4.7
*   .NET Framework 4.7.2
*   .NET Framework 4.8
*   .NET Framework 4.8.1

Starting with version 26.11, GroupDocs.Assembly for .NET includes a build for **.NET Framework 4.8** (`net48`). Projects targeting .NET Framework 4.8 or 4.8.1 get it automatically from NuGet, with no code changes required. Projects targeting .NET Framework 4.6.2–4.7.2 keep working with the .NET Framework 4.6.2 build (`net462`) for now.

{{< alert style="warning" >}}
Microsoft ends support for .NET Framework 4.6.2 on **January 12, 2027**. After that date, we will continue shipping the .NET Framework 4.6.2 build (`net462`) as deprecated for a few more months, and then remove it. From that point, .NET Framework 4.8 will be the minimum supported .NET Framework version. We recommend moving projects that target .NET Framework 4.6.2–4.7.2 to .NET Framework 4.8 before January 2027.
{{< /alert >}}

### Mono Framework

*   Mono 2.6.7 or later

## Development Environments

GroupDocs.Assembly for .NET can be used to develop applications in any development environment that targets the .NET platform, but the following environments are explicitly supported:

*   Microsoft Visual Studio 2010
*   Microsoft Visual Studio 2011
*   Microsoft Visual Studio 2012
*   Microsoft Visual Studio 2013
*   Microsoft Visual Studio 2015
*   Microsoft Visual Studio 2017
*   Microsoft Visual Studio 2019
*   Xamarin.Android
*   Xamarin.IOS
*   Xamarin.Mac
*   MonoDevelop 2.4 and later

For a container or a serverless function the list is shorter and the fonts matter more: [Document generation in Docker and serverless]({{< ref "/assembly/net/use-cases/running-in-docker-and-serverless.md" >}}).
