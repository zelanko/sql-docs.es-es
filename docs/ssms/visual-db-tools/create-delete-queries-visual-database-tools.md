---
title: Crear consultas de eliminación
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- row removal [SQL Server], Delete query
- Delete query
- queries [SQL Server], types
- removing rows
- removing data
- data deletions [SQL Server]
- deleting rows
- deleting data
ms.assetid: 0db3af43-1ec4-48c8-b769-2bb9c76d3434
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: cb40fee1f7176c9d1fe64e22cda220513f88d58e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75254373"
---
# <a name="create-delete-queries-visual-database-tools"></a>Crear consultas de eliminación (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Puede eliminar todas las filas de una tabla utilizando una consulta de eliminación.  
  
> [!NOTE]  
> Cuando se eliminan todas las filas de una tabla, se borran los datos, pero no la tabla. Para eliminar una tabla de una base de datos, haga clic en la tabla con el botón derecho en el Explorador de objetos y haga clic en **Eliminar**.  
  
Cuando se crea una consulta de eliminación, el panel Criterios cambia para reflejar las opciones disponibles para eliminar filas. Dado que en una consulta Eliminar no se muestran datos, se quitan las columnas Resultados, Ordenar por y Criterio de ordenación. Asimismo, como no se pueden especificar columnas individuales para eliminarlas, no aparecerán las casillas situadas junto a los nombres de columna en el rectángulo que representa la tabla o el objeto con valores de tabla.  
  
Si el Diseñador de consultas y vistas no puede eliminar una o varias filas, no se eliminará ninguna de ellas y recibirá un mensaje en el que se indicarán las filas que contienen información que no se puede eliminar de la base de datos.  
  
> [!CAUTION]  
> No es posible deshacer la operación de ejecutar una consulta de eliminación. Como medida de precaución, haga una copia de seguridad de los datos antes de ejecutar una consulta Eliminar.  
  
### <a name="to-create-a-delete-query"></a>Para crear una consulta Eliminar  
  
1.  Agregue tabla de la que se van a eliminar filas al panel Diagrama.  
  
2.  En el menú **Diseñador de consultas** , seleccione **Cambiar tipo**y, luego, haga clic en **Eliminar**. **Nota** Si aparece más de una tabla en el panel Diagrama al iniciar la consulta de eliminación, el Diseñador de consultas y vistas mostrará el [cuadro de diálogo Eliminar tabla](../../ssms/visual-db-tools/delete-table-dialog-box-visual-database-tools.md) para solicitar el nombre de la tabla de la que se van a eliminar filas.  
  
Al ejecutar una consulta de eliminación, no se muestra ningún resultado en el [panel Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). En su lugar, aparece un mensaje que indica cuántas filas se han eliminado.  
  
## <a name="see-also"></a>Consulte también  
[Tipos de consultas compatibles &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
