---
title: sp_helptracertokenhistory (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- sp_helptracertokenhistory_TSQL
- sp_helptracertokenhistory
helpviewer_keywords:
- sp_helptracertokenhistory
ms.assetid: 96910d1c-be76-43eb-9c93-4477e6761749
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c6ecccbb6c545fe9a4da6f50b2bdc6100dad57a0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sphelptracertokenhistory-transact-sql"></a>sp_helptracertokenhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información detallada de latencia acerca de los testigos de seguimiento especificados. Se devuelve una fila por cada suscriptor. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación o en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helptracertokenhistory [ @publication = ] 'publication'   
        , [ @tracer_id = ] tracer_id  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicación***'**  
 Es el nombre de la publicación en la que se ha insertado el token de seguimiento. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@tracer_id=** ] *tracer_id*  
 Es el identificador del token de seguimiento en el [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) qué historial se devuelve información de tabla. *tracer_id* es **int**, no tiene ningún valor predeterminado.  
  
 [  **@publisher=** ] **'***publisher***'**  
 El nombre del publicador. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Este parámetro solo debe especificarse para no -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 El nombre de la base de datos de publicación. *publisher_db* es **sysname**, su valor predeterminado es null. Si el procedimiento almacenado se ejecuta en el publicador, se omite este parámetro.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**distributor_latency**|**bigint**|Número de segundos entre la confirmación del registro del token de seguimiento en el publicador y la confirmación del registro en el distribuidor.|  
|**suscriptor**|**sysname**|Nombre del suscriptor que ha recibido el token de seguimiento.|  
|**subscriber_db**|**sysname**|Nombre de la base de datos de suscripciones en la que se ha insertado el testigo de seguimiento.|  
|**subscriber_latency**|**bigint**|Número de segundos entre la confirmación del registro del token de seguimiento en el distribuidor y la confirmación del registro en el suscriptor.|  
|**overall_latency**|**bigint**|Número de segundos entre la confirmación del registro del token de seguimiento en el publicador y la confirmación del registro del token en el suscriptor.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helptracertokenhistory** se utiliza en la replicación transaccional.  
  
 Ejecutar [sp_helptracertokens &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) para obtener una lista de los testigos de seguimiento para la publicación.  
  
 Un valor NULL en el conjunto de resultados significa que no es posible calcular las estadísticas de latencia. Esto es debido a que no se ha recibido el token de seguimiento en el distribuidor o en uno de los suscriptores.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokenhistor_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor, el **db_owner** fijo de base de datos en la base de datos de publicación, o **db_owner** fijo de base de datos o  **replmonitor** roles en la base de datos de distribución pueden ejecutar **sp_helptracertokenhistory**.  
  
## <a name="see-also"></a>Vea también  
 [Medir la latencia y validar las conexiones de la replicación transaccional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
