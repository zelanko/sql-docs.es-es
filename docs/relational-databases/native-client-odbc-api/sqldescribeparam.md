---
title: SQLDescribeParam | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aa74f982a5ff1894651d68f06689cba476a16452
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73787108"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para describir los parámetros de cualquier instrucción SQL, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client genera y ejecuta una [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción SELECT cuando se llama a SQLDescribeParam en un identificador de instrucción ODBC preparado. Los metadatos del conjunto de resultados determinan las características de los parámetros en la instrucción preparada. SQLDescribeParam puede devolver cualquier código de error que puede devolver SQLExecute o SQLExecDirect.  
  
 Las mejoras en el motor de base [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] de datos a partir de permiten a SQLDescribeParam obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por SQLDescribeParam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en versiones anteriores de. Para obtener más información, vea [Detección de metadatos](../../relational-databases/native-client/features/metadata-discovery.md).  
  
 También nuevo en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], *ParameterSizePtr* ahora devuelve un valor que se alinea con la definición del tamaño, en caracteres, de la columna o expresión del marcador de parámetro correspondiente tal y como se define en la [especificación de ODBC](https://go.microsoft.com/fwlink/?LinkId=207044). En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, *ParameterSizePtr* podía ser el valor correspondiente de **SQL_DESC_OCTET_LENGTH** para el tipo, o un valor de tamaño de columna irrelevante que se proporcionó a SQLBindParameter para un tipo, cuyo valor se debe pasar por alto (**SQL_INTEGER**, por ejemplo).  
  
 El controlador no admite la llamada a SQLDescribeParam en las siguientes situaciones:  
  
-   Después de SQLExecDirect para [!INCLUDE[tsql](../../includes/tsql-md.md)] las instrucciones UPDATE o DELETE que contengan la cláusula FROM.  
  
-   En cualquier instrucción ODBC o [!INCLUDE[tsql](../../includes/tsql-md.md)] que contenga un parámetro en una cláusula HAVING o se compare con el resultado de una función SUM.  
  
-   En cualquier instrucción ODBC o [!INCLUDE[tsql](../../includes/tsql-md.md)] que dependa de una subconsulta que contiene parámetros.  
  
-   En instrucciones ODBC SQL que contengan marcadores de parámetros en ambas expresiones de una comparación, igualdad o predicado cuantificado.  
  
-   En cualquier consulta donde uno de los parámetros sea un parámetro a una función.  
  
-   Cuando hay comentarios (/* \*/) en el [!INCLUDE[tsql](../../includes/tsql-md.md)] comando.  
  
 Al procesar un lote de [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones, el controlador tampoco admite la llamada a SQLDescribeParam para los marcadores de parámetros en instrucciones posteriores a la primera instrucción del lote.  
  
 Al describir los parámetros de los procedimientos almacenados preparados, SQLDescribeParam usa el procedimiento almacenado del sistema [sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md) para recuperar las características de los parámetros. sp_sproc_columns puede informar sobre los procedimientos almacenados de la base de datos de usuario actual. Preparar un nombre completo de procedimiento almacenado permite que SQLDescribeParam se ejecute en las bases de datos. Por ejemplo, el procedimiento almacenado del sistema [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) se puede preparar y ejecutar en cualquier base de datos como:  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 Al ejecutar SQLDescribeParam después de la preparación correcta, se devuelve un conjunto de filas vacío cuando se conecta a cualquier base de datos pero **maestra**. La misma llamada, preparada como se indica a continuación, hace que SQLDescribeParam se realice correctamente independientemente de la base de datos de usuario actual:  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 En el caso de los tipos de datos de valores grandes, el valor devuelto en *DataTypePtr* es SQL_VARCHAR, SQL_VARBINARY o SQL_NVARCHAR. Para indicar que el tamaño del parámetro de tipo de datos de valor grande es "ilimitado" [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el controlador ODBC de Native Client establece *ParameterSizePtr* en 0. Se devuelven los valores de tamaño real para los parámetros estándar **VARCHAR** .  
  
> [!NOTE]  
>  Si el parámetro ya se ha enlazado con un tamaño máximo para los parámetros SQL_VARCHAR, SQL_WVARCHAR o SQL_VARBINARY, se devuelve el tamaño enlazado del parámetro, no "ilimitado".  
  
 Para enlazar un parámetro de entrada de tamaño "ilimitado", se deben utilizar datos en ejecución. No es posible enlazar un parámetro de salida de tamaño "ilimitado" (no hay ningún método para la transmisión de datos de un parámetro de salida, como [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) en el caso de los conjuntos de resultados).  
  
 Para los parámetros de salida se debe enlazar un búfer y, si el valor es demasiado grande, el búfer se rellena y se devuelve un mensaje SQL_SUCCESS_WITH_INFO junto con la advertencia "Datos tipo String, se truncarán por la derecha". Los datos truncados se descartan.  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam y parámetros con valores de tabla  
 Una aplicación puede recuperar información de parámetros con valores de tabla para una instrucción preparada con SQLDescribeParam. Para obtener más información, vea [metadatos de parámetros con valores de tabla para instrucciones](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)preparadas.  
  
 Para obtener más información sobre los parámetros con valores de tabla en general, vea [parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
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
  
 Para obtener más información, vea [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>SQLDescribeParam admite UDT CLR grandes  
 **SQLDescribeParam** admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [tipos CLR grandes definidos por el usuario &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLDescribeParam función)](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
