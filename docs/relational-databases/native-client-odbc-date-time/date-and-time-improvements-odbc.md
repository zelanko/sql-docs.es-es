---
title: Fecha y hora mejoras (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC]
- ODBC, date/time improvements
ms.assetid: e31d5ca5-2103-498f-954c-1ee93e217186
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cce440e7ff1dad34af5a80ad8a6a70fbaa892247
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="date-and-time-improvements-odbc"></a>Fecha y hora mejoras (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ha introducido nuevos tipos de datos de fecha y hora. En esta sección se describe la forma en que estos nuevos tipos se exponen como extensiones en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  Para obtener información general de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para el nuevo valor de fecha y tipos de datos de hora, vea [fecha y hora mejoras](../../relational-databases/native-client/features/date-and-time-improvements.md). Para obtener un ejemplo que muestra la compatibilidad de la fecha y hora ODBC, vea [Use tipos de fecha y hora](../../relational-databases/native-client-odbc-how-to/use-date-and-time-types.md).  
  
 Para obtener más información acerca de los tipos de datos de fecha y hora, vea [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Compatibilidad con tipos de datos para mejoras de fecha y hora de ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 Proporciona información sobre los tipos ODBC que admiten tipos de fecha y hora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Metadatos &#40;ODBC&#41;](http://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
 Describe la información devuelta en el descriptor de parámetro de implementación (IPD) y sus campos de descriptor (IRD) de fila de implementación, así como los metadatos de columna devueltos por **SQLColumns** y **SQLProcedureColumns**. También describe los metadatos de tipo de datos devuelto por **SQLGetTypeInfo**.  
  
 [Conversiones de tipos de datos de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-odbc.md)  
 Describe cómo convertir entre valores datetime y datetimeoffset.  
  
 [Compatibilidad con sql_variant para tipos de fecha y hora](../../relational-databases/native-client-odbc-date-time/sql-variant-support-for-date-and-time-types.md)  
 Describe la compatibilidad de la función SQL_VARIANT con la funcionalidad mejorada de fecha y hora.  
  
 [Cambios en la copia de forma masiva para tipos mejorada fecha y hora &#40;de OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Describe las mejoras de fecha y hora para admitir operaciones de copia masiva.  
  
 [Comportamiento con versiones anteriores de SQL Server el tipo mejoradas de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 Describe el comportamiento esperado cuando una aplicación cliente mediante las características mejorada fecha y hora se comunica con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y cuando un cliente compilado con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client envía comandos a un servidor que admite características de fecha y hora mejoradas.  
  
 [Las API de ODBC admiten las características mejoradas de fecha y hora](../../relational-databases/native-client-odbc-date-time/odbc-api-support-for-enhanced-date-and-time-features.md)  
 Hace una lista de las funciones ODBC que admiten la funcionalidad mejorada de fecha y hora.  
  
## <a name="see-also"></a>Vea también  
 [Cliente nativo de SQL Server & #40; ODBC & #41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
