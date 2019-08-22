---
title: Usar el tipo de datos sql_variant | Microsoft Docs
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
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025842"
---
# <a name="using-sql_variant-data-type"></a>Uso del tipo de datos Sql_variant

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

A partir de la versión 6.3.0, el controlador JDBC admite el tipo de los tipos de. También se admite sql_variant al usar características como parámetros con valores de tabla y BulkCopy con algunas limitaciones que se mencionan más adelante en esta página. No todos los tipos de datos se pueden almacenar en el tipo de datos sql_variant. Para obtener una lista de los tipos de datos admitidos con sql_variant, consulte la SQL Server [docs](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql).

##  <a name="populating-and-retrieving-a-table"></a>Rellenar y recuperar una tabla:
Suponiendo que una tiene una tabla con una columna sql_variant como:

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

Un script de ejemplo para insertar valores mediante la instrucción:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

Insertando valor mediante la instrucción preparada:

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

Si se conoce el tipo subyacente de los datos que se pasan, se puede usar el establecedor respectivo. Por ejemplo, `preparedStatement.setInt()` se puede utilizar al insertar un valor entero.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

Para leer los valores de la tabla, se pueden usar los captadores respectivos. Por ejemplo, `getInt()` se `getString()` pueden usar los métodos o si se conocen los valores procedentes del servidor:    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sql_variant"></a>Usar procedimientos almacenados con sql_variant:   
Tener un procedimiento almacenado como:     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
Los parámetros de salida deben estar registrados:

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sql_variant"></a>Limitaciones de sql_variant:
- Al usar TVP para rellenar una tabla `datetime` con un `smalldatetime` `getSmallDateTime()` `getDateTime()` / `date` / valor almacenado en un sql_variant, llamar / / `getDate()` a en un ResultSet no funciona y produce la excepción siguiente:
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    Solución alternativa: `getString()` use `getObject()` o en su lugar. 
    
- No se admite el uso de TVP para rellenar una tabla y enviar un valor null en un sql_variant y se produce una excepción:
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>Vea también

[Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
