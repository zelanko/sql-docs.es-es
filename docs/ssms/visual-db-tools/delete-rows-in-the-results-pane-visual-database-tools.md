---
title: Eliminar filas en el panel Resultados (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- View Designer, Results pane
- removing rows
- row removal [SQL Server], Visual Database Tools Results pane
- row deletions [SQL Server], Visual Database Tools Results pane
- Query Designer [SQL Server], Results pane
- deleting rows
- Results pane
ms.assetid: a1147905-fe4a-4fac-b576-a17622477e66
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b63dddd7dc856409e81a0b5ff62998a3eb91fd1b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="delete-rows-in-the-results-pane-visual-database-tools"></a>Eliminar filas en el panel Resultados (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Elimine las filas en el panel Resultados si quiere quitar registros de la base de datos. Si desea eliminar todas las filas, puede utilizar una consulta Delete. Para más información, consulte [Crear consultas de eliminación &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md). Si desea eliminar las filas únicamente en el panel Resultados, cambie los criterios de la consulta. Para más información, consulte [Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md).  
  
### <a name="to-delete-a-row-or-rows"></a>Para eliminar una o varias filas  
  
1.  Seleccione el cuadro situado a la izquierda de la fila o filas que desea eliminar en el panel Resultados.  
  
2.  Presione SUPR.  
  
3.  En el cuadro de mensaje de confirmación, haga clic en **Sí**.  
  
> [!CAUTION]  
> Las filas que se eliminen de este modo se quitarán definitivamente de la base de datos y no se podrán recuperar.  
  
> [!NOTE]  
> Si alguna de las filas seleccionadas no se pudiera eliminar de la base de datos, no se suprimirá ninguna y aparecerá un mensaje en el que se indicarán las filas que no se han podido eliminar.  
  
## <a name="see-also"></a>Ver también  
[Crear consultas de eliminación &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md)  
[Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
