---
id: evaluation-limitations-and-licensing
url: assembly/python-net/evaluation-limitations-and-licensing
title: Evaluation Limitations and Licensing
weight: 5
description: "GroupDocs.Assembly for Python provides different plans for purchase or offers a Free Trial and a 30-day Temporary License for evaluation."
keywords: free, free trial, evaluation, groupdocs assembly java
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
toc: True
---

To study the system, you may want quick access to the API. To make this easier, GroupDocs.Assembly provides different plans for purchase and offers a Free Trial and a 30-day Temporary License for evaluation.

{{< alert style="info" >}}GroupDocs.Assembly also works without the license in trial mode with certain limitations{{< /alert >}}

## Purchased License

After buying, apply the license file or include it as an embedded resource. 

License needs to be set:
- Only once per application domain
- Before using any other GroupDocs.Viewer classes

## Evaluation Version Limitations

You can easily download GroupDocs.Assembly for evaluation. The evaluation download is the same as the purchased download. The evaluation version simply becomes licensed when you add a few lines of code to apply the license. You will face following limitations while using the API without the license.  

| Document | Spreadsheet | Presentation |
| --- | --- | --- |
| GroupDocs.Assembly (without a license specified) generates the document reports with full product functionality, but it inserts an evaluation watermark at the top of the document | When a Spreadsheet report is generated it contains an extra worksheet with Evaluation Copyright Warning on it, you can't hide the Evaluation Copyright Warning (the extra worksheet) | When a presentation report is generated using GroupDocs.Assembly, an Evaluation Watermark is injected at the center of each slide |
| It limits the maximum document size to several hundred paragraphs | When running your program, you can only generate 100 Spreadsheet reports using GroupDocs.Assembly. If your application exceeds this number, an exception will be thrown |  |
|  | You can't re-specify the script path (e.g in the web.config file) |  |

## Licensing 

The license file contains details such as the product name, number of developers it is licensed to, subscription expiry date and so on. It contains the digital signature, so don't modify the file. Even inadvertent addition of an extra line break into the file will invalidate it. You need to set a license before utilizing GroupDocs.Assembly API if you want to avoid its evaluation limitations. 

The license can be loaded from a file or stream object.

### Applying license from file

The code below will explain how to apply a  product license.

{{< tabs "example1">}}
{{< tab "Python" >}}

```python
import groupdocs.assembly as ga
import constants
import os
  

def run():
    if os.path.exists(constants.license_path):    
        license = ga.License()
        license.set_license(constants.license_path)
        print("License set successfully.")
    else:
       print("\n")
```

{{< /tab >}}
{{< /tabs >}}

### Applying license from stream

The following code snippet shows how to set a license from a stream:

{{< tabs "example2">}}
{{< tab "Python" >}}

```python
import groupdocs.assembly as ga
import constants
import os
from os.path import join

def run():
    if os.path.exists(constants.license_path):
        with open(constants.license_path, "rb") as stream:
            ga.License().set_license(stream)

        print("License set successfully.")
    else:
        print("\nWe do not ship any license with this example. " +
              "\nVisit the GroupDocs site to obtain either a temporary or permanent license. " +
              "\nLearn more about licensing at https://purchase.groupdocs.com/faqs/licensing. " +
              "\nLearn how to request a temporary license at https://purchase.groupdocs.com/temporary-license.")

if __name__ == "__main__":
    run()
```

{{< /tab >}}
{{< /tabs >}}


### Applying Metered License

{{< alert style="info" >}}
You can also set [Metered](https://reference.groupdocs.com/python-net/assembly/groupdocs.assembly/metered) license as an alternative to license file. It is a new licensing mechanism that will be used along with existing licensing method. It is useful for the customers who want to be billed based on the usage of the API features. For more details, please refer to [Metered Licensing FAQ](https://purchase.groupdocs.com/faqs/licensing/metered) section.
{{< /alert >}}

Here are the simple steps to use the `Metered` class.

1.  Create an instance of `Metered` class.
2.  Pass public & private keys to `setMeteredKey` method.
3.  Do processing (perform task).
4.  call method `getConsumptionQuantity` of the `Metered` class.
5.  It will return the amount/quantity of API requests that you have consumed so far.
6.  call method `getConsumptionCredit` of the `Metered` class (Since version 19.5).
7.  It will return the credit that you have consumed so far.

Following is the sample code demonstrating how to use `Metered` class.
{{< tabs "example3">}}
{{< tab "Python" >}}
```python
import groupdocs.assembly as ga

def run():
    public_key = "*****"  # Your public key
    private_key = "*****"  # Your private key

    ga.Metered().set_metered_key(public_key, private_key)

    print("License set successfully.")

if __name__ == "__main__":
    run()


```
{{< /tab >}}
{{< /tabs >}}

{{< alert style="info" >}}
Calling [License.setLicense](https://reference.groupdocs.com/assembly/python-net/com.groupdocs.assembly.licensing/License) multiple times is not harmful but simply wastes processor time. It is called once when the application starts.
{{< /alert >}}