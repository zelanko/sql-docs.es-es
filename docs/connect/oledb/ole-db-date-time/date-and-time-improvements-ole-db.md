---
title: Fecha y hora mejoras (OLE DB) | Documentos de Microsoft
description: Mejoras de fecha y hora (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b237922b02d8f037f0116452a378c31774a149f1
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="date-and-time-improvements-ole-db"></a>Fecha y hora mejoras (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] introduce nuevos tipos de datos de fecha y hora. Esta sección describe cómo se exponen estos nuevos tipos como extensiones de controlador de OLE DB para SQL Server. Para obtener información general del controlador OLE DB para la compatibilidad con SQL Server para el nuevo valor de fecha y tipos de datos de hora, vea [fecha y hora mejoras](../../oledb/features/date-and-time-improvements.md). Para obtener un ejemplo, vea [características uso mejorado de fecha y hora &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md).  
  
 Para obtener más información acerca de los tipos de datos de fecha y hora, vea [datetime &#40;Transact-SQL&#41;](../../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Compatibilidad con tipos de datos para mejoras de fecha y hora de OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 Proporciona información acerca de OLE DB (controlador OLE DB para SQL Server) que admiten los tipos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos de fecha y hora.  
  
 [Metadatos &#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
 Contiene información acerca de la estructura DBBINDING, **ICommandWithParameters:: GetParameterInfo**, **ICommandWithParameters:: SetParameterInfo**, **IColumnsRowset:: GetColumnsRowset**e I**ColumnsInfo::GetColumnInfo**. También proporciona información sobre actualizaciones a conjuntos de filas de esquema de OLE DB.  
  
 [Enlaces y conversiones &#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
 Describe las reglas para realizar conversiones entre el servidor y el cliente tanto para tipos de datos existentes como nuevos.  
  
 [Cambios en la copia de forma masiva para tipos mejorada fecha y hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)  
 Describe las mejoras de fecha y hora para admitir operaciones de copia masiva.  
  
 [Compatibilidad de API de OLE DB con las mejoras de fecha y hora](../../oledb/ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 Describe las API de OLE DB que admiten las características mejoradas de fecha y hora.  
  
 [Comparaciones en IRowsetFind](../../oledb/ole-db-date-time/comparability-for-irowsetfind.md)  
 Describe los tipos de fecha y hora y **IRowsetFind**.  
 
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para SQL Server &#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
  
  
