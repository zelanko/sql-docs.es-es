---
title: Posición de captura siguiente | Documentos de Microsoft
description: Obteniendo filas - siguiente posición de captura
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
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 58dc620996d8cba998ce8efbd5bcd3f3bbfa3e31
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="fetching-rows---next-fetch-position"></a>Obteniendo filas - siguiente posición de captura
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para SQL Server mantiene un seguimiento de la siguiente posición de captura hasta que una secuencia de llamadas a la **GetNextRows** método (sin saltos, cambios de dirección o intervención llamadas a la **FindNextRow** **Seek**, o **RestartPosition** métodos) lee el conjunto de filas completo sin omitir ni repetir ninguna fila. La siguiente posición de captura cambia mediante una llamada a **IRowset:: GetNextRows**, **IRowset:: RestartPosition**, o **IRowsetIndex:: Seek**, o mediante una llamada a **FindNextRow** con un valor null *pBookmark* valor. Al llamar a **FindNextRow** con un NULL *pBookmark* valor no afecta a la siguiente posición de captura.  
  
## <a name="see-also"></a>Vea también  
 [Captura de filas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
