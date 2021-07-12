---
id: evaluation-limitations-and-licensing
url: assembly/java/evaluation-limitations-and-licensing
title: Evaluation Limitations and Licensing
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}You can use GroupDocs.Assembly without the license. The usage and functionalities are pretty much same as the licensed one but you will face few limitations while using the API without license.{{< /alert >}}

## Evaluation Version Limitations

You can easily download GroupDocs.Assembly for evaluation. The evaluation download is the same as the purchased download. The evaluation version simply becomes licensed when you add a few lines of code to apply the license. You will face few limitations while using the API without the license. See the limitations below regarding each supported format while using non-licensed GroupDocs.Assembly:

| Document | Spreadsheet | Presentation |
| --- | --- | --- |
| GroupDocs.Assembly (without a license specified) generates the document reports with full product functionality, but it inserts an evaluation watermark at the top of the document | When a Spreadsheet report is generated it contains an extra worksheet with Evaluation Copyright Warning on it, you can't hide the Evaluation Copyright Warning (the extra worksheet) | When a presentation report is generated using GroupDocs.Assembly, an Evaluation Watermark is injected at the center of each slide |
| It limits the maximum document size to several hundred paragraphs | When running your program, you can only generate 100 Spreadsheet reports using GroupDocs.Assembly. If your application exceeds this number, an exception will be thrown |
| | You can't re-specify the script path (e.g in the web.config file) | |

## Licensing

The license file contains details such as the product name, number of developers it is licensed to, subscription expiry date and so on. It contains the digital signature, so don't modify the file. Even inadvertent addition of an extra line break into the file will invalidate it. You need to set a license before utilizing GroupDocs.Assembly API if you want to avoid its evaluation limitations. 

The license can be loaded from a file or stream object. The easiest way to set a license is to put the license file in the same folder as the GroupDocs.Assembly.jar file and specify the file name, without a path, as shown in the examples below.

### Applying License from File

The code below will explain how to apply license from the file.

{{< gist GroupDocsGists 4749779f9e9aa688011bec1b98f0f57e >}}



### Applying License from Stream

Following code snippet shows how to apply license from the stream.

{{< gist GroupDocsGists 1e7b64c7376118958c7c084544042b85 >}}



### Applying Metered License

{{< alert style="warning" >}}Since version 18.9, the Metered licensing security has been improved. Metered licensing is now applicable only in Java runtime version 8u101 or above. Please use other types of licensing if you are using v18.9 or greater in Java 7.{{< /alert >}}{{< alert style="info" >}}You can also set Metered license as an alternative to license file. It is a new licensing mechanism that will be used along with existing licensing method. It is useful for the customers who want to be billed based on the usage of the API features. For more details, please refer to [Metered Licensing FAQ](https://purchase.groupdocs.com/faqs/licensing/metered) section.{{< /alert >}}

Here are the simple steps to use the `Metered` class.

1.  Create an instance of `Metered` class.
2.  Pass public & private keys to `setMeteredKey` method.
3.  Do processing (perform task).
4.  call method `getConsumptionCredit` of the `Metered` class (Since version 19.5).
5.  It will return the credit that you have consumed so far.

Following is the sample code demonstrating how to use `Metered` class.

{{< gist GroupDocsGists f33c57a23b6ea00affe1d69c635678ff >}}


