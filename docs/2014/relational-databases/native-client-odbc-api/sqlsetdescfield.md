---
title: SQLSetDescField | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f65c26e1c6b9588b770acf1a66409dfde8ea1072
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188678"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
  SQLSetDescField puede utilizarse para establecer los campos de descriptor de parámetros con valores de tabla y las columnas de parámetros con valores de tabla. Para obtener información acerca de los campos disponibles, consulte [campos de Descriptor de parámetro con valores de tabla](../native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md) y [campos de Descriptor para las columnas constituyentes de parámetros con valores de tabla](../native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md).  
  
## <a name="remarks"></a>Comentarios  
 Las columnas de parámetro con valores de tabla únicamente están disponibles cuando el campo de encabezado del descriptor SQL_SOPT_SS_PARAM_FOCUS está establecido en el ordinal de un registro con SQL_DESC_TYPE establecido en SQL_SS_TABLE. Para obtener más información acerca de SQL_SOPT_SS_PARAM_FOCUS, vea [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Si se realiza un intento para establecer SQL_SOPT_SS_PARAM_FOCUS en el ordinal de un parámetro que no es un parámetro con valores de tabla, SQLSetStmtAttr devuelve SQL_ERROR y se crea un registro de diagnóstico con SQLSTATE = HY024 y el mensaje "valor de atributo no válido". SQL_SOPT_SS_PARAM_FOCUS no cambia cuando se devuelve SQL_ERROR.  
  
 Al establecer SQL_SOPT_SS_PARAM_FOCUS en 0, se restaura acceso a los registros descriptores para parámetros.  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>SQLSetDescField admite las características mejoradas de fecha y hora  
 Las características de fecha y hora se han mejorado en ODBC. Para obtener información sobre el campo descriptor proporcionado para los nuevos tipos de fecha y hora, vea [Parameter and Result Metadata](../native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Para obtener más información, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>SQLSetDescField admite UDT CLR grandes  
 SQLSetDescField admite tipos de definidos por el usuario CLR (UDT) grandes. Para obtener más información, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>SQLSetDescField admite columnas dispersas  
 SQLSetDecField puede usarse para establecer SQL_SOPT_SS_NAME_SCOPE en el descriptor de parámetro de aplicación (APD) a los valores SQL_SS_NAME_SCOPE_EXTENDED y SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET.  
  
 Para obtener más información, consulte [Sparse Columns Support &#40;ODBC&#41;](../native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLSetDescField](https://go.microsoft.com/fwlink/?LinkId=80705)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
