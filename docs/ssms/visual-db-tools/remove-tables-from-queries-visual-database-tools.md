---
description: Quitar tablas de las consultas (Visual Database Tools)
title: Quitar tablas de consultas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 51402e1a0017f80b192bde54d7ef53aff99f61d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491605"
---
# <a name="remove-tables-from-queries-visual-database-tools"></a>Quitar tablas de las consultas (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Puede quitar una tabla, o cualquier objeto con valores de tabla, de la consulta.  
  
> [!NOTE]  
> Si se quitan tablas u objetos con valores de tabla, no se eliminan de la base de datos; solo se quitan de la consulta actual. Para obtener información detallada sobre cómo quitar una tabla de una base de datos, vea [Procedimientos para: eliminar tablas de una base de datos](https://msdn.microsoft.com/ca6aa3e9-9885-44c3-bafc-aec441fd97ec).  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>Para quitar una tabla o un objeto con estructura de tabla  
  
-   En el **panel Diagrama**, seleccione la tabla, vista, función definida por el usuario, sinónimo o consulta y, a continuación, presione la tecla Supr, o bien haga clic con el botón derecho en el objeto y elija **Quitar** en el cuadro de diálogo que aparecerá. Puede seleccionar y quitar varios objetos a la vez.  
  
    o bien  
  
-   Quite todas las referencias al objeto en el **panel SQL**.  
  
Cuando quite una tabla o un objeto con valores de tabla, el Diseñador de consultas y vistas quitará automáticamente las combinaciones que relacionen la tabla o el objeto con valores de tabla, así como las referencias a las columnas del objeto en el **panel SQL** y el **panel Criterios**. Sin embargo, si la consulta contiene expresiones complejas que hacen referencia al objeto, éste no se quitará automáticamente hasta que se hayan quitado todas las referencias al mismo.  
  
## <a name="see-also"></a>Consulte también  
[Agregar tablas a consultas](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[Crear alias de tablas](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[Especificar criterios de búsqueda](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Resumir los resultados de la consulta](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Realizar operaciones básicas con consultas](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
