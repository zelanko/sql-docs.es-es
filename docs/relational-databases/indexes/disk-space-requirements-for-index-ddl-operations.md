---
title: "Requisitos de espacio en disco para operaciones DDL de índice | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- temporary disk space [SQL Server]
ms.assetid: 35930826-c870-44c1-a966-a6a4638f62ef
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c71784eb7a7a8e9ed2456cb7ae7718fafc9e1e6a
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="disk-space-requirements-for-index-ddl-operations"></a>Requisitos de espacio en disco para operaciones DDL de índice
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  El espacio en disco es una consideración importante a la hora de crear, volver a generar o quitar índices. Un espacio en disco inadecuado puede degradar el rendimiento e incluso provocar errores en las operaciones de índice. En este tema se proporciona información general que puede ayudar a determinar la cantidad de espacio necesario para las operaciones de lenguaje de definición de datos (DDL).  
  
## <a name="index-operations-that-require-no-additional-disk-space"></a>Operaciones de índice que no requieren espacio en disco adicional  
 Las siguientes operaciones de índice no requieren espacio en disco adicional:  
  
-   ALTER INDEX REORGANIZE; sin embargo, se requiere espacio de registro.  
  
-   DROP INDEX cuando se quita un índice no clúster.  
  
-   DROP INDEX cuando se quita un índice clúster sin conexión sin especificar la cláusula MOVE TO y no existen índices no clúster.  
  
-   CREATE TABLE (restricciones PRIMARY KEY o UNIQUE).  
  
## <a name="index-operations-that-require-additional-disk-space"></a>Operaciones de índice que requieren espacio en disco adicional  
 Todas las demás operaciones DDL de índice requieren espacio temporal en disco adicional para utilizarlo durante la operación y espacio en disco permanente para almacenar la estructura (o estructuras) del nuevo índice.  
  
 Cuando se crea una nueva estructura de índice, se requiere espacio en disco para ambas estructuras, la antigua (origen) y la nueva (destino), en los archivos y grupos de archivos correspondientes. La asignación de la estructura antigua no se cancela hasta que no se confirma la transacción de creación del índice.  
  
 Las siguientes operaciones DDL de índice crean estructuras y requieren espacio en disco adicional:  
  
-   CREATE INDEX  
  
-   CREATE INDEX WITH DROP_EXISTING  
  
-   ALTER INDEX REBUILD  
  
-   ALTER TABLE ADD CONSTRAINT (PRIMARY KEY o UNIQUE)  
  
-   ALTER TABLE DROP CONSTRAINT (PRIMARY KEY o UNIQUE) cuando la restricción se basa en un índice clúster  
  
-   DROP INDEX MOVE TO (se aplica solo a ndices clúster)  
  
## <a name="temporary-disk-space-for-sorting"></a>Espacio temporal en disco para ordenación  
 Además del espacio en disco necesario para las estructuras de origen y destino, se necesita espacio temporal en disco para la ordenación, a menos que el optimizador de consultas busque un plan de ejecución que no requiera ordenación.  
  
 Si se requiere ordenación, ésta se produce en un nuevo índice a la vez. Por ejemplo, cuando se vuelve a generar un índice clúster con los índices no clúster que van asociados en una instrucción única, los índices se ordenan uno tras otro. Por lo tanto, el espacio temporal en disco que se necesita para ordenar solo tiene que ser tan grande como el índice más grande de la operación. Éste casi siempre se corresponde con el índice clúster.  
  
 Si la opción SORT_IN_TEMPDB está establecida en ON, el índice más grande debe caber en **tempdb**. Aunque esta opción aumenta la cantidad de espacio temporal en disco utilizado para crear un índice, puede reducir el tiempo necesario para crear el índice cuando **tempdb** se encuentra en un conjunto de discos diferente al de la base de datos de usuario.  
  
 Si SORT_IN_TEMPDB está establecido en OFF (el valor predeterminado), cada índice, incluidos los índices con particiones, se ordena en su espacio en disco de destino y solo se necesita espacio en disco para las nuevas estructuras de índice.  
  
 Para obtener un ejemplo de cálculo de espacio en disco, vea [Index Disk Space Example](../../relational-databases/indexes/index-disk-space-example.md).  
  
## <a name="temporary-disk-space-for-online-index-operations"></a>Espacio temporal en disco para operaciones de índice en línea  
 Cuando se realizan operaciones de índice en línea, se necesita espacio temporal en disco adicional.  
  
 Cuando se crea un índice clúster, se vuelve a generar o se quita en línea, se crea un índice no clúster temporal para asignar los antiguos marcadores a los nuevos. Si la opción SORT_IN_TEMPDB está establecida en ON, el índice temporal se crea en **tempdb**. Si SORT_IN_TEMPDB está establecida en OFF, se utiliza el mismo grupo de archivos o esquema de particiones que el índice de destino. El índice de asignación temporal contiene un registro para cada fila de la tabla y su contenido es la unión de las columnas de marcadores antiguos y nuevos, que incluye los identificadores únicos y los identificadores de registro, y solo una copia única de cualquier columna que se utilice en ambos marcadores. Para obtener más información sobre las operaciones de índices en línea, vea [Realizar operaciones de índice en línea](../../relational-databases/indexes/perform-index-operations-online.md).  
  
> [!NOTE]  
>  La opción SORT_IN_TEMPDB no se puede establecer para instrucciones DROP INDEX. El índice de asignación temporal se crea siempre en el mismo grupo de archivos o esquema de particiones que el índice de destino.  
  
 Las operaciones de índice en línea utilizan versiones de fila para aislar la operación de índice de los efectos de modificaciones efectuadas por otras transacciones. Así se evita la necesidad de solicitar que se compartan bloqueos en filas que se han leído. Las operaciones simultáneas de eliminación y actualización de usuarios durante las operaciones de índice en línea requieren espacio para registros de versión en **tempdb**. Para obtener más información, vea [Realizar operaciones de índice en línea](../../relational-databases/indexes/perform-index-operations-online.md) .  
  
## <a name="related-tasks"></a>Related Tasks  
 [Index Disk Space Example](../../relational-databases/indexes/index-disk-space-example.md)  
  
 [Espacio en disco del registro de transacciones para operaciones de índice](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)  
  
 [Calcular el tamaño de una tabla](../../relational-databases/databases/estimate-the-size-of-a-table.md)  
  
 [Estimar el tamaño de un índice clúster](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)  
  
 [Estimar el tamaño de un índice no clúster](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
 [Estimar el tamaño de un montón](../../relational-databases/databases/estimate-the-size-of-a-heap.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 [Especificar el factor de relleno para un índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)  
  
 [Reorganizar y volver a generar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
  
