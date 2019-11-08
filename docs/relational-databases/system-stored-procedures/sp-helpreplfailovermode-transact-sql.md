---
title: sp_helpreplfailovermode (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords:
- sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
author: stevestein
ms.author: sstein
ms.openlocfilehash: b998a11acd71175e8868b669d9491822f60d2b33
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632754"
---
# <a name="sp_helpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra el modo de conmutación por error actual de una suscripción. Este procedimiento almacenado se ejecuta en el suscriptor de cualquier base de datos. Para obtener más información sobre los modos de conmutación por error, consulte [suscripciones actualizables para la replicación transaccional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` es el nombre del publicador que participa en la actualización de este suscriptor. *Publisher* es de **tipo sysname**y no tiene ningún valor predeterminado. El publicador debe estar configurado para publicación.  
  
`[ @publisher_db = ] 'publisher_db'` es el nombre de la base de datos de publicación. *publisher_db* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publication = ] 'publication'` es el nombre de la publicación que participa en la actualización de este suscriptor. *Publication*es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @failover_mode_id = ] 'failover_mode_id' OUTPUT` devuelve el valor entero del modo de conmutación por error y es un parámetro de **salida** . *failover_mode_id* es de **tinyint** con un valor predeterminado de **0**. Devuelve **0** para la actualización inmediata y **1** para la actualización en cola.  
  
`[ @failover_mode = ] 'failover_mode' OUTPUT` devuelve el modo en el que se realizan las modificaciones de datos en el suscriptor. *failover_mode* es de tipo **nvarchar (10)** y su valor predeterminado es NULL. Es un parámetro de **salida** .  
  
|Value|Descripción|  
|-----------|-----------------|  
|**inmediato**|Actualización inmediata: las actualizaciones del suscriptor se propagan inmediatamente al publicador utilizando un protocolo de confirmación en dos fases (2PC).|  
|**en cola**|Actualización en cola: las actualizaciones realizadas en el suscriptor se almacenan en una cola.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpreplfailovermode** se utiliza en la replicación de instantáneas o transaccional para la que se habilitan las suscripciones para la actualización inmediata con la actualización en cola como conmutación por error, en caso de error.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_helpreplfailovermode**.  
  
## <a name="see-also"></a>Vea también  
 [sp_setreplfailovermode &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
