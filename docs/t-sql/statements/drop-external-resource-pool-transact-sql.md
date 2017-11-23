---
title: Quitar grupo de recursos externo (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL RESOURCE POOL
- DROP_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs: TSQL
helpviewer_keywords: DROP EXTERNAL RESOURCE POOL statement
ms.assetid: e2fa01bd-96ff-4ea9-bb08-6cb6b6adf68c
caps.latest.revision: "6"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: edd6e956bc9453317c928a099469e65ddf5e0e0f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="drop-external-resource-pool-transact-sql"></a>Quitar grupo de recursos externo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Elimina un grupo de recursos externos del regulador de recursos usa para definir los recursos para los procesos externos. Para los servicios de R rige el grupo externo `rterm.exe`, `BxlServer.exe`y otros procesos generados por ellos. Grupos de recursos externos se crean mediante [CREATE EXTERNAL RESOURCE POOL &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-resource-pool-transact-sql.md) y modificar mediante [ALTER EXTERNAL RESOURCE POOL &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-external-resource-pool-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DROP EXTERNAL RESOURCE POOL pool_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *pool_name*  
 El nombre del grupo de recursos externos va a eliminar.  
  
## <a name="remarks"></a>Comentarios  
 No se puede quitar un grupo de recursos externos si contiene grupos de cargas de trabajo.  
  
 No se pueden quitar los grupos de recursos de servidor predeterminados o internos del regulador de recursos.  
  
 La reconfiguración n  
  
 Si va a ejecutar instrucciones de DDL, se recomienda familiarizarse primero con los estados del regulador de recursos. Para obtener más información, consulte [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere `CONTROL SERVER` permiso.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el grupo de recursos externo denominado `ex_pool`.  
  
```  
DROP EXTERNAL RESOURCE POOL ex_pool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Opción de configuración de servidor scripts externos habilitados](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Problemas conocidos de SQL Server R Services](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [Modificar grupo de recursos externo &#40; Transact-SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [Eliminar grupo de recursos &#40; Transact-SQL &#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)  
  
  
