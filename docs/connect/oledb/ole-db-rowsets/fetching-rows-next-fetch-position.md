---
title: Posición de captura siguiente | Microsoft Docs
description: 'Capturar filas: siguiente posición de captura'
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
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 9e73572d72cb178d254c7bea1318c7fc7c68ab56
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43019892"
---
# <a name="fetching-rows---next-fetch-position"></a>Capturar filas: siguiente posición de captura
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server realiza el seguimiento de la siguiente posición de captura para que una secuencia de llamadas al método **GetNextRows** (sin saltos, cambios de dirección ni llamadas interpuestas a métodos **FindNextRow**, **Seek** o **RestartPosition**) lea el conjunto de filas completo sin omitir ni repetir ninguna fila. La siguiente posición de captura cambia mediante una llamada a **IRowset::GetNextRows**, **IRowset::RestartPosition** o **IRowsetIndex::Seek**, o bien mediante una llamada a **FindNextRow** con un valor *pBookmark* NULL. La llamada a **FindNextRow** con un valor *pBookmark* que no sea NULL no afecta a la siguiente posición de captura.  
  
## <a name="see-also"></a>Ver también  
 [Capturar filas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
