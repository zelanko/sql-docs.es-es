---
title: Quitar tablas de las consultas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
author: stevestein
ms.author: sstein
ms.openlocfilehash: fab5380e13742f3cd289ce17f26ad2e5fb9089ec
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064871"
---
# <a name="remove-tables-from-queries-visual-database-tools"></a>Quitar tablas de las consultas (Visual Database Tools)
  Puede quitar una tabla, o cualquier objeto con valores de tabla, de la consulta.  
  
> [!NOTE]  
>  Si se quitan tablas u objetos con valores de tabla, no se eliminan de la base de datos; solo se quitan de la consulta actual. Para obtener más información sobre cómo quitar una tabla de una base de datos, vea [Delete tables &#40;Motor de base de datos&#41;](../../relational-databases/tables/delete-tables-database-engine.md).  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>Para quitar una tabla o un objeto con estructura de tabla  
  
-   En el **panel Diagrama**, seleccione la tabla, vista, función definida por el usuario, sinónimo o consulta y, a continuación, presione la tecla Supr, o bien haga clic con el botón derecho en el objeto y elija **Quitar** en el cuadro de diálogo que aparecerá. Puede seleccionar y quitar varios objetos a la vez.  
  
     O bien  
  
-   Quite todas las referencias al objeto en el **panel SQL**.  
  
 Cuando quite una tabla o un objeto con valores de tabla, el Diseñador de consultas y vistas quitará automáticamente las combinaciones que relacionen la tabla o el objeto con valores de tabla, así como las referencias a las columnas del objeto en el **panel SQL** y el **panel Criterios**. Sin embargo, si la consulta contiene expresiones complejas que hacen referencia al objeto, éste no se quitará automáticamente hasta que se hayan quitado todas las referencias al mismo.  
  
## <a name="see-also"></a>Consulte también  
 [Agregar tablas a las consultas &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Crear alias de tabla &#40;Visual Database Tools&#41;](create-table-aliases-visual-database-tools.md)   
 [Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Realizar operaciones básicas con consultas (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
