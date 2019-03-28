---
title: sp_help_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5e0bbf6e8befa751ee680cd97c2a29ad9f0fe084
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527697"
---
# <a name="sphelpproxy-transact-sql"></a>sp_help_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información de uno o varios servidores proxy.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @subsystem_name = ] 'subsystem_name' ,  
    [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @proxy_id = ] id` El número de identificación del proxy del servidor proxy para mostrar información. El *proxy_id* es **int**, su valor predeterminado es null. Ya sea el *id* o el *proxy_name* se puede especificar.  
  
`[ @proxy_name = ] 'proxy_name'` El nombre del servidor proxy para mostrar información. El *proxy_name* es **sysname**, su valor predeterminado es null. Ya sea el *id* o el *proxy_name* se puede especificar.  
  
`[ @subsystem_name = ] 'subsystem_name'` El nombre del subsistema para mostrar los servidores proxy para. El *subsystem_name* es **sysname**, su valor predeterminado es null. Cuando *subsystem_name* se especifica, *nombre* también debe especificarse.  
  
 En la tabla siguiente se muestran los valores disponibles para cada subsistema.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|ActiveScripting|Script ActiveX|  
|CmdExec|Sistema operativo (CmdExec)|  
|Snapshot|Agente de instantáneas de replicación|  
|LogReader|Agente de registro del LOG de replicación|  
|Distribución|Agente de distribución de replicación|  
|Mezcla|Replication Merge Agent|  
|QueueReader|Agente de lectura de cola de replicación|  
|ANALYSISQUERY|Comando de Analysis Services|  
|ANALYSISCOMMAND|Consulta de Analysis Services|  
|Dts|Ejecución de paquetes SSIS|  
|PowerShell|Script de PowerShell|  
  
`[ @name = ] 'name'` El nombre de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para mostrar los servidores proxy para inicio de sesión. El nombre es **nvarchar (256)**, su valor predeterminado es null. Cuando *nombre* se especifica, *subsystem_name* también debe especificarse.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Número de identificación del proxy.|  
|**Nombre**|**sysname**|Nombre del proxy.|  
|**credential_identity**|**sysname**|Nombre de dominio y nombre de usuario de Microsoft Windows para la credencial asociada con el proxy.|  
|**enabled**|**tinyint**|Si el proxy está habilitado. { **0** = no habilitado, **1** = habilitado}|  
|**description**|**nvarchar(1024)**|Descripción de este proxy.|  
|**user_sid**|**varbinary(85)**|Id. de seguridad del usuario de Windows para este proxy.|  
|**credential_id**|**int**|Identificador de la credencial asociada con este proxy.|  
|**credential_identity_exists**|**int**|Si existe credential_identity. { 0 = no existe, 1 = existe }|  
  
## <a name="remarks"></a>Comentarios  
 Si no se proporcionan parámetros, **sp_help_proxy** muestra información de todos los servidores proxy de la instancia.  
  
 Para determinar qué servidores proxy de un inicio de sesión se puede usar para un subsistema dado, especifique *nombre* y *subsystem_name*. Cuando se proporcionan estos argumentos, **sp_help_proxy** muestra los servidores proxy que el inicio de sesión especificado el acceso y que es posible que se puede usar para el subsistema especificado.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. A otros usuarios debe concederse el rol fijo de base de datos **SQLAgentOperatorRole** en la base de datos **msdb** .  
  
 Para obtener más información acerca de **SQLAgentOperatorRole**, consulte [Roles fijos de base de datos de SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
> [!NOTE]  
>  El **credential_identity** y **user_sid** solo se devuelven las columnas en el conjunto de resultados cuando los miembros de **sysadmin** ejecutar este procedimiento almacenado.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-information-for-all-proxies"></a>A. Mostrar información de todos los servidores proxy  
 El ejemplo siguiente muestra información de todos los servidores proxy de la instancia.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-proxy"></a>b. Mostrar información de un proxy específico  
 El ejemplo siguiente muestra información del proxy denominado `Catalog application proxy`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del Agente SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
  
  
