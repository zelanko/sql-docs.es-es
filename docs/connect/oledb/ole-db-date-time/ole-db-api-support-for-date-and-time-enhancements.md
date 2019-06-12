---
title: Compatibilidad de la API de OLE DB con las mejoras de fecha y hora | Microsoft Docs
description: Compatibilidad de la API de OLE DB con las mejoras de fecha y hora
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 9819a16a60cc453b8f4277c0fe49053aeca59f48
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66769294"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Compatibilidad de API de OLE DB con las mejoras de fecha y hora
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Las siguientes API de OLE DB son compatibles con las características mejoradas de fecha y hora.  
  
|Función|Descripción|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Se agrega una marca de la estructura DBBINDING para habilitar las aplicaciones para diferenciar entre **datetime**, **datetime2**, y **smalldatetime** valores. Para obtener más información, consulte [Parameter and Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Para obtener más información, consulte [cambios de copia masiva para tipos mejorada de fecha y hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md).|  
|ICommandWithParameters::GetParameterInfo|Para obtener más información, consulte[Parameter and Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Para obtener más información, consulte[Parameter and Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Para obtener más información, consulte[Parameter and Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Para obtener más información, consulte[Parameter and Rowset Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Para obtener detalles de los conjuntos de filas de esquema afectados, consulte[fecha y hora y conjuntos de filas de esquema](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md).|  
|IRowsetFastLoad|Esta interfaz admite los nuevos tipos de fecha y hora, pero no hay ningún cambio en su interfaz.|  
|ITableDefinition::CreateTable|Para obtener más información, consulte [compatibilidad con tipos de datos para OLE DB mejoras de fecha y hora](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Consulte también  
 [Mejoras de fecha y hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
