---
title: Volver a sincronizar filas (controlador OLE DB)
description: Para actualizar los datos en conjuntos de filas, OLE DB Driver for SQL Server admite IRowsetResynch solo en los conjuntos de filas admitidos por el cursor de SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 65ae67a91fc7fb5f3caaa341dbfcb00dc2e5d796
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859963"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>Actualizar datos en conjuntos de filas: volver a sincronizar filas
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server admite **IRowsetResynch** en conjuntos de filas compatibles con cursores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **IRowsetResynch** no está disponible a petición. El consumidor debe solicitar la interfaz antes de abrir el conjunto de filas.  
  
## <a name="see-also"></a>Consulte también  
 [Actualizar datos en conjuntos de filas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
