---
title: "Uso de tipos de datos básicos | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 66da5301a12427ed50a212abf74a0700d89e8668
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2018
---
# <a name="using-basic-data-types"></a>Usar tipos de datos básicos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] utiliza los tipos de datos básicos de JDBC para convertir el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos a un formato que pueda entender el lenguaje de programación Java y viceversa. El controlador JDBC proporciona compatibilidad con la API de JDBC 4.0, que incluye el **SQLXML** tipo de datos y los tipos de datos nacionales (Unicode), como **NCHAR**, **NVARCHAR**, **LONGNVARCHAR**, y **NCLOB**.  
  
## <a name="data-type-mappings"></a>Asignaciones de tipo de datos  
 En la tabla siguiente se enumera las asignaciones predeterminadas entre las opciones básicas [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], JDBC y los tipos de datos de lenguaje de programación Java:  
  
|Tipos de SQL Server|Tipos de JDBC (Tipos de java.sql.)|Tipos del lenguaje Java|  
|----------------------|-----------------------------------|-------------------------|  
|bigint|bigint|long|  
|binary|BINARY|byte[]|  
|bit|BIT|boolean|  
|char|CHAR|String|  
|date|DATE|java.sql.Date|  
|datetime|TIMESTAMP|java.sql.Timestamp|  
|datetime2|TIMESTAMP|java.sql.Timestamp|  
|datetimeoffset (2)|microsoft.sql.Types.DATETIMEOFFSET|microsoft.sql.DateTimeOffset|  
|decimal|DECIMAL|java.math.BigDecimal|  
|float|DOUBLE|double|  
|imagen|LONGVARBINARY|byte[]|  
|int|INTEGER|int|  
|money|DECIMAL|java.math.BigDecimal|  
|NCHAR|CHAR<br /><br /> NCHAR (Java SE 6.0)|String|  
|ntext|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String|  
|numeric|NUMERIC|java.math.BigDecimal|  
|nvarchar|VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)|String|  
|nvarchar(max)|VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)|String|  
|real|REAL|float|  
|smalldatetime|TIMESTAMP|java.sql.Timestamp|  
|smallint|SMALLINT|short|  
|smallmoney|DECIMAL|java.math.BigDecimal|  
|texto|LONGVARCHAR|String|  
|time|TIME (1)|java.sql.Time (1)|  
|timestamp|BINARY|byte[]|  
|tinyint|TINYINT|short|  
|udt|VARBINARY|byte[]|  
|uniqueidentifier|CHAR|String|  
|varbinary|VARBINARY|byte[]|  
|varbinary(max)|VARBINARY|byte[]|  
|varchar|VARCHAR|String|  
|ntext|VARCHAR|String|  
|xml|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String<br /><br /> SQLXML|  
|SQLVARIANT|SQLVARIANT|Object|  
  
 (1) para utilizar java.sql.Time con el tiempo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo, debe establecer el **sendTimeAsDatetime** propiedad de conexión en false.  
  
 (2) mediante programación se pueden obtener acceso a valores de **datetimeoffset** con [clase DateTimeOffset](../../connect/jdbc/reference/datetimeoffset-class.md).  
  
 Las siguientes secciones proporcionan ejemplos de cómo puede usar el controlador JDBC y los tipos de datos básicos. Para obtener un ejemplo más detallado de cómo usar los tipos de datos básicos en una aplicación Java, consulte [ejemplo básico de tipos de datos](../../connect/jdbc/basic-data-types-sample.md).  
  
## <a name="retrieving-data-as-a-string"></a>Recuperar datos como una cadena  
 Si tiene que recuperar datos desde un origen de datos que se asigna a ninguno de los tipos de datos básicos de JDBC para verlos como una cadena, o si los datos fuertemente tipados no están necesarios, puede usar el [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) (clase), como en el siguiente ejemplo:  
  
 [!code[JDBC#UsingBasicDataTypes1](../../connect/jdbc/codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>Recuperar datos por tipos de datos  
 Si tiene que recuperar datos desde un origen de datos y sabe el tipo de datos que se van a recuperar, use uno de get\<tipo > clase métodos de SQLServerResultSet, también conocido como el *métodos captadores*. Puede usar un nombre de columna o un índice de columna con get\<tipo > métodos, como en el siguiente ejemplo:  
  
 [!code[JDBC#UsingBasicDataTypes2](../../connect/jdbc/codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
>  El getUnicodeStream y getBigDecimal con métodos de escala están en desuso y no son compatibles con el controlador JDBC.  
  
## <a name="updating-data-by-data-type"></a>Actualizar datos por tipos de datos  
 Si tiene que actualizar el valor de un campo en un origen de datos, use alguna de las actualizaciones\<tipo > métodos de la clase SQLServerResultSet. En el ejemplo siguiente, la [updateInt](../../connect/jdbc/reference/updateint-method-sqlserverresultset.md) método se utiliza junto con la [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) método para actualizar los datos del origen de datos:  
  
 [!code[JDBC#UsingBasicDataTypes3](../../connect/jdbc/codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
>  El controlador JDBC no puede actualizar una columna SQL Server con un nombre de columna que tenga más de 127 caracteres de largo. Si se intenta una actualización a una columna cuyo nombre tenga más de 127 caracteres, se genera una excepción.  
  
## <a name="updating-data-by-parameterized-query"></a>Actualizar datos mediante una consulta con parámetros  
 Si tiene que actualizar datos en un origen de datos mediante una consulta con parámetros, puede establecer el tipo de datos de los parámetros mediante uno de los conjuntos\<tipo > métodos de la [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) (clase), también conocido como el *métodos establecedor*. En el ejemplo siguiente, la [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) método se usa para precompilar la consulta con parámetros y, a continuación, el [setString](../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md) método se usa para establecer el valor de cadena del parámetro antes de la [executeUpdate](../../connect/jdbc/reference/executeupdate-method.md) se llama al método.  
  
 [!code[JDBC#UsingBasicDataTypes4](../../connect/jdbc/codesnippet/Java/using-basic-data-types_4.java)]  
  
 Para obtener más información acerca de las consultas con parámetros, vea [con una instrucción SQL con parámetros](../../connect/jdbc/using-an-sql-statement-with-parameters.md).  
  
## <a name="passing-parameters-to-a-stored-procedure"></a>Pasar de parámetros a un procedimiento almacenado  
 Si tiene que pasar parámetros de tipo en un procedimiento almacenado, puede establecer los parámetros de índice o nombre mediante uno de los conjuntos\<tipo > métodos de la [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clase. En el ejemplo siguiente, la [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) método se usa para configurar la llamada al procedimiento almacenado y, a continuación, el [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) método se usa para establecer el parámetro para la llamada antes de la [ executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) se llama al método.  
  
 [!code[JDBC#UsingBasicDataTypes5](../../connect/jdbc/codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
>  En este ejemplo, se devuelve un conjunto de resultados con los resultados de la ejecución del procedimiento almacenado.  
  
 Para obtener más información sobre cómo usar el controlador JDBC con procedimientos almacenados y parámetros de entrada, consulte [mediante un procedimiento almacenado con parámetros de entrada](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md).  
  
## <a name="retrieving-parameters-from-a-stored-procedure"></a>Recuperación de parámetros desde un procedimiento almacenado  
 Si tiene que recuperar parámetros desde un procedimiento almacenado, primero debe registrar un parámetro de salida por nombre o índice mediante el uso de la [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) método de la clase SQLServerCallableStatement y, a continuación, asigne el Devuelve el parámetro de salida a una variable adecuada después de haber ejecutado la llamada al procedimiento almacenado. En el ejemplo siguiente, se utiliza el método prepareCall para configurar la llamada al procedimiento almacenado, el método registerOutParameter se utiliza para configurar el parámetro de salida y, a continuación, el [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) método se usa para establecer el parámetro para el llamada antes de que se llama al método executeQuery. El valor devuelto por el parámetro de salida del procedimiento almacenado se recupera utilizando la [getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md) método.  
  
 [!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
>  Además del parámetro de salida devuelto, puede que también se devuelva un conjunto de resultados con los resultados de ejecución del procedimiento almacenado.  
  
 Para obtener más información sobre cómo usar el controlador JDBC con procedimientos almacenados y parámetros de salida, consulte [mediante un procedimiento almacenado con parámetros de salida](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md).  
  
## <a name="see-also"></a>Vea también  
 [Describir los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
