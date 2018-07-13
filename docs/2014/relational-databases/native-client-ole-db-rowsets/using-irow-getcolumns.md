---
title: 'Mediante IRow:: GetColumns | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21046f1ab8c25a9f929f8e6cf95281e74c157ae6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430054"
---
# <a name="using-irowgetcolumns"></a>Usar IRow::GetColumns
  El **IRow** implementación permite el acceso secuencial de solo avance a las columnas. Puede obtener acceso a todas las columnas de la fila con una sola llamada a **IRow:: GetColumns** o llamar a **IRow:: GetColumns** varias veces cada vez que tenga acceso de varias columnas en la fila.  
  
 Varias llamadas a **IRow:: GetColumns** no debe superponerse. Por ejemplo, si la primera llamada a **IRow:: GetColumns** recupera columnas 1, 2 y 3, la segunda llamada a **IRow:: GetColumns** debe llamar a las columnas 4, 5 y 6. Si las llamadas posteriores a **IRow:: GetColumns** se superponen, el indicador de estado (campo dwstatus en DBCOLUMNACCESS) se establece en DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Vea también  
 [Capturar una única fila con IRow](fetching-a-single-row-with-irow.md)  
  
  
