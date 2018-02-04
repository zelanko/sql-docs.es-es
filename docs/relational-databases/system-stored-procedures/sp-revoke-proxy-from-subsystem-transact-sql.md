---
title: sp_revoke_proxy_from_subsystem (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_subsystem
- sp_revoke_login_from_subsystem_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_proxy_from_subsystem
ms.assetid: b87bc8ba-3ea8-4aed-b54b-32c3d82d9d2a
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3408c3ddee13886edaaa410341379ee50d4f9cb3
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sprevokeproxyfromsubsystem-transact-sql"></a>sp_revoke_proxy_from_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoca el acceso a un subsistema desde un proxy.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_revoke_proxy_from_subsystem   
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@proxy_id** = ] *id*  
 Número de identificación del proxy desde el que se revoca el acceso. El *proxy_id* es **int**, su valor predeterminado es null. Cualquier *proxy_id* o *proxy_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [  **@proxy_name**  =] **'***proxy_name***'**  
 Nombre del proxy desde el que se revoca el acceso. El *proxy_name* es **sysname**, su valor predeterminado es null. Cualquier *proxy_id* o *proxy_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [ **@subsystem_id** = ] *id*  
 El id. del subsistema al que se revoca el acceso. El *subsystem_id* es **int**, su valor predeterminado es null. Cualquier *subsystem_id* o *subsystem_name* debe especificarse, pero no pueden especificarse ambos. En la tabla siguiente se muestran los valores disponibles para cada subsistema.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**2**|Script ActiveX<br /><br /> **\*\*Importante \* \***  subsistema de scripts de ActiveX en el que se va a quitar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.|  
|**3**|Sistema operativo (CmdExec)|  
|**4**|Agente de instantáneas de replicación|  
|**5**|Agente de registro del LOG de replicación|  
|**6**|Agente de distribución de replicación|  
|**7**|Agente de mezcla de replicación|  
|**8**|Agente de lectura de cola de replicación|  
|**9**|Comando de Analysis Services|  
|**10**|Consulta de Analysis Services|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] ejecución de paquetes|  
|**12**|Script de PowerShell|  
  
 [ **@subsystem_name**= ] **'***subsystem_name***'**  
 Nombre del subsistema al que se revoca el acceso. El *subsystem_name* es **sysname**, su valor predeterminado es null. Cualquier *subsystem_id* o *subsystem_name* debe especificarse, pero no pueden especificarse ambos. En la tabla siguiente se muestran los valores disponibles para cada subsistema.  
  
|Value|Description|  
|-----------|-----------------|  
|ActiveScripting|Script ActiveX|  
|CmdExec|Sistema operativo (CmdExec)|  
|Snapshot|Agente de instantáneas de replicación|  
|LogReader|Agente de registro del LOG de replicación|  
|Distribución|Agente de distribución de replicación|  
|Mezcla|Agente de mezcla de replicación|  
|QueueReader|Agente de lectura de cola de replicación|  
|ANALYSISQUERY|Comando de Analysis Services|  
|ANALYSISCOMMAND|Consulta de Analysis Services|  
|Dts|[!INCLUDE[ssIS](../../includes/ssis-md.md)] ejecución de paquetes|  
|PowerShell|Script de PowerShell|  
  
## <a name="remarks"></a>Comentarios  
 Al revocar el acceso a un subsistema no se cambian los permisos de la entidad de seguridad especificada en el proxy.  
  
> [!NOTE]  
>  Para determinar los pasos de trabajo hacen referencia a un proxy, haga clic en el **proxy** nodo bajo **Agente SQL Server** en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y, a continuación, haga clic en **propiedades**. En el **propiedades de la cuenta de Proxy** cuadro de diálogo, seleccione la **referencias** página para ver todos los pasos de trabajo que hacen referencia a este proxy.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_revoke_proxy_from_subsystem**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se revoca el acceso al subsistema de [!INCLUDE[ssIS](../../includes/ssis-md.md)] para el proxy `Catalog application proxy`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_proxy_from_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_name = N'Dts';  
```  
  
## <a name="see-also"></a>Vea también  
 [Agente SQL Server almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Implementar la seguridad del Agente SQL Server](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [sp_grant_proxy_to_subsystem &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
