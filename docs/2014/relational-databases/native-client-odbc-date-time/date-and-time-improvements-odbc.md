---
title: Mejoras de fecha y hora (ODBC) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6ce8f906fc1949a80bfa8e5a541ecf1e83878775
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020405"
---
# <a name="date-and-time-improvements-odbc"></a>Mejoras en la fecha y la hora (ODBC)
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ha introducido nuevos tipos de datos de fecha y hora. En esta sección se describe la forma en que estos nuevos tipos se exponen como extensiones en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  Para obtener información general de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la compatibilidad de Native Client con los nuevos tipos de datos de fecha y hora, vea [mejoras de fecha y hora](../native-client/features/date-and-time-improvements.md). Para obtener un ejemplo que muestra la compatibilidad de fecha y hora de ODBC, vea [usar tipos de fecha y hora](../native-client-odbc-how-to/use-date-and-time-types.md).  
  
 Para obtener más información general sobre los tipos de datos de fecha y hora, consulte [datetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql).  
  
## <a name="in-this-section"></a>En esta sección  
 [Compatibilidad con tipos de datos para mejoras de fecha y hora de ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 Proporciona información sobre los tipos ODBC que admiten tipos de fecha y hora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Metadatos &#40;&#41;ODBC](../../database-engine/dev-guide/metadata-odbc.md)  
 Describe información devuelta en los campos del descriptor de parámetro de implementación (IPD) y el descriptor de fila de implementación (IRD), así como los metadatos de columna devueltos por `SQLColumns` y `SQLProcedureColumns`. También describe metadatos de tipo de datos devueltos por `SQLGetTypeInfo`.  
  
 [conversiones de tipos de datos datetime &#40;ODBC&#41;](datetime-data-type-conversions-odbc.md)  
 Describe cómo convertir entre valores datetime y datetimeoffset.  
  
 [Compatibilidad con sql_variant para tipos de fecha y hora](sql-variant-support-for-date-and-time-types.md)  
 Describe la compatibilidad de la función SQL_VARIANT con la funcionalidad mejorada de fecha y hora.  
  
 [Cambios de copia masiva para tipos de fecha y hora mejorados &#40;OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Describe las mejoras de fecha y hora para admitir operaciones de copia masiva.  
  
 [Comportamiento mejorado de tipos de fecha y hora con versiones anteriores de SQL Server &#40;ODBC&#41;](enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 Describe el comportamiento esperado cuando una aplicación cliente que usa las características mejoradas de fecha y hora se comunica con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , y cuando un cliente compilado con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client envía comandos a un servidor que admite características mejoradas de fecha y hora.  
  
 [Las API de ODBC admiten las características mejoradas de fecha y hora](odbc-api-support-for-enhanced-date-and-time-features.md)  
 Hace una lista de las funciones ODBC que admiten la funcionalidad mejorada de fecha y hora.  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
