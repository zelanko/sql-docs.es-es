---
title: sp_posttracertoken (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedur+I741es
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- posttracerttoken
- posttracerttoken_TSQL
- sp_posttracertoken
- sp_posttracertoken_TSQL
helpviewer_keywords:
- sp_posttracertoken
ms.assetid: 24da5cd2-1c45-475e-93db-5bdf660f1c2c
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79102a0a4c9e0b2122b23f01a7e7808c0d610967
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spposttracertoken-transact-sql"></a>sp_posttracertoken (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este procedimiento envía un testigo de seguimiento al registro de transacciones del publicador y empieza el proceso de seguimiento de las estadísticas de latencia. La información se registra cuando el token de seguimiento se escribe en el registro de transacciones, cuando lo recoge el Agente de registro del LOG y cuando lo aplica el Agente de distribución. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación. Para más información, consulte [Medir la latencia y validar las conexiones de la replicación transaccional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_posttracertoken [ @publication = ] 'publication'   
    [ , [ @tracer_token_id = ] tracer_token_id OUTPUT  
    [ , [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publication**=] **'***publicación***'**  
 Es el nombre de la publicación para la que se va a medir la latencia. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@tracer_token_id=** ] *tracer_token_id***salida**  
 Es el identificador del token de seguimiento insertado. *tracer_token_id* es **int** con un valor predeterminado es NULL y es un parámetro de salida. Este valor puede utilizarse para ejecutar [sp_helptracertokenhistory &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md) o [sp_deletetracertokenhistory &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md) sin ejecutar primero [sp_helptracertokens &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md).  
  
 [  **@publisher=** ] **'***publisher***'**  
 Especifica un no[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *Publisher* es **sysname**, su valor predeterminado es null y no se debe especificar para una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_posttracertoken** se utiliza en la replicación transaccional.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-posttracertoken-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos puede ejecutar **sp_posttracertoken**.  
  
## <a name="see-also"></a>Vea también  
 [Medir la latencia y validar las conexiones de la replicación transaccional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
