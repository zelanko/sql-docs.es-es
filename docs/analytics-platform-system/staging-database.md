---
title: Usar una base de datos de ensayo
description: SQL Server almacenamiento de datos paralelos (PDW) utiliza una base de datos provisional para almacenar los datos temporalmente durante el proceso de carga.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: dcd7f95833695cc5f9f791d83a6221c35e88f58e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400282"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>Usar una base de datos de ensayo en almacenamiento de datos paralelos (PDW)
SQL Server almacenamiento de datos paralelos (PDW) utiliza una base de datos provisional para almacenar los datos temporalmente durante el proceso de carga. De forma predeterminada, PDW de SQL Server usa la base de datos de destino como base de datos de almacenamiento provisional, lo que puede provocar la fragmentación de la tabla. Para reducir la fragmentación de la tabla, puede crear una base de datos de almacenamiento provisional definida por el usuario. O bien, cuando la reversión de un error de carga no es un problema, puede usar el modo de carga fastappend para mejorar el rendimiento omitiendo la tabla temporal y cargando directamente en la tabla de destino.  
  
## <a name="staging-database-basics"></a><a name="StagingDatabase"></a>Conceptos básicos de bases de datos de ensayo  
Una *base* de datos de ensayo es una base de datos de PDW creada por el usuario que almacena los datos temporalmente mientras se cargan en el dispositivo. Cuando se especifica una base de datos de almacenamiento provisional para una carga, el dispositivo copia primero los datos en la base de datos de ensayo y, a continuación, copia los datos de las tablas temporales de la base de datos de ensayo en tablas permanentes en la base de datos de destino.  
  
Cuando una base de datos de ensayo no se especifica para una carga, SQL ServerPDW crea las tablas temporales en la base de datos de destino y las usa para almacenar los datos cargados antes de insertar los datos cargados en las tablas de destino permanentes.  
  
Cuando una carga usa el *modo fastappend*, SQL ServerPDW omite el uso de las tablas temporales y anexa los datos directamente a la tabla de destino. El modo fastappend mejora el rendimiento de la carga de los escenarios de ELT en los que los datos se cargan en una tabla que es una tabla temporal desde el punto de vista de la aplicación. Por ejemplo, un proceso ELT podría cargar datos en una tabla temporal, procesar los datos mediante la limpieza y el duping y, a continuación, insertar los datos en la tabla de hechos de destino. En este caso, no es necesario que PDW cargue primero los datos en una tabla temporal interna antes de insertar los datos en la tabla temporal de la aplicación. El modo fastappend evita el paso de carga adicional, lo que mejora significativamente el rendimiento de la carga. Para usar el modo fastappend, debe usar el modo de transacciones múltiples, lo que significa que la recuperación de una carga errónea o anulada debe controlarse mediante su propio proceso de carga.  
  
**Ventajas de las bases de datos provisionales**  
  
La principal ventaja de una base de datos provisional es reducir la fragmentación de la tabla. Si no se utiliza una base de datos de almacenamiento provisional, los datos se cargan en tablas temporales en la base de datos de destino. Cuando las tablas temporales se crean y se colocan en la base de datos de destino, se intercalan las páginas de las tablas temporales y las tablas permanentes. Con el tiempo, se produce la fragmentación de la tabla y se degrada el rendimiento. Por el contrario, una base de datos provisional garantiza que las tablas temporales se crean y se colocan en un espacio de archivo independiente que las tablas permanentes.  
  
**Estructuras de tabla de base de datos de ensayo**  
  
La estructura de almacenamiento de cada tabla de base de datos depende de la tabla de destino.  
  
-   En el caso de cargas en un índice de almacén de columnas agrupado o montón, la tabla de ensayo es un montón.  
  
-   En el caso de las cargas en un índice clúster de almacén, la tabla de ensayo es un índice clúster de almacén.  
  
## <a name="permissions"></a><a name="Permissions"></a>Permisos  
Requiere el permiso CREATE (para crear una tabla temporal) en la base de datos de ensayo. 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="best-practices-for-creating-a-staging-database"></a><a name="CreatingStagingDatabase"></a>Prácticas recomendadas para crear una base de datos de ensayo  
  
1.  Solo debe haber una base de datos de ensayo por cada dispositivo. La base de datos provisional se puede compartir con todos los trabajos de carga de todas las bases de datos de destino.  
  
2.  El tamaño de la base de datos provisional es específico del cliente. Inicialmente, al rellenar el dispositivo por primera vez, la base de datos de ensayo debe ser lo suficientemente grande como para alojar los trabajos de carga iniciales. Estos trabajos de carga tienden a ser grandes porque pueden producirse varias cargas simultáneamente. Una vez que se han completado los trabajos de carga iniciales y el sistema está en producción, es probable que el tamaño de cada trabajo de carga sea menor. Cuando las cargas son pequeñas, puede reducir el tamaño de la base de datos provisional para acomodar los tamaños de carga más pequeños. Para reducir el tamaño, puede quitar la base de datos de ensayo y volver a crearla con asignaciones de tamaño menor, o puede usar la instrucción [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) .  
  
    Al crear la base de datos provisional, utilice las siguientes directrices.  
  
    -   El tamaño de la tabla replicada debe ser el tamaño estimado, por nodo de proceso, de todas las tablas replicadas que se cargarán simultáneamente. El tamaño suele ser de 25-30 GB.  
  
    -   El tamaño de la tabla distribuida debe ser el tamaño estimado, por dispositivo, de todas las tablas distribuidas que se cargarán simultáneamente.  
  
    -   Normalmente, el tamaño del registro es similar al tamaño de la tabla replicada.  
  
## <a name="examples"></a><a name="Examples"></a>Ejemplos  
  
### <a name="a-create-a-staging-database"></a>A. Crear una base de datos de ensayo 
En el ejemplo siguiente se crea una base de datos de ensayo, Stagedb, para su uso con todas las cargas en el dispositivo. Supongamos que calcula que cinco tablas replicadas de tamaño 5 GB se cargarán simultáneamente. Esta simultaneidad da como resultado la asignación de al menos 25 GB para el tamaño replicado. Supongamos que calcula que seis tablas distribuidas de los tamaños 100, 200, 400, 500, 500 y 550 GB se cargarán simultáneamente. Esta simultaneidad da como resultado la asignación de al menos 2250 GB para el tamaño de la tabla distribuida.  
  
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
  
