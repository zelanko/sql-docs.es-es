---
title: sp_helptracertokens (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_helptracertokens
- sp_helptracertokens_TSQL
helpviewer_keywords:
- sp_helptracertokens
ms.assetid: 61f27234-531d-4b37-8fa3-fe4c32e6f521
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 635a49188cd4c109bf194353e038f5666e033bf9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sphelptracertokens-transact-sql"></a>sp_helptracertokens (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada testigo de seguimiento que se ha insertado en una publicación para determinar la latencia. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación o en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helptracertokens [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicación***'**  
 Es el nombre de la publicación en la que se han insertado tokens de seguimiento. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher=** ] **'***publisher***'**  
 El nombre del publicador. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Este parámetro solo debe especificarse para no -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 El nombre de la base de datos de publicación. *publisher_db* es **sysname**, su valor predeterminado es null. Si el procedimiento almacenado se ejecuta en el publicador, se omite este parámetro.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|Identifica un registro de un token de seguimiento.|  
|**publisher_commit**|**datetime**|Fecha y hora a la que el registro de token se confirmó en el publicador de la base de datos de publicaciones.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helptracertokens** se utiliza en la replicación transaccional.  
  
 **sp_helptracertokens** se utiliza para obtener los identificadores de símbolo (token) de seguimiento al ejecutar [sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokens-tran_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor, el **db_owner** fijo de base de datos en la base de datos de publicación, o **db_owner** fijo de base de datos o  **replmonitor** roles en la base de datos de distribución pueden ejecutar **sp_helptracertokenhistory**.  
  
## <a name="see-also"></a>Vea también  
 [Medir la latencia y validar las conexiones de la replicación transaccional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
