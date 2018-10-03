---
title: sp_dropmergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepublication
- sp_dropmergepublication_TSQL
helpviewer_keywords:
- sp_dropmergepublication
ms.assetid: 9e1cb96e-5889-4f97-88cd-f60cf313ce68
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3af5f792b7305ba9f35ba278f45d07cf8f74f655
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687195"
---
# <a name="spdropmergepublication-transact-sql"></a>sp_dropmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una publicación de combinación y su Agente de instantáneas asociado. Antes de quitar una publicación de combinación, es necesario quitar todas las suscripciones. Los artículos de la publicación se quitan automáticamente. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropmergepublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación que se va a quitar. *publicación* es **sysname**, no tiene ningún valor predeterminado. Si **todas**, se quitan todas las publicaciones de mezcla existentes, así como el trabajo del agente de instantáneas asociado a ellos. Si especifica un valor determinado para *publicación*, se quitan solo esa publicación y su trabajo de agente de instantáneas asociado.  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 Se utiliza para quitar una publicación sin realizar tareas de limpieza en el distribuidor. *ignore_distributor* es **bit**, su valor predeterminado es **0**. Este parámetro también se utiliza al volver a instalar el distribuidor.  
  
 [  **@reserved=**] *reservado*  
 Está reservado para su uso futuro. *reservado* es **bit**, su valor predeterminado es **0**.  
  
 [  **@ignore_merge_metadata=** ] *ignore_merge_metadata*  
 Exclusivamente para uso interno.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropmergepublication** se utiliza en la replicación de mezcla.  
  
 **sp_dropmergepublication** quita recursivamente todos los artículos que están asociados con una publicación y, a continuación, quita la propia publicación. No se puede quitar una publicación si tiene una o más suscripciones. Para obtener información acerca de cómo quitar suscripciones, vea [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md) y [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
 Ejecutar **sp_dropmergepublication** quitar una publicación no quita los objetos publicados de la base de datos de publicación o los objetos correspondientes de la base de datos de suscripción. Utilice DROP \<objeto > para quitar estos objetos manualmente si es necesario.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_dropmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepublication-_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_dropmergepublication**.  
  
## <a name="see-also"></a>Vea también  
 [Eliminar una publicación](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
