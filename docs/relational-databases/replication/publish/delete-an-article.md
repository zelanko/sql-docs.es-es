---
title: Eliminación de una artículo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], dropping
- sp_droparticle
- sp_dropmergearticle
- deleting articles
- removing articles
- dropping articles
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 40a543a8b95853cacfb00f284e916ca216cd57b3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759230"
---
# <a name="delete-an-article"></a>Eliminar un artículo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo eliminar un artículo en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Replication Management Objects (RMO). Para obtener información sobre las condiciones en que se pueden quitar artículos, y si la eliminación de un artículo requiere una nueva instantánea o la reinicialización de las suscripciones, vea [Agregar y quitar artículos de publicaciones existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 **En este tema**  
  
-   **Para eliminar un artículo, mediante:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Los artículos pueden eliminarse mediante programación con procedimientos almacenados de replicación. Los procedimientos almacenados que se usen dependerán del tipo de publicación a la que pertenece el artículo.  
  
#### <a name="to-delete-an-article-from-a-snapshot-or-transactional-publication"></a>Para eliminar un artículo de una publicación de instantáneas o transaccional  
  
1.  Ejecute [sp_droparticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md) para eliminar un artículo, especificado por **@article**, de una publicación, especificado por **@publication**. Especifique un valor de **1** para **@force_invalidate_snapshot**.  
  
2.  (Opcional) Para quitar completamente el objeto publicado de la base de datos, ejecute el comando `DROP <objectname>` en el publicador de la base de datos de publicación.  
  
#### <a name="to-delete-an-article-from-a-merge-publication"></a>Para eliminar un artículo de una publicación de combinación  
  
1.  Ejecute [sp_dropmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) para eliminar un artículo, especificado por **@article**, de una publicación, especificado por **@publication**. Si es necesario, especifique un valor de **1** para **@force_invalidate_snapshot** y un valor de **1** para **@force_reinit_subscription**.  
  
2.  (Opcional) Para quitar completamente el objeto publicado de la base de datos, ejecute el comando `DROP <objectname>` en el publicador de la base de datos de publicación.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 En el siguiente ejemplo se elimina un artículo de una publicación transaccional Dado que este cambio invalida la instantánea existente, se especifica un valor de **1** para el parámetro **@force_invalidate_snapshot** .  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article AS sysname;  
SET @publication = N'AdvWorksProductTran';   
SET @article = N'Product';   
  
-- Drop the transactional article.  
USE [AdventureWorks]  
EXEC sp_droparticle   
  @publication = @publication,   
  @article = @article,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
 El ejemplo siguiente elimina dos artículos de una publicación de combinación. Dado que estos cambios invalidan la instantánea existente, se especifica un valor de **1** para el parámetro **@force_invalidate_snapshot** .  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article1 AS sysname;  
DECLARE @article2 AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @article1 = N'SalesOrderDetail';   
SET @article2 = N'SalesOrderHeader';   
  
-- Remove articles from a merge publication.  
USE [AdventureWorks]  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article1,  
  @force_invalidate_snapshot = 1;  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article2,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Puede eliminar artículos mediante programación utilizando Replication Management Objects (RMO). Las clases RMO que usa para eliminar un artículo dependen del tipo de publicación al que pertenece el artículo.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>Para eliminar un artículo que pertenece a una publicación transaccional o de instantáneas  
  
1.  Cree una conexión al publicador mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.TransArticle> .  
  
3.  Establezca las propiedades <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>y <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> .  
  
4.  Establezca la conexión del paso 1 para la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Compruebe la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para asegurarse de que el artículo existe. Si el valor de esta propiedad es **false**, se definieron incorrectamente las propiedades de artículo en el paso 3, o bien el artículo no existe.  
  
6.  Llame al método <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> .  
  
7.  Cierre todas las conexiones.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-merge-publication"></a>Para eliminar un artículo que pertenece a una publicación de combinación  
  
1.  Cree una conexión al publicador mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.MergeArticle> .  
  
3.  Establezca las propiedades <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>y <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> .  
  
4.  Establezca la conexión del paso 1 para la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Compruebe la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para asegurarse de que el artículo existe. Si el valor de esta propiedad es **false**, se definieron incorrectamente las propiedades de artículo en el paso 3, o bien el artículo no existe.  
  
6.  Llame al método <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> .  
  
7.  Cierre todas las conexiones.  
  
## <a name="see-also"></a>Ver también  
 [Agregar y quitar artículos de publicaciones existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Conceptos de procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
