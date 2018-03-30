---
title: IDBProperties (OLE DB) | Documentos de Microsoft
description: Interfaz IDBProperties (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea67dba9a2a0f884a297ef0c1fffee053b1cbe8b
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  La especificación estándar OLE DB permite a los proveedores especificar VT_EMPTY para **DBPROPINFO::vValues**. Sin embargo, controlador de OLE DB para OLE DB de SQL Server siempre devuelve VT_EMPTY cuando se llama a **IDBProperties:: GetPropertyInfo** con **DBPROPSET_ROWSETALL** para recuperar las propiedades del conjunto de filas.  
  
## <a name="see-also"></a>Vea también  
 [Interfaces &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
