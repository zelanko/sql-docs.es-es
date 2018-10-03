---
title: sp_addqreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addqreader_agent_TSQL
- sp_addqreader_agent
helpviewer_keywords:
- sp_addqreader_agent
ms.assetid: dc9f591a-e67e-4ba8-bf47-defd5eda0822
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e6700e0d060e426fef09e8db118b373d7919175a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830403"
---
# <a name="spaddqreaderagent-transact-sql"></a>sp_addqreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un Agente de lectura de cola a un distribuidor específico. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos de distribución o en el publicador de la base de datos de publicaciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addqreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name'  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_login**=] **'***job_login***'**  
 Es el inicio de sesión de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows en la que se ejecuta el agente. *job_login* es **nvarchar (257)**, no tiene ningún valor predeterminado. Esta cuenta de Windows siempre se utiliza para conexiones del agente con el distribuidor.  
  
 [ **@job_password**=] **'***job_password***'**  
 Es la contraseña de la cuenta de Windows en la que se ejecuta el agente. *job_password* es **sysname**, no tiene ningún valor predeterminado.  
  
> [!IMPORTANT]  
>  No almacene información de autenticación en archivos de script. Para una mayor seguridad, los nombres de inicio de sesión y las contraseñas se deben proporcionar en tiempo de ejecución.  
  
 [ **@job_name**=] **'***job_name***'**  
 Es el nombre de un trabajo del agente existente. *job_name* es **sysname**, su valor predeterminado es null. Este parámetro solamente se especifica cuando se crea el agente a partir de un trabajo existente, en lugar de hacerlo con un trabajo recién creado (el valor predeterminado).  
  
 [  **@frompublisher=** ] *frompublisher*  
 Especifica si el procedimiento se ejecuta en el publicador. *frompublisher* es de tipo bit, con un valor predeterminado de **0**. Un valor de **1** significa que el procedimiento se ejecuta en el publicador de la base de datos de publicación.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addqreader_agent** se utiliza en la replicación transaccional.  
  
 **sp_addqreader_agent** debe ejecutarse al menos una vez en un distribuidor que admite la actualización en cola tras [sp_adddistributiondb](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) pero antes [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md).  
  
 El trabajo del agente de lector de cola se quita al ejecutar [sp_dropdistributiondb](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_addqreader_agent**.  
  
## <a name="see-also"></a>Vea también  
 [Habilitar suscripciones actualizables para publicaciones transaccionales](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [Actualizar scripts de replicación &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_changeqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md)   
 [sp_helpqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md)  
  
  
