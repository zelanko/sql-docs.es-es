---
title: "Replicar cambios de esquema | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicación [SQL Server], cambiar esquema"
  - "esquemas [replicación de SQL Server], replicar cambios"
ms.assetid: c09007f0-9374-4f60-956b-8a87670cd043
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# Replicar cambios de esquema
  En este tema se describe cómo replicar cambios de esquema en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Si realiza los siguientes cambios del esquema en un artículo publicado, se propagan de forma predeterminada a los suscriptores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   **Para replicar cambios de esquema con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   La instrucción ALTER TABLE … DROP COLUMN siempre se replica en todos los suscriptores cuya suscripción contenga las columnas que se van a quitar, aunque deshabilite la replicación de cambios de esquema.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Si no desea replicar los cambios de esquema para una publicación, deshabilite la replicación de cambios de esquema en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para deshabilitar la replicación de los cambios de esquema  
  
1.  En el **Opciones de suscripción** página de la **Propiedades de la publicación - \< publicación>** diálogo cuadro, establezca el valor de la **replicar cambios de esquema** propiedad **False**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Para propagar únicamente los cambios de esquema específicos, establezca la propiedad en **True** antes de un cambio de esquema y vuelva a establecerla en **False** después de realizar el cambio. A la inversa, para propagar la mayoría de los cambios de esquema, excepto un cambio determinado, establezca la propiedad en **False** antes de un cambio de esquema y vuelva a establecerla en **True** después de realizar el cambio.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede utilizar los procedimientos almacenados de replicación para especificar si se replican estos cambios de esquema. El procedimiento almacenado que utiliza depende del tipo de publicación.  
  
#### Para crear una instantánea o una publicación transaccional que no replique cambios de esquema  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addpublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), especificando un valor de **0** para **@replicate_ddl**. Para obtener más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### Para crear una publicación de combinación que no replique cambios de esquema  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), especificando un valor de **0** para **@replicate_ddl**. Para obtener más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### Para deshabilitar temporalmente la replicación de cambios de esquema para una instantánea o una publicación transaccional  
  
1.  Para una publicación con la replicación de cambios de esquema, ejecute [sp_changepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), especificando un valor de **replicate_ddl** para **@property** y un valor de **0** para **@value**.  
  
2.  Ejecute el comando DDL en el objeto publicado.  
  
3.  (Opcional) Volver a habilitar la replicación de cambios de esquema mediante la ejecución de [sp_changepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), especificando un valor de **replicate_ddl** para **@property** y un valor de **1** para **@value**.  
  
#### Para deshabilitar temporalmente la replicación de cambios de esquema para una publicación de combinación  
  
1.  Para una publicación con la replicación de cambios de esquema, ejecute [sp_changemergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), especificando un valor de **replicate_ddl** para **@property** y un valor de **0** para **@value**.  
  
2.  Ejecute el comando DDL en el objeto publicado.  
  
3.  (Opcional) Volver a habilitar la replicación de cambios de esquema mediante la ejecución de [sp_changemergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), especificando un valor de **replicate_ddl** para **@property** y un valor de **1** para **@value**.  
  
## Vea también  
 [Realizar cambios de esquema en bases de datos de publicaciones](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [Realizar cambios de esquema en bases de datos de publicaciones](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  