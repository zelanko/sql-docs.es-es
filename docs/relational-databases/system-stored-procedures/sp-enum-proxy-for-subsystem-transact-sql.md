---
title: sp_enum_proxy_for_subsystem (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_proxy_for_subsystem_TSQL
- sp_enum_proxy_for_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_proxy_for_subsystems
ms.assetid: 580cc3be-1068-4a96-8d15-78ca3a5bb719
ms.author: vanto
author: VanMSFT
manager: craigg
ms.openlocfilehash: d521a16fa7c18e67e1929cb0e38aecf862d6c18a
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822643"
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
`[ @proxy_id = ] proxy_id` El número de identificación del proxy que se muestra información. El *proxy_id* es **int**, su valor predeterminado es null. Ya sea el *id* o el *proxy_name* se puede especificar.  
  
`[ @proxy_name = ] 'proxy_name'` El nombre del servidor proxy para mostrar información. El *proxy_name* es **sysname**, su valor predeterminado es null. Ya sea el *id* o el *proxy_name* se puede especificar.  
  
`[ @subsystem_id = ] subsystem_id` El número de identificación del subsistema para mostrar información. El *subsystem_id* es **int**, su valor predeterminado es null. Ya sea el *subsystem_id* o *subsystem_name* se puede especificar.  
  
`[ @subsystem_name = ] 'subsystem_name'` El nombre del subsistema para mostrar información. El *subsystem_name* es **sysname**, su valor predeterminado es null. Ya sea el *subsystem_id* o *subsystem_name* se puede especificar.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|Número de identificación del subsistema.|  
|**subsystem_name**|**sysname**|Nombre del subsistema.|  
|**proxy_id**|**int**|Número de identificación del proxy.|  
|**proxy_name**|**sysname**|Nombre del proxy.|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="remarks"></a>Comentarios  
 Si no se proporcionan parámetros, **sp_enum_proxy_for_subsystem** muestra información acerca de todos los servidores proxy en la instancia para cada subsistema.  
  
 Cuando se proporciona un Id. o nombre del proxy, **sp_enum_proxy_for_subsystem** subsistemas de listas que el proxy tenga acceso a. Cuando se proporciona un Id. o nombre de subsistema, **sp_enum_proxy_for_subsystem** muestra los servidores proxy que tienen acceso a ese subsistema.  
  
 Cuando se suministra información acerca del proxy y del subsistema, el conjunto de resultados devuelve una fila si el proxy especificado tiene acceso al subsistema especificado.  
  
 Este procedimiento almacenado se encuentra en **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución para este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-all-associations"></a>A. Mostrar todas las asociaciones  
 En el ejemplo siguiente se muestran todos los permisos establecidos entre los servidores proxy y los subsistemas de la instancia actual.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem ;  
GO  
```  
  
### <a name="b-determining-if-a-proxy-has-access-to-a-specific-subsystem"></a>b. Determinar si un proxy tiene acceso a un subsistema específico  
 En el ejemplo siguiente se devuelve una fila si el proxy `Catalog application proxy` tiene acceso al subsistema `ActiveScripting`. En caso contrario, se devuelve un conjunto de resultados vacío.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem  
    @subsystem_name = 'ActiveScripting',  
    @proxy_name = 'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_grant_proxy_to_subsystem &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
