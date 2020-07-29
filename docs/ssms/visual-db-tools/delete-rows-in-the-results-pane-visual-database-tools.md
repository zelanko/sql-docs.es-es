---
title: Eliminar filas en el panel de resultados
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- removing rows
- row removal [SQL Server], Visual Database Tools Results pane
- row deletions [SQL Server], Visual Database Tools Results pane
- Query Designer [SQL Server], Results pane
- deleting rows
- Results pane
ms.assetid: a1147905-fe4a-4fac-b576-a17622477e66
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 71e70000e6a4b1c6208e19f5d233f44fb31b965b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008338"
---
# <a name="delete-rows-in-the-results-pane-visual-database-tools"></a>Eliminar filas en el panel Resultados (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Elimine las filas en el panel Resultados si desea quitar los registros en la base de datos. Si desea eliminar todas las filas, puede utilizar una consulta Delete. Para más información, consulte [Crear consultas de eliminación &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md). Si desea eliminar las filas únicamente en el panel Resultados, cambie los criterios de la consulta. Para más información, consulte [Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md).  
  
### <a name="to-delete-a-row-or-rows"></a>Para eliminar una o varias filas  
  
1.  Seleccione el cuadro situado a la izquierda de la fila o filas que desea eliminar en el panel Resultados.  
  
2.  Presione SUPR.  
  
3.  En el cuadro de mensaje de confirmación, haga clic en **Sí**.  
  
> [!CAUTION]  
> Las filas que se eliminen de este modo se quitarán definitivamente de la base de datos y no se podrán recuperar.  
  
> [!NOTE]  
> Si alguna de las filas seleccionadas no se pudiera eliminar de la base de datos, no se suprimirá ninguna y aparecerá un mensaje en el que se indicarán las filas que no se han podido eliminar.  
  
## <a name="see-also"></a>Consulte también  
[Crear consultas de eliminación &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md)  
[Especificar criterios de búsqueda (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
