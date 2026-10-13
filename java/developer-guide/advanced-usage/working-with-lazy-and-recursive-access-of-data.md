---
id: working-with-lazy-and-recursive-access-of-data
url: assembly/java/working-with-lazy-and-recursive-access-of-data
title: Working with Lazy And Recursive Access of Data
weight: 26
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by GroupDocs.Assembly for Java 26.10 or greater.{{< /alert >}}

## Purpose

At some point, you may want to generate a report over an object graph whose shape is not known in advance, fetching its data lazily (only when a template actually requests it) and recursively (following related and child entities) using GroupDocs.Assembly for Java. This is quite possible to accomplish using custom types.

A template reads a property of such an entity with indexer syntax, for example `root["Name"]`: the engine resolves an indexer on a Java type through its public `get(String)` method. Related and child entities are exposed as public fields (`Entities` and `Children` in the example below), whose types in turn provide `get(String)` methods returning a single entity or an `Iterable` of entities.

## Creating Template

![](https://raw.githubusercontent.com/atirtahirgroupdocs/GroupDocs_Assembly_NET/master/Examples/Data/Screenshots/template.PNG)

The template uses the following expressions: `root["Name"]` to read a property of the root entity, `root.Entities["Account"]["Login"]` to read a property of a related entity, and `<<foreach [child in root.Children["Children"]]>>` to iterate over child entities.

## Download Template

Get template from here.

*   [Lazy and recursive.docx](https://github.com/atirtahirgroupdocs/GroupDocs_Assembly_NET/blob/master/Examples/Data/Source/Word%20Templates/Lazy%20And%20Recursive.docx?raw=true)

## Generating The Report

```java
import com.groupdocs.assembly.*;
import java.util.UUID;

public static void lazilyAndRecursively() throws Exception
{
    DynamicEntity entity = new DynamicEntity(UUID.randomUUID());

    DocumentAssembler assembler = new DocumentAssembler();

    assembler.assembleDocument("Lazy and Recursive.docx", "Lazy and Recursive Out.docx",
        new DataSourceInfo(entity, "root"));
}
```

The `DynamicEntity` class used above is defined as follows:

```java
import java.util.Arrays;
import java.util.UUID;

/**
 * An entity whose properties are fetched by name rather than declared, so a report can be generated
 * lazily and recursively over an object graph of unknown shape.
 */
public class DynamicEntity
{
    /**
     * Provides access to individual related entities by their names.
     */
    public final ReferencedEntities Entities;

    /**
     * Provides access to enumerations of related entities by their names.
     */
    public final ChildEntities Children;

    private final UUID mId;

    public DynamicEntity(UUID id)
    {
        // In this example we use UUID to represent an entity identifier. In a real-life application
        // the identifier can be of any type or even missing.
        mId = id;

        // In this example we simply initialize the fields in the constructor. In a real-life
        // application the lookups below can fetch their data lazily, when they are first called.
        Entities = new ReferencedEntities(this);
        Children = new ChildEntities(this);
    }

    /**
     * Gets a property value by its name.
     */
    public String get(String propertyName)
    {
        // In this example we simply return a property name as its value. In a real-life application
        // a real property value should be returned. This value can be cached using for example a
        // Map, or fetched every time the property is requested.
        return propertyName + " Value";
    }

    public static class ReferencedEntities
    {
        private final DynamicEntity mRootEntity;

        ReferencedEntities(DynamicEntity rootEntity)
        {
            // The reference to the root entity allows to access fields of the root entity (such as
            // an identifier) in the lookup below for a real-life application.
            mRootEntity = rootEntity;
        }

        public DynamicEntity get(String propertyName)
        {
            // In this example we simply return the root entity. In a real-life application an entity
            // corresponding to propertyName for the given root entity should be returned.
            return mRootEntity;
        }
    }

    public static class ChildEntities
    {
        private final DynamicEntity mRootEntity;

        ChildEntities(DynamicEntity rootEntity)
        {
            mRootEntity = rootEntity;
        }

        public Iterable<DynamicEntity> get(String propertyName)
        {
            // In this example we simply return the root entity three times. In a real-life application
            // the entities corresponding to propertyName for the given root entity should be returned.
            return Arrays.asList(mRootEntity, mRootEntity, mRootEntity);
        }
    }
}
```
