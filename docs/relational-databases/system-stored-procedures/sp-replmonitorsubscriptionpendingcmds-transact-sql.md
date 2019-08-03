---
title: sp_replmonitorsubscriptionpendingcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorsubscriptionpendingcmds_TSQL
- sp_replmonitorsubscriptionpendingcmds
helpviewer_keywords:
- sp_replmonitorsubscriptionpendingcmds
ms.assetid: df5b955a-feb0-4863-9b3b-7f71e9653b3d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6059c4834c37c3c61227fdaf3c9ea3c94e1b5b9a
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770903"
---
# <a name="spreplmonitorsubscriptionpendingcmds-transact-sql"></a>sp_replmonitorsubscriptionpendingcmds (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Devuelve información sobre el número de comandos pendientes para una suscripción a una publicación transaccional y una estimación aproximada del tiempo que requiere procesarlos. Este procedimiento almacenado devuelve una fila para cada suscripción devuelta. Este procedimiento almacenado, que se utiliza para supervisar la replicación, se ejecuta en el distribuidor en la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replmonitorsubscriptionpendingcmds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @subscription_type = ] subscription_type  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`Es el nombre del publicador. *Publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'`Es el nombre de la base de datos publicada. *publisher_db* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publication = ] 'publication'`Es el nombre de la publicación. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @subscriber = ] 'subscriber'`Es el nombre del suscriptor. *Subscriber* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @subscriber_db = ] 'subscriber_db'`Es el nombre de la base de datos de suscripciones. *subscriber_db* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @subscription_type = ] subscription_type`Si el tipo de suscripción. *publication_type* es de **tipo int**y no tiene ningún valor predeterminado y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Suscripción de inserción.|  
|**1**|Suscripción de extracción|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**pendingcmdcount**|**int**|El número de comandos pendientes para la suscripción.|  
|**estimatedprocesstime**|**int**|Estimación del número de segundos requeridos para enviar todos los comandos pendientes al suscriptor.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_replmonitorsubscriptionpendingcmds** se utiliza con la replicación transaccional.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** en el distribuidor o los miembros del rol fijo de base de datos **db_owner** en la base de datos de distribución pueden ejecutar **sp_replmonitorsubscriptionpendingcmds**. Los miembros de la lista de acceso a la publicación para una publicación que utiliza la base de datos de distribución pueden ejecutar **sp_replmonitorsubscriptionpendingcmds** para devolver comandos pendientes para esa publicación.  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación mediante programación](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
