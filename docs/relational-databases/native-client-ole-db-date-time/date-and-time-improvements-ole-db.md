---
description: SQL Server Native Client mejoras de fecha y hora (OLE DB)
title: Mejoras en la fecha y la hora (OLE DB)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
author: markingmyname
ms.author: maghan
ms.custom: seo-dt-2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7d6afbedc35ca1da8f3d9325fc4721d92062f4d2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97435023"
---
# <a name="sql-server-native-client-date-and-time-improvements-ole-db"></a>SQL Server Native Client mejoras de fecha y hora (OLE DB)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduce nuevos tipos de datos de fecha y hora. En esta sección se describe la forma en que estos nuevos tipos se exponen como extensiones en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  Para obtener información general de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compatibilidad de Native Client con los nuevos tipos de datos de fecha y hora, vea [mejoras de fecha y hora](../../relational-databases/native-client/features/date-and-time-improvements.md). Para obtener un ejemplo, consulte [Usar las características mejoradas de fecha y hora &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md).  
  
 Para obtener más información general sobre los tipos de datos de fecha y hora, consulte [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Compatibilidad con tipos de datos para mejoras de fecha y hora de OLE DB](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 Proporciona información sobre los tipos de OLE DB ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client) que admiten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos de fecha y hora.  
  
 [Metadatos &#40;OLE DB&#41;](./data-type-support-for-ole-db-date-and-time-improvements.md)  
 Contiene información sobre la estructura DBBINDING, **ICommandWithParameters::GetParameterInfo**, **ICommandWithParameters::SetParameterInfo**, **IColumnsRowset::GetColumnsRowset** e I **ColumnsInfo::GetColumnInfo**. También proporciona información sobre actualizaciones a conjuntos de filas de esquema de OLE DB.  
  
 [Enlaces y conversiones &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 Describe las reglas para realizar conversiones entre el servidor y el cliente tanto para tipos de datos existentes como nuevos.  
  
 [Cambios de copia masiva para tipos de fecha y hora mejorados &#40;OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Describe las mejoras de fecha y hora para admitir operaciones de copia masiva.  
  
 [Compatibilidad de API de OLE DB con las mejoras de fecha y hora](../../relational-databases/native-client-ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 Describe las API de OLE DB que admiten las características mejoradas de fecha y hora.  
  
 [Comparaciones en IRowsetFind](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 Describe los tipos de fecha y hora e **IRowsetFind**.  
  
 [Nuevas características de fecha y hora con versiones anteriores de SQL Server &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 Describe el comportamiento que se espera cuando una aplicación cliente que utiliza características mejoradas de fecha y hora se comunica con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cuando un cliente compilado con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client envía comandos a un servidor que admite características mejoradas de fecha y hora.  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
