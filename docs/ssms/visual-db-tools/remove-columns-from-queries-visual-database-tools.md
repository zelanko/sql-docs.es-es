---
title: Quitar columnas de las consultas (Visual Database Tools) | Microsoft Docs
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
- removing columns
- queries [SQL Server], columns
- deleting columns
- dropping columns
ms.assetid: 6d9819b8-ee2f-4838-9713-c5e3ad37ab46
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb5152ae022bd736492f01d2a370443cc42850b5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="remove-columns-from-queries-visual-database-tools"></a>Quitar columnas de las consultas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Si ya no quiere usar una columna en una consulta, puede quitarla. Si lo hace, el Diseñador de consultas y vistas quitará las referencias a la columna de la lista SELECT, la especificación de orden, los criterios de búsqueda, el **panel SQL**y las especificaciones de agrupación existentes.  
  
> [!NOTE]  
> Si desea quitar una columna únicamente de los resultados de una consulta de tipo SELECT, puede hacerlo sin quitarla definitivamente de la consulta. Para detalles, consulte [Quitar columnas de los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md).  
  
### <a name="to-remove-a-column-from-the-query"></a>Para quitar una columna de la consulta  
  
-   En el **panel Criterios**, seleccione la fila de cuadrícula que contiene la columna que desea quitar y, luego, presione la tecla SUPR.  
  
    -O bien-  
  
-   Quite todas las referencias a la columna en el [panel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
## <a name="see-also"></a>Ver también  
[Agregar columnas a las consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Realizar operaciones básicas con consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
