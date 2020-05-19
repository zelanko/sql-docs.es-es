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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4237ebcc22318fdd6a93af09a79d7f8e2bea8989
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705992"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client notifica la columna adicional USERTYPE en el conjunto de resultados de `SQLGetTypeInfo` . USERTYPE notifica la definición de tipo de datos de DB-Library y resulta de gran utilidad para los programadores que migran las aplicaciones existentes de DB-Library a ODBC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata la identidad como un atributo, mientras que ODBC la considera como un tipo de datos. Para resolver esta falta de coincidencia, `SQLGetTypeInfo` devuelve los tipos de datos: **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity**y **numericidentity**. La `SQLGetTypeInfo` columna del conjunto de resultados AUTO_UNIQUE_VALUE notifica el valor true para estos tipos de datos.  
  
 En **VARCHAR**, **nvarchar** y **varbinary**, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client continúa notificando 8000, 4000 y 8000, respectivamente para el valor COLUMN_SIZE, aunque realmente es ilimitado. El motivo de ello es garantizar la compatibilidad con versiones anteriores.  
  
 En el caso del tipo de datos **XML** , el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client informa SQL_SS_LENGTH_UNLIMITED de COLUMN_SIZE para indicar un tamaño ilimitado.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo y parámetros con valores de tabla  
 El tipo de tabla para los parámetros con valores de tabla es realmente un metatipo, es decir, un tipo que se usa para definir otros tipos. Por lo tanto, no tiene que exponerse a través de SQLGetTypeInfo. Las aplicaciones deben usar SQLTables, en lugar de SQLGetTypeInfo, para recuperar los metadatos de los tipos de tabla utilizados con parámetros con valores de tabla.  
  
 Para obtener más información sobre la recuperación de metadatos para los parámetros con valores de tabla, vea [atributos de instrucción que afectan a los parámetros con valores de tabla](../native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Para obtener más información sobre los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>SQLGetTypeInfo admite las características mejoradas de fecha y hora  
 Para obtener los valores devueltos para los tipos de fecha y hora, vea [Catalog Metadata](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obtener más información general, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Compatibilidad de SQLGetTypeInfo para UDT CLR grandes  
 `SQLGetTypeInfo` admite tipos CLR definidos por el usuario (UDT) grandes. Para obtener más información, vea [tipos CLR grandes definidos por el usuario &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLGetTypeInfo función)](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
