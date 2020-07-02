---
title: sp_help_operator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_operator
- sp_help_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_operator
ms.assetid: caedc43d-44b8-415a-897e-92923f6de3b8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 79a123faab9b587d56d957a3f9e1765e8619f97d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85634304"
---
# <a name="sp_help_operator-transact-sql"></a>sp_help_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Presenta información acerca de los operadores definidos en el servidor.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_operator  
     { [ @operator_name = ] 'operator_name'   
     | [ @operator_id = ] operator_id }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @operator_name = ] 'operator_name'`Nombre del operador. *operator_name* es de **tipo sysname**. Si no se especifica *operator_name* , se devuelve información acerca de todos los operadores.  
  
`[ @operator_id = ] operator_id`Número de identificación del operador para el que se solicita información. *operator_id*es de **tipo int**y su valor predeterminado es NULL.  
  
> [!NOTE]  
>  Se debe especificar *operator_id* o *operator_name* , pero no se pueden especificar ambos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Número de identificación del operador.|  
|**name**|**sysname**|Nombre del operador.|  
|**activó**|**tinyint**|El operador está disponible para recibir notificaciones:<br /><br /> **1** = sí<br /><br /> **0** = no|  
|**email_address**|**nvarchar(100**|Dirección de correo electrónico del operador.|  
|**last_email_date**|**int**|Fecha de la última notificación al operador mediante correo electrónico.|  
|**last_email_time**|**int**|Hora de la última notificación al operador mediante correo electrónico.|  
|**pager_address**|**nvarchar(100**|Dirección del buscapersonas del operador.|  
|**last_pager_date**|**int**|Fecha de la última notificación al operador mediante buscapersonas.|  
|**last_pager_time**|**int**|Hora de la última notificación al operador mediante buscapersonas.|  
|**weekday_pager_start_time**|**int**|Hora inicial a partir de la cual el operador está disponible para recibir notificaciones mediante buscapersonas durante los días laborables.|  
|**weekday_pager_end_time**|**int**|Hora en que el operador deja de estar disponible para recibir notificaciones mediante buscapersonas los días laborables.|  
|**saturday_pager_start_time**|**int**|Hora inicial a partir de la cual el operador está disponible para recibir notificaciones mediante buscapersonas los sábados.|  
|**saturday_pager_end_time**|**int**|Hora en que el operador deja de estar disponible para recibir notificaciones mediante buscapersonas los sábados.|  
|**sunday_pager_start_time**|**int**|Hora inicial a partir de la cual el operador está disponible para recibir notificaciones mediante buscapersonas los domingos.|  
|**sunday_pager_end_time**|**int**|Hora en que el operador deja de estar disponible para recibir notificaciones mediante buscapersonas los domingos.|  
|**pager_days**|**tinyint**|Una máscara de bits (**1** = domingo, **64** = sábado) de los días de la semana que indica cuándo está disponible el operador para recibir notificaciones por buscapersonas.|  
|**netsend_address**|**nvarchar(100**|Dirección de red del operador para notificaciones por mensaje emergente de red.|  
|**last_netsend_date**|**int**|Fecha de la última notificación al operador mediante un mensaje emergente de red.|  
|**last_netsend_time**|**int**|Hora de la última notificación al operador mediante un mensaje emergente de red.|  
|**category_name**|**sysname**|Nombre de la categoría de operadores a la que pertenece este operador.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_operator** se debe ejecutar desde la base de datos **msdb** .  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se proporciona información sobre el operador `François Ajenstat`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_operator  
    @operator_name = N'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_operator &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_update_operator &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
