---
title: "Ver informaci&#243;n de conflictos para publicaciones de mezcla (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "resolución de conflictos de replicación de mezcla [replicación de SQL Server], ver conflictos"
  - "sp_helpmergeconflictrows"
  - "ver información de conflictos"
  - "resolución de conflictos [replicación de SQL Server], replicación de mezcla"
  - "sp_helpmergearticleconflicts"
ms.assetid: 4907fe35-10ee-4f81-b924-fc419b1864d2
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Ver informaci&#243;n de conflictos para publicaciones de mezcla (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
  Cuando se resuelve un conflicto en la replicación de mezcla, los datos de la fila que falta se escriben en una tabla de conflictos. Estos datos de conflicto se pueden ver mediante programación usando los procedimientos almacenados de replicación. Para obtener más información, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### Para ver información de conflictos y los datos de la fila perdedora para todos los tipos de conflictos  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Tenga en cuenta los valores de las siguientes columnas en el conjunto de resultados:  
  
    -   **centralized_conflicts** -1 indica que las filas de conflicto se almacenan en el publicador y 0 indica que no se almacenan filas de conflicto en el publicador.  
  
    -   **decentralized_conflicts** -1 indica que las filas de conflicto se almacenan en el suscriptor y 0 indica que no se almacenan filas de conflicto en el suscriptor.  
  
        > [!NOTE]  
        >  El comportamiento de registro de conflictos de una publicación de mezcla se establece mediante la **@conflict_logging** parámetro de [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). El uso de la **@centralized_conflicts** parámetro ha quedado desusado.  
  
     En la tabla siguiente se describe los valores de estas columnas según el valor especificado para **@conflict_logging**.  
  
    |valor @conflict_logging|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publisher**|1|0|  
    |**subscriber**|0|1|  
    |**both**|1|1|  
  
2.  En el publicador de la base de datos de publicación o en el suscriptor de la base de datos de suscripción, ejecute [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Especifique un valor para **@publication** para devolver únicamente información de conflicto para los artículos que pertenecen a una publicación concreta. Esto devuelve información de la tabla de conflictos para los artículos con conflictos. Tenga en cuenta el valor de **conflict_table** para cualquier artículo de interés. Si el valor de **conflict_table** para un artículo es NULL, sólo los conflictos de eliminación se han producido en este artículo.  
  
3.  (Opcional) Revise las filas de conflicto para los artículos de interés. Según los valores de **centralized_conflicts** y **decentralized_conflicts** del paso 1, realice una de las siguientes acciones:  
  
    -   En el publicador de la base de datos de publicación, ejecute [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Especifique una tabla de conflictos para el artículo (del paso 1) para **@conflict_table**. (Opcional) Especifique un valor de **@publication** para restringir la información de conflicto devuelta a una publicación específica. Esto devuelve datos de fila y otra información para la fila perdedora.  
  
    -   En el suscriptor en la base de datos de suscripción, ejecute [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Especifique una tabla de conflictos para el artículo (del paso 1) para **@conflict_table**. Esto devuelve datos de fila y otra información para la fila perdedora.  
  
### Para ver información únicamente acerca de los conflictos en los que se produjo un error en la eliminación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Tenga en cuenta los valores de las siguientes columnas en el conjunto de resultados:  
  
    -   **centralized_conflicts** -1 indica que las filas de conflicto se almacenan en el publicador y 0 indica que no se almacenan filas de conflicto en el publicador.  
  
    -   **decentralized_conflicts** -1 indica que las filas de conflicto se almacenan en el suscriptor y 0 indica que no se almacenan filas de conflicto en el suscriptor.  
  
        > [!NOTE]  
        >  El comportamiento de registro de conflictos de una publicación de mezcla se establece mediante la **@conflict_logging** parámetro de [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). El uso de la **@centralized_conflicts** parámetro ha quedado desusado.  
  
2.  En el publicador de la base de datos de publicación o en el suscriptor de la base de datos de suscripción, ejecute [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Especifique un valor para **@publication** para devolver únicamente información de tabla de conflictos para los artículos que pertenecen a una publicación concreta. Esto devuelve información de la tabla de conflictos para los artículos con conflictos. Tenga en cuenta el valor de **source_object** para cualquier artículo de interés. Si el valor de **conflict_table** para un artículo es NULL, sólo los conflictos de eliminación se han producido en este artículo.  
  
3.  (Opcional) Revise la información de conflictos para conflictos de eliminación. Según los valores de **centralized_conflicts** y **decentralized_conflicts** del paso 1, realice una de las siguientes acciones:  
  
    -   En el publicador de la base de datos de publicación, ejecute [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Especifique el nombre de la tabla de origen (desde el paso 1) en el que se produjo el conflicto para **@source_object**. (Opcional) Especifique un valor de **@publication** para restringir la información de conflicto devuelta a una publicación específica. Esto devuelve elimine la información de eliminación de conflictos almacenada en el publicador.  
  
    -   En el suscriptor en la base de datos de suscripción, ejecute [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Especifique el nombre de la tabla de origen (desde el paso 1) en el que se produjo el conflicto para **@source_object**. (Opcional) Especifique un valor de **@publication** para restringir la información de conflicto devuelta a una publicación específica. Esto devuelve elimine la información de eliminación de conflictos almacenada en el suscriptor.  
  
## Vea también  
 [Detección y resolución de conflictos de replicación de mezcla avanzada](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  