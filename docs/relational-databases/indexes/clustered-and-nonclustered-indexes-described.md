---
title: Índices agrupados y no agrupados descritos | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- query optimizer [SQL Server], index usage
- index concepts [SQL Server]
ms.assetid: b7d6b323-728d-4763-a987-92e6292f6f7a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4687887715ffb9df13168bc1ee1dc78418c196c3
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/17/2018
ms.locfileid: "49383920"
---
# <a name="clustered-and-nonclustered-indexes-described"></a>Índices agrupados y no agrupados descritos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Un índice es una estructura de disco asociada con una tabla o una vista que acelera la recuperación de filas de la tabla o de la vista. Un índice contiene claves generadas a partir de una o varias columnas de la tabla o la vista. Dichas claves están almacenadas en una estructura (árbol b) que permite que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] busque de forma rápida y eficiente la fila o filas asociadas a los valores de cada clave.  
  
 Una tabla o una vista puede contener los siguientes tipos de índices:  
  
-   Clúster  
  
    -   Los índices clúster ordenan y almacenan las filas de los datos de la tabla o vista de acuerdo con los valores de la clave del índice. Son columnas incluidas en la definición del índice. Solo puede haber un índice clúster por cada tabla, porque las filas de datos solo pueden estar almacenadas de una forma.  
  
    -   La única ocasión en la que las filas de datos de una tabla están ordenadas es cuando la tabla contiene un índice clúster. Cuando una tabla tiene un índice clúster, la tabla se denomina tabla agrupada. Si una tabla no tiene un índice clúster, sus filas de datos están almacenadas en una estructura sin ordenar denominada montón.  
  
-   No agrupado  
  
    -   Los índices no clúster tienen una estructura separada de las filas de datos. Un índice no clúster contiene los valores de clave de índice no clúster y cada entrada de valor de clave tiene un puntero a la fila de datos que contiene el valor clave.  
  
    -   El puntero de una fila de índice no clúster hacia una fila de datos se denomina localizador de fila. La estructura del localizador de filas depende de si las páginas de datos están almacenadas en un montón o en una tabla agrupada. Si están en un montón, el localizador de filas es un puntero hacia la fila. Si están en una tabla agrupada, el localizador de fila es la clave de índice clúster.  
  
    -   Puede agregar columnas sin clave al nivel hoja de un índice no agrupado con el fin de eludir los límites existentes para las claves de índice, así como para ejecutar consultas indexadas y totalmente cubiertas. Para más información, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md). Para obtener más información sobre los límites para las claves de índice, consulte [Especificaciones de capacidad máxima para SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md). 
  
 Tanto los índices clúster como los no clúster pueden ser únicos. Esto significa que dos filas no pueden tener el mismo valor para la clave de índice. De lo contrario, el índice no es único y varias filas pueden compartir el mismo valor de clave. Para obtener más información, vea [Crear vistas indexadas](../../relational-databases/indexes/create-unique-indexes.md).  
  
 Los índices se mantienen automáticamente para una tabla o vista cuando se modifican los datos de la tabla.  
  
 Vea [Indexes](../../relational-databases/indexes/indexes.md) para los tipos adicionales de índices de propósito especial.  
  
## <a name="indexes-and-constraints"></a>Índices y restricciones  
 Los índices se crean automáticamente cuando las restricciones PRIMARY KEY y UNIQUE se definen en las columnas de tabla. Por ejemplo, cuando cree una tabla e identifique una determinada columna como la clave principal, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] creará automáticamente una restricción PRIMARY KEY y un índice en esa columna. Para obtener más información, consulte [Create Primary Keys](../../relational-databases/tables/create-primary-keys.md) y [Create Unique Constraints](../../relational-databases/tables/create-unique-constraints.md).  
  
## <a name="how-indexes-are-used-by-the-query-optimizer"></a>Cómo usa los índices el optimizador de consultas  
 Los índices bien diseñados pueden reducir las operaciones de E/S de disco y consumen menos recursos del sistema, con lo que mejoran el rendimiento de la consulta. Los índices pueden ser útiles para diversas consultas que contienen instrucciones SELECT, UPDATE, DELETE o MERGE. Fíjese en la consulta `SELECT Title, HireDate FROM HumanResources.Employee WHERE EmployeeID = 250` en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Cuando se ejecuta la consulta, el optimizador de consultas evalúa cada método disponible para recuperar datos y selecciona el método más eficiente. El método puede ser un recorrido de la tabla o puede ser recorrer uno o más índices si existen.  
  
 Al realizar un recorrido de la tabla, el optimizador de consultas leerá todas las filas de la tabla y extraerá las filas que cumplen con los criterios de la consulta. Un recorrido de la tabla genera muchas operaciones de E/S de disco y puede consumir recursos. No obstante, puede ser el método más eficaz si, por ejemplo, el conjunto de resultados de la consulta es un porcentaje elevado de filas de la tabla.  
  
 Cuando el optimizador de consultas utiliza un índice, busca en las columnas de clave de índice, busca la ubicación de almacenamiento de las filas que necesita la consulta y extrae las filas coincidentes de esa ubicación. Generalmente, la búsqueda del índice es mucho más rápida que la búsqueda de la tabla porque, a diferencia de la tabla, un índice frecuentemente contiene muy pocas columnas por fila y las filas están ordenadas.  
  
 El optimizador de consultas normalmente selecciona el método más eficaz cuando ejecuta consultas. No obstante, si no hay índices disponibles, el optimizador de consultas debe utilizar un recorrido de la tabla. Su tarea consiste en designar y crear los índices que sean más educados para su entorno para que el optimizador de consultas tenga una selección de índices eficientes entre los cuales elegir. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona el [Asistente para la optimización de motor de base de datos](../../relational-databases/performance/database-engine-tuning-advisor.md) , que sirve de ayuda en el análisis del entorno de su base de datos y para seleccionar los índices apropiados.  
  
> [!IMPORTANT] 
> Para obtener más información sobre las directrices de diseño de índices y los datos internos, consulte la [Guía de diseño de índices de SQL Server](../../relational-databases/sql-server-index-design-guide.md).

## <a name="related-content"></a>Contenido relacionado  
 [Guía de diseño de índices de SQL Server](../../relational-databases/sql-server-index-design-guide.md)     
 [Crear índices clúster](../../relational-databases/indexes/create-clustered-indexes.md)  
 [Crear índices no clúster](../../relational-databases/indexes/create-nonclustered-indexes.md)  
  
  
