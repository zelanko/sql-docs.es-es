---
title: sp_syspolicy_set_config_history_retention (Transact-SQL) | Documentos de Microsoft
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
- sp_syspolicy_set_config_history_retention_TSQL
- sp_syspolicy_set_config_history_retention
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_set_config_history_retention
ms.assetid: 2574898a-e724-4447-b96c-ff778471339d
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c93bfce977e0bba92ab9ef4f5fbacf9a3dffdb50
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spsyspolicysetconfighistoryretention-transact-sql"></a>sp_syspolicy_set_config_history_retention (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Especifica el número de días que se mantiene el historial de evaluación de directivas para la administración basada en directivas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syspolicy_set_config_history_retention [ @value = ] value  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@value=** ] *valor*  
 Es el número de días que se conserva el historial de administración basada en directivas. *valor* es **sqlvariant**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Debe ejecutar sp_syspolicy_set_config_history_retention en el contexto de la base de datos del sistema msdb.  
  
 Si *valor* se establece en 0, el historial no se eliminará automáticamente.  
  
 Para ver el valor actual de retención del historial, ejecute la consulta siguiente:  
  
```  
SELECT current_value FROM msdb.dbo.syspolicy_configuration  
WHERE name = 'HistoryRetentionInDays'  
```  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de base de datos PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Posible elevación de credenciales: los usuarios del rol PolicyAdministratorRole pueden crear desencadenadores del servidor y programar ejecuciones de directivas que pueden afectar al funcionamiento de la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por ejemplo, los usuarios del rol PolicyAdministratorRole pueden crear una directiva que puede evitar que la mayoría de los objetos se creen en [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Debido a esta posible elevación de credenciales, el rol PolicyAdministratorRole se debería conceder únicamente a los usuarios que sean de confianza para controlar la configuración de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se establece la retención del historial de evaluación de directivas en 28 días.  
  
```  
EXEC msdb.dbo.sp_syspolicy_set_config_history_retention @value = 28;  
  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de administración basada en directivas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql.md)  
  
  
