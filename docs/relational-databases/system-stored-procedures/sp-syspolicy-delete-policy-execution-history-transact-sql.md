---
title: sp_syspolicy_delete_policy_execution_history (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
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
- sp_syspolicy_delete_policy_execution_history
- sp_syspolicy_delete_policy_execution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_delete_policy_execution_history
ms.assetid: fe651af9-267e-45ec-b4e7-4b0698fb1be3
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 319a2b151fd41fcb94ed624a70f2c46c3e3dab91
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
 [  **@policy_id=** ] *policy_id*  
 Es el identificador de la directiva para la que desea eliminar el historial de ejecución. *policy_id* es **int**y es necesario. Puede ser NULL.  
  
 [  **@oldest_date=** ] **'***oldest_date***'**  
 Es la fecha más antigua para la que desea mantener el historial de ejecución de directivas. Se eliminan todos los historiales de ejecución anteriores a esta fecha. *oldest_date* es **datetime**y es necesario. Puede ser NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Debe ejecutar sp_syspolicy_delete_policy_execution_history en el contexto de la base de datos del sistema msdb.  
  
 Para obtener los valores de *policy_id*, y para ver las fechas del historial de ejecución, puede usar la consulta siguiente:  
  
```  
SELECT a.name AS N'policy_name', b.policy_id, b.start_date, b.end_date  
FROM msdb.dbo.syspolicy_policies AS a   
INNER JOIN msdb.dbo.syspolicy_policy_execution_history AS b  
ON a.policy_id = b.policy_id  
```  
  
 El comportamiento siguiente se aplica si especifica NULL para uno o ambos valores:  
  
-   Para eliminar el historial de ejecución de todas las directivas, especifique NULL para *policy_id* y *oldest_date*.  
  
-   Para eliminar el historial de ejecución de todas las directivas de una directiva concreta, especifique un identificador de la directiva *policy_id*, y especifique NULL como *oldest_date*.  
  
-   Para eliminar el historial de ejecución de directiva para todas las directivas antes de una fecha concreta, especifique NULL para *policy_id*y especifique una fecha para *oldest_date*.  
  
 Para almacenar el historial de ejecución de directivas, puede abrir el registro de historial de directivas en el Explorador de objetos y exportar el historial de ejecución a un archivo. Para acceder al registro de historial de directivas, expanda **administración**, haga clic en **administración de directivas de**y, a continuación, haga clic en **Ver historial**.  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de base de datos PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Posible elevación de credenciales: los usuarios del rol PolicyAdministratorRole pueden crear desencadenadores del servidor y programar ejecuciones de directivas que pueden afectar al funcionamiento de la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por ejemplo, los usuarios del rol PolicyAdministratorRole pueden crear una directiva que puede evitar que la mayoría de los objetos se creen en [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Debido a esta posible elevación de credenciales, el rol PolicyAdministratorRole se debería conceder únicamente a los usuarios que sean de confianza para controlar la configuración de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
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
  
  
