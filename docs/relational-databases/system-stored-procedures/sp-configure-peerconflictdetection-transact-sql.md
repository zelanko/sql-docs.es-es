---
title: sp_configure_peerconflictdetection (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_configure_peerconflictdetection_TSQL
- sp_configure_peerconflictdetection
helpviewer_keywords:
- sp_configure_peerconflictdetection
ms.assetid: 45117cb2-3247-433f-ba3d-7fa19514b1c3
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1fed4cb47795554df26deb08f496edba86b5a4d
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/10/2018
---
# <a name="spconfigurepeerconflictdetection-transact-sql"></a>sp_configure_peerconflictdetection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Configura la detección de conflictos para una publicación que participa en una topología de replicación transaccional punto a punto. Para obtener más información, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md). Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_configure_peerconflictdetection [ @publication = ] 'publication'  
    [ , [ @action = ] 'action']  
    [ , [ @originator_id = ] originator_id ]  
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @continue_onconflict = ] 'continue_onconflict']  
    [ , [ @local = ] 'local']  
    [ , [ @timeout = ] timeout ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @publication=] '*publicación*'  
 Es el nombre de la publicación para la que se desea configurar la detección de conflictos. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ @action= ] '*action*'  
 Especifica si se habilita o deshabilita la detección de conflictos para una publicación. *acción* es **nvarchar (5)**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**enable**|Habilita la detección de conflictos para una publicación.|  
|**disable**|Deshabilita la detección de conflictos para una publicación.|  
|NULL (predeterminado)||  
  
 [ @originator_id= ] *originator_id*  
 Especifica un Id. para un nodo en una topología punto a punto. *originator_id* es **int**, su valor predeterminado es null. Este identificador se utiliza para la detección de conflictos si *acción* está establecido en **habilitar**. Especifique un id. positivo distinto de cero que no se haya utilizado jamás en la topología. Para obtener una lista de identificadores que ya se hayan utilizado, consulte la tabla del sistema [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) .  
  
 [ @conflict_retention= ] *conflict_retention*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @continue_onconflict= ] '*continue_onconflict*' ]  
 Determina si el Agente de distribución continúa procesando los cambios después de la detección de un conflicto. *continue_onconflict* es **nvarchar (5)** con un valor predeterminado de FALSE.  
  
> [!CAUTION]  
>  Recomendamos que utilice el valor predeterminado de FALSE. Cuando esta opción está establecida en TRUE, el Agente de distribución intenta converger los datos en la topología aplicando la fila en conflicto del nodo que tiene el Id. de originador más alto. Este método no garantiza la convergencia. Debe asegurarse de que la topología sea coherente una vez detectado un conflicto. Para obtener más información, vea "Controlar los conflictos" en [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
 [ @local= ] '*local*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @timeout= ] *timeout*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 sp_configure_peerconflictdetection se utiliza en la replicación transaccional punto a punto. Para usar la detección de conflictos, todos los nodos deben estar ejecutando [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versiones posteriores y la detección deben habilitarse para todos los nodos.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol fijo de servidor sysadmin o al rol fijo de base de datos db_owner.  
  
## <a name="see-also"></a>Vea también  
 [Detección de conflictos en la replicación punto a punto](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  (Replicación transaccional punto a punto)  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
