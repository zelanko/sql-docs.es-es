---
title: Actualización de datos en conjuntos de filas (controlador OLE DB)
description: Obtenga información sobre cómo OLE DB Driver for SQL Server actualiza los datos de SQL Server cuando un consumidor actualiza un conjunto de filas modificable que contiene esos datos.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, updating data
- OLE DB Driver for SQL Server, data updates
- data updates [SQL Server], OLE DB
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 40bb8663cd2d49ceaeda2305797fb42bdacc4324
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859952"
---
# <a name="updating-data-in-rowsets"></a>Actualizar datos en conjuntos de filas
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server actualiza los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando un consumidor actualiza un conjunto de filas modificable que contiene esos datos. Se crea un conjunto de filas modificable cuando el consumidor solicita compatibilidad para las interfaces **IRowsetUpdate** o **IRowsetChange**.  
  
 Todos los conjuntos de filas modificables de OLE DB Driver for SQL Server usan cursores [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para admitir el conjunto de filas. La propiedad de conjunto de filas DBPROP_LOCKMODE modifica el comportamiento de control de simultaneidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en cursores y determina el comportamiento de la captura de filas del conjunto de filas y la generación de errores de integridad de datos en los conjuntos de filas actualizables.  
  
 OLE DB Driver for SQL Server admite la sincronización de filas antes o después de una actualización.  
  
> [!NOTE]  
>  IRowChange::SetColumns está disponible para establecer los valores de una o más columnas con nombre de un objeto de fila.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Actualizar datos en cursores de SQL Server](../../oledb/ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [Volver a sincronizar filas](../../oledb/ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
