---
title: "Eliminar un art&#237;culo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "artículos [replicación de SQL Server], anular"
  - "sp_droparticle"
  - "sp_dropmergearticle"
  - "eliminar artículos"
  - "artículos, quitar"
  - "quitar artículos"
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Eliminar un art&#237;culo
  En este tema se describe cómo eliminar un artículo en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Replication Management Objects (RMO). Para obtener información sobre las condiciones en los artículos que se pueden quitar y si se quita un artículo requiere una nueva instantánea o la reinicialización de suscripciones, consulte [Agregar y quitar artículos de publicaciones existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 **En este tema**  
  
-   **Para eliminar un artículo, mediante:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Los artículos pueden eliminarse mediante programación con procedimientos almacenados de replicación. Los procedimientos almacenados que se usen dependerán del tipo de publicación a la que pertenece el artículo.  
  
#### Para eliminar un artículo de una publicación de instantáneas o transaccional  
  
1.  Ejecutar [sp_droparticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md) Para eliminar un artículo, especificado por **@article**, de una publicación, especificada por **@publication**. Especifique un valor de **1** para **@force_invalidate_snapshot**.  
  
2.  (Opcional) Para quitar completamente el objeto publicado de la base de datos, ejecute el comando `DROP <objectname>` en el publicador de la base de datos de publicación.  
  
#### Para eliminar un artículo de una publicación de combinación  
  
1.  Ejecutar [sp_dropmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) Para eliminar un artículo, especificado por **@article**, de una publicación, especificada por **@publication**. Si es necesario, especifique un valor de **1** para **@force_invalidate_snapshot** y un valor de **1** para **@force_reinit_subscription**.  
  
2.  (Opcional) Para quitar completamente el objeto publicado de la base de datos, ejecute el comando `DROP <objectname>` en el publicador de la base de datos de publicación.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 En el siguiente ejemplo se elimina un artículo de una publicación transaccional Dado que este cambio invalida la instantánea existente, un valor de **1** se especifica para el **@force_invalidate_snapshot** parámetro.  
  
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
  
 El ejemplo siguiente elimina dos artículos de una publicación de combinación. Dado que estos cambios invalidarán la instantánea existente, un valor de **1** se especifica para el **@force_invalidate_snapshot** parámetro.  
  
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
  
#### Para eliminar un artículo que pertenece a una publicación transaccional o de instantáneas  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransArticle> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, y <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> Propiedades.  
  
4.  Establezca la conexión del paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
5.  Compruebe el <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> propiedad para comprobar que existe el artículo. Si el valor de esta propiedad es **false**, se definieron incorrectamente las propiedades de artículo en el paso 3, o bien el artículo no existe.  
  
6.  Llame a la <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> método.  
  
7.  Cierre todas las conexiones.  
  
#### Para eliminar un artículo que pertenece a una publicación de combinación  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergeArticle> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, y <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> Propiedades.  
  
4.  Establezca la conexión del paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
5.  Compruebe el <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> propiedad para comprobar que existe el artículo. Si el valor de esta propiedad es **false**, se definieron incorrectamente las propiedades de artículo en el paso 3, o bien el artículo no existe.  
  
6.  Llame a la <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> método.  
  
7.  Cierre todas las conexiones.  
  
## Vea también  
 [Agregar y quitar artículos de publicaciones existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  