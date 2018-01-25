---
title: 'Mediante IRow:: GetColumns | Documentos de Microsoft'
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
caps.latest.revision: "30"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eb1111d34d719817838b842e6d69601b2f33f5aa
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2018
---
# <a name="using-irowgetcolumns"></a>Usar IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El **IRow** implementación permite el acceso secuencial de solo avance y solo a las columnas. Se pueden tener acceso a todas las columnas de la fila con una sola llamada a **IRow:: GetColumns** o llamar a **IRow:: GetColumns** varias veces, cada vez que tener acceso a varias columnas de la fila.  
  
 Varias llamadas a **IRow:: GetColumns** no debe superponerse. Por ejemplo, si la primera llamada a **IRow:: GetColumns** recupera columnas 1, 2 y 3, la segunda llamada a **IRow:: GetColumns** debería llamar a para las columnas 4, 5 y 6. Si más adelante se llama a **IRow:: GetColumns** se superponen, el indicador de estado (campo dwstatus en DBCOLUMNACCESS) se establece en DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Vea también  
 [Capturar una única fila con IRow](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
