---
id: changing-background-color-dynamically
url: assembly/net/changing-background-color-dynamically
title: Changing Background Color Dynamically
weight: 36
description: ""
keywords: 
productName: GroupDocs.Assembly for .NET
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 17.12 or greater{{< /alert >}}

You can set text background color for document contents dynamically using backColor tags.

### The Code

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/net/the-business-layer/){{< /alert >}}{{< gist GroupDocsGists ee5d086fa3fa545f0b9f78647054674b >}}

### Color Values

A color expression of a backColor tag must return a value of one of the following types:

*   A string containing the name of a known color, that is, the case-insensitive name of a member of the [KnownColor](https://msdn.microsoft.com/en-us/library/system.drawing.knowncolor(v=vs.110).aspx) enumeration such as "red"
*   A string containing a hex value: "#RRGGBB", "#RGB" or "#AARRGGBB", such as "#FF0000" (red)
*   An integer value defining RGB (red, green, blue) components of the color such as 0xFFFF00 (yellow)
*   A value of the [Color](http://msdn.microsoft.com/en-us/library/system.drawing.color(v=vs.110).aspx) type

{{< alert style="info" >}}Hex strings are supported by version 26.11 or greater. Before, they gave no color.{{< /alert >}}

In the following example, the colors come from data as hex strings and a color name:

```
<<foreach [s in statuses]>><<backColor [s.Color]>><<[s.Name]>><</backColor>>
<</foreach>>
```

```csharp
public class OrderStatus
{
    public string Name { get; set; }
    public string Color { get; set; }
}

OrderStatus[] statuses =
{
    new OrderStatus { Name = "Paid", Color = "#C6EFCE" },
    new OrderStatus { Name = "Pending", Color = "#FFEB9C" },
    new OrderStatus { Name = "Overdue", Color = "#F00" },
    new OrderStatus { Name = "Cancelled", Color = "LightGray" },
};

new DocumentAssembler().AssembleDocument("Hex color.docx", "output.docx",
    new DataSourceInfo(statuses, "statuses"));
```

The four lines get the backgrounds `C6EFCE`, `FFEB9C`, `FF0000` and `D3D3D3`. Example: [SetBackColorFromHexString.cs](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/GroupDocs.Assembly.Examples.CSharp/AdvancedUsage/SetBackColorFromHexString.cs).

### Download

*   [Change Background Color Dynamically.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Source/Word%20Templates/In-Table%20List%20with%20Running%20(Progressive)%20Total_BackgroundColor.docx)
