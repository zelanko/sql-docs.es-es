---
title: SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 81ba57c6e66f156f13055ff5ec941fa8f0c86381
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298457"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client notifica la columna adicional USERTYPE en el conjunto de resultados de **SQLGetTypeInfo**. USERTYPE notifica la definición de tipo de datos de DB-Library y resulta de gran utilidad para los programadores que migran las aplicaciones existentes de DB-Library a ODBC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata la identidad como un atributo, mientras que ODBC la considera como un tipo de datos. Para resolver esta falta de coincidencia, **SQLGetTypeInfo** devuelve los tipos de datos: **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity**y **numericidentity**. La columna del conjunto de resultados **SQLGetTypeInfo** AUTO_UNIQUE_VALUE notifica el valor true para estos tipos de datos.  
  
 En **VARCHAR**, **nvarchar** y **varbinary**, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client continúa notificando 8000, 4000 y 8000, respectivamente para el valor COLUMN_SIZE, aunque realmente es ilimitado. El motivo de ello es garantizar la compatibilidad con versiones anteriores.  
  
 En el **xml** caso del tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML, el controlador ODBC de Native Client informa SQL_SS_LENGTH_UNLIMITED de COLUMN_SIZE para indicar un tamaño ilimitado.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo y parámetros con valores de tabla  
 El tipo de tabla para los parámetros con valores de tabla es realmente un metatipo, es decir, un tipo que se usa para definir otros tipos. Por lo tanto, no tiene que exponerse a través de SQLGetTypeInfo. Las aplicaciones deben usar SQLTables, en lugar de SQLGetTypeInfo, para recuperar los metadatos de los tipos de tabla utilizados con parámetros con valores de tabla.  
  
 Para obtener más información sobre la recuperación de metadatos para los parámetros con valores de tabla, vea [atributos de instrucción que afectan a los parámetros con valores de tabla](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Para obtener más información sobre los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>SQLGetTypeInfo admite las características mejoradas de fecha y hora  
 Para obtener los valores devueltos para los tipos de fecha y hora, vea [Catalog Metadata](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obtener más información general, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Compatibilidad de SQLGetTypeInfo para UDT CLR grandes  
 **SQLGetTypeInfo** admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [tipos CLR grandes definidos por el usuario &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLGetTypeInfo función)](https://go.microsoft.com/fwlink/?LinkId=59356)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
