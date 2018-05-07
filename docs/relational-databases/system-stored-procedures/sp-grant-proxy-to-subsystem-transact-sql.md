---
title: sp_grant_proxy_to_subsystem (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_subsystem_TSQL
- sp_grant_login_to_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_proxy_to_subsystem
ms.assetid: 866aaa27-a1e0-453a-9b1b-af39431ad9c2
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a52e19c374c0b1ac14749e1e1bcc53f3a30d2b2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spgrantproxytosubsystem-transact-sql"></a>sp_grant_proxy_to_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede acceso al proxy a un subsistema.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_grant_proxy_to_subsystem  
     { [ @proxy_id = ] proxy_id | [ @proxy_name = ] 'proxy_name' },  
     { [ @subsystem_id = ] subsystem_id | [ @subsystem_name = ] 'subsystem_name' }  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@proxy_id =** ] *Id.*  
 Número de identificación del proxy al que se va a conceder acceso. El *proxy_id* es **int**, su valor predeterminado es null. Cualquier *proxy_id* o *proxy_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [  **@proxy_name =** ] **'***proxy_name***'**  
 Nombre del proxy al que se va a conceder el acceso. El *proxy_name* es **sysname**, su valor predeterminado es null. Cualquier *proxy_id* o *proxy_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [  **@subsystem_id =** ] *Id.*  
 Número de Id. del subsistema al que se va a conceder el acceso. El *subsystem_id* es **int**, su valor predeterminado es null. Cualquier *subsystem_id* o *subsystem_name* debe especificarse, pero no pueden especificarse ambos. En la tabla siguiente se muestran los valores disponibles para cada subsistema.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**2**|Script[!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX<br /><br /> **\*\* Importante \* \***  subsistema de scripts de ActiveX en el que se va a quitar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.|  
|**3**|Sistema operativo (**CmdExec**)|  
|**4**|Agente de instantáneas de replicación|  
|**5**|Agente de registro del LOG de replicación|  
|**6**|Agente de distribución de replicación|  
|**7**|Agente de mezcla de replicación|  
|**8**|Agente de lectura de cola de replicación|  
|**9**|Consulta de Analysis Services|  
|**10**|Comando de Analysis Services|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] ejecución de paquetes|  
|**12**|Script de PowerShell|  
  
 [  **@subsystem_name =** ] **'***subsystem_name***'**  
 Nombre del subsistema al que se va a conceder el acceso. El **subsystem_name** es **sysname**, su valor predeterminado es null. Cualquier *subsystem_id* o *subsystem_name* debe especificarse, pero no pueden especificarse ambos. En la tabla siguiente se muestran los valores disponibles para cada subsistema.  
  
|Value|Description|  
|-----------|-----------------|  
|**ActiveScripting**|Script ActiveX|  
|**CmdExec**|Sistema operativo (**CmdExec**)|  
|**Snapshot**|Agente de instantáneas de replicación|  
|**LogReader**|Agente de registro del LOG de replicación|  
|**Distribución**|Agente de distribución de replicación|  
|**Mezcla**|Agente de mezcla de replicación|  
|**QueueReader**|Agente de lectura de cola de replicación|  
|**ANALYSISQUERY**|Consulta de Analysis Services|  
|**ANALYSISCOMMAND**|Comando de Analysis Services|  
|**Dts**|Ejecución de paquetes SSIS|  
|**PowerShell**|Script de PowerShell|  
  
## <a name="remarks"></a>Comentarios  
 La concesión de acceso al proxy a un subsistema no cambia los permisos para la entidad de seguridad especificada en el proxy.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_grant_proxy_to_subsystem**.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-granting-access-to-a-subsystem-by-id"></a>A. Conceder acceso a un subsistema mediante el identificador  
 En el siguiente ejemplo se concede acceso al proxy `Catalog application proxy` al subsistema de scripts ActiveX.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_id = 2;  
GO  
```  
  
### <a name="b-granting-access-to-a-subsystem-by-name"></a>B. Conceder acceso a un subsistema mediante el nombre.  
 En el siguiente ejemplo se concede acceso al proxy `Catalog application proxy` al subsistema de ejecución de paquetes SSIS.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = N'Catalog application proxy',  
    @subsystem_name = N'Dts' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Implementar la seguridad del Agente SQL Server](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [sp_revoke_proxy_from_subsystem &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-proxy-from-subsystem-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_update_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-proxy-transact-sql.md)  
  
  
