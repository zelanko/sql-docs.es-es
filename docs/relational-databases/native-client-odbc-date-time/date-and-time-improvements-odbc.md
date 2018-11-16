---
title: Mejoras de fecha y hora (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6669ab863896acd9633171fd4c3e7330f9edd74f
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51659814"
---
# <a name="date-and-time-improvements-odbc"></a>Mejoras en la fecha y la hora (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ha introducido nuevos tipos de datos de fecha y hora. En esta sección se describe la forma en que estos nuevos tipos se exponen como extensiones en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  Para obtener información general de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client con la nueva fecha y tipos de datos de hora, vea [mejoras de fecha y hora](../../relational-databases/native-client/features/date-and-time-improvements.md). Para obtener un ejemplo que muestra la compatibilidad de la fecha y hora ODBC, vea [Use tipos de fecha y hora](../../relational-databases/native-client-odbc-how-to/use-date-and-time-types.md).  
  
 Para obtener información general acerca de los tipos de datos de fecha y hora, vea [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Compatibilidad con tipos de datos para mejoras de fecha y hora de ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 Proporciona información sobre los tipos ODBC que admiten tipos de fecha y hora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Metadatos &#40;ODBC&#41;](https://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
 Describe la información devuelta en el descriptor de parámetro de implementación (IPD) y de los campos de descriptor (IRD) de fila de implementación, así como los metadatos de columna devueltos por **SQLColumns** y **SQLProcedureColumns**. También se describen los metadatos de tipo de datos devuelto por **SQLGetTypeInfo**.  
  
 [las conversiones de tipos de datos de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-odbc.md)  
 Describe cómo convertir entre valores datetime y datetimeoffset.  
  
 [Compatibilidad con sql_variant para tipos de fecha y hora](../../relational-databases/native-client-odbc-date-time/sql-variant-support-for-date-and-time-types.md)  
 Describe la compatibilidad de la función SQL_VARIANT con la funcionalidad mejorada de fecha y hora.  
  
 [Cambios en la copia de forma masiva para tipos mejorada fecha y hora &#40;de OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Describe las mejoras de fecha y hora para admitir operaciones de copia masiva.  
  
 [Comportamiento con versiones anteriores de SQL Server de tipos mejorada de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 Describe el comportamiento esperado cuando una aplicación cliente mediante las características mejorada fecha y hora se comunica con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y cuando un cliente compilado con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client envía comandos a un servidor que admite mejoradas características de fecha y hora.  
  
 [Las API de ODBC admiten las características mejoradas de fecha y hora](../../relational-databases/native-client-odbc-date-time/odbc-api-support-for-enhanced-date-and-time-features.md)  
 Hace una lista de las funciones ODBC que admiten la funcionalidad mejorada de fecha y hora.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
