---
title: SQLSetDescField ? Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f699610ce3aac1443439aa5d293e92104f3033d5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292147"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSetDescField se puede utilizar para establecer campos descriptores para parámetros con valores de tabla y columnas de parámetros con valores de tabla. Para obtener información sobre los campos disponibles, vea Campos de descriptor de [parámetros con](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md) valores de tabla y Campos de [descriptor para columnas constituyentes](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)de parámetros con valores de tabla .  
  
## <a name="remarks"></a>Observaciones  
 Las columnas de parámetro con valores de tabla únicamente están disponibles cuando el campo de encabezado del descriptor SQL_SOPT_SS_PARAM_FOCUS está establecido en el ordinal de un registro con SQL_DESC_TYPE establecido en SQL_SS_TABLE. Para obtener más información acerca de SQL_SOPT_SS_PARAM_FOCUS, vea [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Si se intenta establecer SQL_SOPT_SS_PARAM_FOCUS en el ordinal de un parámetro que no es un parámetro con valores de tabla, SQLSetStmtAttr devuelve SQL_ERROR y se crea un registro de diagnóstico con SQLSTATE a HY024 y el mensaje "Valor de atributo no válido". SQL_SOPT_SS_PARAM_FOCUS no cambia cuando se devuelve SQL_ERROR.  
  
 Al establecer SQL_SOPT_SS_PARAM_FOCUS en 0, se restaura acceso a los registros descriptores para parámetros.  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [Parámetros con valores ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)de tabla &#40;&#41;ODBC .  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>SQLSetDescField admite las características mejoradas de fecha y hora  
 Las características de fecha y hora se han mejorado en ODBC. Para obtener información sobre el campo descriptor proporcionado para los nuevos tipos de fecha y hora, vea [Parameter and Result Metadata](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Para obtener más información, vea Mejoras de [fecha y hora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>SQLSetDescField admite UDT CLR grandes  
 SQLSetDescField admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [Tipos definidos por el usuario de CLR grandes &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>SQLSetDescField admite columnas dispersas  
 SQLSetDecField se puede utilizar para establecer SQL_SOPT_SS_NAME_SCOPE en el descriptor de parámetro de aplicación (APD) en los valores SQL_SS_NAME_SCOPE_EXTENDED y SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET.  
  
 Para obtener más información, vea [Compatibilidad con columnas dispersas &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLSetDescField](https://go.microsoft.com/fwlink/?LinkId=80705)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
