---
title: Mejoras de fecha y hora (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC]
- ODBC, date/time improvements
ms.assetid: e31d5ca5-2103-498f-954c-1ee93e217186
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d56689bb045a6540bfdfbb9c7147dc34db110bde
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63207006"
---
# <a name="date-and-time-improvements-odbc"></a>Mejoras en la fecha y la hora (ODBC)
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ha introducido nuevos tipos de datos de fecha y hora. En esta sección se describe la forma en que estos nuevos tipos se exponen como extensiones en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  Para obtener información general de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client con la nueva fecha y tipos de datos de hora, vea [mejoras de fecha y hora](../native-client/features/date-and-time-improvements.md). Para obtener un ejemplo que muestra la compatibilidad de la fecha y hora ODBC, vea [Use tipos de fecha y hora](../native-client-odbc-how-to/use-date-and-time-types.md).  
  
 Para obtener información general acerca de los tipos de datos de fecha y hora, vea [datetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql).  
  
## <a name="in-this-section"></a>En esta sección  
 [Compatibilidad con tipos de datos para mejoras de fecha y hora de ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 Proporciona información sobre los tipos ODBC que admiten tipos de fecha y hora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Metadatos &#40;ODBC&#41;](../../database-engine/dev-guide/metadata-odbc.md)  
 Describe información devuelta en los campos del descriptor de parámetro de implementación (IPD) y el descriptor de fila de implementación (IRD), así como los metadatos de columna devueltos por `SQLColumns` y `SQLProcedureColumns`. También describe metadatos de tipo de datos devueltos por `SQLGetTypeInfo`.  
  
 [las conversiones de tipos de datos de fecha y hora &#40;ODBC&#41;](datetime-data-type-conversions-odbc.md)  
 Describe cómo convertir entre valores datetime y datetimeoffset.  
  
 [Compatibilidad con sql_variant para tipos de fecha y hora](sql-variant-support-for-date-and-time-types.md)  
 Describe la compatibilidad de la función SQL_VARIANT con la funcionalidad mejorada de fecha y hora.  
  
 [Cambios en la copia de forma masiva para tipos mejorada fecha y hora &#40;de OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Describe las mejoras de fecha y hora para admitir operaciones de copia masiva.  
  
 [Comportamiento con versiones anteriores de SQL Server de tipos mejorada de fecha y hora &#40;ODBC&#41;](enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 Describe el comportamiento esperado cuando una aplicación cliente mediante las características mejorada fecha y hora se comunica con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y cuando un cliente compilado con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client envía comandos a un servidor que admite mejoradas características de fecha y hora.  
  
 [Las API de ODBC admiten las características mejoradas de fecha y hora](odbc-api-support-for-enhanced-date-and-time-features.md)  
 Hace una lista de las funciones ODBC que admiten la funcionalidad mejorada de fecha y hora.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
