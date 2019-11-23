---
title: Replicación de cambios de esquema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 84918dd3f50d129485911fc880e67c0152fa905c
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882245"
---
# <a name="replicate-schema-changes"></a>Replicate Schema Changes
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
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   La instrucción ALTER TABLE... La instrucción DROP COLUMN siempre se replica en todos los suscriptores cuya suscripción contenga las columnas que se van a quitar, aunque se deshabilite la replicación de cambios de esquema.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Si no quiere replicar los cambios de esquema para una publicación, deshabilite la replicación de cambios de esquema en el cuadro de diálogo **Propiedades de la publicación: \<publicación>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-disable-replication-of-schema-changes"></a>Para deshabilitar la replicación de los cambios de esquema  
  
1.  En la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** , establezca el valor de la propiedad **Replicar cambios de esquema** en **False**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Para propagar únicamente los cambios de esquema específicos, establezca la propiedad en **True** antes de un cambio de esquema y vuelva a establecerla en **False** después de realizar el cambio. A la inversa, para propagar la mayoría de los cambios de esquema, excepto un cambio determinado, establezca la propiedad en **False** antes de un cambio de esquema y vuelva a establecerla en **True** después de realizar el cambio.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede utilizar los procedimientos almacenados de replicación para especificar si se replican estos cambios de esquema. El procedimiento almacenado que utiliza depende del tipo de publicación.  
  
#### <a name="to-create-a-snapshot-or-transactional-publication-that-does-not-replicate-schema-changes"></a>Para crear una instantánea o una publicación transaccional que no replique cambios de esquema  
  
1.  En la base de datos de publicación del publicador, ejecute [ &#40;sp_addpublication&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)y especifique un valor de **0** para **\@replicate_ddl**. Para obtener más información, consulte [Create a Publication](create-a-publication.md).  
  
#### <a name="to-create-a-merge-publication-that-does-not-replicate-schema-changes"></a>Para crear una publicación de combinación que no replique cambios de esquema  
  
1.  En la base de datos de publicación del publicador, ejecute [ &#40;sp_addmergepublication&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)y especifique un valor de **0** para **\@replicate_ddl**. Para obtener más información, consulte [Create a Publication](create-a-publication.md).  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-snapshot-or-transactional-publication"></a>Para deshabilitar temporalmente la replicación de cambios de esquema para una instantánea o una publicación transaccional  
  
1.  Para una publicación con replicación de cambios de esquema, [ejecute &#40;sp_changepublication Transact-&#41;SQL](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), especificando un valor de **replicate_ddl** para **\@propiedad** y un valor de **0** para **\@valor**.  
  
2.  Ejecute el comando DDL en el objeto publicado.  
  
3.  Opta Vuelva a habilitar la replicación de cambios de esquema ejecutando [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), especificando un valor de **replicate_ddl** para **\@propiedad** y un valor de **1** para **\@valor**.  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-merge-publication"></a>Para deshabilitar temporalmente la replicación de cambios de esquema para una publicación de combinación  
  
1.  Para una publicación con replicación de cambios de esquema, [ejecute &#40;sp_changemergepublication Transact-&#41;SQL](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), especificando un valor de **replicate_ddl** para **\@propiedad** y un valor de **0** para **\@valor**.  
  
2.  Ejecute el comando DDL en el objeto publicado.  
  
3.  Opta Vuelva a habilitar la replicación de cambios de esquema ejecutando [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), especificando un valor de **replicate_ddl** para **\@propiedad** y un valor de **1** para **\@valor**.  
  
## <a name="see-also"></a>Vea también  
 [Realizar cambios de esquema en bases de datos de publicaciones](make-schema-changes-on-publication-databases.md)   
 [Realizar cambios de esquema en bases de datos de publicaciones](make-schema-changes-on-publication-databases.md)  
  
  
