---
title: Definición y modificación de un filtro de columna | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], column
- modifying filters, column
- modifying filters
- column filters [SQL Server replication]
ms.assetid: d7c3186a-9a8c-45d8-ab34-05beec4c26dd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7e00ceeae68ccc791c3680e029e13844fa6ec683
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68731066"
---
# <a name="define-and-modify-a-column-filter"></a>Definir y modificar un filtro de columna
  En este tema se describe cómo definir y modificar un filtro de columna en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   **Para definir y modificar un filtro de columna con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Algunas columnas no se pueden filtrar. Para obtener más información, vea [Filtrar datos publicados](filter-published-data.md). Si modifica un filtro de columna después de que las suscripciones se hayan inicializado, deberá generar una nueva instantánea y reinicializar todas las suscripciones después de efectuar el cambio. Para obtener más información sobre los requisitos para los cambios de propiedad, consulte [Cambiar las propiedades de la publicación y de los artículos](change-publication-and-article-properties.md) (Cambiar las propiedades de la publicación y de los artículos).  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 Defina los filtros de columna en la página **Artículos** del Asistente para nueva publicación. Para obtener más información sobre cómo usar el Asistente para nueva publicación, vea [Crear una publicación](create-a-publication.md).  
  
 Defina y modifique los filtros de columna en la página **Artículos** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** . Para obtener más información sobre cómo cambiar las propiedades de la publicación, vea [Ver y modificar propiedades de publicación](view-and-modify-publication-properties.md).  
  
#### <a name="to-define-a-column-filter"></a>Para definir un filtro de columna  
  
1.  En la página **Artículos** del Asistente para nueva publicación, expanda la tabla que se va a filtrar en el panel **Objetos para publicar** .  
  
2.  Desactive la casilla situada junto a cada columna que desee filtrar.  
  
#### <a name="to-modify-column-filtering"></a>Para modificar filtros de columna  
  
1.  En la página **Artículos** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** , expanda la tabla que quiere filtrar en el panel **Objetos que se van a publicar**.  
  
2.  Desactive la casilla situada junto a cada columna que desee filtrar y asegúrese de que activa las casillas de las columnas que se deben incluir en el artículo.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Al crear los artículos de la tabla, puede definir qué columnas desea incluir en el artículo y cambiar las columnas una vez definido el artículo. Puede crear y modificar columnas filtradas mediante programación usando los procedimientos almacenados de replicación.  
  
> [!NOTE]  
>  Los procedimientos siguientes suponen que la tabla subyacente no ha cambiado. Para obtener información sobre la replicación de los cambios del lenguaje de definición de datos (DDL) a tablas publicadas, vea [Realizar cambios de esquema en bases de datos de publicaciones](make-schema-changes-on-publication-databases.md).  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>Para definir un filtro de columna para un artículo publicado en una instantánea o publicación transaccional  
  
1.  Defina el artículo que se va a filtrar. Para más información, consulte [Define an Article](define-an-article.md).  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql). Esto define las columnas que se van a incluir o quitar del artículo.  
  
    -   Si se publican solo unas columnas de una tabla con muchas columnas, ejecute [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) una vez para cada columna que se está agregando. Especifique el nombre de la columna en **\@column** y un valor de **add** en **\@operation**.  
  
    -   Si se publica la mayoría de las columnas en una tabla con muchas columnas, ejecute [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) y especifique un valor de **null** para **\@column** y un valor de **add** en **\@operation** para agregar todas las columnas. Después, ejecute [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql), una vez para cada columna que se va a excluir, y especifique un valor de **drop** para **\@operation** y el nombre de la columna excluida en **\@column**.  
  
3.  En la base de datos de publicación del publicador, ejecute [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql). Especifique el nombre de la publicación para **\@publication** y el nombre del artículo filtrado para **\@article**. Esto crea los objetos de sincronización para el artículo filtrado.  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>Para cambiar un filtro de columna para que incluya las columnas adicionales para un artículo publicado en una instantánea o publicación transaccional  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) para cada columna que se está agregando. Especifique el nombre de la columna en **\@column** y un valor de **add** en **\@operation**.  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql). Especifique el nombre de la publicación para **\@publication** y el nombre del artículo filtrado para **\@article**. Si la publicación tiene suscripciones existentes, especifique un valor de **1** para **\@change_active**. Esto vuelve a crear los objetos de sincronización para el artículo filtrado.  
  
3.  Vuelva a ejecutar el trabajo del Agente de instantáneas para que la publicación genere una instantánea actualizada.  
  
4.  Reinicialice las suscripciones. Para obtener más información, vea [Reinicializar suscripciones](../reinitialize-subscriptions.md).  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>Para cambiar un filtro de columna para quitar columnas para un artículo publicado en una instantánea o publicación transaccional  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) para cada columna que se está quitando. Especifique el nombre de la columna para **\@column** y un valor de **drop** para **\@operation**.  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql). Especifique el nombre de la publicación para **\@publication** y el nombre del artículo filtrado para **\@article**. Si la publicación tiene suscripciones existentes, especifique un valor de **1** para **\@change_active**. Esto vuelve a crear los objetos de sincronización para el artículo filtrado.  
  
3.  Vuelva a ejecutar el trabajo del Agente de instantáneas para que la publicación genere una instantánea actualizada.  
  
4.  Reinicialice las suscripciones. Para obtener más información, vea [Reinicializar suscripciones](../reinitialize-subscriptions.md).  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-merge-publication"></a>Para definir un filtro de columna para un artículo publicado en una publicación de combinación  
  
1.  Defina el artículo que se va a filtrar. Para más información, consulte [Define an Article](define-an-article.md).  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql). Esto define las columnas que se van a incluir o quitar del artículo.  
  
    -   Si se publican solo unas columnas de una tabla con muchas columnas, ejecute [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) una vez para cada columna que se está agregando. Especifique el nombre de la columna en **\@column** y un valor de **add** en **\@operation**.  
  
    -   Si se publica la mayoría de las columnas en una tabla con muchas columnas, ejecute [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) y especifique un valor de **null** para **\@column** y un valor de **add** en **\@operation** para agregar todas las columnas. Después, ejecute [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql), una vez para cada columna que se va a excluir, y especifique un valor de **drop** para **\@operation** y el nombre de la columna excluida para **\@column**.  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-merge-publication"></a>Para cambiar un filtro de columna para que incluya columnas adicionales para un artículo publicado en una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) para cada columna que se está agregando. Especifique el nombre de la columna para **\@column**, un valor de **add** para **\@operation** y un valor de **1** para **\@force_invalidate_snapshot** y **\@force_reinit_subscription**.  
  
2.  Vuelva a ejecutar el trabajo del Agente de instantáneas para que la publicación genere una instantánea actualizada.  
  
3.  Reinicialice las suscripciones. Para obtener más información, vea [Reinicializar suscripciones](../reinitialize-subscriptions.md).  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-merge-publication"></a>Para cambiar un filtro de columna para quitar columnas para un artículo publicado en una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) para cada columna que se está quitando. Especifique el nombre de la columna para **\@column**, un valor de **drop** para **\@operation** y un valor de **1** para **\@force_invalidate_snapshot** y **\@force_reinit_subscription**.  
  
2.  Vuelva a ejecutar el trabajo del Agente de instantáneas para que la publicación genere una instantánea actualizada.  
  
3.  Reinicialice las suscripciones. Para obtener más información, vea [Reinicializar suscripciones](../reinitialize-subscriptions.md).  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 En este ejemplo de replicación transaccional, la columna `DaysToManufacture` se quita de un artículo basado en la tabla `Product` .  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createtranpub.sql#sp_addtranarticle)]  
  
 En este ejemplo de replicación de mezcla, la columna `CreditCardApprovalCode` se quita de un artículo basado en la tabla `SalesOrderHeader` .  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergearticle)]  
  
## <a name="see-also"></a>Consulte también  
 [Cambiar las propiedades de la publicación y de los artículos](change-publication-and-article-properties.md)   
 [Filtrar datos publicados](filter-published-data.md)   
 [Filtrar datos publicados para la replicación de mezcla](../merge/filter-published-data-for-merge-replication.md)  
  
  
