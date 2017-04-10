---
title: "Definir y modificar un filtro de columna | Microsoft Docs"
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
  - "filtros [replicación de SQL Server], columna"
  - "modificar filtros, columna"
  - "modificar filtros"
  - "filtros de columna [replicación de SQL Server]"
ms.assetid: d7c3186a-9a8c-45d8-ab34-05beec4c26dd
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Definir y modificar un filtro de columna
  En este tema se describe cómo definir y modificar un filtro de columna en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   **Para definir y modificar un filtro de columna con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Algunas columnas no se puede filtrar; Para obtener más información, consulte [filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md). Si modifica un filtro de columna después de que las suscripciones se hayan inicializado, deberá generar una nueva instantánea y reinicializar todas las suscripciones después de efectuar el cambio. Para obtener más información acerca de los requisitos para los cambios de propiedad, vea [Propiedades de artículo y publicación de cambio](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Defina los filtros de columna en la página **Artículos** del Asistente para nueva publicación. Para obtener más información acerca de cómo utilizar el Asistente para nueva publicación, vea [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md).  
  
 Definir y modificar los filtros de columna en el **artículos** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información acerca de la publicación y las propiedades de artículo, consulte [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para definir un filtro de columna  
  
1.  En la página **Artículos** del Asistente para nueva publicación, expanda la tabla que se va a filtrar en el panel **Objetos para publicar** .  
  
2.  Desactive la casilla situada junto a cada columna que desee filtrar.  
  
#### Para modificar filtros de columna  
  
1.  En el **artículos** página de la **Propiedades de la publicación - \< publicación>** diálogo cuadro, expanda la tabla que desea filtrar en la **objetos para publicar** panel.  
  
2.  Desactive la casilla situada junto a cada columna que desee filtrar y asegúrese de que activa las casillas de las columnas que se deben incluir en el artículo.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Al crear los artículos de la tabla, puede definir qué columnas desea incluir en el artículo y cambiar las columnas una vez definido el artículo. Puede crear y modificar columnas filtradas mediante programación usando los procedimientos almacenados de replicación.  
  
> [!NOTE]  
>  Los procedimientos siguientes suponen que la tabla subyacente no ha cambiado. Para obtener información sobre la replicación de cambios DDL (lenguaje) de definición de datos en las tablas publicadas, consulte [hacer cambios de esquema en bases de datos de publicación](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
#### Para definir un filtro de columna para un artículo publicado en una instantánea o publicación transaccional  
  
1.  Defina el artículo que se va a filtrar. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Esto define las columnas que se van a incluir o quitar del artículo.  
  
    -   Si se publican solo unas pocas columnas de una tabla con muchas columnas, ejecute [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) para cada columna que se va a agregar. Especifique el nombre de la columna para **@column** y un valor de **add** para **@operation**.  
  
    -   Si publica la mayoría de las columnas de una tabla con muchas columnas, ejecute [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), especificando un valor de **nulo** para **@column** y un valor de **Agregar** para **@operation** para agregar todas las columnas. A continuación, ejecute [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), una vez para cada columna que se excluye, especificando un valor de **drop** para **@operation** y el nombre de columna excluida para **@column**.  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Especifique el nombre de la publicación para **@publication** y el nombre del artículo filtrado para **@article**. Esto crea los objetos de sincronización para el artículo filtrado.  
  
#### Para cambiar un filtro de columna para que incluya las columnas adicionales para un artículo publicado en una instantánea o publicación transaccional  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) para cada columna que se va a agregar. Especifique el nombre de la columna para **@column** y un valor de **add** para **@operation**.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Especifique el nombre de la publicación para **@publication** y el nombre del artículo filtrado para **@article**. Si la publicación tiene suscripciones existentes, especifique un valor de **1** para **@change_active**. Esto vuelve a crear los objetos de sincronización para el artículo filtrado.  
  
3.  Vuelva a ejecutar el trabajo del Agente de instantáneas para que la publicación genere una instantánea actualizada.  
  
4.  Reinicialice las suscripciones. Para obtener más información, consulte [reinicializar suscripciones](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### Para cambiar un filtro de columna para quitar columnas para un artículo publicado en una instantánea o publicación transaccional  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) para cada columna que se va a quitar. Especifique el nombre de la columna para **@column** y un valor de **drop** para **@operation**.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Especifique el nombre de la publicación para **@publication** y el nombre del artículo filtrado para **@article**. Si la publicación tiene suscripciones existentes, especifique un valor de **1** para **@change_active**. Esto vuelve a crear los objetos de sincronización para el artículo filtrado.  
  
3.  Vuelva a ejecutar el trabajo del Agente de instantáneas para que la publicación genere una instantánea actualizada.  
  
4.  Reinicialice las suscripciones. Para obtener más información, consulte [reinicializar suscripciones](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### Para definir un filtro de columna para un artículo publicado en una publicación de combinación  
  
1.  Defina el artículo que se va a filtrar. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md). Esto define las columnas que se van a incluir o quitar del artículo.  
  
    -   Si se publican solo unas pocas columnas de una tabla con muchas columnas, ejecute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) para cada columna que se va a agregar. Especifique el nombre de la columna para **@column** y un valor de **add** para **@operation**.  
  
    -   Si publica la mayoría de las columnas de una tabla con muchas columnas, ejecute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md), especificando un valor de **nulo** para **@column** y un valor de **Agregar** para **@operation** para agregar todas las columnas. A continuación, ejecute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md), una vez para cada columna que se excluye, especificando un valor de **drop** para **@operation** y el nombre de columna excluida para **@column**.  
  
#### Para cambiar un filtro de columna para que incluya columnas adicionales para un artículo publicado en una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) para cada columna que se va a agregar. Especifique el nombre de columna para **@column**, un valor de **Agregar** para **@operation** y un valor de **1** para ambos **@force_invalidate_snapshot** y **@force_reinit_subscription**.  
  
2.  Vuelva a ejecutar el trabajo del Agente de instantáneas para que la publicación genere una instantánea actualizada.  
  
3.  Reinicialice las suscripciones. Para obtener más información, consulte [reinicializar suscripciones](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### Para cambiar un filtro de columna para quitar columnas para un artículo publicado en una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) para cada columna que se va a quitar. Especifique el nombre de columna para **@column**, un valor de **drop** para **@operation** y un valor de **1** para ambos **@force_invalidate_snapshot** y **@force_reinit_subscription**.  
  
2.  Vuelva a ejecutar el trabajo del Agente de instantáneas para que la publicación genere una instantánea actualizada.  
  
3.  Reinicialice las suscripciones. Para obtener más información, consulte [reinicializar suscripciones](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 En este ejemplo de replicación transaccional, la columna `DaysToManufacture` se quita de un artículo basado en la tabla `Product` .  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_1.sql)]  
  
 En este ejemplo de replicación de mezcla, la columna `CreditCardApprovalCode` se quita de un artículo basado en la tabla `SalesOrderHeader` .  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_2.sql)]  
  
## Vea también  
 [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Filtrar datos publicados para la replicación de mezcla](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  