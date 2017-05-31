---
title: "Especificar el seguimiento de conflictos y el nivel de resolución para los artículos de mezcla | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], levels
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 81e9ecb6-1d31-4a78-b32a-96f7f4d67077
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 18b5650ce77b40deb101a16ebd1379600394dcbf
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="specify-the-conflict-tracking-and-resolution-level-for-merge-articles"></a>Especificar el seguimiento de conflictos y el nivel de resolución para artículos de mezcla
  En este tema se describe cómo especificar el seguimiento de conflictos y el nivel de resolución para artículos de mezcla en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Cuando se sincroniza una suscripción a una publicación de combinación, la replicación comprueba los conflictos producidos por los cambios a los mismos datos realizados en el Publicador y el Suscriptor. Puede especificar si los conflictos se detectan en el nivel de fila, donde cualquier cambio a la fila se considera un conflicto, o en el nivel de columna, donde solo se consideran un conflicto los cambios a la misma fila y columna. La resolución de conflictos para los artículos se realiza en el nivel de fila. Para obtener más información sobre la detección y resolución de conflictos cuando se usan registros lógicos, vea [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   **Para especificar el seguimiento de conflictos y el nivel de resolución para artículos de mezcla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si modifica el nivel de seguimiento después de que se hayan inicializado las suscripciones, se deben reinicializar dichas suscripciones. Para obtener más información sobre los efectos de los cambios de propiedad, vea [Change Publication and Article Properties](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) (Cambiar las propiedades de la publicación y de los artículos).  
  
-   Con el seguimiento por columna y por fila, la resolución de conflictos se realiza siempre en el nivel de fila: la fila ganadora sobrescribe la fila perdedora. La replicación de mezcla también le permite especificar que se realice un seguimiento de los conflictos y se resuelvan en el nivel de registro lógico, pero dichas opciones no están disponibles en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Para obtener información acerca de cómo establecer estas opciones con procedimientos almacenados de replicación, vea [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Especifique seguimiento de nivel de columna o fila para los artículos de mezcla en la pestaña **Propiedades** del cuadro de diálogo **Propiedades del artículo**, disponible en el Asistente para nueva publicación y el cuadro de diálogo **Propiedades de la publicación: \<publicación>**. Para obtener más información sobre el uso del asistente y el acceso al cuadro de diálogo, vea [Crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-row--or-column-level-tracking"></a>Para especificar el seguimiento por fila o por columna  
  
1.  En la página **Artículos** del Asistente para nueva publicación o en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, seleccione una tabla.  
  
2.  Haga clic en **Propiedades del artículo**y, a continuación, haga clic en **Establecer propiedades del artículo de tabla resaltado** o en **Establecer propiedades de todos los artículos de la tabla**.  
  
3.  En la pestaña **Propiedades** del cuadro de diálogo **Propiedades del artículo: \<artículo>**, seleccione uno de los valores siguientes para la propiedad **Nivel de seguimiento**: **Seguimiento por fila** o **Seguimiento por columna**.  
  
4.  Si se encuentra en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-specify-conflict-tracking-options-for-a-new-merge-article"></a>Para especificar las opciones de seguimiento de conflictos para un nuevo artículo de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) y especifique uno de los valores siguientes para **@column_tracking**:  
  
    -   **true** : Use el seguimiento del nivel de columna para el artículo.  
  
    -   **falso** : Use el seguimiento de nivel de fila, que es el valor predeterminado.  
  
#### <a name="to-change-conflict-tracking-options-for-a-merge-article"></a>Para cambiar las opciones de seguimiento de conflictos para un artículo de mezcla  
  
1.  Para determinar las opciones de seguimiento de conflictos para un artículo de mezcla, ejecute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Tenga en cuenta el valor de la opción **column_tracking** en el conjunto de resultados para el artículo. Un valor de **1** indica que se está usando el seguimiento del nivel de columna y un valor de **0** indica que se está usando el seguimiento de nivel de fila.  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique un valor de **column_tracking** para **@property** y uno de los valores siguientes para **@value**:  
  
    -   **true** : Use el seguimiento del nivel de columna para el artículo.  
  
    -   **falso** : Use el seguimiento de nivel de fila, que es el valor predeterminado.  
  
     Especifique un valor de **1** para **@force_invalidate_snapshot** y **@force_reinit_subscription**.  
  
## <a name="see-also"></a>Vea también  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Detectar y solucionar conflictos de replicación de mezcla](../../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)  
  
  
