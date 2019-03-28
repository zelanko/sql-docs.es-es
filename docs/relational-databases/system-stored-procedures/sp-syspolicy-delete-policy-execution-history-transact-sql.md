---
title: sp_syspolicy_delete_policy_execution_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_delete_policy_execution_history
- sp_syspolicy_delete_policy_execution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_delete_policy_execution_history
ms.assetid: fe651af9-267e-45ec-b4e7-4b0698fb1be3
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 6660eba76675fbe261af33f647d60456ced839d2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536967"
---
# <a name="spsyspolicydeletepolicyexecutionhistory-transact-sql"></a>sp_syspolicy_delete_policy_execution_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina el historial de ejecución de directivas para la administración basada en directivas. Puede utilizar este procedimiento almacenado para eliminar el historial de ejecución de una directiva concreta o de todas las directivas, y el historial de ejecución anterior a una fecha concreta.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syspolicy_delete_policy_execution_history [ @policy_id = ] policy_id ]  
    [ , [ @oldest_date = ] 'oldest_date' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @policy_id = ] policy_id` Es el identificador de la directiva para el que desea eliminar el historial de ejecución. *policy_id* es **int**y es necesario. Puede ser NULL.  
  
`[ @oldest_date = ] 'oldest_date'` Es la fecha más antigua para la que desea mantener el historial de ejecución de directiva. Se eliminan todos los historiales de ejecución anteriores a esta fecha. *oldest_date* es **datetime**y es necesario. Puede ser NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Debe ejecutar sp_syspolicy_delete_policy_execution_history en el contexto de la base de datos del sistema msdb.  
  
 Para obtener los valores de *policy_id*, y para ver las fechas del historial de ejecución, puede usar la siguiente consulta:  
  
```  
SELECT a.name AS N'policy_name', b.policy_id, b.start_date, b.end_date  
FROM msdb.dbo.syspolicy_policies AS a   
INNER JOIN msdb.dbo.syspolicy_policy_execution_history AS b  
ON a.policy_id = b.policy_id  
```  
  
 El comportamiento siguiente se aplica si especifica NULL para uno o ambos valores:  
  
-   Para eliminar el historial de ejecución de todas las directivas, especifique NULL para *policy_id* y *oldest_date*.  
  
-   Para eliminar el historial de ejecución de todas las directivas de una directiva concreta, especifique un identificador de directiva para *policy_id*, y especifique NULL como *oldest_date*.  
  
-   Para eliminar el historial de ejecución de directiva para todas las directivas antes de una fecha concreta, especifique NULL para *policy_id*y especifique una fecha para *oldest_date*.  
  
 Para almacenar el historial de ejecución de directivas, puede abrir el registro de historial de directivas en el Explorador de objetos y exportar el historial de ejecución a un archivo. Para obtener acceso al registro de historial de directivas, expanda **administración**, haga clic en **administración de directivas**y, a continuación, haga clic en **Ver historial**.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de base de datos PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Posible elevación de credenciales: Los usuarios del rol PolicyAdministratorRole pueden crear desencadenadores del servidor y programar ejecuciones de directivas que pueden afectar al funcionamiento de la instancia de la [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por ejemplo, los usuarios del rol PolicyAdministratorRole pueden crear una directiva que puede evitar que la mayoría de los objetos se creen en [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Debido a esta posible elevación de credenciales, el rol PolicyAdministratorRole se debería conceder únicamente a los usuarios que sean de confianza para controlar la configuración de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se elimina el historial de ejecución de directivas anterior a una fecha concreta de una directiva con el identificador 7.  
  
```  
EXEC msdb.dbo.sp_syspolicy_delete_policy_execution_history @policy_id = 7  
, @oldest_date = '2009-02-16 16:00:00.000';  
  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de administración basada en directivas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_set_config_history_retention &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [sp_syspolicy_purge_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-purge-history-transact-sql.md)  
  
  
