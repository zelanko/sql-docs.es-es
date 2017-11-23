---
title: sp_helpreplfailovermode (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords: sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 212775844dde7400ca3ddb17753091aa56b582f1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra el modo de conmutación por error actual de una suscripción. Este procedimiento almacenado se ejecuta en el suscriptor de cualquier base de datos. Para obtener más información acerca de los modos de conmutación por error, consulte [suscripciones actualizables para replicación transaccional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre del publicador que participa en la actualización de este suscriptor. *Publisher* es **sysname**, no tiene ningún valor predeterminado. El publicador debe estar configurado para publicación.  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación que participa en la actualización de este suscriptor. *publicación*es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@failover_mode_id=**] **'***failover_mode_id***' salida**  
 Devuelve el valor entero del modo de conmutación por error y es un **salida** parámetro. *failover_mode_id* es un **tinyint** con un valor predeterminado de **0**. Devuelve **0** para la actualización inmediata y **1** actualización en cola.  
  
 [**@failover_mode=**] **'***failover_mode***' salida**  
 Devuelve el modo en que se realizan las modificaciones de datos en el suscriptor. *failover_mode* es un **nvarchar (10)** con un valor predeterminado es NULL. Es un **salida** parámetro.  
  
|Valor|Description|  
|-----------|-----------------|  
|**inmediata**|Actualización inmediata: las actualizaciones del suscriptor se propagan inmediatamente al publicador utilizando un protocolo de confirmación en dos fases (2PC).|  
|**en cola**|Actualización en cola: las actualizaciones realizadas en el suscriptor se almacenan en una cola.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpreplfailovermode** se utiliza en la replicación de instantáneas o replicación transaccional para las suscripciones que están habilitadas para actualización inmediata con actualización en cola como conmutación por error, en caso de error.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos puede ejecutar **sp_helpreplfailovermode**.  
  
## <a name="see-also"></a>Vea también  
 [sp_setreplfailovermode &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
