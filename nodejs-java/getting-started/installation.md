---
id: installation
url: assembly/nodejs-java/installation
title: Installation
weight: 4
description: "Install GroupDocs.Assembly for Node.js via Java from npm, set up Java, verify the installation and troubleshoot common problems."
keywords: installation, npm, node.js, java, groupdocs assembly
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---

## Prerequisites

- Node.js 20 LTS or later
- JDK 8 or later (17 LTS recommended) with `JAVA_HOME` set
- Native build tools for node-gyp

See [System Requirements](/assembly/nodejs-java/system-requirements/) for details.

## Install from npm

GroupDocs.Assembly for Node.js via Java is published on npm as [@groupdocs/groupdocs.assembly](https://www.npmjs.com/package/@groupdocs/groupdocs.assembly). Install it into your project:

```bash
npm install @groupdocs/groupdocs.assembly
```

During installation npm:

1. Builds the [java](https://www.npmjs.com/package/java) bridge package, which lets Node.js call the Java API.
2. Runs the package's `postinstall` script, which downloads the GroupDocs.Assembly JAR file (`groupdocs-assembly-nodejs-<version>.jar`) into `node_modules/@groupdocs/groupdocs.assembly/lib/`.

## Verify installation

Create a file named `check.js`:

```javascript
'use strict';

const groupdocs = require('@groupdocs/groupdocs.assembly');

const assembler = new groupdocs.DocumentAssembler();
console.log('GroupDocs.Assembly loaded:', assembler !== undefined);

process.exit(0);
```

Run it:

```bash
node check.js
```

{{< alert style="info" >}}
GroupDocs.Assembly runs inside a Java virtual machine started by the `java` bridge, and the JVM keeps the Node.js process alive after your code finishes. Call `process.exit()` at the end of standalone scripts.
{{< /alert >}}

## Download the JAR file manually

If the `postinstall` step cannot download the JAR file (for example, behind a corporate proxy), the package prints a warning when you load it. Download the file again from the package folder:

```bash
cd node_modules/@groupdocs/groupdocs.assembly
npm run postinstall
```

Or download `groupdocs-assembly-nodejs-<version>.jar` from `https://releases.groupdocs.com/java/repo/com/groupdocs/groupdocs-assembly-nodejs/<version>/` and place it in `node_modules/@groupdocs/groupdocs.assembly/lib/`.

## Troubleshooting

- **node-gyp build errors**: install the build tools listed in [System Requirements](/assembly/nodejs-java/system-requirements/#build-tools), restart the terminal and run `npm install` again.
- **`jni.h` not found**: a JRE is installed instead of a JDK, or `JAVA_HOME` points to the wrong folder.
- **Java not found at runtime**: set `JAVA_HOME` and add `JAVA_HOME/bin` to `PATH`.
- **The script does not exit**: add `process.exit()` at the end of the script.
- **`Can not resolve method` on Java 16 or later**: call `require('java').options.push('--add-opens=java.base/java.lang=ALL-UNNAMED')` before requiring `@groupdocs/groupdocs.assembly`. See [System Requirements](/assembly/nodejs-java/system-requirements/#java).
- **Permission errors when writing reports**: make sure the process can write to the output folder.
