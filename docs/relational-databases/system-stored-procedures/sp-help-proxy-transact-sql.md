---
title: sp_help_proxy (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f7053bfc6ccbca71783d0bbcdb8b9b5544f9d20
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
 [ **@proxy_id** =] *Id.*  
 Número de identificación del proxy del que se muestra información. El *proxy_id* es **int**, su valor predeterminado es null. Ya sea la *Id. de* o *proxy_name* se puede especificar.  
  
 [ **@proxy_name** =] **'***proxy_name***'**  
 Nombre del proxy del que se va a mostrar información. El *proxy_name* es **sysname**, su valor predeterminado es null. Ya sea la *Id. de* o *proxy_name* se puede especificar.  
  
 [ **@subsystem_name** =] '*subsystem_name*'  
 Nombre del subsistema del que se van a mostrar los servidores proxy. El *subsystem_name* es **sysname**, su valor predeterminado es null. Cuando *subsystem_name* se especifica, *nombre* también debe especificarse.  
  
 En la tabla siguiente se muestran los valores disponibles para cada subsistema.  
  
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
|Dts|Ejecución de paquetes SSIS|  
|PowerShell|Script de PowerShell|  
  
 [ **@name** =] '*nombre*'  
 Nombre del inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del que se van a mostrar los servidores proxy. El nombre es **nvarchar (256)**, su valor predeterminado es null. Cuando *nombre* se especifica, *subsystem_name* también debe especificarse.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Número de identificación del proxy.|  
|**Nombre**|**sysname**|Nombre del proxy.|  
|**credential_identity**|**sysname**|Nombre de dominio y nombre de usuario de Microsoft Windows para la credencial asociada con el proxy.|  
|**enabled**|**tinyint**|Si el proxy está habilitado. { **0** = no habilitado, **1** = habilitado}|  
|**Descripción**|**nvarchar(1024)**|Descripción de este proxy.|  
|**user_sid**|**varbinary(85)**|Id. de seguridad del usuario de Windows para este proxy.|  
|**credential_id**|**int**|Identificador de la credencial asociada con este proxy.|  
|**credential_identity_exists**|**int**|Si existe credential_identity. { 0 = no existe, 1 = existe }|  
  
## <a name="remarks"></a>Comentarios  
 Si no se proporcionan parámetros, **sp_help_proxy** muestra información de todos los servidores proxy de la instancia.  
  
 Para determinar los servidores proxy que un inicio de sesión pueden usar para un subsistema dado, especifique *nombre* y *subsystem_name*. Cuando se proporcionan estos argumentos, **sp_help_proxy** muestra los servidores proxy que el inicio de sesión especificado puede acceso y que puede utilizarse para el subsistema especificado.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. A otros usuarios debe concederse el rol fijo de base de datos **SQLAgentOperatorRole** en la base de datos **msdb** .  
  
 Para obtener más información acerca de **SQLAgentOperatorRole**, consulte [Roles fijos de base de datos de SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
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
  
### <a name="b-listing-information-for-a-specific-proxy"></a>B. Mostrar información de un proxy específico  
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
  
  
