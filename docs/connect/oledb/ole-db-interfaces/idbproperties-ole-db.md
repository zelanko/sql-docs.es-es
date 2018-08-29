---
title: IDBProperties (OLE DB) | Microsoft Docs
description: Interfaz IDBProperties (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: a5b8c3626cd95d19b6eb79d28d042bed38a4b602
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43017320"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La especificación estándar OLE DB permite a los proveedores especificar VT_EMPTY para **DBPROPINFO::vValues**. En cambio, el controlador OLE DB para SQL Server siempre devuelve VT_EMPTY cuando se llama a **IDBProperties::GetPropertyInfo** con **DBPROPSET_ROWSETALL** para recuperar propiedades de conjuntos de filas.  
  
## <a name="see-also"></a>Ver también  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
