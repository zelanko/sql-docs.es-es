---
title: Conjunto de filas LINKEDSERVERS (OLE DB) | Microsoft Docs
description: Conjunto de filas LINKEDSERVERS (OLE DB)
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
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 9fe4ab1b6fd245bdb7ac0bd08acb0564742e1188
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694953"
---
# <a name="schema-rowsets---linkedservers-rowset"></a>Conjuntos de filas de esquema: conjunto de filas LINKEDSERVERS
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El conjunto de filas **LINKEDSERVERS** enumera los orígenes de datos de la organización que pueden participar en consultas distribuidas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 El conjunto de filas **LINKEDSERVERS** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Descripción|  
|-----------------|--------------------|-----------------|  
|SVR_NAME|DBTYPE_WSTR|Nombre de un servidor vinculado.|  
|SVR_PRODUCT|DBTYPE_WSTR|Fabricante u otro nombre que identifica el tipo de almacén de datos representado por el nombre del servidor vinculado.|  
|SVR_PROVIDERNAME|DBTYPE_WSTR|Nombre descriptivo del proveedor OLE DB que se usa para consumir datos del servidor.|  
|SVR_DATASOURCE|DBTYPE_WSTR|Cadena DBPROP_INIT_DATASOURCE de OLE DB que se usa para adquirir un origen de datos del proveedor.|  
|SVR_PROVIDERSTRING|DBTYPE_WSTR|Valor DBPROP_INIT_PROVIDERSTRING de OLE DB que se usa para adquirir un origen de datos del proveedor.|  
|SVR_LOCATION|DBTYPE_WSTR|Cadena OLE DB DBPROP_INIT_LOCATION de OLE DB que se usa para adquirir un origen de datos del proveedor.|  
  
 El conjunto de filas está ordenado en SRV_NAME y se admite una restricción única en SRV_NAME.  
  
## <a name="see-also"></a>Ver también  
 [Compatibilidad con conjuntos de filas de esquema &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)  
  
  
