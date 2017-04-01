---
title: "Establecer el nivel de compatibilidad para publicaciones de mezcla | Microsoft Docs"
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
  - "compatibilidad [SQL Server], replicación"
  - "compatibilidad con versiones anteriores [SQL Server], replicación"
  - "publicaciones [replicación de SQL Server], compatibilidad con versiones anteriores"
ms.assetid: db47ac73-948b-4d77-b272-bb3565135ea5
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Establecer el nivel de compatibilidad para publicaciones de mezcla
  En este tema se describe cómo establecer el nivel de compatibilidad para las publicaciones de mezcla en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. La replicación de mezcla emplea el nivel de compatibilidad de la publicación para determinar qué características pueden usar las publicaciones de una base de datos determinada.  
  
 **En este tema**  
  
-   **Para establecer el nivel de compatibilidad para publicaciones de mezcla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Establezca el nivel de compatibilidad en la página **Tipos de suscriptor** del Asistente para nueva publicación. Para obtener más información sobre el acceso a este asistente, consulte [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md). Después de crear una publicación de instantáneas, el nivel de compatibilidad se puede aumentar pero no se puede reducir. Aumentar el nivel de compatibilidad en la **General** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md). Si aumenta el nivel de compatibilidad, las suscripciones existentes en los servidores que se ejecuten con versiones anteriores al nivel de compatibilidad no se podrán sincronizar.  
  
> [!NOTE]  
>  Debido a que el nivel de compatibilidad tiene implicaciones en otras propiedades de la publicación y en cuanto a qué propiedades del artículo son válidas, no cambie el nivel de compatibilidad ni otras propiedades en el mismo uso del cuadro de diálogo. La instantánea de la publicación se volverá a generar después de cambiar la propiedad.  
  
#### Para establecer el nivel de compatibilidad de la publicación  
  
-   En la página **Tipos de suscriptor** del Asistente para nueva publicación, seleccione los tipos de suscriptores que admitirá la publicación.  
  
#### Para aumentar el nivel de compatibilidad de la publicación  
  
-   En la **General** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione **nivel de compatibilidad**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 El nivel de compatibilidad para una publicación de combinación se puede establecer mediante programación cuando una publicación se crea o bien, se puede modificar mediante programación en un momento posterior. Puede usar procedimientos almacenados de replicación para establecer o cambiar esta propiedad de publicación.  
  
#### Para establecer el nivel de compatibilidad de la publicación para una publicación de combinación  
  
1.  En el publicador, ejecute [sp_addmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), especificando un valor para **@publication_compatibility_level** para que la publicación sea compatible con versiones anteriores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### Para cambiar el nivel de compatibilidad de la publicación de una publicación de combinación  
  
1.  Ejecutar [sp_changemergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), especificando **publication_compatibility_level** para **@property** y el nivel de compatibilidad de la publicación apropiada para **@value**.  
  
#### Para determinar el nivel de compatibilidad de la publicación de una publicación de combinación  
  
1.  Ejecutar [sp_helpmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especificando la publicación deseada.  
  
2.  Busque el nivel de compatibilidad en el **backward_comp_level** columna del conjunto de resultados.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 Este ejemplo crea una publicación de combinación y establece el nivel de compatibilidad de la publicación.  
  
```  
-- To avoid storing the login and password in the script file, the values   
-- are passed into SQLCMD as scripting variables. For information about   
-- how to use scripting variables on the command line and in SQL Server  
-- Management Studio, see the "Executing Replication Scripts" section in  
-- the topic "Programming Replication Using System Stored Procedures".  
  
--Add a new merge publication.  
DECLARE @publicationDB AS sysname;  
DECLARE @publication AS sysname;  
DECLARE @login AS sysname;  
DECLARE @password AS sysname;  
SET @publicationDB = N'AdventureWorks2012';   
SET @publication = N'AdvWorksSalesOrdersMerge'   
SET @login = $(Login);  
SET @password = $(Password);  
  
-- Create a new merge publication.   
USE [AdventureWorks2012]  
EXEC sp_addmergepublication   
@publication = @publication,   
-- Set the compatibility level to SQL Server 2014.  
@publication_compatibility_level = '120RTM';   
  
-- Create the snapshot job for the publication.  
EXEC sp_addpublication_snapshot   
@publication = @publication,  
@job_login = @login,  
@job_password = @password;  
GO  
```  
  
 Este ejemplo cambia el nivel de compatibilidad de la publicación para la publicación de combinación.  
  
> [!NOTE]  
>  Cambiar el nivel de compatibilidad de la publicación podría no permitirse si la publicación usa alguna característica que requiera un nivel de compatibilidad determinado. Para obtener más información, consulte [compatibilidad con versiones anteriores de replicación](../../../relational-databases/replication/replication-backward-compatibility.md).  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
  
-- Change the publication compatibility level to   
-- SQL Server 2012.  
EXEC sp_changemergepublication   
@publication = @publication,   
@property = N'publication_compatibility_level',   
@value = N'110RTM';  
GO  
  
```  
  
 Este ejemplo devuelve el nivel de compatibilidad de la publicación actual para la publicación de combinación.  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
EXEC sp_helpmergepublication   
@publication = @publication;  
GO  
  
```  
  
## Vea también  
 [Crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md)  
  
  