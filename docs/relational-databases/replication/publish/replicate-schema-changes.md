---
title: Replicación de cambios de esquema | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], schema changes
- schemas [SQL Server replication], replicating changes
ms.assetid: c09007f0-9374-4f60-956b-8a87670cd043
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a436eb86fdaad06e97da94e821d50437e6d938ee
ms.sourcegitcommit: 636c02bd04f091ece934e78640b2363d88cac28d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67860583"
---
# <a name="replicate-schema-changes"></a>Replicar cambios de esquema
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 Si no quiere replicar los cambios de esquema para una publicación, deshabilite la replicación de cambios de esquema en el cuadro de diálogo **Propiedades de la publicación: \<publicación>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-disable-replication-of-schema-changes"></a>Para deshabilitar la replicación de los cambios de esquema  
  
1.  En la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** , establezca el valor de la propiedad **Replicar cambios de esquema** en **False**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     To propagate only specific schema changes, set the property to **True** before a schema change, and then set it to **False** after the change is made. Conversely, to propagate most schema changes, but not a given change, set the property to **False** before the schema change, and then set it to **True** after the change is made.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede utilizar los procedimientos almacenados de replicación para especificar si se replican estos cambios de esquema. El procedimiento almacenado que utiliza depende del tipo de publicación.  
  
#### <a name="to-create-a-snapshot-or-transactional-publication-that-does-not-replicate-schema-changes"></a>Para crear una instantánea o una publicación transaccional que no replique cambios de esquema  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) y especifique un valor de **0** para **@replicate_ddl** . Para obtener más información, vea [Crear una suscripción](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-create-a-merge-publication-that-does-not-replicate-schema-changes"></a>Para crear una publicación de combinación que no replique cambios de esquema  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) y especifique un valor de **0** para **@replicate_ddl** . Para obtener más información, vea [Crear una suscripción](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-snapshot-or-transactional-publication"></a>Para deshabilitar temporalmente la replicación de cambios de esquema para una instantánea o una publicación transaccional  
  
1.  Para una publicación con replicación de cambios de esquema, ejecute [sp_changepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) y especifique un valor de **replicate_ddl** para **@property** y un valor de **0** para **@value** .  
  
2.  Ejecute el comando DDL en el objeto publicado.  
  
3.  (Opcional) vuelva a habilitar la replicación de cambios de esquema ejecutando [sp_changepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) y especificando un valor de **replicate_ddl** para **@property** y un valor de **1** para **@value** .  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-merge-publication"></a>Para deshabilitar temporalmente la replicación de cambios de esquema para una publicación de combinación  
  
1.  Para una publicación con replicación de cambios de esquema, ejecute [sp_changemergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) y especifique un valor de **replicate_ddl** para **@property** y un valor de **0** para **@value** .  
  
2.  Ejecute el comando DDL en el objeto publicado.  
  
3.  (Opcional) vuelva a habilitar la replicación de cambios de esquema ejecutando [sp_changemergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) y especificando un valor de **replicate_ddl** para **@property** y un valor de **1** para **@value** .  
  
## <a name="see-also"></a>Consulte también  
 [Realizar cambios de esquema en bases de datos de publicaciones](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [Realizar cambios de esquema en bases de datos de publicaciones](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
