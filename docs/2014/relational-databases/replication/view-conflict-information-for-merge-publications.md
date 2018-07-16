---
title: Ver información de conflictos para publicaciones de mezcla (programación de replicación Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- sp_helpmergeconflictrows
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
- sp_helpmergearticleconflicts
ms.assetid: 4907fe35-10ee-4f81-b924-fc419b1864d2
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48225870d89fc6bf39355957187fac84a704093d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37316105"
---
# <a name="view-conflict-information-for-merge-publications-replication-transact-sql-programming"></a>Ver información de conflictos para publicaciones de mezcla (programación de la replicación con Transact-SQL)
  Cuando se resuelve un conflicto en la replicación de mezcla, los datos de la fila que falta se escriben en una tabla de conflictos. Estos datos de conflicto se pueden ver mediante programación usando los procedimientos almacenados de replicación. Para obtener más información, consulte [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### <a name="to-view-conflict-information-and-losing-row-data-for-all-types-of-conflicts"></a>Para ver información de conflictos y los datos de la fila perdedora para todos los tipos de conflictos  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql). Tenga en cuenta los valores de las siguientes columnas en el conjunto de resultados:  
  
    -   **centralized_conflicts** : 1 indica que las filas de conflicto están almacenadas en el Publicador y 0 indica que las filas de conflicto no están almacenadas en el Publicador.  
  
    -   **decentralized_conflicts** : 1 indica que las filas de conflicto están almacenadas en el Suscriptor y 0 indica que las filas de conflicto no están almacenadas en el Suscriptor.  
  
        > [!NOTE]  
        >  El comportamiento del registro de conflictos de una publicación de combinación se establece usando el parámetro **@conflict_logging** de [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). El uso del parámetro **@centralized_conflicts** ha quedado desusado.  
  
     La tabla siguiente describe los valores de estas columnas basados en el valor especificado para **@conflict_logging**.  
  
    |Valor @conflict_logging|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |`publisher`|1|0|  
    |`subscriber`|0|1|  
    |`both`|1|1|  
  
2.  En el publicador de la base de datos de publicación o en el suscriptor de la base de datos de suscripciones, ejecute [sp_helpmergearticleconflicts](/sql/relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql). Especifique un valor para **@publication** para devolver únicamente información de conflicto para los artículos que pertenecen a una publicación concreta. Esto devuelve información de la tabla de conflictos para los artículos con conflictos. Tenga en cuenta el valor de **conflict_table** para cualquier artículo de interés. Si el valor de **conflict_table** para un artículo es NULL, basta con que elimine los conflictos que se han producido en este artículo.  
  
3.  (Opcional) Revise las filas de conflicto para los artículos de interés. Según los valores de **centralized_conflicts** y **decentralized_conflicts** del paso 1, realice una de las siguientes operaciones:  
  
    -   En la base de datos de publicación del publicador, ejecute [sp_helpmergeconflictrows](/sql/relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql). Especifique una tabla de conflictos para el artículo (del paso 1) para **@conflict_table**. (Opcional) Especifique un valor de **@publication** para restringir la información de conflicto devuelta a una publicación concreta. Esto devuelve datos de fila y otra información para la fila perdedora.  
  
    -   En el suscriptor de la base de datos de suscripciones, ejecute [sp_helpmergeconflictrows](/sql/relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql). Especifique una tabla de conflictos para el artículo (del paso 1) para **@conflict_table**. Esto devuelve datos de fila y otra información para la fila perdedora.  
  
### <a name="to-view-information-only-on-conflicts-where-the-delete-failed"></a>Para ver información únicamente acerca de los conflictos en los que se produjo un error en la eliminación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql). Tenga en cuenta los valores de las siguientes columnas en el conjunto de resultados:  
  
    -   **centralized_conflicts** : 1 indica que las filas de conflicto están almacenadas en el Publicador y 0 indica que las filas de conflicto no están almacenadas en el Publicador.  
  
    -   **decentralized_conflicts** : 1 indica que las filas de conflicto están almacenadas en el Suscriptor y 0 indica que las filas de conflicto no están almacenadas en el Suscriptor.  
  
        > [!NOTE]  
        >  El comportamiento del registro de conflictos de una publicación de combinación se establece usando el parámetro **@conflict_logging** de [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). El uso del parámetro **@centralized_conflicts** ha quedado desusado.  
  
2.  En el publicador de la base de datos de publicación o en el suscriptor de la base de datos de suscripciones, ejecute [sp_helpmergearticleconflicts](/sql/relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql). Especifique un valor para **@publication** para devolver únicamente información de tabla de conflictos para los artículos que pertenecen a una publicación concreta. Esto devuelve información de la tabla de conflictos para los artículos con conflictos. Tenga en cuenta el valor de **source_object** para cualquier artículo de interés. Si el valor de **conflict_table** para un artículo es NULL, basta con que elimine los conflictos que se han producido en este artículo.  
  
3.  (Opcional) Revise la información de conflictos para conflictos de eliminación. Según los valores de **centralized_conflicts** y **decentralized_conflicts** del paso 1, realice una de las siguientes operaciones:  
  
    -   En la base de datos de publicación del publicador, ejecute [sp_helpmergedeleteconflictrows](/sql/relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql). Especifique el nombre de la tabla de origen (del paso 1) en la que el conflicto se produjo para **@source_object**. (Opcional) Especifique un valor de **@publication** para restringir la información de conflicto devuelta a una publicación concreta. Esto devuelve elimine la información de eliminación de conflictos almacenada en el publicador.  
  
    -   En el suscriptor de la base de datos de suscripciones, ejecute [sp_helpmergedeleteconflictrows](/sql/relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql). Especifique el nombre de la tabla de origen (del paso 1) en la que el conflicto se produjo para **@source_object**. (Opcional) Especifique un valor de **@publication** para restringir la información de conflicto devuelta a una publicación concreta. Esto devuelve elimine la información de eliminación de conflictos almacenada en el suscriptor.  
  
## <a name="see-also"></a>Vea también  
 [Replicación de mezcla avanzada: detección y resolución de conflictos](merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
