---
title: Reglas para actualizar resultados (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- View Designer, Results pane
- updating query results
- Query Designer [SQL Server], Results pane
- Results pane
ms.assetid: de131ef0-ccbd-446f-9400-b93c7b8fa537
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f617973f041218de7b77b64350b8953dbaa0d149
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="rules-for-updating-results-visual-database-tools"></a>Reglas para actualizar resultados (Visual Database Tools)
En muchos casos, puede actualizar el conjunto de resultados mostrado en el [panel Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). Sin embargo, en algunos casos no es posible realizar esta actualización.  
  
En general, para actualizar resultados, el [Diseñador de consultas y vistas](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) debe tener información suficiente para identificar de forma exclusiva la fila en la tabla. Por ejemplo, si la consulta incluye una clave principal en la lista de resultados. Además, debe tener permisos suficientes para actualizar la base de datos.  
  
Si la consulta se basa en una vista, se podrá actualizar. Se aplican las mismas directrices, con la salvedad de que se aplican a las tablas subyacentes en la vista, no solamente a la propia vista.  
  
> [!NOTE]  
> El Diseñador de consultas y vistas no puede determinar con antelación si se puede actualizar un conjunto de resultados basado en una vista. Por lo tanto, muestra todas las vistas, aunque es posible que no se puedan actualizar.  
  
La siguiente tabla resume casos específicos en los que sería posible o no actualizar los resultados de la consulta en el panel Resultados. En muchos casos, la base de datos que se utiliza establece si se pueden actualizar los resultados de la consulta.  
  
|Query|¿Pueden actualizarse los resultados?|  
|---------|---------------------------|  
|Consulta basada en una tabla con clave principal en la lista de resultados|Sí (con la excepción de lo mostrado a continuación).|  
|Consulta basada en una tabla sin índice único y sin clave principal|Depende de la consulta y de la base de datos. Algunas bases de datos permiten actualizaciones si hay suficiente información disponible para identificar registros de forma exclusiva.|  
|Consulta basada en varias tablas que no están combinadas|No.|  
|Consulta basada en datos marcados como de solo lectura en la base de datos|No.|  
|Consulta basada en una vista que incluye una tabla sin restricciones|Sí (con la excepción de lo mostrado a continuación).|  
|Consulta basada en tablas combinadas con una relación uno a uno|Sí (con la excepción de lo mostrado a continuación).|  
|Consulta basada en tablas combinadas con una relación uno a varios|Normalmente.|  
|Consulta basada en tres o más tablas en las que existe una relación varios a varios|No.|  
|Consulta basada en una tabla para la que no se dispone de permiso de actualización|Pueden eliminarse pero no actualizarse.|  
|Consulta basada en una tabla para la que no se dispone de permiso de eliminación|Pueden actualizarse pero no eliminarse.|  
|Consulta de funciones agregadas|No.|  
|Consulta basada en una subconsulta que contiene totales o funciones de agregado|No.|  
|Consulta que incluye la palabra clave DISTINCT para excluir filas duplicadas|No.|  
|Consulta cuya cláusula FROM incluye una función definida por el usuario que devuelve una tabla y la función definida por el usuario contiene varias instrucciones SELECT|No.|  
|Consulta cuya cláusula FROM incluya una función inline definida por el usuario|Sí.|  
  
Además, es posible que no pueda actualizar columnas específicas de los resultados de la consulta. La siguiente lista resume tipos específicos de columnas que no se pueden actualizar en el panel Resultados.  
  
-   Columnas basadas en expresiones  
  
-   Columnas basadas en funciones escalares definidas por el usuario  
  
-   Filas o columnas eliminadas por otro usuario  
  
-   Filas o columnas bloqueadas por otro usuario (normalmente, las filas bloqueadas se pueden actualizar en cuanto se desbloquean)  
  
-   Columnas de marca de tiempo o BLOB  
  
## <a name="see-also"></a>Vea también  
[Temas de procedimientos de diseño de consultas y vistas &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  

