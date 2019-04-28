---
title: SQLGetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLGetDescRec function
ms.assetid: f3389ff2-f3be-4035-9fb5-c9ebc2f15025
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41bd489752dc1b4084d9c012cad97413c6ff98b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657718"
---
# <a name="sqlgetdescrec"></a>SQLGetDescRec
  Este tema describe la funcionalidad SQLGetDescRec específica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="sqlgetdescrec-and-table-valued-parameters"></a>SQLGetDescRec y parámetros con valores de tabla  
 SQLGetDescRec puede utilizarse para obtener los valores de atributos de parámetros con valores de tabla y las columnas de parámetros con valores de tabla. El *RecNumber* parámetro del SQLGetDescRec corresponde a la *ParameterNumber* parámetro de SQLBindParameter.  
  
 Las columnas de parámetro con valores de tabla únicamente están disponibles cuando el campo de encabezado del descriptor SQL_SOPT_SS_PARAM_FOCUS está establecido en el ordinal de un registro con SQL_DESC_TYPE establecido en SQL_SS_TABLE. Para obtener más información acerca de SQL_SOPT_SS_PARAM_FOCUS sobre, consulte [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 SQLGetDescRec devuelve los datos siguientes:  
  
|Parámetro|Parámetro con valores de tabla|Columnas de parámetros con valores de tabla y otros parámetros|  
|---------------|-----------------------------|----------------------------------------------------------|  
|*Name*|El nombre del parámetro formal de una llamada de procedimiento almacenado; de lo contrario, una cadena de longitud 0.|El nombre de la columna de parámetros con valores de tabla.|  
|*TypePtr*|SQL_DESC_TYPE. Para los parámetros con valores de tabla, es SQL_SS_TABLE.|SQL_DESC_TYPE|  
|*SubTypePtr*|No definido|SQL_DESC_DATETIME_INTERVAL_CODE (para registros de tipo SQL_DATETIME o SQL_INTERVAL).|  
|*LengthPtr*|0|SQL_DESC_OCTET_LENGTH|  
|*PrecisionPtr*|0|SQL_DESC_PRECISION|  
|*ScalePtr*|0|SQL_DESC_SCALE|  
|*NullablePtr*|1|SQL_DESC_NULLABLE|  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgetdescrec-support-for-enhanced-date-and-time-features"></a>SQLGetDescRec admite las características mejoradas de fecha y hora  
 Los valores devueltos para los tipos de fecha y hora son los siguientes:  
  
||*TypePtr*|*SubTypePtr*|*LengthPtr*|*PrecisionPtr*|*ScalePtr*|  
|-|---------------|------------------|-----------------|--------------------|----------------|  
|datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 Para obtener más información, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgetdescrec-support-for-large-clr-udts"></a>SQLGetDescRec admite UDT CLR grandes  
 `SQLGetDescRec` admite tipos CLR definidos por el usuario (UDT) grandes. Para obtener más información, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLGetDescRec](https://go.microsoft.com/fwlink/?LinkId=80707)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
