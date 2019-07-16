---
title: Uso de una base de datos provisional - almacenamiento de datos paralelos | Microsoft Docs
description: Almacenamiento de datos paralelos (PDW) de SQL Server usa una base de datos de almacenamiento provisional para almacenar datos temporalmente durante el proceso de carga.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 824ad4dedee0224023f50b6855b2de1e53581304
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960037"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>Uso de una base de datos provisional en el almacenamiento de datos paralelos (PDW)
Almacenamiento de datos paralelos (PDW) de SQL Server usa una base de datos de almacenamiento provisional para almacenar datos temporalmente durante el proceso de carga. De forma predeterminada, SQL Server PDW usa la base de datos de destino como la base de datos de almacenamiento provisional, lo que puede provocar la fragmentación de las tablas. Para reducir la fragmentación de las tablas, puede crear una base de datos de almacenamiento provisional definido por el usuario. O bien, cuando la reversión de un error de carga no es un problema, puede usar el modo de carga de fastappend para mejorar el rendimiento mediante la omisión de la tabla temporal y cargando directamente en la tabla de destino.  
  
## <a name="StagingDatabase"></a>Conceptos básicos de la base de datos de almacenamiento provisional  
Un *base de datos provisional* es una base PDW creada por el usuario que almacene datos temporalmente mientras se cargan en el dispositivo. Cuando se especifica una base de datos de almacenamiento provisional para una carga, el dispositivo primero copia los datos en la base de datos provisional y, a continuación, copia los datos de tablas temporales en la base de datos de ensayo en tablas permanentes en la base de datos de destino.  
  
Cuando una base de datos de almacenamiento provisional no se especifica para una carga, ServerPDW SQL crea las tablas temporales en la base de datos de destino y los utiliza para almacenar los datos cargados antes de insertar los datos cargados en las tablas de destino permanente.  
  
Cuando se usa una carga el *modo fastappend*, ServerPDW SQL omite el uso de tablas temporales por completo y anexa los datos directamente a la tabla de destino. El modo fastappend mejora el rendimiento de carga para los escenarios ELT donde los datos se cargan en una tabla que es una tabla temporal desde el punto de vista de la aplicación. Por ejemplo, un proceso ELT podría cargar datos en una tabla temporal, procesar los datos mediante la deduplicación de cancelación y limpieza y, a continuación, inserte los datos en la tabla de hechos de destino. En este caso, no es necesario para PDW cargar primero los datos en una tabla temporal interna antes de insertar los datos en la tabla temporal de la aplicación. El modo fastappend evita el paso de la carga adicional, lo que mejora significativamente el rendimiento de carga. Para utilizar el modo fastappend, debe utilizar el modo de transacción múltiple, lo que significa que la recuperación a partir de una carga con errores o anuló deberá controlarse mediante su propio proceso de carga.  
  
**Ventajas de la base de datos de almacenamiento provisional**  
  
La principal ventaja de una base de datos de almacenamiento provisional es reducir la fragmentación de la tabla. Si no se usa una base de datos de almacenamiento provisional, los datos se cargan en tablas temporales de la base de datos de destino. Cuando obtengan crean tablas temporales y se quitan en la base de datos de destino, las páginas de las tablas temporales y tablas permanentes se convierten en intercalada. Con el tiempo, la fragmentación de las tablas se produce y degrada el rendimiento. En cambio, una base de datos de ensayo garantiza que las tablas temporales se crean y quitan en un espacio de archivo independiente de las tablas permanentes.  
  
**Estructuras de tabla de base de datos de almacenamiento provisional**  
  
La estructura de almacenamiento para cada tabla de base de datos depende de la tabla de destino.  
  
-   Para las cargas en un montón o índice agrupado, la tabla de ensayo es un montón.  
  
-   Para las cargas en un índice agrupado de almacén de filas, la tabla de ensayo es un índice agrupado de almacén de filas.  
  
## <a name="Permissions"></a>Permissions  
Requiere el permiso de creación (para crear una tabla temporal) en la base de datos de almacenamiento provisional. 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="CreatingStagingDatabase"></a>Procedimientos recomendados para crear una base de datos provisional  
  
1.  Solo debe haber una base de datos de almacenamiento provisional por dispositivo. La base de datos de almacenamiento provisional se puede compartir por todos los trabajos de carga para todas las bases de datos de destino.  
  
2.  El tamaño de la base de datos de almacenamiento provisional es específica del cliente. Inicialmente, al rellenar primero el dispositivo, la base de datos de almacenamiento provisional debe ser lo suficientemente grande como para dar cabida a los trabajos de carga inicial. Estos trabajos de carga tienden a ser grandes, porque pueden se producen varias cargas al mismo tiempo. Después de han completado los trabajos de carga inicial y el sistema está en producción, es probable que sea más pequeño el tamaño de cada carga de trabajo. Cuando las cargas son pequeñas, puede reducir el tamaño de la base de datos de almacenamiento provisional para dar cabida a los tamaños más pequeños de carga. Para reducir el tamaño, puede quitar la base de datos provisional y volver a crearla con una asignación menor tamaño, o puede usar el [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) instrucción.  
  
    Al crear la base de datos de almacenamiento provisional, utilice las instrucciones siguientes.  
  
    -   El tamaño de la tabla replicada debe ser el tamaño estimado por nodo de proceso, de todas las tablas replicadas que se cargará al mismo tiempo. Normalmente, el tamaño es 25-30 GB.  
  
    -   El tamaño de una tabla distribuida debe ser el tamaño estimado por dispositivo, de todas las tablas distribuidas que se cargará al mismo tiempo.  
  
    -   El tamaño del registro es normalmente similar al tamaño de la tabla replicada.  
  
## <a name="Examples"></a>Ejemplos  
  
### <a name="a-create-a-staging-database"></a>A. Crear una base de datos provisional 
El ejemplo siguiente crea una base de datos provisional, Stagedb, para su uso con todas las cargas en el dispositivo. Suponga que calcule que replica cinco tablas de tamaño de que 5 GB se cargará al mismo tiempo. Esta simultaneidad da lugar a asignar al menos 25 GB para el tamaño replicado. Supongamos que calcula que distribuyen seis tablas de tamaños de 100, 200, 400, 500, 500 y 550 GB se cargan al mismo tiempo. Esta simultaneidad da como resultado asignar 2250 GB como mínimo para el tamaño de una tabla distribuida.  
  
```sql  
CREATE DATABASE Stagedb  
WITH (  
  
    AUTOGROW = ON,  
  
    REPLICATED_SIZE = 25 GB,  
  
    DISTRIBUTED_SIZE = 2250 GB,  
  
    LOG_SIZE = 25 GB  
  
);  
```  

<!-- MISSING LINKS
 
## See Also  
[Common metadata query examples](metadata-query-examples.md)  

-->
  
