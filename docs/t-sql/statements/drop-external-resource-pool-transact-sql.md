---
title: DROP EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL RESOURCE POOL
- DROP_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL RESOURCE POOL statement
ms.assetid: e2fa01bd-96ff-4ea9-bb08-6cb6b6adf68c
author: dphansen
ms.author: davidph
manager: cgronlund
ms.openlocfilehash: f4326901f40c580e869cae11ed184ca70cd7b442
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68892744"
---
# <a name="drop-external-resource-pool-transact-sql"></a>DROP EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Elimina un grupo de recursos externos de Resource Governor que sirve para definir los recursos de los procesos externos. 

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
En [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] en [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], el grupo externo rige `rterm.exe`, `BxlServer.exe` y otros procesos generados por ellos.
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
En [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)], el grupo externo rige `rterm.exe`, `python.exe`, `BxlServer.exe` y otros procesos generados por ellos.
::: moniker-end

Los grupos de recursos externos se crean por medio de [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md) y se modifican a través de [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md).  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```
DROP EXTERNAL RESOURCE POOL pool_name  
```  
  
## <a name="arguments"></a>Argumentos

*pool_name*  
Nombre del grupo de recursos externos que se va a eliminar.  
  
## <a name="remarks"></a>Observaciones

No se puede quitar un grupo de recursos externo si contiene grupos de cargas de trabajo.  

No se pueden quitar los grupos de recursos de servidor predeterminados o internos del regulador de recursos.  

Si va a ejecutar instrucciones de DDL, se recomienda familiarizarse primero con los estados del regulador de recursos. Para obtener más información, vea [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  

## <a name="permissions"></a>Permisos

Requiere el permiso `CONTROL SERVER`.  

## <a name="examples"></a>Ejemplos

En el siguiente ejemplo se quita el grupo de recursos externos denominado `ex_pool`.  

```sql
DROP EXTERNAL RESOURCE POOL ex_pool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  

## <a name="see-also"></a>Consulte también

+ [Opción de configuración de servidor Scripts externos habilitados](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)
+ [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)
+ [Problemas conocidos de SQL Server R Services](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)
+ [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)
+ [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
+ [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)
+ [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
