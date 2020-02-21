---
title: Mejoras de fecha y hora (OLE DB) | Microsoft Docs
description: Mejoras de fecha y hora (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c4a93078b84cf5146f94043496bea0fdaed9fc80
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015706"
---
# <a name="date-and-time-improvements-ole-db"></a>Mejoras en la fecha y la hora (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] introduce nuevos tipos de datos de fecha y hora. En esta sección se describe la forma en que estos nuevos tipos se exponen como extensiones en OLE DB Driver for SQL Server. Para obtener información general sobre la compatibilidad de OLE DB Driver for SQL Server con los nuevos tipos de datos de fecha y hora, consulte [Mejoras de fecha y hora](../../oledb/features/date-and-time-improvements.md). Para obtener un ejemplo, consulte [Usar las características mejoradas de fecha y hora &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md).  
  
 Para obtener más información general sobre los tipos de datos de fecha y hora, consulte [datetime &#40;Transact-SQL&#41;](../../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Compatibilidad con tipos de datos para mejoras de fecha y hora de OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 Proporciona información sobre los tipos OLE DB (OLE DB Driver for SQL Server) que admiten tipos de datos de fecha y hora de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Metadatos &#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
 Contiene información sobre la estructura DBBINDING, **ICommandWithParameters::GetParameterInfo**, **ICommandWithParameters::SetParameterInfo**, **IColumnsRowset::GetColumnsRowset** e I**ColumnsInfo::GetColumnInfo**. También proporciona información sobre actualizaciones a conjuntos de filas de esquema de OLE DB.  
  
 [Enlaces y conversiones &#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
 Describe las reglas para realizar conversiones entre el servidor y el cliente tanto para tipos de datos existentes como nuevos.  
  
 [Cambios de copia masiva para tipos de fecha y hora mejorados &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)  
 Describe las mejoras de fecha y hora para admitir operaciones de copia masiva.  
  
 [Compatibilidad de API de OLE DB con las mejoras de fecha y hora](../../oledb/ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 Describe las API de OLE DB que admiten las características mejoradas de fecha y hora.  
  
 [Comparaciones en IRowsetFind](../../oledb/ole-db-date-time/comparability-for-irowsetfind.md)  
 Describe los tipos de fecha y hora e **IRowsetFind**.  
 
  
## <a name="see-also"></a>Consulte también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
