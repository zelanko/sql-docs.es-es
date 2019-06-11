---
title: sp_enum_login_for_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_login_for_proxy_TSQL
- sp_enum_login_for_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_login_for_proxy
ms.assetid: 62a75019-248a-44c8-a5cc-c79f55ea3acf
ms.author: vanto
author: VanMSFT
manager: jroth
ms.openlocfilehash: fd5b172b7029376d6f9641552315fc64e734cc8a
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822630"
---
# <a name="spenumloginforproxy-transact-sql"></a>sp_enum_login_for_proxy (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra las asociaciones entre las entidades de seguridad y los servidores proxy.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_enum_login_for_proxy  
    [ @name = ] 'name'  
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'` El nombre de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entidad de seguridad, inicio de sesión, el rol de servidor, o **msdb** rol de base de datos para mostrar los servidores proxy para. El nombre es **nvarchar (256)** , su valor predeterminado es null.  
  
`[ @proxy_id = ] id` El número de identificación del proxy del servidor proxy para mostrar información. El *proxy_id* es **int**, su valor predeterminado es null. Ya sea el *id* o el *proxy_name* se puede especificar.  
  
`[ @proxy_name = ] 'proxy_name'` El nombre del servidor proxy para mostrar información. El *proxy_name* es **sysname**, su valor predeterminado es null. Ya sea el *id* o el *proxy_name* se puede especificar.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Número de identificación del proxy.|  
|**proxy_name**|**sysname**|Nombre del proxy.|  
|**Nombre**|**sysname**|Nombre de la entidad de seguridad para la asociación.|  
|**flags**|**int**|Tipo de la entidad de seguridad.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión<br /><br /> **1** = rol fijo del sistema<br /><br /> **2** = rol de base de datos en **msdb**|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="remarks"></a>Comentarios  
 Si no se proporcionan parámetros, **sp_enum_login_for_proxy** muestra información acerca de todos los inicios de sesión en la instancia para cada servidor proxy.  
  
 Cuando se proporciona un Id. o nombre del proxy, **sp_enum_login_for_proxy** se enumeran los inicios de sesión que tienen acceso al proxy. Cuando se proporciona un nombre de inicio de sesión, **sp_enum_login_for_proxy** listas de los servidores proxy que el inicio de sesión tiene acceso a.  
  
 Cuando se suministra información acerca del proxy y un nombre de inicio de sesión, el conjunto de resultados devuelve una fila si el inicio de sesión especificado tiene acceso al proxy especificado.  
  
 Este procedimiento almacenado se encuentra en **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución para este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-all-associations"></a>A. Mostrar todas las asociaciones  
 En el ejemplo siguiente se muestran todos los permisos establecidos entre los inicios de sesión y los servidores proxy de la instancia actual.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy ;  
GO  
```  
  
### <a name="b-listing-proxies-for-a-specific-login"></a>b. Mostrar los servidores proxy para un inicio de sesión específico  
 En el ejemplo siguiente se muestran los servidores proxy a los que tiene acceso el inicio de sesión `terrid`.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy  
    @name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_help_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
