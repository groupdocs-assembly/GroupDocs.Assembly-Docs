---
id: business-case-of-a-shopping-store
url: assembly/python-net/business-case-of-a-shopping-store
title: Business Case of a Shopping Store
weight: 1
description: "The shop behind the GroupDocs.Assembly for Python via .NET examples: its customers, products and orders, the reports it needs, and the shape of its data as Python dicts and lists."
keywords: business case, shopping store, customers, orders, products, dict, Python, GroupDocs.Assembly
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}This business case has been conceived for the demonstration purpose and serves well for a typical shopping store. There may be simpler or complex scenarios in real life businesses.{{< /alert >}}

The examples of this documentation report on Harbor Lane Provisions, a specialty-food wholesaler at 18 Quayside Road, Port Ellery. It sells coffee, cheese, oil, honey and biscuits to restaurants and cafés: Quayside Bistro, Lantern Street Café, Saltmarsh Deli and Pier Nine Kitchen.

## Business Case

1.  There are many customers of the shopping store.
2.  The store offers multiple products.
3.  A customer may place multiple orders.
4.  An order may have many products.
5.  The data may or may not be stored in a database system.

## Reporting Requirements

1.  A report based on some criteria is to be generated.
2.  The report can be in any of the formats: Documents, Spreadsheets, Presentations, emails, HTML and text.
3.  The report developer must be able to define templates and then generate reports.

## Business Objects

### Python Data

The .NET examples declare `Customer`, `Order`, `Product` and `Service` classes. In Python, the same objects are dicts and lists: a dict's keys are the members a template reads, and a list is a sequence a template iterates. One customer of the shop looks as follows (one of its three orders shown):

```json
{
  "CustomerName": "Quayside Bistro",
  "ShippingAddress": "3 Harbour Steps, Port Ellery",
  "CustomerContactNumber": "+1 555 0142 811",
  "Barcode": "20150114001",
  "Photo": "quayside-bistro.png",
  "Document": "outer-document.docx",
  "Color": "#2E8B7A",
  "Order": [
    {
      "OrderNumber": 10001,
      "Product": {
        "ProductName": "Harbor Blend whole bean coffee",
        "UnitInStock": 240,
        "Discount": 0,
        "ProductPrice": "$18.40"
      },
      "ProductQuantity": 30,
      "Price": 552,
      "OrderDate": "2015-01-14T00:00:00",
      "ShippingDate": "2015-01-15T00:00:00",
      "Barcode": "HLP-10001",
      "Services": [
        { "ServiceName": "Next-day delivery" },
        { "ServiceName": "Menu pairing advice" }
      ]
    }
  ]
}
```

A template reads it as it reads the C# objects: `<<[customer.CustomerName]>>`, `<<foreach [o in customer.Order]>><<[o.Product.ProductName]>><</foreach>>`. The order dates are strings in JSON; the examples whose templates read a date turn them into `datetime` objects while loading the file. [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}) describes every data file and how the examples load it.

### Database Entities

The .NET examples also read the customers, orders and products from an SQL database. A Python application reads such rows with its database driver and passes them as dicts, one per row, as shown in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).

## Templates Location

Each example reads its template from the folder it runs in, by the template's file name. The tabs beside each example link the template and the data files it reads, so you can download them into one folder and run the example there. In your own application, keep the templates wherever suits you, and organize them in sub-folders as you see fit.

## Reports Location

Each example writes its report into the folder it runs in, under a name derived from the template's (`in-table-list-report.docx` for `in-table-list.docx`). In your own application, pass any path, or a stream, as the report.
