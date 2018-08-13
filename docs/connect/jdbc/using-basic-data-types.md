---
title: Uso de tipos de datos básicos | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d58e4913be6db14bec53f5e8bbf63055b2a1344
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662357"
---
# <a name="using-basic-data-types"></a>Usar tipos de datos básicos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa los tipos de datos básicos de JDBC para convertir los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] a un formato que el lenguaje de programación Java pueda entender y viceversa. El controlador JDBC proporciona compatibilidad con la API de JDBC 4.0, que incluye el **SQLXML** tipo de datos y los tipos de datos nacionales (Unicode), como **NCHAR**, **NVARCHAR**, **LONGNVARCHAR**, y **NCLOB**.  
  
## <a name="data-type-mappings"></a>Asignaciones de tipo de datos

En la siguiente tabla se muestran las asignaciones predeterminadas entre los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] básicos, JDBC y del lenguaje de programación Java:  
  
| Tipos de SQL Server   | Tipos de JDBC (Tipos de java.sql.)                        | Tipos del lenguaje Java          |
| ------------------ | -------------------------------------------------- | ---------------------------- |
| BIGINT             | bigint                                             | long                         |
| binary             | BINARY                                             | byte[]                       |
| bit                | BIT                                                | boolean                      |
| char               | CHAR                                               | String                       |
| Date               | DATE                                               | java.sql.Date                |
| DATETIME           | timestamp                                          | java.sql.Timestamp           |
| datetime2          | timestamp                                          | java.sql.Timestamp           |
| datetimeoffset (2) | microsoft.sql.Types.DATETIMEOFFSET                 | microsoft.sql.DateTimeOffset |
| Decimal            | DECIMAL                                            | java.math.BigDecimal         |
| FLOAT              | DOUBLE                                             | double                       |
| imagen              | LONGVARBINARY                                      | byte[]                       |
| INT                | INTEGER                                            | INT                          |
| money              | DECIMAL                                            | java.math.BigDecimal         |
| NCHAR              | CHAR<br /><br /> NCHAR (Java SE 6.0)               | String                       |
| ntext              | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | String                       |
| NUMERIC            | NUMERIC                                            | java.math.BigDecimal         |
| NVARCHAR           | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | String                       |
| nvarchar(max)      | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | String                       |
| REAL               | real                                               | FLOAT                        |
| smalldatetime      | timestamp                                          | java.sql.Timestamp           |
| SMALLINT           | SMALLINT                                           | short                        |
| smallmoney         | DECIMAL                                            | java.math.BigDecimal         |
| texto               | LONGVARCHAR                                        | String                       |
| time               | TIME (1)                                           | java.sql.Time (1)            |
| timestamp          | BINARY                                             | byte[]                       |
| TINYINT            | TINYINT                                            | short                        |
| udt                | VARBINARY                                          | byte[]                       |
| UNIQUEIDENTIFIER   | CHAR                                               | String                       |
| varbinary          | VARBINARY                                          | byte[]                       |
| varbinary(max)     | VARBINARY                                          | byte[]                       |
| varchar            | VARCHAR                                            | String                       |
| ntext       | VARCHAR                                            | String                       |
| xml                | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | String<br /><br /> SQLXML    |
| sqlvariant         | SQLVARIANT                                         | Objeto                       |
| geometry           | VARBINARY                                          | byte[]                       |
| geography          | VARBINARY                                          | byte[]                       |
  
(1) Para usar java.sql.Time con el tipo de hora [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], debe establecer la propiedad de conexión **sendTimeAsDatetime** en FALSE.  
  
(2) mediante programación puede tener acceso a los valores de **datetimeoffset** con [clase DateTimeOffset](../../connect/jdbc/reference/datetimeoffset-class.md).  
  
Las siguientes secciones proporcionan ejemplos de cómo puede usar el controlador JDBC y los tipos de datos básicos. Si quiere obtener un ejemplo detallado sobre cómo usar los tipos de datos básicos en una aplicación de Java, consulte [Ejemplo de tipos de datos básicos](../../connect/jdbc/basic-data-types-sample.md).  
  
## <a name="retrieving-data-as-a-string"></a>Recuperar datos como una cadena

Si tiene que recuperar datos de un origen de datos que se asigne a cualquiera de los tipos de datos básicos de JDBC para verlos como una cadena, o si no se necesitan datos fuertemente tipados, puede usar el método [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) de la clase [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), como en el siguiente ejemplo:  
  
[!code[JDBC#UsingBasicDataTypes1](../../connect/jdbc/codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>Recuperar datos por tipos de datos

Si tiene que recuperar datos de un origen de datos y sabe el tipo de datos que se van a recuperar, use uno de los métodos get\<Type> de la clase SQLServerResultSet, también conocidos como *métodos de captador*. Con los métodos get\<Type>, puede usar un nombre de columna o un índice de columna, como en el siguiente ejemplo:  
  
[!code[JDBC#UsingBasicDataTypes2](../../connect/jdbc/codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
> El getUnicodeStream y getBigDecimal con métodos de escalado están en desuso y no son compatibles con el controlador JDBC.

## <a name="updating-data-by-data-type"></a>Actualizar datos por tipos de datos

Si tiene que actualizar el valor de un campo en un origen de datos, use uno de la actualización\<tipo > métodos de la clase SQLServerResultSet. En el siguiente ejemplo, se usa el método [updateInt](../../connect/jdbc/reference/updateint-method-sqlserverresultset.md) en conjunción con el método [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) para actualizar los datos del origen de datos:  
  
[!code[JDBC#UsingBasicDataTypes3](../../connect/jdbc/codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
> El controlador JDBC no puede actualizar una columna SQL Server con un nombre de columna que tenga más de 127 caracteres de largo. Si se intenta una actualización a una columna cuyo nombre tenga más de 127 caracteres, se genera una excepción.  
  
## <a name="updating-data-by-parameterized-query"></a>Actualizar datos mediante una consulta con parámetros

Si tiene que actualizar datos de un origen de datos mediante el uso de una consulta con parámetros, puede establecer el tipo de datos de los parámetros con los métodos set\<Type> de la clase [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), también conocidos como *métodos de establecedor*. En el siguiente ejemplo, se usa el método [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) para precompilar la consulta con parámetros y, luego, el método [setString](../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md) para establecer el valor de cadena del parámetro antes de llamar al método [executeUpdate](../../connect/jdbc/reference/executeupdate-method.md).  
  
[!code[JDBC#UsingBasicDataTypes4](../../connect/jdbc/codesnippet/Java/using-basic-data-types_4.java)]  
  
Para obtener más información acerca de las consultas con parámetros, vea [utilizando una instrucción SQL con parámetros](../../connect/jdbc/using-an-sql-statement-with-parameters.md).  

## <a name="passing-parameters-to-a-stored-procedure"></a>Pasar de parámetros a un procedimiento almacenado

Si tiene que pasar parámetros tipados a un procedimiento almacenado, puede establecerlos por índice o por nombre mediante el uso de uno de los métodos set\<Type> de la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). En el siguiente ejemplo, se usa el método [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) para configurar la llamada al procedimiento almacenado y, luego, el método [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) para establecer el parámetro para la llamada antes de llamar al método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md).  
  
[!code[JDBC#UsingBasicDataTypes5](../../connect/jdbc/codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
> En este ejemplo, se devuelve un conjunto de resultados con los resultados de la ejecución del procedimiento almacenado.

Para obtener más información sobre cómo usar el controlador JDBC con procedimientos almacenados y parámetros de entrada, consulte [mediante un procedimiento almacenado con parámetros de entrada](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md).  

## <a name="retrieving-parameters-from-a-stored-procedure"></a>Recuperación de parámetros desde un procedimiento almacenado

Si tiene que recuperar parámetros de un procedimiento almacenado, primero debe registrar un parámetro de salida por el nombre o el índice con el método [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) de la clase SQLServerCallableStatement y, luego, asignar el parámetro de salida devuelto a una variable adecuada tras haber ejecutado la llamada al procedimiento almacenado. En el siguiente ejemplo, se usa el método prepareCall para configurar la llamada al procedimiento almacenado, el método registerOutParameter para configurar el parámetro de salida y el método [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) para establecer el parámetro para la llamada antes de llamar al método executeQuery. El valor que devuelve el parámetro de salida del procedimiento almacenado se recupera con el método [getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md).  
  
[!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
> Además del parámetro de salida devuelto, puede que también se devuelva un conjunto de resultados con los resultados de ejecución del procedimiento almacenado.  
  
Para obtener más información sobre cómo usar el controlador JDBC con procedimientos almacenados y parámetros de salida, vea [mediante un procedimiento almacenado con parámetros de salida](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md).  

## <a name="see-also"></a>Ver también

[Describir los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
