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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef6334f6fe4671f2563add857f6dd58ce67a2840
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63237844"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Compatibilidad de API de OLE DB con las mejoras de fecha y hora
  Las siguientes API de OLE DB son compatibles con las características mejoradas de fecha y hora.  
  
|Función|Descripción|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Se agrega una marca en la estructura DBBINDING para habilitar las aplicaciones para diferenciar entre valores `datetime`, `datetime2` y `smalldatetime`. Para obtener más información, consulte [Parameter and Rowset Metadata](metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Para obtener más información, consulte [cambios de copia masiva para tipos mejorada de fecha y hora &#40;OLE DB y ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).|  
|ICommandWithParameters::GetParameterInfo|Para obtener más información, consulte[Parameter and Rowset Metadata](metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Para obtener más información, consulte[Parameter and Rowset Metadata](metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Para obtener más información, consulte[Parameter and Rowset Metadata](metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Para obtener más información, consulte[Parameter and Rowset Metadata](metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Para obtener detalles de los conjuntos de filas de esquema afectados, consulte[fecha y hora y conjuntos de filas de esquema](../native-client-ole-db-rowsets/rowsets.md).|  
|IRowsetFastLoad|Esta interfaz admite los nuevos tipos de fecha y hora, pero no hay ningún cambio en su interfaz.|  
|ITableDefinition::CreateTable|Para obtener más información, consulte [compatibilidad con tipos de datos para OLE DB mejoras de fecha y hora](data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Vea también  
 [Mejoras de fecha y hora &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
