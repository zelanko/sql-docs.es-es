---
title: sp_deletetracertokenhistory (Transact-SQL) | Microsoft Docs
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
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2734c4f1922ccd7258383dd5e79665cf26c8b4fc
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43023519"
---
# <a name="spdeletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita los registros desde el [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) y [MStracer_history &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-history-transact-sql.md) las tablas del sistema. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación o en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_deletetracertokenhistory [ @publication = ] 'publication'   
    [ , [ @tracer_id = ] tracer_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicación***'**  
 Es el nombre de la publicación en la que se ha insertado el token de seguimiento. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@tracer_id=** ] *tracer_id*  
 Es el identificador del token de seguimiento que se va a eliminar. *tracer_id* es **int**, su valor predeterminado es null. Si **null**, a continuación, se eliminan todos los testigos de seguimiento que pertenecen a la publicación.  
  
 [  **@cutoff_date=** ] *cutoff_date*  
 Especifica una fecha límite, de modo que se quitan todos los tokens de seguimiento insertados en la publicación antes de esa fecha. *cutoff_date* es de tipo datetime y su valor predeterminado es null.  
  
 [  **@publisher=** ] **'***publisher***'**  
 El nombre del publicador. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Este parámetro solo debe especificarse para que no sean de[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 El nombre de la base de datos de publicación. *publisher_db* es **sysname**, su valor predeterminado es null. Si el procedimiento almacenado se ejecuta en el publicador, se omite este parámetro.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_deletetracertokenhistory** se utiliza en la replicación transaccional.  
  
 Al ejecutar **sp_deletetracertokenhistory**, solo se puede especificar uno de *tracer_id* o *cutoff_date*. Si se especifican ambos parámetros, se produce un error.  
  
 Si no se ejecutan **sp_deletetracertokenhistory** para quitar los metadatos de token de seguimiento, se quitará la información cuando se produce la limpieza de historial programada regularmente.  
  
 Id. de token de seguimiento se puede determinar mediante la ejecución de [sp_helptracertokens &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) o consultando el [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) tabla del sistema.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor, el **db_owner** fijo de base de datos en la base de datos de publicación o **db_owner** fijo de base de datos o  **replmonitor** roles en la base de datos de distribución pueden ejecutar **sp_deletetracertokenhistory**.  
  
## <a name="see-also"></a>Vea también  
 [Medir la latencia y validar las conexiones de la replicación transaccional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)  
  
  
