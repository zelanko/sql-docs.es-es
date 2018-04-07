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
- drivers
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
ms.openlocfilehash: 7c5870fefce6e4d989235f5ec1d0672e4b77866d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="fetching-rows---next-fetch-position"></a>Obteniendo filas - siguiente posición de captura
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para SQL Server mantiene un seguimiento de la siguiente posición de captura hasta que una secuencia de llamadas a la **GetNextRows** método (sin saltos, cambios de dirección o intervención llamadas a la **FindNextRow** **Seek**, o **RestartPosition** métodos) lee el conjunto de filas completo sin omitir ni repetir ninguna fila. La siguiente posición de captura cambia mediante una llamada a **IRowset:: GetNextRows**, **IRowset:: RestartPosition**, o **IRowsetIndex:: Seek**, o mediante una llamada a **FindNextRow** con un valor null *pBookmark* valor. Al llamar a **FindNextRow** con un NULL *pBookmark* valor no afecta a la siguiente posición de captura.  
  
## <a name="see-also"></a>Vea también  
 [Captura de filas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
