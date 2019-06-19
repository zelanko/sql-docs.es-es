---
title: sp_browsereplcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsereplcmds_TSQL
- sp_browsereplcmds
helpviewer_keywords:
- sp_browsereplcmds
ms.assetid: 30abcb41-1d18-4f43-a692-4c80914c0450
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7918e257428fd85ddb54867ee5144f45a3bf89f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62996364"
---
# <a name="spbrowsereplcmds-transact-sql"></a>sp_browsereplcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve un conjunto de resultados en una versión legible de los comandos replicados almacenados en la base de datos de distribución y se utiliza como herramienta de diagnóstico. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_browsereplcmds [ [ @xact_seqno_start = ] 'xact_seqno_start' ]  
    [ , [ @xact_seqno_end = ] 'xact_seqno_end' ]   
    [ , [ @originator_id = ] 'originator_id' ]  
    [ , [ @publisher_database_id = ] 'publisher_database_id' ]  
    [ , [ @article_id = ] 'article_id' ]  
    [ , [ @command_id= ] command_id ]  
    [ , [ @agent_id = ] agent_id ]  
    [ , [ @compatibility_level = ] compatibility_level ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @xact_seqno_start = ] 'xact_seqno_start'` Especifica el número de secuencia exacta menor valor para devolver. *xact_seqno_start* es **nchar (22)** , su valor predeterminado es 0 x 00000000000000000000.  
  
`[ @xact_seqno_end = ] 'xact_seqno_end'` Especifica el número de secuencia exacta de mayor a devolver. *xact_seqno_end* es **nchar (22)** , su valor predeterminado es 0xFFFFFFFFFFFFFFFFFFFF.  
  
`[ @originator_id = ] 'originator_id'` Especifica si los comandos con los valores especificados *originator_id* se devuelven. *originator_id* es **int**, su valor predeterminado es null.  
  
`[ @publisher_database_id = ] 'publisher_database_id'` Especifica si los comandos con los valores especificados *publisher_database_id* se devuelven. *publisher_database_id* es **int**, su valor predeterminado es null.  
  
`[ @article_id = ] 'article_id'` Especifica si los comandos con los valores especificados *article_id* se devuelven. *article_id* es **int**, su valor predeterminado es null.  
  
`[ @command_id = ] command_id` Es la ubicación del comando en [MSrepl_commands &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msrepl-commands-transact-sql.md) descodificarse. *$command_id* es **int**, su valor predeterminado es null. Si se especifica, se deben especificar además, todos los demás parámetros y *xact_seqno_start*debe ser idéntica a *xact_seqno_end*.  
  
`[ @agent_id = ] agent_id` Especifica que se devuelven únicamente los comandos de un agente de replicación específico. *valor de agent_id* es **int**, su valor predeterminado es null.  
  
`[ @compatibility_level = ] compatibility_level` Es la versión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el que el *compatibility_level* es **int**, su valor predeterminado de 9000000.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**varbinary(16)**|Número de secuencia del comando.|  
|**originator_srvname**|**sysname**|Servidor en el que se originó la transacción.|  
|**originator_db**|**sysname**|Base de datos en la que se originó la transacción.|  
|**article_id**|**int**|ID. del artículo.|  
|**Tipo**|**int**|Tipo de comando.|  
|**partial_command**|**bit**|Indica si se trata de un comando parcial.|  
|**hashkey**|**int**|Exclusivamente para uso interno.|  
|**originator_publication_id**|**int**|Id. de la publicación en la que se originó la transacción.|  
|**originator_db_version**|**int**|Versión de la base de datos en la que se originó la transacción.|  
|**originator_lsn**|**varbinary(16)**|Identifica el número de flujo de registro (LSN) para el comando de la publicación en la que se origina. Se utiliza en la replicación transaccional punto a punto.|  
|**command**|**nvarchar(1024)**|Comando [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|**command_id**|**int**|Identificador del comando en [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md).|  
  
 Los comandos largos se pueden dividir en varias filas en el conjunto de resultados.  
  
## <a name="remarks"></a>Comentarios  
 **sp_browsereplcmds** se utiliza en la replicación transaccional.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o los miembros de la **db_owner** o **replmonitor** roles fijos de base de datos en la base de datos de distribución pueden ejecutar **sp_browsereplcmds**.  
  
## <a name="see-also"></a>Vea también  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
