---
title: "Especificar el seguimiento de conflictos y el nivel de resoluci&#243;n para art&#237;culos de mezcla | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "resolución de conflictos de replicación de mezcla [replicación de SQL Server], niveles"
  - "artículos [replicación de SQL Server], resolución de conflictos"
  - "resolución de conflictos [replicación de SQL Server], replicación de mezcla"
ms.assetid: 81e9ecb6-1d31-4a78-b32a-96f7f4d67077
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Especificar el seguimiento de conflictos y el nivel de resoluci&#243;n para art&#237;culos de mezcla
  En este tema se describe cómo especificar el seguimiento de conflictos y el nivel de resolución para artículos de mezcla en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Cuando se sincroniza una suscripción a una publicación de combinación, la replicación comprueba los conflictos producidos por los cambios a los mismos datos realizados en el Publicador y el Suscriptor. Puede especificar si los conflictos se detectan en el nivel de fila, donde cualquier cambio a la fila se considera un conflicto, o en el nivel de columna, donde solo se consideran un conflicto los cambios a la misma fila y columna. La resolución de conflictos para los artículos se realiza en el nivel de fila. Para obtener más información sobre la detección y resolución de conflictos cuando se usan registros lógicos, vea [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   **Para especificar el seguimiento de conflictos y el nivel de resolución para artículos de mezcla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si modifica el nivel de seguimiento después de que se hayan inicializado las suscripciones, se deben reinicializar dichas suscripciones. Para obtener más información acerca de los efectos de los cambios de propiedad, vea [Propiedades de artículo y publicación de cambio](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
-   Con el seguimiento por columna y por fila, la resolución de conflictos se realiza siempre en el nivel de fila: la fila ganadora sobrescribe la fila perdedora. La replicación de mezcla también le permite especificar que se realice un seguimiento de los conflictos y se resuelvan en el nivel de registro lógico, pero dichas opciones no están disponibles en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Para obtener información acerca de cómo establecer estas opciones con procedimientos almacenados de replicación, vea [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Especificar la columna de nivel de fila o de seguimiento para artículos de mezcla en la **propiedades** ficha de la **Propiedades del artículo** cuadro de diálogo, que está disponible en el Asistente para nueva publicación y la **Propiedades de publicación: \< publicación>** cuadro de diálogo. Para obtener más información sobre cómo usar el asistente y acceso al cuadro de diálogo, vea [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar el seguimiento por fila o por columna  
  
1.  En el **artículos** página del Asistente para nueva publicación o **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione una tabla.  
  
2.  Haga clic en **Propiedades del artículo**y, a continuación, haga clic en **Establecer propiedades del artículo de tabla resaltado** o en **Establecer propiedades de todos los artículos de la tabla**.  
  
3.  En la **propiedades** ficha de la **Propiedades del artículo \< artículo>** cuadro de diálogo, seleccione uno de los siguientes valores para el **nivel de seguimiento** propiedad: **seguimiento de nivel de fila** o **el seguimiento de nivel de columna**.  
  
4.  Si se encuentra en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para especificar las opciones de seguimiento de conflictos para un nuevo artículo de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) y especifique uno de los siguientes valores para **@column_tracking**:  
  
    -   **True** -Use el seguimiento de nivel de columna para el artículo.  
  
    -   **false** -seguimiento de nivel de fila de uso, que es el valor predeterminado.  
  
#### Para cambiar las opciones de seguimiento de conflictos para un artículo de mezcla  
  
1.  Para determinar el conflicto de opciones de seguimiento de un artículo de mezcla, ejecute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Tenga en cuenta el valor de la **column_tracking** opción en el conjunto de resultados para el artículo. Un valor de **1** significa que se utiliza el seguimiento de nivel de columna y el valor de **0** significa que se utiliza el seguimiento de nivel de fila.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique un valor de **column_tracking** para **@property** y uno de los siguientes valores para **@value**:  
  
    -   **True** -Use el seguimiento de nivel de columna para el artículo.  
  
    -   **false** -seguimiento de nivel de fila de uso, que es el valor predeterminado.  
  
     Especifique un valor de **1** para ambos **@force_invalidate_snapshot** y **@force_reinit_subscription**.  
  
## Vea también  
 [Detección y resolución de conflictos de replicación de mezcla avanzada](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Detectar y solucionar conflictos en registros lógicos](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md)   
 [Definir una relación de registros lógicos entre artículos de tabla de mezcla](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Detectar y solucionar conflictos de replicación de mezcla](../../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md)  
  
  