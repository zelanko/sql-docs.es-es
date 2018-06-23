---
title: Posición de captura siguiente | Documentos de Microsoft
description: Obteniendo filas - siguiente posición de captura
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
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 46e6e3b9898d6c1adbe4df4bdc2b33444b623df9
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2018
ms.locfileid: "35690118"
---
# <a name="fetching-rows---next-fetch-position"></a>Obteniendo filas - siguiente posición de captura
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server mantiene un seguimiento de la siguiente posición de captura hasta que una secuencia de llamadas a la **GetNextRows** método (sin saltos, cambios de dirección o intervención llamadas a la **FindNextRow** **Seek**, o **RestartPosition** métodos) lee el conjunto de filas completo sin omitir ni repetir ninguna fila. La siguiente posición de captura cambia mediante una llamada a **IRowset:: GetNextRows**, **IRowset:: RestartPosition**, o **IRowsetIndex:: Seek**, o mediante una llamada a **FindNextRow** con un valor null *pBookmark* valor. Al llamar a **FindNextRow** con un NULL *pBookmark* valor no afecta a la siguiente posición de captura.  
  
## <a name="see-also"></a>Vea también  
 [Capturar filas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
