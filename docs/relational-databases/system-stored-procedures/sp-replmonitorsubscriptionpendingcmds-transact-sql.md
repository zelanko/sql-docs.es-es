---
title: el sp_replmonitorsubscriptionpendingcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorsubscriptionpendingcmds_TSQL
- sp_replmonitorsubscriptionpendingcmds
helpviewer_keywords:
- sp_replmonitorsubscriptionpendingcmds
ms.assetid: df5b955a-feb0-4863-9b3b-7f71e9653b3d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 432b95c4c19e47dc1df6ffd2273a3163a8d860d7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799783"
---
# <a name="spreplmonitorsubscriptionpendingcmds-transact-sql"></a>sp_replmonitorsubscriptionpendingcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@publisher** =] **'***publisher***'**  
 Es el nombre del publicador. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 Es el nombre de la base de datos publicada. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publication** =] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@subscriber** =] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@subscriber_db** = ] **'***subscriber_db***'**  
 Es el nombre de la base de datos de suscripción. *subscriber_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@subscription_type** =] *subscription_type*  
 Es el tipo de suscripción. *publication_type* es **int**, no tiene ningún valor predeterminado y puede ser uno de estos valores.  
  
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
 **sp_replmonitorsubscriptionpendingcmds** se usa con la replicación transaccional.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor o los miembros de la **db_owner** rol fijo de base de datos en la base de datos de distribución puede ejecutar **sp_ replmonitorsubscriptionpendingcmds**. Lista de miembros de acceso de la publicación para una publicación que utiliza la base de datos de distribución puede ejecutar **sp_replmonitorsubscriptionpendingcmds** para devolver comandos pendientes para esa publicación.  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación mediante programación](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
