---
title: 'Mediante IRow:: GetColumns | Documentos de Microsoft'
description: 'Mediante IRow:: GetColumns para tener acceso a todas las columnas de una fila'
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
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d4d42ce2793f2f33ec1fc61b95a52074f0c10705
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-irowgetcolumns"></a>Usar IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El **IRow** implementación permite el acceso secuencial de solo avance y solo a las columnas. Se pueden tener acceso a todas las columnas de la fila con una sola llamada a **IRow:: GetColumns** o llamar a **IRow:: GetColumns** varias veces, cada vez que tener acceso a varias columnas de la fila.  
  
 Varias llamadas a **IRow:: GetColumns** no debe superponerse. Por ejemplo, si la primera llamada a **IRow:: GetColumns** recupera columnas 1, 2 y 3, la segunda llamada a **IRow:: GetColumns** debería llamar a para las columnas 4, 5 y 6. Si más adelante se llama a **IRow:: GetColumns** se superponen, el indicador de estado (campo dwstatus en DBCOLUMNACCESS) se establece en DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Vea también  
 [Capturar una única fila con IRow](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
