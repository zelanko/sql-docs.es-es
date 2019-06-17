---
title: SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60c4c4d364f9c07e9ca241dd357535f7f7acb42d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046703"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informes de controladores ODBC de Native Client establece la columna adicional USERTYPE en el resultado de `SQLGetTypeInfo`. USERTYPE notifica la definición de tipo de datos de DB-Library y resulta de gran utilidad para los programadores que migran las aplicaciones existentes de DB-Library a ODBC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata la identidad como un atributo, mientras que ODBC la considera como un tipo de datos. Para resolver este error de coincidencia, `SQLGetTypeInfo` devuelve los tipos de datos: **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity** , y **numericidentity**. La `SQLGetTypeInfo` columna del conjunto de resultados auto_unique_value del notifica el valor TRUE para estos tipos de datos.  
  
 Para **varchar**, **nvarchar** y **varbinary**, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client seguirá notificando 8000, 4000 y 8000 respectivamente para el valor de COLUMN_SIZE valor, incluso aunque realmente es ilimitado. El motivo de ello es garantizar la compatibilidad con versiones anteriores.  
  
 Para el **xml** tipo de datos, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client notifica SQL_SS_LENGTH_UNLIMITED para COLUMN_SIZE denotar un tamaño ilimitado.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo y parámetros con valores de tabla  
 El tipo de tabla para los parámetros con valores de tabla es efectivamente una meta-tipo-que es, un tipo que se usan para definir otros tipos. Por lo tanto, no tiene que exponerse a través de SQLGetTypeInfo. Las aplicaciones deben usar SQLTables, en lugar de SQLGetTypeInfo, para recuperar los metadatos para los tipos de tabla usa parámetros con valores de tabla.  
  
 Para obtener más información acerca de cómo recuperar metadatos para parámetros con valores de tabla, vea [declaración de atributos que los parámetros de Affect Table-Valued](../native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>SQLGetTypeInfo admite las características mejoradas de fecha y hora  
 Para obtener los valores devueltos para los tipos de fecha y hora, vea [Catalog Metadata](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obtener más información, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Compatibilidad de SQLGetTypeInfo para UDT CLR grandes  
 `SQLGetTypeInfo` admite tipos CLR definidos por el usuario (UDT) grandes. Para obtener más información, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Función SQLGetTypeInfo](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
