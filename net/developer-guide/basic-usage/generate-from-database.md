---
id: assembly-basic-usage-database-datasource
url: assembly/net/basic-usage-database-datasource
linktitle: Generate from Database
title: Generate Document from Database
weight: 9
description: "Create reports from database data using DataSet, DataTable, or IDataReader as data sources for templates."
keywords: database, DataSet, DataTable, ADO.NET, SQL, database binding, generate from database, assemble from database
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for .NET seamlessly integrates with ADO.NET, allowing you to generate documents directly from database queries. You can use DataSet, DataTable, DataView, or IDataReader as data sources, making it easy to create reports from SQL Server, Oracle, MySQL, and other databases.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) - wraps data sources
- ADO.NET classes: DataSet, DataTable, DataView, IDataReader

Here are the steps to generate documents from databases:

* Connect to your database using ADO.NET
* Execute SQL queries and populate DataSet or DataTable
* Create a template document with expression tags referencing table and column names
* Use DocumentAssembler to assemble the template with database data
* Save the assembled document

{{< alert style="info" >}}
GroupDocs.Assembly supports all standard ADO.NET data sources, including DataSet, DataTable, DataView, DataRow, DataRowView, IDataReader, and IDataRecord.
{{< /alert >}}

## Generate Document from DataTable

The simplest approach is to use a DataTable:

```csharp
using GroupDocs.Assembly;
using System.Data;
using System.Data.SqlClient;

public static void GenerateFromDataTable()
{
    // Connect to database and populate DataTable
    string connectionString = "Server=localhost;Database=MyDB;Integrated Security=true;";
    string query = "SELECT CustomerName, Email, Balance FROM Customers";
    
    DataTable customersTable = new DataTable();
    
    using (SqlConnection connection = new SqlConnection(connectionString))
    {
        using (SqlCommand command = new SqlCommand(query, connection))
        {
            using (SqlDataAdapter adapter = new SqlDataAdapter(command))
            {
                adapter.Fill(customersTable);
            }
        }
    }
    
    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx", 
        new DataSourceInfo(customersTable, "customers"));
    
    Console.WriteLine("Document generated from DataTable successfully.");
}
```

## Template Example for DataTable

In your template, reference columns by name:

```
Customers List:

<<foreach [in customers]>>
<<[CustomerName]>> - <<[Email]>> - Balance: <<[Balance]:"C">>
<</foreach>>
```

## Generate Document from DataSet

When working with multiple tables, use DataSet:

```csharp
using GroupDocs.Assembly;
using System.Data;
using System.Data.SqlClient;

public static void GenerateFromDataSet()
{
    string connectionString = "Server=localhost;Database=MyDB;Integrated Security=true;";
    
    DataSet dataSet = new DataSet();
    
    using (SqlConnection connection = new SqlConnection(connectionString))
    {
        // Load customers table
        using (SqlDataAdapter adapter = new SqlDataAdapter(
            "SELECT * FROM Customers", connection))
        {
            adapter.Fill(dataSet, "Customers");
        }
        
        // Load orders table
        using (SqlDataAdapter adapter = new SqlDataAdapter(
            "SELECT * FROM Orders", connection))
        {
            adapter.Fill(dataSet, "Orders");
        }
    }
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx", 
        new DataSourceInfo(dataSet, "ds"));
    
    Console.WriteLine("Document generated from DataSet successfully.");
}
```

## Template Example for DataSet

Reference tables by name in your template:

```
Customers:
<<foreach [in ds.Customers]>>
<<[CustomerName]>> - <<[Email]>>
<</foreach>>

Orders:
<<foreach [in ds.Orders]>>
Order #<<[OrderId]>> - Amount: <<[Amount]:"C">>
<</foreach>>
```

## Generate Document from IDataReader

For large datasets, use IDataReader for efficient streaming:

```csharp
using GroupDocs.Assembly;
using System.Data;
using System.Data.SqlClient;

public static void GenerateFromDataReader()
{
    string connectionString = "Server=localhost;Database=MyDB;Integrated Security=true;";
    string query = "SELECT CustomerName, Email, Balance FROM Customers";
    
    using (SqlConnection connection = new SqlConnection(connectionString))
    {
        connection.Open();
        
        using (SqlCommand command = new SqlCommand(query, connection))
        using (SqlDataReader reader = command.ExecuteReader())
        {
            DocumentAssembler assembler = new DocumentAssembler();
            assembler.AssembleDocument("Template.docx", "Output.docx", 
                new DataSourceInfo(reader, "customers"));
            
            Console.WriteLine("Document generated from DataReader successfully.");
        }
    }
}
```

## Using DataView for Filtered Data

You can use DataView to filter and sort data before assembly:

```csharp
using GroupDocs.Assembly;
using System.Data;
using System.Data.SqlClient;

public static void GenerateFromDataView()
{
    string connectionString = "Server=localhost;Database=MyDB;Integrated Security=true;";
    
    DataTable customersTable = new DataTable();
    
    using (SqlConnection connection = new SqlConnection(connectionString))
    {
        using (SqlDataAdapter adapter = new SqlDataAdapter(
            "SELECT * FROM Customers", connection))
        {
            adapter.Fill(customersTable);
        }
    }
    
    // Create filtered and sorted DataView
    DataView customersView = new DataView(customersTable);
    customersView.RowFilter = "Balance > 1000";
    customersView.Sort = "CustomerName ASC";
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx", 
        new DataSourceInfo(customersView, "customers"));
    
    Console.WriteLine("Document generated from DataView successfully.");
}
```

## Working with Related Tables

DataSet supports data relations for master-detail reports:

```csharp
using GroupDocs.Assembly;
using System.Data;
using System.Data.SqlClient;

public static void GenerateWithRelations()
{
    string connectionString = "Server=localhost;Database=MyDB;Integrated Security=true;";
    
    DataSet dataSet = new DataSet();
    
    using (SqlConnection connection = new SqlConnection(connectionString))
    {
        using (SqlDataAdapter adapter = new SqlDataAdapter(
            "SELECT * FROM Customers", connection))
        {
            adapter.Fill(dataSet, "Customers");
        }
        
        using (SqlDataAdapter adapter = new SqlDataAdapter(
            "SELECT * FROM Orders", connection))
        {
            adapter.Fill(dataSet, "Orders");
        }
    }
    
    // Create relation
    DataRelation relation = new DataRelation(
        "CustomerOrders",
        dataSet.Tables["Customers"].Columns["CustomerId"],
        dataSet.Tables["Orders"].Columns["CustomerId"]);
    dataSet.Relations.Add(relation);
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx", 
        new DataSourceInfo(dataSet.Tables["Customers"], "customers"));
    
    Console.WriteLine("Document generated with relations successfully.");
}
```

Template with relations:

```
<<foreach [in customers]>>
Customer: <<[CustomerName]>>
Orders:
<<foreach [in GetChildRows(\"CustomerOrders\")]>>
  - Order #<<[OrderId]>>: <<[Amount]:"C">>
<</foreach>>
<</foreach>>
```

{{< alert style="warning" >}}
When using database connections, always ensure proper disposal of resources. Use `using` statements or try-finally blocks to close connections and readers.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with complex database queries, stored procedures, parameterized queries, and performance optimization for large datasets, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

