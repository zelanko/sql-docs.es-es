---
title: Compatibilidad de la API de OLE DB con las mejoras de fecha y hora | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, date/time improvements
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
author: rothja
ms.author: jroth
ms.openlocfilehash: cdb17f0d2104373ea797ff9403cc417dfaa3d868
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056255"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Compatibilidad de API de OLE DB con las mejoras de fecha y hora
  Las siguientes API de OLE DB son compatibles con las características mejoradas de fecha y hora.  
  
|Función|Descripción|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Se agrega una marca en la estructura DBBINDING para habilitar las aplicaciones para diferenciar entre valores `datetime`, `datetime2` y `smalldatetime`. Para más información, consulte [Parámetros y metadatos de conjuntos de filas](metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Para obtener más información, vea [cambios de copia masiva para tipos de fecha y hora mejorados &#40;OLE DB y ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).|  
|ICommandWithParameters::GetParameterInfo|Para más información, consulte [Parámetros y metadatos de conjuntos de filas](metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Para más información, consulte [Parámetros y metadatos de conjuntos de filas](metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Para más información, consulte [Parámetros y metadatos de conjuntos de filas](metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Para más información, consulte [Parámetros y metadatos de conjuntos de filas](metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Para obtener detalles de los conjuntos de filas de esquema afectados, consulte [Fecha y hora y conjuntos de filas de esquema](../native-client-ole-db-rowsets/rowsets.md).|  
|IRowsetFastLoad|Esta interfaz admite los nuevos tipos de fecha y hora, pero no hay ningún cambio en su interfaz.|  
|ITableDefinition::CreateTable|Para obtener más información [Compatibilidad con tipos de datos para mejoras de fecha y hora de OLE DB](data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Consulte también  
 [Mejoras de fecha y hora &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
