---
title: sp_setreplfailovermode (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_setreplfailovermode
- sp_setreplfailovermode_TSQL
helpviewer_keywords:
- sp_setreplfailovermode
ms.assetid: ca98a4c3-bea4-4130-88d7-79e0fd1e85f6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 68851fb6ad9a242536cc81c6688b7caed1067a2c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spsetreplfailovermode-transact-sql"></a>sp_setreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Permite definir el modo de funcionamiento de conmutación por error para las suscripciones habilitadas para actualización inmediata con actualización en cola como conmutación por error. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción. Para obtener más información acerca de los modos de conmutación por error, consulte [suscripciones actualizables para replicación transaccional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_setreplfailovermode [ @publisher= ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication= ] 'publication' ]  
    [ , [ @failover_mode= ] 'failover_mode' ]  
    [ , [ @override = ] override ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado. La publicación debe existir.  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación*es **sysname**, no tiene ningún valor predeterminado.  
  
 [**@failover_mode=**] **'***failover_mode***'**  
 Es el modo de conmutación por error de la suscripción. *failover_mode* es **nvarchar (10)** y puede tener uno de estos valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**inmediata** o **sincronización**|A medida que se vayan modificando los datos en el suscriptor, se realiza una copia masiva de las modificaciones en el publicador.|  
|**en cola**|Las modificaciones de datos se almacenan en un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cola.|  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queue Server ha quedado desusado y ya no se admite.  
  
 [  **@override** =] *invalidar*  
 Exclusivamente para uso interno.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_setreplfailovermode** se utiliza en la replicación de instantáneas o replicación transaccional para las suscripciones que están habilitadas, ya sea para actualización en cola con conmutación por error a actualización inmediata o de actualización inmediata con conmutación por error en cola la actualización.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_setreplfailovermode**.  
  
## <a name="see-also"></a>Vea también  
 [Cambiar entre modos de actualización para una suscripción transaccional actualizable](../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
