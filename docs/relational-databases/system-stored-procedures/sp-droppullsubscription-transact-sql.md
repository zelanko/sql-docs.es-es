---
title: sp_droppullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droppullsubscription
- sp_droppullsubscription_TSQL
helpviewer_keywords:
- sp_droppullsubscription
ms.assetid: 7352d94a-f8f2-42ea-aaf1-d08c3b5a0e76
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0343855bbc3d82e58a0a0252109dee6255ee766f
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54134055"
---
# <a name="spdroppullsubscription-transact-sql"></a>sp_droppullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una suscripción de la base de datos actual del suscriptor. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripciones de extracción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_droppullsubscription [ @publisher= ] 'publisher'  
        , [ @publisher_db= ] 'publisher_db'  
        , [ @publication= ] 'publication'  
    [ , [ @reserved= ] reserved ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=** ] **'**_publisher_**'**  
 Es el nombre del servidor remoto. *publicador* es **sysname**, no tiene ningún valor predeterminado. Si **todas**, se quita la suscripción de todos los publicadores.  
  
 [  **@publisher_db=** ] **'**_publisher_db_**'**  
 Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, no tiene ningún valor predeterminado. **todos los** significa que todas las bases de datos del publicador.  
  
 [  **@publication=** ] **'**_publicación_**'**  
 Es el nombre de publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado. Si **todas**, se quita la suscripción a todas las publicaciones.  
  
 [  **@reserved=** ] *reservado*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_droppullsubscription** se utiliza en la replicación de instantáneas y transaccional.  
  
 **sp_droppullsubscription** elimina la fila correspondiente en el [MSreplication_subscriptions &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) tabla y el agente de distribución correspondiente en el suscriptor. Si no quedan filas en [MSreplication_subscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md), quita la tabla.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-droppullsubscription-_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el usuario que creó la suscripción de extracción puede ejecutar **sp_droppullsubscription**. El **db_owner** sólo es capaz de ejecutar el rol fijo de base de datos **sp_droppullsubscription** si el usuario que creó la suscripción de extracción pertenece a este rol.  
  
## <a name="see-also"></a>Vea también  
 [Eliminar una suscripción de extracción](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
