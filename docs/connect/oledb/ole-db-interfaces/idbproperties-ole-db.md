---
title: IDBProperties (OLE DB) | Documentos de Microsoft
description: Interfaz IDBProperties (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
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
manager: craigg
ms.openlocfilehash: 6c373967091794a5621c722c084bac7a086bf5a0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  La especificación estándar OLE DB permite a los proveedores especificar VT_EMPTY para **DBPROPINFO::vValues**. Sin embargo, controlador de OLE DB para OLE DB de SQL Server siempre devuelve VT_EMPTY cuando se llama a **IDBProperties:: GetPropertyInfo** con **DBPROPSET_ROWSETALL** para recuperar las propiedades del conjunto de filas.  
  
## <a name="see-also"></a>Vea también  
 [Interfaces & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
