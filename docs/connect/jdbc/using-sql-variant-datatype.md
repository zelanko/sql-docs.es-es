---
title: Uso del tipo de datos Sql_variant | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdede5d41d5ad7fc22cfed3f1efa9f95612032ca
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "69025842"
---
# <a name="using-sql_variant-data-type"></a>Uso del tipo de datos Sql_variant

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

A partir de la versión 6.3.0, el controlador JDBC admite el tipo de datos sql_variant. Sql_variant también se admite al usar características como parámetros con valores de tabla y BulkCopy con algunas limitaciones mencionadas más adelante en esta página. No todos los tipos de datos se pueden almacenar en el tipo de datos sql_variant. Para obtener una lista de tipos de datos admitidos con sql_variant, compruebe la [documentación](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql) de SQL Server.

##  <a name="populating-and-retrieving-a-table"></a>Rellenar y recuperar una tabla:
Suponiendo que se disponga de una tabla con una columna sql_variant como:

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

Un script de ejemplo para insertar valores mediante una declaración de instrucción:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

Inserción de un valor mediante la instrucción preparada:

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

Si se conoce el tipo subyacente de los datos que se pasan, se podrá usar el establecedor correspondiente. Por ejemplo, se puede usar `preparedStatement.setInt()` al insertar un valor entero.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

Para leer los valores de una tabla, se pueden usar los captadores correspondientes. Por ejemplo, se pueden usar los métodos `getInt()` o `getString()` si se conocen los valores del servidor:    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sql_variant"></a>Utilizar los procedimientos almacenados con sql_variant:   
Posesión de un procedimiento almacenado como:     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
Los parámetros de salida deben registrarse:

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sql_variant"></a>Limitaciones de sql_variant:
- Al usar TVP para rellenar una tabla con un valor `datetime`/`smalldatetime`/`date` almacenado en sql_variant, la llamada a `getDateTime()`/`getSmallDateTime()`/`getDate()` en un elemento ResultSet no funciona e inicia la siguiente excepción:
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    Solución alternativa: use `getString()` o `getObject()` en su lugar. 
    
- El uso de TVP para rellenar una tabla y el envío de un valor NULL en sql_variant no se admiten e inician una excepción:
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>Consulte también

[Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
