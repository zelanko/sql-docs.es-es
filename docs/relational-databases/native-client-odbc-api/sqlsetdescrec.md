---
title: SQLSetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescRec function
ms.assetid: 203d02a2-aa09-462b-a489-a2cdd6f6023b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 785c5f308745f93070dae4ca5a5e7355e8359764
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012404"
---
# <a name="sqlsetdescrec"></a>SQLSetDescRec
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  En este tema se describe la funcionalidad de SQLSetDescRec que es específica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="sqlsetdescrec-and-table-valued-parameters"></a>SQLSetDescRec y parámetros con valores de tabla  
 SQLSetDescRec se puede usar para establecer los campos de descriptor para los parámetros con valores de tabla y las columnas de parámetro con valores de tabla. Las columnas de parámetro con valores de tabla únicamente están disponibles cuando el campo de encabezado del descriptor SQL_SOPT_SS_PARAM_FOCUS está establecido en el ordinal de un registro con SQL_DESC_TYPE establecido en SQL_SS_TABLE. Para obtener más información acerca de SQL_SOPT_SS_PARAM_FOCUS, vea [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 En la tabla siguiente se describe la asignación entre parámetros y campos descriptor.  
  
|Parámetro|Atributo relacionado para tipos de parámetros que no son valores de tabla, incluidas columnas de parámetros con valores de tabla|Atributo relacionado para parámetros con valores de tabla|  
|---------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------|  
|*Tipo*|SQL_DESC_TYPE|SQL_SS_TABLE|  
|*Subtipo*|Se ignora.|Para registros de tipo SQL_DATETIME o SQL_INTERVAL, establézcalo en SQL_DESC_DATETIME_INTERVAL_CODE.|  
|*Longitud*|SQL_DESC_OCTET_LENGTH|Longitud del nombre de tipo de parámetro con valores de tabla. Puede ser SQL_NTS si el nombre de tipo termina en NULL, o cero si no se requiere el nombre de tipo de parámetro con valores de tabla.|  
|*Precisión*|SQL_DESC_PRECISION|SQL_DESC_ARRAY_SIZE|  
|*Escala*|SQL_DESC_SCALE|Sin usar. Este parámetro debería ser cero.|  
|*DataPtr*|SQL_DESC_DATA_PTR en APD|SQL_CA_SS_TYPE_NAME<br /><br /> Este parámetro es opcional para las llamadas a procedimientos almacenados y puede especificarse NULL si no se requiere. Este parámetro se debe especificar en instrucciones SQL que no son llamadas a procedimientos.<br /><br /> *DataPtr* también actúa como un valor único que la aplicación puede usar para identificar este parámetro con valores de tabla cuando se usa el enlace de filas variable.|  
|*StringLengthPtr*|SQL_DESC_OCTET_LENGTH_PTR|SQL_DESC_OCTET_LENGTH_PTR<br /><br /> Para un parámetro con valores de tabla, éste es el número de filas que se van a transferir o SQL_DATA_AT_EXEC. Es un puntero a un valor que contiene el número de filas que se van a transferir con SQLExecDirect.|  
|*IndicatorPtr*|SQL_DESC_INDICATOR_PTR|SQL_DESC_INDICATOR_PTR|  
  
 Para obtener más información sobre los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescrec-support-for-enhanced-date-and-time-features"></a>SQLSetDescRec admite las características mejoradas de fecha y hora  
 Los valores permitidos para los tipos de fecha y hora son los siguientes:  
  
||*Tipo*|*Subtipo*|*Longitud*|*Precisión*|*Escala*|  
|-|------------|---------------|--------------|-----------------|-------------|  
|datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 Para obtener más información, vea [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescrec-support-for-large-clr-udts"></a>SQLSetDescRec admite UDT CLR grandes  
 **SQLSetDescRec** admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [tipos CLR grandes definidos por el usuario &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLSetDescRec](https://go.microsoft.com/fwlink/?LinkId=80704)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
