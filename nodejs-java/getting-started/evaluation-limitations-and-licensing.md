---
id: evaluation-limitations-and-licensing
url: assembly/nodejs-java/evaluation-limitations-and-licensing
aliases:
    - /assembly/nodejs-java/licensing-and-subscription/
title: Evaluation Limitations and Licensing
weight: 6
description: "Evaluation limitations of GroupDocs.Assembly for Node.js via Java and how to apply a license from a file or stream, or a metered license."
keywords: license, licensing, evaluation, temporary license, metered license, node.js
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---

{{< alert style="info" >}}You can use GroupDocs.Assembly without a license. The functionality is the same as in the licensed version, but the evaluation version has the limitations listed below.{{< /alert >}}

## Evaluation version limitations

The evaluation package is the same as the purchased one. It becomes licensed when you apply a license in your code. Without a license, GroupDocs.Assembly has the following limitations:

| Document | Spreadsheet | Presentation |
| --- | --- | --- |
| Reports are generated with full functionality, but an evaluation watermark is inserted at the top of the document. | The report contains an extra worksheet with an evaluation copyright warning. The worksheet cannot be hidden. | An evaluation watermark is inserted in the center of each slide. |
| The maximum document size is limited to several hundred paragraphs. | Only 100 spreadsheet reports can be generated per program run. After that, an exception is thrown. | |

To test GroupDocs.Assembly without these limitations, request a free 30-day [temporary license](https://purchase.groupdocs.com/temporary-license/). To buy a license, see the [pricing page](https://purchase.groupdocs.com/pricing/assembly/nodejs-java/).

## Licensing

The license file contains details such as the product name, the number of developers it is licensed to and the subscription expiry date. It is digitally signed, so do not modify it: even an extra line break invalidates it.

Set the license:

- Once per process, when the application starts. Calling `setLicense` again is not harmful, but wastes time.
- Before you use any other GroupDocs.Assembly classes.

### Apply a license from a file

```javascript
'use strict';

const groupdocs = require('@groupdocs/groupdocs.assembly');

const license = new groupdocs.License();
license.setLicense("GroupDocs.Assembly.lic");

console.log("License set successfully.");
```

### Apply a license from a stream

Use the `readDataFromStream` helper to convert a Node.js readable stream into a Java input stream:

```javascript
'use strict';

const fs = require('fs');
const groupdocs = require('@groupdocs/groupdocs.assembly');

const licenseStream = fs.createReadStream("GroupDocs.Assembly.lic");

groupdocs.readDataFromStream(licenseStream, (inputStream) => {
    const license = new groupdocs.License();
    license.setLicense(inputStream);

    console.log("License set successfully.");
});
```

### Apply a metered license

{{< alert style="info" >}}
A metered license is an alternative to a license file. You are billed based on your usage of the API. Metered licensing requires an Internet connection. For more details, see the [Metered Licensing FAQ](https://purchase.groupdocs.com/faqs/licensing/metered).
{{< /alert >}}

To use a metered license:

1. Create an instance of the `Metered` class.
2. Pass your public and private keys to the `setMeteredKey` method.
3. Process documents.
4. Call the static `Metered.getConsumptionQuantity` method to get the number of API requests consumed so far.
5. Call the static `Metered.getConsumptionCredit` method to get the credits consumed so far.

```javascript
'use strict';

const groupdocs = require('@groupdocs/groupdocs.assembly');

const publicKey = "*****";  // Your public key
const privateKey = "*****"; // Your private key

const metered = new groupdocs.Metered();
metered.setMeteredKey(publicKey, privateKey);

// ... assemble documents ...

console.log("Consumption quantity:", groupdocs.Metered.getConsumptionQuantity());
console.log("Consumption credit:", groupdocs.Metered.getConsumptionCredit());
```
