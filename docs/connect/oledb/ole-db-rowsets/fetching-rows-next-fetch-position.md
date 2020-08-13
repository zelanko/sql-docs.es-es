---
title: Siguiente posición de captura (controlador OLE DB) | Microsoft Docs
description: 'Capturar filas: siguiente posición de captura'
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: d6fd65f54f0c6f6aa219595e1948ce758c50b4db
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244206"
---
# <a name="fetching-rows---next-fetch-position-ole-db-driver"></a>Captura de filas: siguiente posición de captura (controlador OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server realiza el seguimiento de la siguiente posición de captura para que una secuencia de llamadas al método **GetNextRows** (sin saltos, cambios de dirección ni llamadas interpuestas a métodos **FindNextRow**, **Seek** o **RestartPosition**) lea el conjunto de filas completo sin omitir ni repetir ninguna fila. La siguiente posición de captura cambia mediante una llamada a **IRowset::GetNextRows**, **IRowset::RestartPosition** o **IRowsetIndex::Seek**, o bien mediante una llamada a **FindNextRow** con un valor *pBookmark* NULL. La llamada a **FindNextRow** con un valor *pBookmark* que no sea NULL no afecta a la siguiente posición de captura.  
  
## <a name="see-also"></a>Consulte también  
 [Capturar filas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
