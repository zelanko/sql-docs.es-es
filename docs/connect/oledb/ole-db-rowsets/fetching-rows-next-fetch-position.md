---
title: Posición de captura siguiente | Documentos de Microsoft
description: Obteniendo filas - siguiente posición de captura
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-rowsets
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
ms.openlocfilehash: b3e7bb16d9f2c04525a0646b9f4647fdd1e811e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="fetching-rows---next-fetch-position"></a>Obteniendo filas - siguiente posición de captura
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para SQL Server mantiene un seguimiento de la siguiente posición de captura hasta que una secuencia de llamadas a la **GetNextRows** método (sin saltos, cambios de dirección o intervención llamadas a la **FindNextRow** **Seek**, o **RestartPosition** métodos) lee el conjunto de filas completo sin omitir ni repetir ninguna fila. La siguiente posición de captura cambia mediante una llamada a **IRowset:: GetNextRows**, **IRowset:: RestartPosition**, o **IRowsetIndex:: Seek**, o mediante una llamada a **FindNextRow** con un valor null *pBookmark* valor. Al llamar a **FindNextRow** con un NULL *pBookmark* valor no afecta a la siguiente posición de captura.  
  
## <a name="see-also"></a>Vea también  
 [Captura de filas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
