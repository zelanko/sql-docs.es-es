---
title: sp_setsubscriptionxactseqno (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
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
- sp_setsubscriptionxactseqno
- sp_setsubscriptionxactseqno_TSQL
helpviewer_keywords:
- sp_setsubscriptionxactseqno
ms.assetid: cdb4e0ba-5370-4905-b03f-0b0c6f080ca6
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7ec407d84267e8a2a03d2a6774e7c86cc469af94
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spsetsubscriptionxactseqno-transact-sql"></a>sp_setsubscriptionxactseqno (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se utiliza durante la solución de problemas para especificar el número de secuencia de registro (LSN) de la siguiente transacción que se va a aplicar al Agente de distribución en el suscriptor, lo que permite al agente omitir una transacción que ha dado error. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción. No se admite para suscriptores que no sean de SQL Server.  
  
> [!CAUTION]  
>  El uso incorrecto de este procedimiento almacenado o la especificación de un valor LSN incorrecto puede ocasionar que el Agente de distribución revierta los cambios ya aplicados en el suscriptor o que omita todos los cambios restantes.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_setsubscriptionxactseqno [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @xact_seqno = ] xact_seqno   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=** ] **'***publisher***'**  
 Es el nombre del publicador. *Publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, no tiene ningún valor predeterminado. Para una no - publicador de SQL Server, *publisher_db* es el nombre de la base de datos de distribución.  
  
 [  **@publication=** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado. Cuando el agente de distribución se comparte por más de una publicación, debe especificar un valor de ALL para *publicación*.  
  
 [  **@xact_seqno=** ] *xact_seqno*  
 Es el LSN de la siguiente transacción en el distribuidor que se tiene que aplicar en el suscriptor. *xact_seqno* es **varbinary (16)**, no tiene ningún valor predeterminado.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**XACT_SEQNO ORIGINAL**|**varbinary (16)**|El LSN original de la siguiente transacción que se va a aplicar en el suscriptor.|  
|**XACT_SEQNO ACTUALIZADA**|**varbinary (16)**|El LSN actualizado de la siguiente transacción que se va a aplicar en el suscriptor.|  
|**NÚMERO DE SECUENCIA DE SUSCRIPCIÓN**|**int**|El número de flujos de suscripción utilizados durante la última sincronización.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_setsubscriptionxactseqno** se utiliza en la replicación transaccional.  
  
 **sp_setsubscriptionxactseqno** no se puede usar en una topología de replicación transaccional punto a punto.  
  
 **sp_setsubscriptionxactseqno** puede utilizarse para omitir una transacción específica que está provocando un error cuando se aplica en el suscriptor. Cuando se produce un error y después se detiene el agente de distribución, llame a [sp_helpsubscriptionerrors &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpsubscriptionerrors-transact-sql.md) en el distribuidor para recuperar el valor de xact_seqno de la transacción errónea y, a continuación, llamar a **sp_setsubscriptionxactseqno**, pasando este valor para *xact_seqno*. Así se garantizará que se procesen solamente los comandos después de este LSN.  
  
 Especifique un valor de **0** para *xact_seqno* para entregar todos los comandos pendientes en la base de datos de distribución en el suscriptor.  
  
 **sp_setsubscriptionxactseqno** puede producir un error si el agente de distribución utiliza flujos de varias suscripciones.  
  
 Cuando se produzca este error, debe ejecutar el Agente de distribución con un flujo de suscripción único. Para más información, consulte [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_setsubscriptionxactseqno**.  
  
  
