---
title: Volver a sincronizar filas | Documentos de Microsoft
description: Volver a sincronizar filas utilizando el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2eab6f3a92154ca5e8c910d03fc477ad3af9d82b
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>Actualizar datos en conjuntos de filas: volver a sincronizar filas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para SQL Server admite **IRowsetResynch** en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatible con cursores conjuntos de filas solo. **IRowsetResynch** no está disponible a petición. El consumidor debe solicitar la interfaz antes de abrir el conjunto de filas.  
  
## <a name="see-also"></a>Vea también  
 [Actualizar datos en conjuntos de filas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
