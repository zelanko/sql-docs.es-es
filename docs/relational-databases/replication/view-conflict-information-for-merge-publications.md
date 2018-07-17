---
title: Ver información de conflictos para publicaciones de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
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
ms.openlocfilehash: 754a5c4bed2ba321987c4b0b820f4ad821369f42
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37351695"
---
# <a name="view-conflict-information-for-merge-publications"></a>Ver información de conflictos para publicaciones de mezcla
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Cuando se resuelve un conflicto en la replicación de mezcla, los datos de la fila que falta se escriben en una tabla de conflictos. Estos datos de conflicto se pueden ver mediante programación usando los procedimientos almacenados de replicación. Para obtener más información, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### <a name="to-view-conflict-information-and-losing-row-data-for-all-types-of-conflicts"></a>Para ver información de conflictos y los datos de la fila perdedora para todos los tipos de conflictos  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Tenga en cuenta los valores de las siguientes columnas en el conjunto de resultados:  
  
    -   **centralized_conflicts** : 1 indica que las filas de conflicto están almacenadas en el Publicador y 0 indica que las filas de conflicto no están almacenadas en el Publicador.  
  
    -   **decentralized_conflicts** : 1 indica que las filas de conflicto están almacenadas en el Suscriptor y 0 indica que las filas de conflicto no están almacenadas en el Suscriptor.  
  
        > [!NOTE]  
        >  El comportamiento del registro de conflictos de una publicación de combinación se establece usando el parámetro **@conflict_logging** de [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). El uso del parámetro **@centralized_conflicts** ha quedado desusado.  
  
     La tabla siguiente describe los valores de estas columnas basados en el valor especificado para **@conflict_logging**.  
  
    |Valor @conflict_logging|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publicador**|1|0|  
    |**suscriptor**|0|1|  
    |**ambos**|1|1|  
  
2.  En el publicador de la base de datos de publicación o en el suscriptor de la base de datos de suscripciones, ejecute [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Especifique un valor para **@publication** para devolver únicamente información de conflicto para los artículos que pertenecen a una publicación concreta. Esto devuelve información de la tabla de conflictos para los artículos con conflictos. Tenga en cuenta el valor de **conflict_table** para cualquier artículo de interés. Si el valor de **conflict_table** para un artículo es NULL, basta con que elimine los conflictos que se han producido en este artículo.  
  
3.  (Opcional) Revise las filas de conflicto para los artículos de interés. Según los valores de **centralized_conflicts** y **decentralized_conflicts** del paso 1, realice una de las siguientes operaciones:  
  
    -   En la base de datos de publicación del publicador, ejecute [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Especifique una tabla de conflictos para el artículo (del paso 1) para **@conflict_table**. (Opcional) Especifique un valor de **@publication** para restringir la información de conflicto devuelta a una publicación concreta. Esto devuelve datos de fila y otra información para la fila perdedora.  
  
    -   En el suscriptor de la base de datos de suscripciones, ejecute [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Especifique una tabla de conflictos para el artículo (del paso 1) para **@conflict_table**. Esto devuelve datos de fila y otra información para la fila perdedora.  
  
### <a name="to-view-information-only-on-conflicts-where-the-delete-failed"></a>Para ver información únicamente acerca de los conflictos en los que se produjo un error en la eliminación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Tenga en cuenta los valores de las siguientes columnas en el conjunto de resultados:  
  
    -   **centralized_conflicts** : 1 indica que las filas de conflicto están almacenadas en el Publicador y 0 indica que las filas de conflicto no están almacenadas en el Publicador.  
  
    -   **decentralized_conflicts** : 1 indica que las filas de conflicto están almacenadas en el Suscriptor y 0 indica que las filas de conflicto no están almacenadas en el Suscriptor.  
  
        > [!NOTE]  
        >  El comportamiento del registro de conflictos de una publicación de combinación se establece usando el parámetro **@conflict_logging** de [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). El uso del parámetro **@centralized_conflicts** ha quedado desusado.  
  
2.  En el publicador de la base de datos de publicación o en el suscriptor de la base de datos de suscripciones, ejecute [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Especifique un valor para **@publication** para devolver únicamente información de tabla de conflictos para los artículos que pertenecen a una publicación concreta. Esto devuelve información de la tabla de conflictos para los artículos con conflictos. Tenga en cuenta el valor de **source_object** para cualquier artículo de interés. Si el valor de **conflict_table** para un artículo es NULL, basta con que elimine los conflictos que se han producido en este artículo.  
  
3.  (Opcional) Revise la información de conflictos para conflictos de eliminación. Según los valores de **centralized_conflicts** y **decentralized_conflicts** del paso 1, realice una de las siguientes operaciones:  
  
    -   En la base de datos de publicación del publicador, ejecute [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Especifique el nombre de la tabla de origen (del paso 1) en la que el conflicto se produjo para **@source_object**. (Opcional) Especifique un valor de **@publication** para restringir la información de conflicto devuelta a una publicación concreta. Esto devuelve elimine la información de eliminación de conflictos almacenada en el publicador.  
  
    -   En el suscriptor de la base de datos de suscripciones, ejecute [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Especifique el nombre de la tabla de origen (del paso 1) en la que el conflicto se produjo para **@source_object**. (Opcional) Especifique un valor de **@publication** para restringir la información de conflicto devuelta a una publicación concreta. Esto devuelve elimine la información de eliminación de conflictos almacenada en el suscriptor.  
  
## <a name="see-also"></a>Ver también  
 [Replicación de mezcla avanzada: detección y resolución de conflictos](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
