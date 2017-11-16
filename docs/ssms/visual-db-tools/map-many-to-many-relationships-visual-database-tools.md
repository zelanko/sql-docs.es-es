---
title: Asignar relaciones de varios a varios (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- relationships [SQL Server], many-to-many
- junction tables [SQL Server]
- many-to-many relationships [SQL Server]
- mapping many-to-many relationships [SQL Server]
- database diagrams [SQL Server], relationships
ms.assetid: 2977cf92-98b5-48b2-b0fd-8fbc7040f2b4
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a3eaab2649f6e84f99761b8c4acce6143eff997f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="map-many-to-many-relationships-visual-database-tools"></a>Asignar relaciones varios a varios (Visual Database Tools)
Las relaciones varios a varios permiten relacionar cada fila de una tabla con muchas filas de otra tabla y viceversa. Por ejemplo, puede crear una relación varios a varios entre la tabla `authors` y la tabla `titles` para asociar a cada autor con todos sus libros y a cada libro con todos sus autores. Si se crea una relación uno a varios desde cada tabla, se indicaría incorrectamente que cada libro tiene un solo autor o que cada autor solo puede escribir un libro.  
  
Las relaciones varios a varios entre tablas se implementan en las bases de datos mediante tablas de unión. Una tabla de unión contiene las columnas de clave principal de las dos tablas que desea relacionar. Después debe crear una relación entre las columnas de clave principal de cada una de las dos tablas y las columnas coincidentes en la tabla de unión. En la base datos pubs, la tabla `titleauthor` es una tabla de unión.  
  
### <a name="to-create-a-many-to-many-relationship-between-tables"></a>Para crear una relación varios a varios entre tablas  
  
1.  Agregue en el diagrama de base de datos las tablas entre las que desea crear una relación varios a varios.  
  
2.  Cree una tercera tabla; para ello, haga clic con el botón derecho en el diagrama y elija **Nueva tabla** en el menú contextual. Se convertirá en la tabla de unión.  
  
3.  En el cuadro de diálogo **Elegir nombre** , cambie el nombre de tabla asignado por el sistema. Por ejemplo, la tabla de unión situada entre la tabla `titles` y la tabla `authors` se denomina ahora `titleauthors`.  
  
4.  Copie las columnas de clave principal de cada una de las otras dos tablas en la tabla de unión. Puede agregar otras columnas a esta tabla, así como a cualquier otra tabla.  
  
5.  En la tabla de unión, establezca la clave principal para incluir todas las columnas de clave principal de las otras dos tablas. Para detalles, consulte [Crear claves principales (Visual Database Tools)](http://msdn.microsoft.com/en-us/85c623ca-4656-4d70-a9db-ee4d897cd214).  
  
6.  Defina una relación uno a varios entre las dos tablas principales y la tabla de unión. La tabla de unión debe estar en el lado "varios" de las dos relaciones que cree. Para detalles, consulte [Crear relaciones entre tablas (Visual Database Tools)](http://msdn.microsoft.com/en-us/867a54b8-5be4-46e6-9702-49ae6dabf67c).  
  
    > [!NOTE]  
    > Al crear una tabla de unión en un diagrama de base de datos, no se insertan datos de las tablas relacionadas en la tabla de unión. Para más información sobre cómo insertar datos en una tabla, consulte [Crear consultas de inserción de resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-insert-results-queries-visual-database-tools.md).  
  
## <a name="see-also"></a>Vea también  
[Trabajar con diagramas de base de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
