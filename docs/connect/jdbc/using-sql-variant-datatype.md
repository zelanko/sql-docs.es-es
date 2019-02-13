---
title: Con el tipo de datos Sql_variant | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8df6fcee7b79f0c85f1182442195eb2cdf8d7ac9
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/05/2019
ms.locfileid: "55737353"
---
# <a name="using-sqlvariant-data-type"></a>Uso del tipo de datos Sql_variant

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

A partir de la versión 6.3.0, el controlador JDBC admite el tipo de datos sql_variant. Sql_variant también se admite cuando con características como parámetros con valores de tabla y BulkCopy con algunas limitaciones mencionadas más adelante en esta página. No todos los tipos de datos pueden almacenarse en el tipo de datos sql_variant. Para obtener una lista de tipos de datos compatibles con sql_variant, compruebe el servidor SQL [Docs](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql).

##  <a name="populating-and-retrieving-a-table"></a>Rellenar y recuperar una tabla:
Suponiendo que uno tiene una tabla con una columna sql_variant como:

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

Un script de ejemplo para insertar valores instrucción using:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

Insertar valor mediante la instrucción preparada:

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

Si se conoce el tipo subyacente de los datos pasados, puede usarse el establecedor correspondiente. Por ejemplo, `preparedStatement.setInt()` se puede usar cuando se inserta un valor entero.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

Para leer los valores de la tabla, se pueden usar los captadores respectivos. Por ejemplo, `getInt()` o `getString()` métodos se pueden usar si se conocen los valores procedentes del servidor:    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sqlvariant"></a>Uso de procedimientos almacenados con sql_variant:   
Tener un procedimiento almacenado, como:     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
Se deben registrar los parámetros de salida:

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sqlvariant"></a>Limitaciones de sql_variant:
- Al usar TVP para rellenar una tabla con un `datetime` / `smalldatetime` / `date` valor almacenado en un sql_variant, una llamada a `getDateTime()` / `getSmallDateTime()` / `getDate()` en un Conjunto de resultados no funciona y produce la excepción siguiente:
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    Solución alternativa: use `getString()` o `getObject()` en su lugar. 
    
- Usar TVP para rellenar una tabla y el envío de un valor null en una sql_variant no se admiten y produce una excepción:
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>Consulte también

[Describir los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
