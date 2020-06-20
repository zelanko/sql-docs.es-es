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
ms.openlocfilehash: bec2f363cd8c4f7dea45935568a88722b19323fc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060423"
---
# <a name="replicate-schema-changes"></a>Replicar cambios de esquema
  En este tema se describe cómo replicar cambios de esquema en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Si realiza los siguientes cambios de esquema en un artículo publicado, se propagan de forma predeterminada a los suscriptores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
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
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   La instrucción ALTER TABLE … DROP COLUMN siempre se replica en todos los suscriptores cuya suscripción contenga las columnas que se van a quitar, aunque deshabilite la replicación de cambios de esquema.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 Si no desea replicar los cambios de esquema para una publicación, deshabilite la replicación de cambios de esquema en el cuadro de diálogo **propiedades de la publicación: \<Publication> ** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-disable-replication-of-schema-changes"></a>Para deshabilitar la replicación de los cambios de esquema  
  
1.  En la **Página opciones de suscripción** del cuadro de diálogo Propiedades de la **publicación: \<Publication> ** , establezca el valor de la propiedad **replicar cambios de esquema** en **false**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Para propagar únicamente los cambios de esquema específicos, establezca la propiedad en **True** antes de un cambio de esquema y vuelva a establecerla en **False** después de realizar el cambio. A la inversa, para propagar la mayoría de los cambios de esquema, excepto un cambio determinado, establezca la propiedad en **False** antes de un cambio de esquema y vuelva a establecerla en **True** después de realizar el cambio.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede utilizar los procedimientos almacenados de replicación para especificar si se replican estos cambios de esquema. El procedimiento almacenado que utiliza depende del tipo de publicación.  
  
#### <a name="to-create-a-snapshot-or-transactional-publication-that-does-not-replicate-schema-changes"></a>Para crear una instantánea o una publicación transaccional que no replique cambios de esquema  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addpublication &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)y especifique un valor de **0** para ** \@ replicate_ddl**. Para obtener más información, vea [Crear una suscripción](create-a-publication.md).  
  
#### <a name="to-create-a-merge-publication-that-does-not-replicate-schema-changes"></a>Para crear una publicación de combinación que no replique cambios de esquema  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergepublication &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)y especifique un valor de **0** para ** \@ replicate_ddl**. Para obtener más información, vea [Crear una suscripción](create-a-publication.md).  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-snapshot-or-transactional-publication"></a>Para deshabilitar temporalmente la replicación de cambios de esquema para una instantánea o una publicación transaccional  
  
1.  Para una publicación con replicación de cambios de esquema, ejecute [sp_changepublication &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), especificando un valor de **replicate_ddl** para la ** \@ propiedad** y un valor de **0** para el ** \@ valor**.  
  
2.  Ejecute el comando DDL en el objeto publicado.  
  
3.  Opta Vuelva a habilitar la replicación de los cambios de esquema mediante la ejecución de [sp_changepublication &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), especificando un valor de **replicate_ddl** para la ** \@ propiedad** y un valor de **1** para el ** \@ valor**.  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-merge-publication"></a>Para deshabilitar temporalmente la replicación de cambios de esquema para una publicación de combinación  
  
1.  Para una publicación con replicación de cambios de esquema, ejecute [sp_changemergepublication &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), especificando un valor de **replicate_ddl** para la ** \@ propiedad** y un valor de **0** para el ** \@ valor**.  
  
2.  Ejecute el comando DDL en el objeto publicado.  
  
3.  Opta Vuelva a habilitar la replicación de los cambios de esquema mediante la ejecución de [sp_changemergepublication &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), especificando un valor de **replicate_ddl** para la ** \@ propiedad** y un valor de **1** para el ** \@ valor**.  
  
## <a name="see-also"></a>Consulte también  
 [Realizar cambios de esquema en bases de datos de publicaciones](make-schema-changes-on-publication-databases.md)   
 [Realizar cambios de esquema en bases de datos de publicaciones](make-schema-changes-on-publication-databases.md)  
  
  
