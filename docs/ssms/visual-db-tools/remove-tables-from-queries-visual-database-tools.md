---
title: Quitar tablas de las consultas (Visual Database Tools) | Microsoft Docs
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
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 726f169be56f64484d505b91ca5d93a6426cbf7c
ms.lasthandoff: 04/11/2017

---
# <a name="remove-tables-from-queries-visual-database-tools"></a>Quitar tablas de las consultas (Visual Database Tools)
Puede quitar una tabla, o cualquier objeto con valores de tabla, de la consulta.  
  
> [!NOTE]  
> Si se quitan tablas u objetos con valores de tabla, no se eliminan de la base de datos; solo se quitan de la consulta actual. Para obtener más información sobre cómo quitar una tabla de una base de datos, consulte [Cómo eliminar tablas de una base de datos (Visual Database Tools)](http://msdn.microsoft.com/en-us/ca6aa3e9-9885-44c3-bafc-aec441fd97ec).  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>Para quitar una tabla o un objeto con estructura de tabla  
  
-   En el **panel Diagrama**, seleccione la tabla, vista, función definida por el usuario, sinónimo o consulta y, a continuación, presione la tecla Supr, o bien haga clic con el botón derecho en el objeto y elija **Quitar** en el cuadro de diálogo que aparecerá. Puede seleccionar y quitar varios objetos a la vez.  
  
    O bien  
  
-   Quite todas las referencias al objeto en el **panel SQL**.  
  
Cuando quite una tabla o un objeto con valores de tabla, el Diseñador de consultas y vistas quitará automáticamente las combinaciones que relacionen la tabla o el objeto con valores de tabla, así como las referencias a las columnas del objeto en el **panel SQL** y el **panel Criterios**. Sin embargo, si la consulta contiene expresiones complejas que hacen referencia al objeto, éste no se quitará automáticamente hasta que se hayan quitado todas las referencias al mismo.  
  
## <a name="see-also"></a>Vea también  
[Agregar tablas a las consultas (Visual Database Tools)](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[Crear alias de tabla (Visual Database Tools)](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[Especificar criterios de búsqueda (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Resumir los resultados de una consulta (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Realizar operaciones básicas con consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  

