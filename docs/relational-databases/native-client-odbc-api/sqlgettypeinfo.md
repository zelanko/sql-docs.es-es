---
title: SQLGetTypeInfo | Documentos de Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
caps.latest.revision: 47
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 83e8c15c06a3a746ccb70489aefd5981e7458ed6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informes de controladores ODBC de Native Client establece la columna adicional USERTYPE en el resultado de **SQLGetTypeInfo**. USERTYPE notifica la definición de tipo de datos de DB-Library y resulta de gran utilidad para los programadores que migran las aplicaciones existentes de DB-Library a ODBC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata la identidad como un atributo, mientras que ODBC la considera como un tipo de datos. Para resolver este error de coincidencia, **SQLGetTypeInfo** devuelve todos los tipos de datos: **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity**, y **numericidentity**. El **SQLGetTypeInfo** columna AUTO_UNIQUE_VALUE del conjunto de resultados notifica el valor TRUE para estos tipos de datos.  
  
 Para **varchar**, **nvarchar** y **varbinary**, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client seguirá notificando 8000, 4000 y 8000 respectivamente para el valor de COLUMN_SIZE el valor, incluso aunque realmente es ilimitado. El motivo de ello es garantizar la compatibilidad con versiones anteriores.  
  
 Para el **xml** tipo de datos, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client notifica SQL_SS_LENGTH_UNLIMITED para COLUMN_SIZE indicar un tamaño ilimitado.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo y parámetros con valores de tabla  
 El tipo de tabla para los parámetros con valores de tabla es efectivamente un metatipo, es decir, un tipo que se utiliza para definir otros tipos. Por lo tanto, no tiene que exponerse a través de SQLGetTypeInfo. Aplicaciones deben usar SQLTables, en lugar de SQLGetTypeInfo, para recuperar los metadatos para los tipos de tabla que se utilizan parámetros con valores de tabla.  
  
 Para obtener más información acerca de cómo recuperar metadatos para los parámetros con valores de tabla, vea [atributos de instrucción que parámetros Affect Table-Valued](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>SQLGetTypeInfo admite las características mejoradas de fecha y hora  
 Para los valores devueltos para los tipos de fecha y hora, vea [metadatos de catálogo](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obtener más información, consulte [fecha y hora mejoras &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Compatibilidad de SQLGetTypeInfo para UDT CLR grandes  
 **SQLGetTypeInfo** admite tipos de definidos por el usuario CLR (UDT) grandes. Para obtener más información, consulte [Large CLR User-Defined tipos & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLGetTypeInfo, función](http://go.microsoft.com/fwlink/?LinkId=59356)   
 [Detalles de implementación de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
