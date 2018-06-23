---
title: 'Mediante IRow:: GetColumns | Documentos de Microsoft'
description: 'Mediante IRow:: GetColumns para tener acceso a todas las columnas de una fila'
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
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: be29bec8c92036b6d53a56f4aab8ccdfc8e8c369
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2018
ms.locfileid: "35690058"
---
# <a name="using-irowgetcolumns"></a>Usar IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El **IRow** implementación permite el acceso secuencial de solo avance y solo a las columnas. Se pueden tener acceso a todas las columnas de la fila con una sola llamada a **IRow:: GetColumns** o llamar a **IRow:: GetColumns** varias veces, cada vez que tener acceso a varias columnas de la fila.  
  
 Varias llamadas a **IRow:: GetColumns** no debe superponerse. Por ejemplo, si la primera llamada a **IRow:: GetColumns** recupera columnas 1, 2 y 3, la segunda llamada a **IRow:: GetColumns** debería llamar a para las columnas 4, 5 y 6. Si más adelante se llama a **IRow:: GetColumns** se superponen, el indicador de estado (campo dwstatus en DBCOLUMNACCESS) se establece en DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Vea también  
 [Capturar una única fila con IRow](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
