---
title: Siguiente posición de captura | Microsoft Docs
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
ms.openlocfilehash: 2ea743770323505c611210c0bb3acd0e93c719cd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994190"
---
# <a name="fetching-rows---next-fetch-position"></a>Capturar filas: siguiente posición de captura
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server realiza el seguimiento de la siguiente posición de captura para que una secuencia de llamadas al método **GetNextRows** (sin saltos, cambios de dirección ni llamadas interpuestas a métodos **FindNextRow**, **Seek** o **RestartPosition**) lea el conjunto de filas completo sin omitir ni repetir ninguna fila. La siguiente posición de captura cambia mediante una llamada a **IRowset::GetNextRows**, **IRowset::RestartPosition** o **IRowsetIndex::Seek**, o bien mediante una llamada a **FindNextRow** con un valor *pBookmark* NULL. La llamada a **FindNextRow** con un valor *pBookmark* que no sea NULL no afecta a la siguiente posición de captura.  
  
## <a name="see-also"></a>Consulte también  
 [Capturar filas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
