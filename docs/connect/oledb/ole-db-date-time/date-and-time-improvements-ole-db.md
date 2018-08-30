---
title: Mejoras de fecha y hora (OLE DB) | Microsoft Docs
description: Mejoras de fecha y hora (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 5bcfb89323051470dc307a8b4828ee6d8dc000a5
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025784"
---
# <a name="date-and-time-improvements-ole-db"></a>Mejoras en la fecha y la hora (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] introduce nuevos tipos de datos de fecha y hora. Esta sección describe cómo se exponen estos nuevos tipos como extensiones en el controlador de OLE DB para SQL Server. Para obtener información general del controlador OLE DB para compatibilidad de SQL Server para la nueva fecha y tipos de datos de tiempo, consulte [mejoras de fecha y hora](../../oledb/features/date-and-time-improvements.md). Para obtener un ejemplo, vea [mejoradas de fecha de uso y las características en tiempo &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md).  
  
 Para obtener información general acerca de los tipos de datos de fecha y hora, vea [datetime &#40;Transact-SQL&#41;](../../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Compatibilidad con tipos de datos para mejoras de fecha y hora de OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 Proporciona información acerca de OLE DB (controlador OLE DB para SQL Server) tipos que admiten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos de fecha y hora.  
  
 [Metadatos &#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
 Contiene información sobre la estructura DBBINDING, **ICommandWithParameters:: GetParameterInfo**, **ICommandWithParameters:: SetParameterInfo**, **IColumnsRowset:: GetColumnsRowset**y yo**ColumnsInfo::GetColumnInfo**. También proporciona información sobre actualizaciones a conjuntos de filas de esquema de OLE DB.  
  
 [Enlaces y conversiones &#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
 Describe las reglas para realizar conversiones entre el servidor y el cliente tanto para tipos de datos existentes como nuevos.  
  
 [Cambios de copia masiva para tipos de fecha y hora mejorados &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)  
 Describe las mejoras de fecha y hora para admitir operaciones de copia masiva.  
  
 [Compatibilidad de API de OLE DB con las mejoras de fecha y hora](../../oledb/ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 Describe las API de OLE DB que admiten las características mejoradas de fecha y hora.  
  
 [Comparaciones en IRowsetFind](../../oledb/ole-db-date-time/comparability-for-irowsetfind.md)  
 Describe los tipos de fecha y hora y **IRowsetFind**.  
 
  
## <a name="see-also"></a>Ver también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
