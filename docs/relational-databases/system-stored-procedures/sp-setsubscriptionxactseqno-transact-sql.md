---
title: sp_setsubscriptionxactseqno (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setsubscriptionxactseqno
- sp_setsubscriptionxactseqno_TSQL
helpviewer_keywords:
- sp_setsubscriptionxactseqno
ms.assetid: cdb4e0ba-5370-4905-b03f-0b0c6f080ca6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bfc49e712e75a862c9c43ce99cc35b56c014cebc
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534657"
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
`[ @publisher = ] 'publisher'` Es el nombre del publicador. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'` Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, no tiene ningún valor predeterminado. Para un publicador que no es - SQL Server, *publisher_db* es el nombre de la base de datos de distribución.  
  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado. Cuando el agente de distribución se comparte por más de una publicación, debe especificar un valor de ALL para *publicación*.  
  
`[ @xact_seqno = ] xact_seqno` Es el LSN de la siguiente transacción en el distribuidor que se aplicará en el suscriptor. *xact_seqno* es **varbinary (16)**, no tiene ningún valor predeterminado.  
  
## <a name="result-set"></a>Tipo de cursor  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**ORIGINAL XACT_SEQNO**|**varbinary(16)**|El LSN original de la siguiente transacción que se va a aplicar en el suscriptor.|  
|**UPDATED XACT_SEQNO**|**varbinary(16)**|El LSN actualizado de la siguiente transacción que se va a aplicar en el suscriptor.|  
|**NÚMERO DE SECUENCIA DE LA SUSCRIPCIÓN**|**int**|El número de flujos de suscripción utilizados durante la última sincronización.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_setsubscriptionxactseqno** se utiliza en la replicación transaccional.  
  
 **sp_setsubscriptionxactseqno** no se puede usar en una topología de replicación transaccional punto a punto.  
  
 **sp_setsubscriptionxactseqno** se puede usar para omitir una transacción específica que está provocando un error cuando se aplica en el suscriptor. Cuando se produce un error y después se detiene el agente de distribución, llame a [sp_helpsubscriptionerrors &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpsubscriptionerrors-transact-sql.md) en el distribuidor para recuperar el valor xact_seqno de la transacción errónea y, a continuación, llamar a **sp_setsubscriptionxactseqno**, pasando este valor para *xact_seqno*. Así se garantizará que se procesen solamente los comandos después de este LSN.  
  
 Especifique un valor de **0** para *xact_seqno* entregar todos los comandos pendientes en la base de datos de distribución al suscriptor.  
  
 **sp_setsubscriptionxactseqno** puede producir un error si el agente de distribución utiliza flujos de varias suscripciones.  
  
 Cuando se produzca este error, debe ejecutar el Agente de distribución con un flujo de suscripción único. Para más información, consulte [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_setsubscriptionxactseqno**.  
  
  
