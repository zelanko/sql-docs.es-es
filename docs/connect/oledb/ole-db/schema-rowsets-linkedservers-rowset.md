---
title: Conjunto de filas LINKEDSERVERS (OLE DB) | Microsoft Docs
description: El conjunto de filas LINKEDSERVERS enumera los orígenes de datos de la organización que pueden participar en consultas distribuidas de OLE DB Driver for SQL Server.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- LINKEDSERVERS rowset
- enumerating data sources [OLE DB]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1639463992bfffe7ea86a97c43564214a92b2cdb
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861552"
---
# <a name="schema-rowsets---linkedservers-rowset"></a>Conjuntos de filas de esquema: conjunto de filas LINKEDSERVERS
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El conjunto de filas **LINKEDSERVERS** enumera los orígenes de datos de la organización que pueden participar en consultas distribuidas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 El conjunto de filas **LINKEDSERVERS** contiene las siguientes columnas.  
  
|Nombre de la columna|Indicador de tipo|Descripción|  
|-----------------|--------------------|-----------------|  
|SVR_NAME|DBTYPE_WSTR|Nombre de un servidor vinculado.|  
|SVR_PRODUCT|DBTYPE_WSTR|Fabricante u otro nombre que identifica el tipo de almacén de datos representado por el nombre del servidor vinculado.|  
|SVR_PROVIDERNAME|DBTYPE_WSTR|Nombre descriptivo del proveedor OLE DB que se usa para consumir datos del servidor.|  
|SVR_DATASOURCE|DBTYPE_WSTR|Cadena DBPROP_INIT_DATASOURCE de OLE DB que se usa para adquirir un origen de datos del proveedor.|  
|SVR_PROVIDERSTRING|DBTYPE_WSTR|Valor DBPROP_INIT_PROVIDERSTRING de OLE DB que se usa para adquirir un origen de datos del proveedor.|  
|SVR_LOCATION|DBTYPE_WSTR|Cadena OLE DB DBPROP_INIT_LOCATION de OLE DB que se usa para adquirir un origen de datos del proveedor.|  
  
 El conjunto de filas está ordenado en SRV_NAME y se admite una restricción única en SRV_NAME.  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad con conjuntos de filas de esquema &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)  
  
  
