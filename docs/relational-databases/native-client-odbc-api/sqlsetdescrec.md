---
title: SQLSetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLSetDescRec function
ms.assetid: 203d02a2-aa09-462b-a489-a2cdd6f6023b
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b3c490d8a087651d5de82226d4ae1f2d8450adc
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43093524"
---
# <a name="sqlsetdescrec"></a>SQLSetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Este tema describe la funcionalidad SQLSetDescRec específica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="sqlsetdescrec-and-table-valued-parameters"></a>SQLSetDescRec y parámetros con valores de tabla  
 SQLSetDescRec puede utilizarse para establecer los campos de descriptor de parámetros con valores de tabla y las columnas de parámetros con valores de tabla. Las columnas de parámetro con valores de tabla únicamente están disponibles cuando el campo de encabezado del descriptor SQL_SOPT_SS_PARAM_FOCUS está establecido en el ordinal de un registro con SQL_DESC_TYPE establecido en SQL_SS_TABLE. Para obtener más información acerca de SQL_SOPT_SS_PARAM_FOCUS, vea [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 En la tabla siguiente se describe la asignación entre parámetros y campos descriptor.  
  
|Parámetro|Atributo relacionado para tipos de parámetro con valores que no son de tabla, incluidas columnas de parámetro con valores de tabla|Atributo relacionado para parámetros con valores de tabla|  
|---------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------|  
|*Tipo*|SQL_DESC_TYPE|SQL_SS_TABLE|  
|*Subtipo*|Omitido|Para registros de tipo SQL_DATETIME o SQL_INTERVAL, establézcalo en SQL_DESC_DATETIME_INTERVAL_CODE.|  
|*Longitud*|SQL_DESC_OCTET_LENGTH|Longitud del nombre de tipo de parámetro con valores de tabla. Puede ser SQL_NTS si el nombre de tipo termina en NULL, o cero si no se requiere el nombre de tipo de parámetro con valores de tabla.|  
|*Precisión*|SQL_DESC_PRECISION|SQL_DESC_ARRAY_SIZE|  
|*Escala*|SQL_DESC_SCALE|Sin usar. Este parámetro debería ser cero.|  
|*DataPtr*|SQL_DESC_DATA_PTR en APD|SQL_CA_SS_TYPE_NAME<br /><br /> Este parámetro es opcional para las llamadas a procedimientos almacenados y puede especificarse NULL si no se requiere. Este parámetro se debe especificar en instrucciones SQL que no son llamadas a procedimientos.<br /><br /> *DataPtr* también actúa como un valor único que la aplicación puede usar para identificar este parámetro con valores de tabla cuando se usa el enlace de filas variable.|  
|*StringLengthPtr*|SQL_DESC_OCTET_LENGTH_PTR|SQL_DESC_OCTET_LENGTH_PTR<br /><br /> Para un parámetro con valores de tabla, éste es el número de filas que se van a transferir o SQL_DATA_AT_EXEC. Esto es un puntero a un valor que contiene el número de filas que se van a transferir con SQLExecDirect.|  
|*IndicatorPtr*|SQL_DESC_INDICATOR_PTR|SQL_DESC_INDICATOR_PTR|  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescrec-support-for-enhanced-date-and-time-features"></a>SQLSetDescRec admite las características mejoradas de fecha y hora  
 Los valores permitidos para los tipos de fecha y hora son los siguientes:  
  
||*Tipo*|*Subtipo*|*Longitud*|*Precisión*|*Escala*|  
|-|------------|---------------|--------------|-----------------|-------------|  
|DATETIME|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|Date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 Para obtener más información, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescrec-support-for-large-clr-udts"></a>SQLSetDescRec admite UDT CLR grandes  
 **SQLSetDescRec** admite tipos de definidos por el usuario CLR (UDT) grandes. Para obtener más información, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLSetDescRec](http://go.microsoft.com/fwlink/?LinkId=80704)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
