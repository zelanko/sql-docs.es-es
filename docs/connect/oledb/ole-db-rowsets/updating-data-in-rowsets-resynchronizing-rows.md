---
title: Volver a sincronizar filas | Documentos de Microsoft
description: Volver a sincronizar filas utilizando el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 99e355ded49f480a6ac0f27dc700d96c8ced9e87
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2018
ms.locfileid: "35690248"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>Actualizar datos en conjuntos de filas: volver a sincronizar filas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server admite **IRowsetResynch** en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatible con cursores conjuntos de filas solo. **IRowsetResynch** no está disponible a petición. El consumidor debe solicitar la interfaz antes de abrir el conjunto de filas.  
  
## <a name="see-also"></a>Vea también  
 [Actualizar datos en conjuntos de filas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
