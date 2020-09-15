---
description: Quitar columnas de las consultas (Visual Database Tools)
title: Quitar columnas de consultas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- removing columns
- queries [SQL Server], columns
- deleting columns
- dropping columns
ms.assetid: 6d9819b8-ee2f-4838-9713-c5e3ad37ab46
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 05a761620a0acb4bc799c0163b69a75881425f62
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88313901"
---
# <a name="remove-columns-from-queries-visual-database-tools"></a>Quitar columnas de las consultas (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Si ya no desea utilizar una columna en una consulta, puede quitarla. Si lo hace, el Diseñador de consultas y vistas quitará las referencias a la columna de la lista SELECT, la especificación de orden, los criterios de búsqueda, el **panel SQL**y las especificaciones de agrupación existentes.  
  
> [!NOTE]  
> Si desea quitar una columna únicamente de los resultados de una consulta de tipo SELECT, puede hacerlo sin quitarla definitivamente de la consulta. Para detalles, consulte [Quitar columnas de los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md).  
  
### <a name="to-remove-a-column-from-the-query"></a>Para quitar una columna de la consulta  
  
-   En el **panel Criterios**, seleccione la fila de cuadrícula que contiene la columna que desea quitar y, luego, presione la tecla SUPR.  
  
    o bien  
  
-   Quite todas las referencias a la columna en el [panel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte también  
[Agregar columnas a las consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Realizar operaciones básicas con consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
