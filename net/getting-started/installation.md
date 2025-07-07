---
id: installation
url: assembly/net/installation
title: Install GroupDocs.Assembly for .NET
linkTitle: Installation
weight: 4
keywords: installation, NuGet package, NuGet package manager
description: "This topic describes how to install GroupDocs.Assembly for .NET."
productName: GroupDocs.Assembly for .NET
hideChildren: False
toc: True
---
This topic describes how to add the **GroupDocs.Assembly** library to your .NET project. You can use a NuGet package to install this library or you can download necessary DLLs from the GroupDocs website: [https://releases.groupdocs.com/assembly/net/](https://releases.groupdocs.com/assembly/net/).

## Install GroupDocs.Assembly using NuGet packages

You can use the following tools to install the **GroupDocs.Assembly** NuGet packages: 

 * [NuGet Package Manager](#use-the-nuget-package-manager)
 * [Package Manager Console](#use-the-package-manager-console)
 * [.NET CLI](#use-the-net-cli)

### Use the NuGet Package Manager

{{< alert style="tip" >}}

Earlier versions of Visual Studio does not include NuGet Package Manager. It can be added as an extension from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/).

* [NuGet Package Manager for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)
* [NuGet Package Manager for Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)
* [NuGet Package Manager for Visual Studio 2010 and 2012](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) 

{{< /alert >}}

Open your project or solution in Visual Studio and follow the steps below to install the **GroupDocs.Assembly** or **GroupDocs.Assembly.CrossPlatform** package using the NuGet Package Manager:

1. In **Solution Explorer**, right-click your project name and select **Manage NuGet Packages** to display the NuGet Package Manager.

    ![Add NuGet package in Visual Studio](/assembly/net/images/getting-started/installation/manage-nuget-packages.png)

2. Select the **Browse** tab and type **GroupDocs.Assembly** or **GroupDocs.Assembly.CrossPlatform** in the search box. Select the latest version of the package and click **Install**.

    ![Install GroupDocs.Assembly NuGet package in Visual Studio](/assembly/net/images/getting-started/installation/install-nuget-package.png)

### Use the Package Manager Console

The [Package Manager Console](https://learn.microsoft.com/en-us/nuget/consume-packages/install-use-packages-powershell) uses PowerShell commands to install, update, and remove NuGet packages. Open your project in Visual Studio and click **Tools** -> **NuGet Package Manager** -> **Package Manager Console** to open the console window. Run the the following command to install the latest version of the package:

{{< tabs "example1">}}
{{< tab "GroupDocs.Assembly for .NET" >}}
```
PM> Install-Package GroupDocs.Assembly
```
{{< /tab >}}
{{< /tabs >}}

![Use Package Manager Console ](/assembly/net/images/getting-started/installation/package-manager-console.png)

### Use the .NET CLI

You can also use the [.NET CLI tool](https://docs.microsoft.com/en-us/dotnet/core/tools/) to install and update NuGet packages. Open a terminal in your project's folder and execute the following command to install the package:

{{< tabs "example2">}}
{{< tab "GroupDocs.Assembly for .NET" >}}
```
dotnet add package GroupDocs.Assembly
```
{{< /tab >}}
{{< /tabs >}}

## Download GroupDocs.Assembly from the official website

Visit [https://releases.groupdocs.com/assembly/net/](https://releases.groupdocs.com/assembly/net/) and download the **GroupDocs.Assembly** assemblies as a ZIP archive or MSI installer. To reference the downloaded assembly files in your project, do the following:

1. Extract files from the ZIP archive or run the MSI installer to install **GroupDocs.Assembly** to a specific location on your computer.
2. Open your solution or project in Visual Studio.
3. In **Solution Explorer**, right-click the **References** or **Dependencies** node, and select **Add Reference** (for a .NET Framework project) or **Add Project Reference** (for a .NET project).

    ![Add project reference in Visual Studio](/assembly/net/images/getting-started/installation/add-project-reference.png)

4. In the **Reference Manager** dialog box, select the **Browse** tab and click **Browse** to locate the _GroupDocs.Assembly.dll_ file for the target framework.

    ![Browse for the GroupDocs.Assembly assembly](/assembly/net/images/getting-started/installation/browse-for-groupdocs-dll.png)

5. Click **OK** to add a reference to the **GroupDocs.Assembly** library to your project.

{{< alert style="warning" >}}
If your application targets .NET Core / .NET 5+, ensure that your project has all the required dependencies installed. Refer to the following page for details: [GroupDocs.Assembly dependencies](https://www.nuget.org/packages/groupdocs.assembly#dependencies-body-tab).
{{< /alert >}}