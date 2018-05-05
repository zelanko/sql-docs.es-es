---
title: Compatibilidad con API de OLE DB de fecha y hora mejoras | Documentos de Microsoft
description: Compatibilidad con la API de OLE DB para mejoras de fecha y hora
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b3ccbf0a43cd64acb69c084ce75cb3673f38a8f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Compatibilidad con API de OLE DB de fecha y hora mejoras
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Las siguientes API de OLE DB son compatibles con las características mejoradas de fecha y hora.  
  
|Función|Description|  
|--------------|-----------------|  
|IAccessor:: CreateAccessor|Se agrega una marca de la estructura DBBINDING para habilitar las aplicaciones distinguir entre los **datetime**, **datetime2**, y **smalldatetime** valores. Para obtener más información, consulte [parámetros y Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|Ibcpsession:: BCPColFmt|Para obtener más información, consulte [cambios en la copia masiva para tipos mejorada de fecha y hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md).|  
|ICommandWithParameters::GetParameterInfo|Para obtener más información, consulte[parámetros y Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|ICommandWithParameters:: SetParameterInfo|Para obtener más información, consulte[parámetros y Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Para obtener más información, consulte[parámetros y Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Para obtener más información, consulte[parámetros y Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Para obtener detalles de los conjuntos de filas de esquema afectados, consulte[fecha y hora y conjuntos de filas de esquema](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md).|  
|IRowsetFastLoad|Esta interfaz admite los nuevos tipos de fecha y hora, pero no hay ningún cambio en su interfaz.|  
|ITableDefinition:: CreateTable|Para obtener más información, consulte [compatibilidad de tipos de datos para mejoras de hora y fecha de OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Vea también  
 [Fecha y hora mejoras & #40; OLE DB & #41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
