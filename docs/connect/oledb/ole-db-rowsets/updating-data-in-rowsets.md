---
title: Actualizar datos en conjuntos de filas | Documentos de Microsoft
description: Actualizar datos en conjuntos de filas mediante el controlador OLE DB para SQL Server
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
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, updating data
- OLE DB Driver for SQL Server, data updates
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dd1941aed59e16497f081b7d6029a8a3a3582b2f
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="updating-data-in-rowsets"></a>Actualizar datos en conjuntos de filas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para actualizaciones de SQL Server [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datos cuando un consumidor actualiza un conjunto de filas modificable que contiene los datos. Se crea un conjunto de filas modificable cuando el consumidor solicita compatibilidad para la **IRowsetChange** o **IRowsetUpdate** interfaz.  
  
 Todos los controlador OLE DB para su uso de conjuntos de filas modificable de SQL Server [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cursores para admitir el conjunto de filas. La propiedad de conjunto de filas DBPROP_LOCKMODE modifica el comportamiento de control de simultaneidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en cursores y determina el comportamiento de la captura de filas del conjunto de filas y la generación de errores de integridad de datos en los conjuntos de filas actualizables.  
  
 El controlador OLE DB para SQL Server admite la sincronización de fila antes o después de una actualización.  
  
> [!NOTE]  
>  IRowChange::SetColumns está disponible para establecer los valores de una o más columnas con nombre de un objeto de fila.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Actualizar datos en cursores de SQL Server](../../oledb/ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [Volver a sincronizar filas](../../oledb/ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
