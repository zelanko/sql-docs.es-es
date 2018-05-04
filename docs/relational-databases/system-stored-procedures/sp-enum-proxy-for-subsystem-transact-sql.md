---
title: sp_enum_proxy_for_subsystem (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- sp_enum_proxy_for_subsystem_TSQL
- sp_enum_proxy_for_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_proxy_for_subsystems
ms.assetid: 580cc3be-1068-4a96-8d15-78ca3a5bb719
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 458ee9e409da49b62a92ade2c8af822263522260
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spenumproxyforsubsystem-transact-sql"></a>sp_enum_proxy_for_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra los permisos de acceso a subsistemas concedidos a los servidores proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_enum_proxy_for_subsystem  
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@proxy_id** =] *proxy_id*  
 Número de identificación del proxy del que se va a mostrar información. El *proxy_id* es **int**, su valor predeterminado es null. Ya sea la *Id. de* o *proxy_name* se puede especificar.  
  
 [ **@proxy_name** =] **'***proxy_name***'**  
 Nombre del proxy del que se va a mostrar información. El *proxy_name* es **sysname**, su valor predeterminado es null. Ya sea la *Id. de* o *proxy_name* se puede especificar.  
  
 [ **@subsystem_id** =] *subsystem_id*  
 Número de identificación del subsistema del que se va a mostrar información. El *subsystem_id* es **int**, su valor predeterminado es null. Ya sea la *subsystem_id* o *subsystem_name* se puede especificar.  
  
 [ **@subsystem_name** =] **'***subsystem_name***'**  
 Nombre del subsistema del que se va a mostrar información. El *subsystem_name* es **sysname**, su valor predeterminado es null. Ya sea la *subsystem_id* o *subsystem_name* se puede especificar.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|Número de identificación del subsistema.|  
|**subsystem_name**|**sysname**|Nombre del subsistema.|  
|**proxy_id**|**int**|Número de identificación del proxy.|  
|**proxy_name**|**sysname**|Nombre del proxy.|  
  
## <a name="remarks"></a>Comentarios  
 Si no se proporcionan parámetros, **sp_enum_proxy_for_subsystem** muestra información acerca de todos los servidores proxy en la instancia para cada subsistema.  
  
 Cuando se proporciona un Id. o nombre del proxy, **sp_enum_proxy_for_subsystem** listas subsistemas a los que el proxy tenga acceso. Cuando se proporciona un Id. o nombre de subsistema, **sp_enum_proxy_for_subsystem** muestra los servidores proxy que tienen acceso a ese subsistema.  
  
 Cuando se suministra información acerca del proxy y del subsistema, el conjunto de resultados devuelve una fila si el proxy especificado tiene acceso al subsistema especificado.  
  
 Este procedimiento almacenado se encuentra en **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Permisos de ejecución para este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-all-associations"></a>A. Mostrar todas las asociaciones  
 En el ejemplo siguiente se muestran todos los permisos establecidos entre los servidores proxy y los subsistemas de la instancia actual.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem ;  
GO  
```  
  
### <a name="b-determining-if-a-proxy-has-access-to-a-specific-subsystem"></a>B. Determinar si un proxy tiene acceso a un subsistema específico  
 En el ejemplo siguiente se devuelve una fila si el proxy `Catalog application proxy` tiene acceso al subsistema `ActiveScripting`. En caso contrario, se devuelve un conjunto de resultados vacío.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem  
    @subsystem_name = 'ActiveScripting',  
    @proxy_name = 'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_grant_proxy_to_subsystem &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
