---
title: Conjunto de filas LINKEDSERVERS (OLE DB) | Documentos de Microsoft
description: Conjunto de filas LINKEDSERVERS (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- LINKEDSERVERS rowset
- enumerating data sources [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ff4c35178b5cc047fb711821b332f43cf0094fc8
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2018
ms.locfileid: "35611730"
---
# <a name="schema-rowsets---linkedservers-rowset"></a>Conjuntos de filas de esquema: conjunto de filas LINKEDSERVERS
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El **LINKEDSERVERS** conjunto de filas enumera los orígenes de datos de organización que pueden participar en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consultas distribuidas.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con el conjunto de filas de esquema &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)  
  
  
