---
title: Conjunto de filas LINKEDSERVERS (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- LINKEDSERVERS rowset
- enumerating data sources [OLE DB]
ms.assetid: 2633fd8a-65e7-498d-9aed-8e4b1cca2381
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ee680d645c40a8471920ce8f8e259f45a9401306
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47760403"
---
# <a name="schema-rowsets---linkedservers-rowset"></a>Conjuntos de filas de esquema: conjunto de filas LINKEDSERVERS
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

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
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con conjuntos de filas de esquema &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)  
  
  
