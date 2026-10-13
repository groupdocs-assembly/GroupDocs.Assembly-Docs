---
id: assembly-basic-usage-database-datasource-java
url: assembly/java/basic-usage-database-datasource
linktitle: Generate from Database
title: Generate Document from Database
weight: 9
description: "Create reports from database data using DataSet and DataTable populated through JDBC as data sources for templates."
keywords: database, DataSet, DataTable, JDBC, ResultSet, SQL, database binding, generate from database, assemble from database
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java seamlessly integrates with JDBC, allowing you to generate documents directly from database queries. You can wrap a `java.sql.ResultSet` into a `DataTable`, or combine several tables into a `DataSet`, making it easy to create reports from MySQL, PostgreSQL, SQL Server, Oracle, SQLite, and other databases. Any JDBC driver can be used.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/datasourceinfo/) - wraps data sources
- [DataTable](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly.system.data/datatable/), [DataSet](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly.system.data/dataset/), and [DataRelation](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly.system.data/datarelation/) - hold the data loaded from JDBC
- JDBC classes: Connection, Statement, ResultSet

Here are the steps to generate documents from databases:

* Connect to your database using JDBC
* Execute SQL queries and populate DataSet or DataTable
* Create a template document with expression tags referencing table and column names
* Use DocumentAssembler to assemble the template with database data
* Save the assembled document

{{< alert style="info" >}}
GroupDocs.Assembly supports `DataSet`, `DataTable`, and `DataRow` objects from the `com.groupdocs.assembly.system.data` package as data sources. A `DataTable` reads all rows of the `ResultSet` when it is created, so the database connection can be closed before the document is assembled.
{{< /alert >}}

## Generate Document from DataTable

The simplest approach is to use a DataTable:

```java
import com.groupdocs.assembly.*;
import com.groupdocs.assembly.system.data.*;
import java.sql.*;

public static void generateFromDataTable() throws Exception
{
    // Connect to database and populate DataTable
    // Any JDBC URL works, e.g. "jdbc:mysql://localhost:3306/MyDB" (the JDBC driver must be on the classpath)
    String connectionString = "jdbc:sqlite:MyDB.db";
    String query = "SELECT CustomerName, Email, Balance FROM Customers";

    DataTable customersTable;

    try (Connection connection = DriverManager.getConnection(connectionString);
         Statement statement = connection.createStatement();
         ResultSet resultSet = statement.executeQuery(query))
    {
        customersTable = new DataTable(resultSet, "Customers");
    }

    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(customersTable, "customers"));

    System.out.println("Document generated from DataTable successfully.");
}
```

## Template Example for DataTable

In your template, reference columns by name:

```
Customers List:

<<foreach [in customers]>>
<<[CustomerName]>> - <<[Email]>> - Balance: <<[Balance]:"$#,##0.00">>
<</foreach>>
```

{{< alert style="info" >}}
Numeric format strings follow the Java `DecimalFormat` pattern syntax (for example, `"$#,##0.00"`); .NET standard format strings such as `"C"` are not supported. Decimal and grouping separators depend on the default locale of the JVM.
{{< /alert >}}

## Generate Document from DataSet

When working with multiple tables, use DataSet:

```java
import com.groupdocs.assembly.*;
import com.groupdocs.assembly.system.data.*;
import java.sql.*;

public static void generateFromDataSet() throws Exception
{
    String connectionString = "jdbc:sqlite:MyDB.db";

    DataSet dataSet = new DataSet();

    try (Connection connection = DriverManager.getConnection(connectionString);
         Statement statement = connection.createStatement())
    {
        // Load customers table
        try (ResultSet resultSet = statement.executeQuery("SELECT * FROM Customers"))
        {
            dataSet.getTables().add(new DataTable(resultSet, "Customers"));
        }

        // Load orders table
        try (ResultSet resultSet = statement.executeQuery("SELECT * FROM Orders"))
        {
            dataSet.getTables().add(new DataTable(resultSet, "Orders"));
        }
    }

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(dataSet, "ds"));

    System.out.println("Document generated from DataSet successfully.");
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
Order #<<[OrderId]>> - Amount: <<[Amount]:"$#,##0.00">>
<</foreach>>
```

## Generate Document from an Entire Database

Instead of querying tables one by one, you can pass a JDBC `Connection` to the `DataSet` constructor. It loads all tables of the database (or of the specified schema) together with their primary keys and the relations defined by foreign keys:

```java
import com.groupdocs.assembly.*;
import com.groupdocs.assembly.system.data.*;
import java.sql.*;

public static void generateFromConnection() throws Exception
{
    String connectionString = "jdbc:sqlite:MyDB.db";

    DataSet dataSet;

    try (Connection connection = DriverManager.getConnection(connectionString))
    {
        dataSet = new DataSet(connection);
        // Or, to load tables of a specific schema:
        // dataSet = new DataSet(connection, "PUBLIC");
    }

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(dataSet, "ds"));

    System.out.println("Document generated from the database successfully.");
}
```

## Filtering and Sorting Data

You can filter and sort data in the SQL query before assembly:

```java
import com.groupdocs.assembly.*;
import com.groupdocs.assembly.system.data.*;
import java.sql.*;

public static void generateFromFilteredData() throws Exception
{
    String connectionString = "jdbc:sqlite:MyDB.db";

    DataTable customersTable;

    try (Connection connection = DriverManager.getConnection(connectionString);
         PreparedStatement statement = connection.prepareStatement(
             "SELECT * FROM Customers WHERE Balance > ? ORDER BY CustomerName ASC"))
    {
        statement.setDouble(1, 1000);

        try (ResultSet resultSet = statement.executeQuery())
        {
            customersTable = new DataTable(resultSet, "Customers");
        }
    }

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(customersTable, "customers"));

    System.out.println("Document generated from filtered data successfully.");
}
```

## Working with Related Tables

DataSet supports data relations for master-detail reports:

```java
import com.groupdocs.assembly.*;
import com.groupdocs.assembly.system.data.*;
import java.sql.*;

public static void generateWithRelations() throws Exception
{
    String connectionString = "jdbc:sqlite:MyDB.db";

    DataSet dataSet = new DataSet();

    try (Connection connection = DriverManager.getConnection(connectionString);
         Statement statement = connection.createStatement())
    {
        try (ResultSet resultSet = statement.executeQuery("SELECT * FROM Customers"))
        {
            dataSet.getTables().add(new DataTable(resultSet, "Customers"));
        }

        try (ResultSet resultSet = statement.executeQuery("SELECT * FROM Orders"))
        {
            dataSet.getTables().add(new DataTable(resultSet, "Orders"));
        }
    }

    // Create relation
    DataRelation relation = new DataRelation(
        "CustomerOrders",
        dataSet.getTables().get("Customers").getColumns().get("CustomerId"),
        dataSet.getTables().get("Orders").getColumns().get("CustomerId"));
    dataSet.getRelations().add(relation);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(dataSet.getTables().get("Customers"), "customers"));

    System.out.println("Document generated with relations successfully.");
}
```

Template with relations (child rows are accessed by the name of the child table):

```
<<foreach [in customers]>>
Customer: <<[CustomerName]>>
Orders:
<<foreach [in Orders]>>
  - Order #<<[OrderId]>>: <<[Amount]:"$#,##0.00">>
<</foreach>>
<</foreach>>
```

{{< alert style="warning" >}}
When using database connections, always ensure proper disposal of resources. Use try-with-resources statements or try-finally blocks to close connections, statements, and result sets.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with complex database queries, stored procedures, parameterized queries, and performance optimization for large datasets, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
