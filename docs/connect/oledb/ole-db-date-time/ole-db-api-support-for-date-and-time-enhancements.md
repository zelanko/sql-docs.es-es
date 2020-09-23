---
title: Compatibilidad de API con las mejoras de fecha y hora (controlador OLE DB)
description: Obtenga información sobre las API de OLE DB que admiten características de fecha y hora mejoradas, incluidos nombres de función y descripciones.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8209c1b1ca6f3c00ce4cd10455c35c8b9d4dfad4
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862348"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Compatibilidad de API de OLE DB con las mejoras de fecha y hora
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Las siguientes API de OLE DB son compatibles con las características mejoradas de fecha y hora.  
  
|Función|Descripción|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Se agrega una marca en la estructura DBBINDING para habilitar las aplicaciones para diferenciar entre valores **datetime**, **datetime2** y **smalldatetime**. Para más información, consulte [Parámetros y metadatos de conjuntos de filas](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Para obtener más información, consulte [Cambios de copia masiva para tipos de fecha y hora mejorados &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md).|  
|ICommandWithParameters::GetParameterInfo|Para más información, consulte [Parámetros y metadatos de conjuntos de filas](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Para más información, consulte [Parámetros y metadatos de conjuntos de filas](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Para más información, consulte [Parámetros y metadatos de conjuntos de filas](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Para más información, consulte [Parámetros y metadatos de conjuntos de filas](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Para obtener detalles de los conjuntos de filas de esquema afectados, consulte [Fecha y hora y conjuntos de filas de esquema](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md).|  
|IRowsetFastLoad|Esta interfaz admite los nuevos tipos de fecha y hora, pero no hay ningún cambio en su interfaz.|  
|ITableDefinition::CreateTable|Para obtener más información [Compatibilidad con tipos de datos para mejoras de fecha y hora de OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Consulte también  
 [Mejoras de fecha y hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
