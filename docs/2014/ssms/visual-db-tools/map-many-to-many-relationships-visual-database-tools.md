---
title: Asignar relaciones de varios a varios (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], many-to-many
- junction tables [SQL Server]
- many-to-many relationships [SQL Server]
- mapping many-to-many relationships [SQL Server]
- database diagrams [SQL Server], relationships
ms.assetid: 2977cf92-98b5-48b2-b0fd-8fbc7040f2b4
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e93eecef54eb5910287a2693311539f5c2fb898e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202415"
---
# <a name="map-many-to-many-relationships-visual-database-tools"></a>Asignar relaciones varios a varios (Visual Database Tools)
  Las relaciones varios a varios permiten relacionar cada fila de una tabla con muchas filas de otra tabla y viceversa. Por ejemplo, puede crear una relación varios a varios entre la tabla `authors` y la tabla `titles` para asociar a cada autor con todos sus libros y a cada libro con todos sus autores. Si se crea una relación uno a varios desde cada tabla, se indicaría incorrectamente que cada libro tiene un solo autor o que cada autor solo puede escribir un libro.  
  
 Las relaciones varios a varios entre tablas se implementan en las bases de datos mediante tablas de unión. Una tabla de unión contiene las columnas de clave principal de las dos tablas que desea relacionar. Después debe crear una relación entre las columnas de clave principal de cada una de las dos tablas y las columnas coincidentes en la tabla de unión. En la base datos pubs, la tabla `titleauthor` es una tabla de unión.  
  
### <a name="to-create-a-many-to-many-relationship-between-tables"></a>Para crear una relación varios a varios entre tablas  
  
1.  Agregue en el diagrama de base de datos las tablas entre las que desea crear una relación varios a varios.  
  
2.  Cree una tercera tabla; para ello, haga clic con el botón derecho en el diagrama y elija **Nueva tabla** en el menú contextual. Se convertirá en la tabla de unión.  
  
3.  En el cuadro de diálogo **Elegir nombre** , cambie el nombre de tabla asignado por el sistema. Por ejemplo, la tabla de unión situada entre la tabla `titles` y la tabla `authors` se denomina ahora `titleauthors`.  
  
4.  Copie las columnas de clave principal de cada una de las otras dos tablas en la tabla de unión. Puede agregar otras columnas a esta tabla, así como a cualquier otra tabla.  
  
5.  En la tabla de unión, establezca la clave principal para incluir todas las columnas de clave principal de las otras dos tablas. Para obtener más información, consulte [Create Primary Keys](../../relational-databases/tables/create-primary-keys.md).  
  
6.  Defina una relación uno a varios entre las dos tablas principales y la tabla de unión. La tabla de unión debe estar en el lado "varios" de las dos relaciones que cree. Para obtener más información, consulte [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md).  
  
    > [!NOTE]  
    >  Al crear una tabla de unión en un diagrama de base de datos, no se insertan datos de las tablas relacionadas en la tabla de unión. Para más información sobre cómo insertar datos en una tabla, consulte [Crear consultas de inserción de resultados &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con diagramas de base de datos &#40;Visual Database Tools&#41;](work-with-database-diagrams-visual-database-tools.md)  
  
  
