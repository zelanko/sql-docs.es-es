---
title: Eliminación de una artículo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
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
ms.openlocfilehash: c3d425e069d8a1e942ee5b7fd6277d4fc4037b15
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48123515"
---
# <a name="delete-an-article"></a>Eliminar un artículo
  En este tema se describe cómo eliminar un artículo en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Replication Management Objects (RMO). Para obtener información sobre las condiciones en que se pueden quitar artículos, y si la eliminación de un artículo requiere una nueva instantánea o la reinicialización de las suscripciones, vea [Agregar y quitar artículos de publicaciones existentes](add-articles-to-and-drop-articles-from-existing-publications.md).  
  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Los artículos pueden eliminarse mediante programación con procedimientos almacenados de replicación. Los procedimientos almacenados que se usen dependerán del tipo de publicación a la que pertenece el artículo.  
  
#### <a name="to-delete-an-article-from-a-snapshot-or-transactional-publication"></a>Para eliminar un artículo de una publicación de instantáneas o transaccional  
  
1.  Ejecute [sp_droparticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql) para eliminar un artículo, especificado por **@article**, de una publicación, especificado por **@publication**. Especifique un valor de **1** para **@force_invalidate_snapshot**.  
  
2.  (Opcional) Para quitar completamente el objeto publicado de la base de datos, ejecute el comando `DROP <objectname>` en el publicador de la base de datos de publicación.  
  
#### <a name="to-delete-an-article-from-a-merge-publication"></a>Para eliminar un artículo de una publicación de combinación  
  
1.  Ejecute [sp_dropmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql) para eliminar un artículo, especificado por **@article**, de una publicación, especificado por **@publication**. Si es necesario, especifique un valor de **1** para **@force_invalidate_snapshot** y un valor de **1** para **@force_reinit_subscription**.  
  
2.  (Opcional) Para quitar completamente el objeto publicado de la base de datos, ejecute el comando `DROP <objectname>` en el publicador de la base de datos de publicación.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 En el siguiente ejemplo se elimina un artículo de una publicación transaccional Dado que este cambio invalida la instantánea existente, se especifica un valor de **1** para el parámetro **@force_invalidate_snapshot** .  
  
 [!code-sql[HowTo#sp_droparticle](../../../snippets/tsql/SQL15/replication/howto/tsql/droptranpub.sql#sp_droparticle)]  
  
 El ejemplo siguiente elimina dos artículos de una publicación de combinación. Dado que estos cambios invalidan la instantánea existente, se especifica un valor de **1** para el parámetro **@force_invalidate_snapshot** .  
  
 [!code-sql[HowTo#sp_dropmergearticle](../../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepub.sql#sp_dropmergearticle)]
 [!code-sql[HowTo#sp_dropmergearticle](../../../snippets/tsql/SQL15/replication/howto/tsql/dropmergearticles.sql#sp_dropmergearticle)]  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Puede eliminar artículos mediante programación utilizando Replication Management Objects (RMO). Las clases RMO que usa para eliminar un artículo dependen del tipo de publicación al que pertenece el artículo.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>Para eliminar un artículo que pertenece a una publicación transaccional o de instantáneas  
  
1.  Cree una conexión al publicador mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.TransArticle> .  
  
3.  Establezca las propiedades <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>y <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> .  
  
4.  Establezca la conexión del paso 1 para la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Compruebe la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para asegurarse de que el artículo existe. Si el valor de esta propiedad es `false`, las propiedades del artículo en el paso 3 se definieron incorrectamente o el artículo no existe.  
  
6.  Llame al método <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> .  
  
7.  Cierre todas las conexiones.  
  
#### <a name="to-delete-an-article-that-belongs-to-a-merge-publication"></a>Para eliminar un artículo que pertenece a una publicación de combinación  
  
1.  Cree una conexión al publicador mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.MergeArticle> .  
  
3.  Establezca las propiedades <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>y <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> .  
  
4.  Establezca la conexión del paso 1 para la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Compruebe la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para asegurarse de que el artículo existe. Si el valor de esta propiedad es `false`, las propiedades del artículo en el paso 3 se definieron incorrectamente o el artículo no existe.  
  
6.  Llame al método <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> .  
  
7.  Cierre todas las conexiones.  
  
## <a name="see-also"></a>Vea también  
 [Agregar y quitar artículos de publicaciones existentes](add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Conceptos de procedimientos almacenados del sistema de replicación](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
