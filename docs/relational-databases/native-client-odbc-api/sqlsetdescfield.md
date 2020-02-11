---
title: SQLSetDescField | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a37821dff5176dfcb42cfd0a9f6424dfcc3f1938
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73785706"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSetDescField se puede usar para establecer los campos de descriptor para los parámetros con valores de tabla y las columnas de parámetro con valores de tabla. Para obtener información acerca de los campos disponibles, vea campos de descriptor de [parámetros con valores de tabla](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md) y [campos de descriptor para columnas de componentes de parámetros con valores de tabla](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md).  
  
## <a name="remarks"></a>Observaciones  
 Las columnas de parámetro con valores de tabla únicamente están disponibles cuando el campo de encabezado del descriptor SQL_SOPT_SS_PARAM_FOCUS está establecido en el ordinal de un registro con SQL_DESC_TYPE establecido en SQL_SS_TABLE. Para obtener más información acerca de SQL_SOPT_SS_PARAM_FOCUS, vea [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Si se realiza un intento de establecer SQL_SOPT_SS_PARAM_FOCUS en el ordinal de un parámetro que no es un parámetro con valores de tabla, SQLSetStmtAttr devuelve SQL_ERROR y se crea un registro de diagnóstico con SQLSTATE = HY024 y el mensaje "valor de atributo no válido". SQL_SOPT_SS_PARAM_FOCUS no cambia cuando se devuelve SQL_ERROR.  
  
 Al establecer SQL_SOPT_SS_PARAM_FOCUS en 0, se restaura acceso a los registros descriptores para parámetros.  
  
 Para obtener más información sobre los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>SQLSetDescField admite las características mejoradas de fecha y hora  
 Las características de fecha y hora se han mejorado en ODBC. Para obtener información sobre el campo descriptor proporcionado para los nuevos tipos de fecha y hora, vea [Parameter and Result Metadata](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Para obtener más información, vea [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>SQLSetDescField admite UDT CLR grandes  
 SQLSetDescField admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [tipos CLR grandes definidos por el usuario &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>SQLSetDescField admite columnas dispersas  
 SQLSetDecField se puede usar para establecer SQL_SOPT_SS_NAME_SCOPE en el descriptor de parámetros de la aplicación (APD) en los valores SQL_SS_NAME_SCOPE_EXTENDED y SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET.  
  
 Para obtener más información, consulte [compatibilidad con columnas Dispersas &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLSetDescField](https://go.microsoft.com/fwlink/?LinkId=80705)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
