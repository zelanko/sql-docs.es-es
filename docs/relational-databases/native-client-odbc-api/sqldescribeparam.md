---
title: SQLDescribeParam ? Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efe1fdccbef4f5c4a393083f6eb81efee759be5c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302596"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para describir los parámetros de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cualquier instrucción SQL, el [!INCLUDE[tsql](../../includes/tsql-md.md)] controlador ODBC de Native Client compila y ejecuta una instrucción SELECT cuando se llama a SQLDescribeParam en un identificador de instrucción ODBC preparado. Los metadatos del conjunto de resultados determinan las características de los parámetros en la instrucción preparada. SQLDescribeParam puede devolver cualquier código de error que SQLExecute o SQLExecDirect podría devolver.  
  
 Las mejoras en el [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] motor de base de datos a partir de permiten a SQLDescribeParam obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]devueltos por SQLDescribeParam en versiones anteriores de . Para obtener más información, vea [Detección de metadatos](../../relational-databases/native-client/features/metadata-discovery.md).  
  
 También es [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]nuevo en , *ParameterSizePtr* ahora devuelve un valor que se alinea con la definición para el tamaño, en caracteres, de la columna o expresión del marcador de parámetro correspondiente tal como se define en la [especificación ODBC](https://go.microsoft.com/fwlink/?LinkId=207044). En versiones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores de Native Client, *ParameterSizePtr* podría ser el valor correspondiente de **SQL_DESC_OCTET_LENGTH** para el tipo, o un valor de tamaño de columna irrelevante que se proporcionó a SQLBindParameter para un tipo, cuyo valor debe omitirse (**SQL_INTEGER**, por ejemplo).  
  
 El controlador no admite la llamada a SQLDescribeParam en las situaciones siguientes:  
  
-   Después de SQLExecDirect para cualquier [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE o DELETE instrucciones que contienen el FROM cláusula.  
  
-   En cualquier instrucción ODBC o [!INCLUDE[tsql](../../includes/tsql-md.md)] que contenga un parámetro en una cláusula HAVING o se compare con el resultado de una función SUM.  
  
-   En cualquier instrucción ODBC o [!INCLUDE[tsql](../../includes/tsql-md.md)] que dependa de una subconsulta que contiene parámetros.  
  
-   En instrucciones ODBC SQL que contengan marcadores de parámetros en ambas expresiones de una comparación, igualdad o predicado cuantificado.  
  
-   En cualquier consulta donde uno de los parámetros sea un parámetro a una función.  
  
-   Cuando hay comentarios \*(/* [!INCLUDE[tsql](../../includes/tsql-md.md)] /) en el comando.  
  
 Al procesar un [!INCLUDE[tsql](../../includes/tsql-md.md)] lote de instrucciones, el controlador tampoco admite la llamada a SQLDescribeParam para marcadores de parámetro en instrucciones después de la primera instrucción del lote.  
  
 Al describir los parámetros de los procedimientos almacenados preparados, SQLDescribeParam utiliza el procedimiento almacenado del sistema [sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md) para recuperar las características de los parámetros. sp_sproc_columns pueden notificar datos para procedimientos almacenados dentro de la base de datos de usuarioactual. La preparación de un nombre de procedimiento almacenado completo permite que SQLDescribeParam se ejecute entre bases de datos. Por ejemplo, el procedimiento almacenado del sistema [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) se puede preparar y ejecutar en cualquier base de datos como:  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 La ejecución de SQLDescribeParam después de una preparación correcta devuelve un conjunto de filas vacío cuando se conecta a cualquier base de datos pero **maestro.** La misma llamada, preparada de la siguiente manera, hace que SQLDescribeParam se realice correctamente independientemente de la base de datos de usuarioactual:  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 Para los tipos de datos de valor grande, el valor devuelto en *DataTypePtr* es SQL_VARCHAR, SQL_VARBINARY o SQL_NVARCHAR. Para indicar que el tamaño del parámetro de tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de datos de valor grande es "ilimitado", el controlador ODBC de Native Client establece *ParameterSizePtr* en 0. Los valores de tamaño real se devuelven para los parámetros **varchar** estándar.  
  
> [!NOTE]  
>  Si el parámetro ya se ha enlazado con un tamaño máximo para los parámetros SQL_VARCHAR, SQL_WVARCHAR o SQL_VARBINARY, se devuelve el tamaño enlazado del parámetro, no "ilimitado".  
  
 Para enlazar un parámetro de entrada de tamaño "ilimitado", se deben utilizar datos en ejecución. No es posible enlazar un parámetro de salida de tamaño "ilimitado" (no hay ningún método para transmitir datos de un parámetro de salida, como lo hace [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) para los conjuntos de resultados).  
  
 Para los parámetros de salida se debe enlazar un búfer y, si el valor es demasiado grande, el búfer se rellena y se devuelve un mensaje SQL_SUCCESS_WITH_INFO junto con la advertencia "Datos tipo String, se truncarán por la derecha". Los datos truncados se descartan.  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam y parámetros con valores de tabla  
 Una aplicación puede recuperar información de parámetros con valores de tabla para una instrucción preparada con SQLDescribeParam. Para obtener más información, vea [Metadatos de parámetros con valores](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)de tabla para instrucciones preparadas .  
  
 Para obtener más información acerca de los parámetros con valores de tabla en general, vea [Parámetros con valores ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)de tabla &#40;&#41;ODBC .  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>SQLDescribeParam admite las características mejoradas de fecha y hora  
 Los valores devueltos para los tipos de fecha y hora son los siguientes:  
  
||*DataTypePtr*|*ParameterSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|------------------------|------------------------|  
|datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Para obtener más información, vea Mejoras de [fecha y hora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>SQLDescribeParam admite UDT CLR grandes  
 **SQLDescribeParam** admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [Tipos definidos por el usuario de CLR grandes &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [FUNción SQLDescribeParam](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
