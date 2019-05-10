---
title: 'SDK de extensión de Java: extensiones de lenguaje de SQL Server'
description: Descripción de la extensibilidad de Microsoft SDK para Java para Microsoft SQL Server de 2019
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c244d67c7f1cd1636fcd2de0b80454c96927b5d7
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65101818"
---
# <a name="microsoft-extensibility-sdk-for-java-for-sql-server"></a>Extensibilidad de Microsoft SDK para Java para SQL Server

En SQL Server CTP 2.5, puede implementar un programa Java para SQL Server con la extensibilidad de Microsoft SDK para Java. Se trata de una interfaz para la extensión del lenguaje Java que se usa para intercambiar datos con SQL Server y para ejecutar código de Java desde SQL Server.

> [!Note]
> El SDK de CTP 2.5 es un importante cambio en las versiones de CTP anteriores. Todas las muestras tenía trabajo deberá actualizarse para usar el SDK en su lugar.

Descargue el [extensibilidad de Microsoft SDK para Java para Microsoft SQL Server](http://aka.ms/mssql-java-lang-extension).

## <a name="implementation-requirements"></a>Requisitos de implementación

La interfaz SDK define un conjunto de requisitos que deben cumplirse para que SQL Server para comunicarse con el tiempo de ejecución de Java. Esto significa que debe seguir algunas reglas de implementación de la clase principal. SQL Server, a continuación, puede ejecutar un método específico en los datos de exchange y de clase de Java mediante la extensión del lenguaje Java.

Para obtener un ejemplo de cómo puede usar el SDK, consulte el [-to-end ejemplo](java-first-sample.md).

## <a name="sdk-classes"></a>Clases del SDK

Este SDK se compone de tres clases.

Dos clases abstractas que definen la interfaz de la extensión de Java se usa para intercambiar datos con SQL Server:

- **AbstractSqlServerExtensionExecutor**
- **AbstractSqlServerExtensionDataset**

La tercera clase es una clase auxiliar que contiene una implementación de un objeto de conjunto de datos. Se trata de una clase opcional para que resulte más fácil empezar a trabajar. Puede usar su propia implementación de dicha clase.

- **PrimitiveDataset**

A continuación ofrece información y código fuente para cada clase de la extensión del lenguaje Java para SQL Server.

## <a name="abstractsqlserverextensionexecutor"></a>AbstractSqlServerExtensionExecutor

Se trata de una clase abstracta que contiene la interfaz utilizada para ejecutar el código de Java por la extensión del lenguaje Java para SQL Server.

La clase principal de Java debe heredar de esta clase. Heredar de esta clase significa que hay ciertos métodos en la clase que debe implementar en su propia clase.

Para heredar de esta clase abstracta, ampliar con el nombre de clase abstracta en la declaración de clase:

```java
public class <MyClass> extends AbstractSqlServerExtensionExecutor {}
```

Como mínimo, debe implementar el método execute(...) la clase principal.

### <a name="method-execute"></a>Método execute

El método execute es el método que se llama desde SQL Server a través de la extensión del lenguaje Java, para llamar a código de Java desde SQL Server. Es recomendable que vea esto como un método clave que se incluyan las principales operaciones que desea ejecutar desde SQL Server.

Para pasar argumentos de método a Java desde SQL Server, use el `@param` parámetro en sp_execute_external_script. El método **ejecutar** toma sus argumentos de este modo.

```java
public AbstractSqlServerExtensionDataset execute(AbstractSqlServerExtensionDataset input, LinkedHashMap<String, Object> params)  {}
```

### <a name="method-init"></a>Método init

El método init se ejecuta después del constructor y antes del método execute. Las operaciones que deben realizarse antes de execute(...) pueden realizarse en este método.

```java
public void init(String sessionId, int taskId, int numtask) {}
```

### <a name="abstractsqlserverextensionexecutor-source-code"></a>Código fuente de AbstractSqlServerExtensionExecutor

Encontrará más detalles a continuación, en el código fuente:

```java
package com.microsoft.sqlserver.javalangextension;

import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionDataset;
import java.lang.UnsupportedOperationException;
import java.util.LinkedHashMap;

/**
 * Abstract class containing interface used by the Java extension
 */
public abstract class AbstractSqlServerExtensionExecutor {
    /* Supported versions of the Java extension */
    public final int SQLSERVER_JAVA_LANG_EXTENSION_V1 = 1;

    /* Members used by the extension to determine application specifics */
    protected int executorExtensionVersion;
    protected String executorInputDatasetClassName;
    protected String executorOutputDatasetClassName;

    public AbstractSqlServerExtensionExecutor() { }

    public void init(String sessionId, int taskId, int numTasks) {
        /* Default implementation of init() is no-op */
    }

    public AbstractSqlServerExtensionDataset execute(AbstractSqlServerExtensionDataset input, LinkedHashMap<String, Object> params) {
        throw new UnsupportedOperationException("AbstractSqlServerExtensionExecutor execute() is not implemented");
    }

    public void cleanup() {
        /* Default implementation of cleanup() is no-op */
    }
}
```

### <a name="abstractsqlserverextensiondataset"></a>AbstractSqlServerExtensionDataset

Clase abstracta que contiene la interfaz para controlar los datos de entrada y salidas utilizados por la extensión de Java.

```java
package com.microsoft.sqlserver.javalangextension;

import java.lang.UnsupportedOperationException;

/**
 * Abstract class containing interface for handling input and output data used by the Java
 * extension.
 */
public class AbstractSqlServerExtensionDataset {
    /**
     * Column metadata interfaces
     */
    public void addColumnMetadata(int columnId, String columnName, int columnType, int precision, int scale) {
        throw new UnsupportedOperationException("addColumnMetadata is not implemented");
    }

    public int getColumnCount() {
        throw new UnsupportedOperationException("getColumnCount is not implemented");
    }

    public String getColumnName(int columnId) {
        throw new UnsupportedOperationException("getColumnName is not implemented");
    }

    public int getColumnPrecision(int columnId) {
        throw new UnsupportedOperationException("getColumnPrecision is not implemented");
    }

    public int getColumnScale(int columnId) {
        throw new UnsupportedOperationException("getColumnScale is not implemented");
    }

    public int getColumnType(int columnId) {
        throw new UnsupportedOperationException("getColumnNullMap is not implemented");
    }

    public boolean[] getColumnNullMap(int columnId) {
        throw new UnsupportedOperationException("getColumnNullMap is not implemented");
    }

    /**
     * Adding column interfaces
     */
    public void addIntColumn(int columnId, int[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addIntColumn is not implemented");
    }

    public void addBooleanColumn(int columnId, boolean[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addBooleanColumn is not implemented");
    }

    public void addLongColumn(int columnId, long[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addLongColumn is not implemented");
    }

    public void addFloatColumn(int columnId, float[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addFloatColumn is not implemented");
    }

    public void addDoubleColumn(int columnId, double[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addDoubleColumn is not implemented");
    }

    public void addShortColumn(int columnId, short[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addShortColumn is not implemented");
    }

    public void addStringColumn(int columnId, String[] rows) {
        throw new UnsupportedOperationException("addStringColumn is not implemented");
    }

    public void addBinaryColumn(int columnId, byte[][] rows) {
        throw new UnsupportedOperationException("addBinaryColumn is not implemented");
    }

    /**
     * Retrieving column interfaces
     */
    public int[] getIntColumn(int columnId) {
        throw new UnsupportedOperationException("getIntColumn is not implemented");
    }

    public long[] getLongColumn(int columnId) {
        throw new UnsupportedOperationException("getLongColumn is not implemented");
    }

    public float[] getFloatColumn(int columnId) {
        throw new UnsupportedOperationException("getFloatColumn is not implemented");
    }

    public short[] getShortColumn(int columnId) {
        throw new UnsupportedOperationException("getShortColumn is not implemented");
    }

    public boolean[] getBooleanColumn(int columnId) {
        throw new UnsupportedOperationException("getBooleanColumn is not implemented");
    }

    public double[] getDoubleColumn(int columnId) {
        throw new UnsupportedOperationException("getDoubleColumn is not implemented");
    }

    public String[] getStringColumn(int columnId) {
        throw new UnsupportedOperationException("getStringColumn is not implemented");
    }

    public byte[][] getBinaryColumn(int columnId) {
        throw new UnsupportedOperationException("getBinaryColumn is not implemented");
    }
}
```

### <a name="primitivedataset"></a>PrimitiveDataset

Esta clase es una implementación de **AbstractSqlServerExtensionDataset** que almacena tipos simples como matrices de tipos primitivos. Se proporciona en el SDK de simplemente como una clase auxiliar que es opcional para usar.

Si no usa esta clase, deberá implementar su propia clase que hereda de **AbstractSqlServerExtensionDataset**.  

```java
package com.microsoft.sqlserver.javalangextension;

import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionDataset;
import java.lang.IllegalArgumentException;
import java.util.HashMap;
import java.util.Map;
import java.util.Map.Entry;

/**
 * Implementation of AbstractSqlServerExtensionDataset that stores
 * simple types as primitives arrays
 */
public class PrimitiveDataset extends AbstractSqlServerExtensionDataset {
    Map<Integer, String>  columnNames;
    Map<Integer, Integer> columnTypes;
    Map<Integer, Integer> columnPrecisions;
    Map<Integer, Integer> columnScales;
    Map<Integer, Object>  columns;
    Map<Integer, boolean[]> columnNullMaps;

    public PrimitiveDataset() {
        columnTypes = new HashMap<>();
        columnNames = new HashMap<>();
        columnPrecisions = new HashMap<>();
        columnScales = new HashMap<>();
        columns = new HashMap<>();
        columnNullMaps = new HashMap<>();
    }

    /**
     * Column metadata interfaces. Metadata is stored in a hash map, using the column ID as the key
     */
    public void addColumnMetadata(int columnId, String columnName, int sqlType, int precision, int scale) {
        if (columnTypes.containsKey(columnId))
        {
            throw new IllegalArgumentException("Metadata for column ID #: " + columnId + " already exists");
        }

        columnTypes.put(columnId, sqlType);
        columnNames.put(columnId, columnName);
        columnPrecisions.put(columnId, precision);
        columnScales.put(columnId, scale);
    }

    public int getColumnCount() {
        return columnTypes.size();
    }

    public String getColumnName(int columnId) {
        checkColumnMetadata(columnId);
        return columnNames.get(columnId);
    }

    public int getColumnPrecision(int columnId) {
        checkColumnMetadata(columnId);
        return columnPrecisions.get(columnId).intValue();
    }

    public int getColumnScale(int columnId) {
        checkColumnMetadata(columnId);
        return columnScales.get(columnId).intValue();
    }

    public int getColumnType(int columnId) {
        checkColumnMetadata(columnId);
        return columnTypes.get(columnId).intValue();
    }

    public boolean[] getColumnNullMap(int columnId) {
        checkColumnMetadata(columnId);
        return columnNullMaps.get(columnId);
    }

    /**
     * Adding column data interfaces. Column data is stored in a hash map, using the column ID as the key and
     * an array of the corresponding type representing each row. Primitives cannot be null, thus null values
     * are represented by an additional boolean array containing a flag to indicate if that value is null.
     * A null indicator array indicates that there are no null values in that column.
     */
    public void addIntColumn(int columnId, int[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addBooleanColumn(int columnId, boolean[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    };

    public void addLongColumn(int columnId, long[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addFloatColumn(int columnId, float[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addDoubleColumn(int columnId, double[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addShortColumn(int columnId, short[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addStringColumn(int columnId, String[] rows) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
    }

    public void addBinaryColumn(int columnId, byte[][] rows) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
    }

    /**
     * Retreiving column data interfaces. For primitive types, calling getColumnNullMap() for the column ID
     * will return the boolean array indicating null values.
     */
    public int[] getIntColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (int[])columns.get(columnId);
    }

    public long[] getLongColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (long[])columns.get(columnId);
    }

    public float[] getFloatColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (float[])columns.get(columnId);
    }

    public short[] getShortColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (short[])columns.get(columnId);
    }

    public boolean[] getBooleanColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (boolean[])columns.get(columnId);
    }

    public double[] getDoubleColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (double[])columns.get(columnId);
    }

    public String[] getStringColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (String[])columns.get(columnId);
    }

    public byte[][] getBinaryColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (byte[][])columns.get(columnId);
    }

    private void checkColumnMetadata(int columnId)
    {
        if (!columnTypes.containsKey(columnId)) {
            throw new IllegalArgumentException("Metadata for column ID #: " + columnId + " does not exist");
        }
    }
}
```

## <a name="next-steps"></a>Pasos siguientes

+ [Ejemplo de Java mediante el SDK de extremo a otro](java-first-sample.md)
+ [Cómo llamar a Java en SQL Server](howto-call-java-from-sql.md)
+ [Extensiones de Java en SQL Server](extension-java.md)
+ [Tipos de datos de SQL Server y Java](java-sql-datatypes.md)
