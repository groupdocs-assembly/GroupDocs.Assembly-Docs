---
id: enumeration-extension-methods
url: assembly/net/enumeration-extension-methods
title: Enumeration Extension Methods
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for .NET
hideChildren: False
---
LINQ Reporting Engine enables you to perform common manipulations on a sequential data through the engine's built-in extension methods for `IEnumerable`. These extension methods mimic some extension methods of [IEnumerable&lt;T&gt;](http://msdn.microsoft.com/en-us/library/9eekhta0\(v=vs.110\).aspx) providing the same signatures and behavior features. Thus you can group, sort and perform other sequential data manipulations in template expressions in a familiar way.

The following table describes these built-in extension methods. The following notation conventions are used within the table:

- `Selector` stands for a lambda function returning a value and taking an enumeration item as its single argument. See “Using Lambda Functions” for more information.
- `ComparableSelector` stands for `Selector` returning [IComparable](http://msdn.microsoft.com/en-US/library/system.icomparable\(v=vs.110\).aspx).
- `EnumerationSelector` stands for `Selector` returning `IEnumerable`.
- `Predicate` stands for `Selector` returning a Boolean value.

Examples in the following table are given using persons and `otherPersons`, enumerations of instances of the `Person` class that is defined as follows.

{{< highlight csharp >}}
public class Person
{
    public String Name { get { ... } }
    public int Age { get { ... } }
    public IEnumerable<Person> Children { get { ... } }
    ...
}
{{< /highlight >}}

|Extension Method |Examples and Notes |
| :- | :- |
|All(Predicate)|{{< highlight csharp >}}
persons.All(p => p.Age < 50){{< /highlight >}}|
|Any()|{{< highlight csharp >}}
persons.Any(){{< /highlight >}}|
|Any(Predicate)|{{< highlight csharp >}}
persons.Any(p => p.Name == "John Smith"){{< /highlight >}}|
|Average(Selector)|{{< highlight csharp >}}
persons.Average(p => p.Age){{< /highlight >}}The input selector must return a value of any type that has predefined or user-defined addition and division operators. |
|Concat(IEnumerable)|{{< highlight csharp >}}
persons.Concat(otherPersons){{< /highlight >}}An implicit reference conversion must exist between types of items of concatenated enumerations. |
|Contains(Object)|{{< highlight csharp >}}
persons.Contains(otherPersons.First()){{< /highlight >}}|
|Count()|{{< highlight csharp >}}
persons.Count(){{< /highlight >}}|
|Count(Predicate)|{{< highlight csharp >}}
persons.Count(p => p.Age > 30){{< /highlight >}}|
|Distinct()|{{< highlight csharp >}}
persons.Distinct(){{< /highlight >}}Items are compared as described in [Comparing Keys of GroupBy and Distinct](#comparing-keys-of-groupby-and-distinct). |
|First()|{{< highlight csharp >}}
persons.First(){{< /highlight >}}|
|First(Predicate)|{{< highlight csharp >}}
persons.First(p => p.Age > 30){{< /highlight >}}|
|FirstOrDefault()|{{< highlight csharp >}}
persons.FirstOrDefault(){{< /highlight >}}|
|FirstOrDefault(Predicate)|{{< highlight csharp >}}
persons.FirstOrDefault(p => p.Age > 30){{< /highlight >}}|
|GroupBy(Selector)|{{< highlight csharp >}}
persons.GroupBy(p => p.Age){{< /highlight >}}Or {{< highlight csharp >}}
persons.GroupBy(    p => new { Age = p.Age, Count = p.Children.Count() }){{< /highlight >}}This method returns an enumeration of group objects. Each group has a unique key defined by the input selector and contains items of the source enumeration associated with this key. You can access the key of a group instance using the Key property. You can treat a group itself as an enumeration of items that the group contains. Keys are compared as described in [Comparing Keys of GroupBy and Distinct](#comparing-keys-of-groupby-and-distinct). |
|Last()|{{< highlight csharp >}}
persons.Last(){{< /highlight >}}|
|Last(Predicate)|{{< highlight csharp >}}
persons.Last(p => p.Age > 100){{< /highlight >}}|
|LastOrDefault()|{{< highlight csharp >}}
persons.LastOrDefault(){{< /highlight >}}|
|LastOrDefault(Predicate)|{{< highlight csharp >}}
persons.LastOrDefault(p => p.Age > 100){{< /highlight >}}|
|Max(ComparableSelector)|{{< highlight csharp >}}
persons.Max(p => p.Age){{< /highlight >}}|
|Min(ComparableSelector)|{{< highlight csharp >}}
persons.Min(p => p.Age){{< /highlight >}}|
|OrderBy(ComparableSelector)|{{< highlight csharp >}}
persons.OrderBy(p => p.Age){{< /highlight >}}Or {{< highlight csharp >}}
persons.OrderBy(p => p.Age).ThenByDescending(p => p.Name){{< /highlight >}}Or {{< highlight csharp >}}
persons.OrderBy(p => p.Age).ThenByDescending(p => p.Name).ThenBy(p => p.Children.Count()){{< /highlight >}}This method returns an enumeration ordered by a single key. To specify additional ordering keys, you can use the following extension methods of an ordered enumeration:- ThenBy(ComparableSelector)- ThenByDescending(ComparableSelector)|
|OrderByDescending(ComparableSelector)|{{< highlight csharp >}}
persons.OrderByDescending(p => p.Age){{< /highlight >}}Or {{< highlight csharp >}}
persons.OrderByDescending(p => p.Age).ThenByDescending(p => p.Name){{< /highlight >}}Or {{< highlight csharp >}}
persons.OrderByDescending(p => p.Age).ThenByDescending(p => p.Name).ThenBy(p => p.Children.Count()){{< /highlight >}}See the previous note. |
|Select(Selector)|{{< highlight csharp >}}
persons.Select(p => p.Name){{< /highlight >}}|
|SelectMany(EnumerationSelector)|{{< highlight csharp >}}
persons.SelectMany(p => p.Children){{< /highlight >}}|
|Single()|{{< highlight csharp >}}
persons.Single(){{< /highlight >}}|
|Single(Predicate)|{{< highlight csharp >}}
persons.Single(p => p.Name == "John Smith"){{< /highlight >}}|
|SingleOrDefault()|{{< highlight csharp >}}
persons.SingleOrDefault(){{< /highlight >}}|
|SingleOrDefault(Predicate)|{{< highlight csharp >}}
persons.SingleOrDefault(p => p.Name == "John Smith"){{< /highlight >}}|
|Skip(int)|{{< highlight csharp >}}
persons.Skip(10){{< /highlight >}}|
|SkipWhile(Predicate)|{{< highlight csharp >}}
persons.SkipWhile(p => p.Age < 21){{< /highlight >}}|
|Sum(Selector)|{{< highlight csharp >}}
persons.Sum(p => p.Children.Count()){{< /highlight >}}The input selector must return a value of any type that has a predefined or user-defined addition operator. |
|Take(int)|{{< highlight csharp >}}
persons.Take(5){{< /highlight >}}|
|TakeWhile(Predicate)|{{< highlight csharp >}}
persons.TakeWhile(p => p.Age < 50){{< /highlight >}}|
|Union(IEnumerable)|{{< highlight csharp >}}
persons.Union(otherPersons){{< /highlight >}}An implicit reference conversion must exist between types of items of united enumerations. |
|Where(Predicate)|{{< highlight csharp >}}
persons.Where(p => p.Age > 18){{< /highlight >}}|

## Predicates over Nullable Boolean Values

{{< alert style="info" >}}This feature is supported by version 26.11 or greater.{{< /alert >}}

Boolean values of JSON, XML and CSV data, and `bool?` members of your own classes, are nullable because the value may be missing. Such values can be returned by a `Predicate` directly, without `== true`. A missing value counts as false.

Suppose we have JSON data like:

```json
[
  { "Title": "Order beans", "Done": true },
  { "Title": "Clean grinder", "Done": false },
  { "Title": "Call supplier", "Done": null }
]
```

If we use the template like following:

```
Done: <<[tasks.Count(t => t.Done)]>> of <<[tasks.Count()]>>
Not done: <<foreach [t in tasks.Where(t => t.Done != true)]>><<[t.Title]>>; <</foreach>>
All done: <<[tasks.All(t => t.Done)]>>
```

The result will be like:

```
Done: 1 of 3
Not done: Clean grinder; Call supplier; 
All done: False
```

{{< alert style="warning" >}}A negation of a missing value is missing as well, so `tasks.Where(t => !t.Done)` returns the tasks with `false` only. To include missing values, compare with `true`: `t.Done != true`.{{< /alert >}}

## Comparing Keys of GroupBy and Distinct

{{< alert style="info" >}}This feature is supported by version 26.11 or greater.{{< /alert >}}

`GroupBy` and `Distinct` compare keys and items depending on where they come from:

- **Nested objects of JSON and XML data** are compared by value, including their own nested objects: `{"Name":"A"}` and `{"Name":"A"}` make one group. Objects of JSON data with different `$id` values are different objects, even if their values are equal.
- **Rows of a `DataSet` of your own** are compared by identity: orders of the same customer row make one group, while two customer rows with equal values stay two groups.
- **Objects of your own classes** are compared as .NET does it, using their `Equals` and `GetHashCode` methods.

To group by a value rather than by an object, use a simple key, such as `GroupBy(o => o.Customer.Name)`.

For example, orders 1 and 3 below hold equal customer objects:

```json
{ "Orders": [
  { "Number": 1, "Paid": true,  "Customer": { "Name": "Quayside Bistro" } },
  { "Number": 2, "Paid": false, "Customer": { "Name": "Harbor Lane Provisions" } },
  { "Number": 3, "Paid": null,  "Customer": { "Name": "Quayside Bistro" } } ] }
```

The following template:

```
<<foreach [g in ds.Orders.GroupBy(o => o.Customer)]>><<[g.Key.Name]>>: <<[g.Count()]>> order(s), paid: <<[g.Count(o => o.Paid)]>>
<<foreach [o in g]>>  #<<[o.Number]>> <<[o.Paid ? "paid" : "due"]>>
<</foreach>><</foreach>>
```

```csharp
JsonDataLoadOptions options = new JsonDataLoadOptions();
options.AlwaysGenerateRootObject = true;

new DocumentAssembler().AssembleDocument("orders.txt", "report.txt",
    new DataSourceInfo(new JsonDataSource("orders.json", options), "ds"));
```

gives one group per customer:

```
Quayside Bistro: 2 order(s), paid: 1
  #1 paid
  #3 due
Harbor Lane Provisions: 1 order(s), paid: 0
  #2 due
```

Example: [UseFileDataLikeTypedObjects.cs](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/GroupDocs.Assembly.Examples.CSharp/AdvancedUsage/UseFileDataLikeTypedObjects.cs).