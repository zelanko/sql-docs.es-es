---
title: Siguiente posición de captura (controlador OLE DB) | Microsoft Docs
description: OLE DB Driver for SQL Server realiza el seguimiento de la posición de captura siguiente para que una secuencia de llamadas al método GetNextRows lea el conjunto de filas completo.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ba713e9da40255d992e7cccf8c8430a205cadf4
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861583"
---
# <a name="fetching-rows---next-fetch-position-ole-db-driver"></a>Captura de filas: siguiente posición de captura (controlador OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server realiza el seguimiento de la siguiente posición de captura para que una secuencia de llamadas al método **GetNextRows** (sin saltos, cambios de dirección ni llamadas interpuestas a métodos **FindNextRow**, **Seek** o **RestartPosition**) lea el conjunto de filas completo sin omitir ni repetir ninguna fila. La siguiente posición de captura cambia mediante una llamada a **IRowset::GetNextRows**, **IRowset::RestartPosition** o **IRowsetIndex::Seek**, o bien mediante una llamada a **FindNextRow** con un valor *pBookmark* NULL. La llamada a **FindNextRow** con un valor *pBookmark* que no sea NULL no afecta a la siguiente posición de captura.  
  
## <a name="see-also"></a>Consulte también  
 [Capturar filas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
