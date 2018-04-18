---
title: sp_help_operator (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/01/2016
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
- sp_help_operator
- sp_help_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_operator
ms.assetid: caedc43d-44b8-415a-897e-92923f6de3b8
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 48495576db891a8acbd944578f45bfa5267fb9c7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpoperator-transact-sql"></a>sp_help_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Presenta información acerca de los operadores definidos en el servidor.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_operator  
     { [ @operator_name = ] 'operator_name'   
     | [ @operator_id = ] operator_id }  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@operator_name=** ] **'***operator_name***'**  
 El nombre del operador. *operator_name* es **sysname**. Si *operator_name* no es se especifica, se devuelve información sobre todos los operadores.  
  
 [  **@operator_id=** ] *operator_id*  
 Es el número de identificación del operador acerca del que se solicita información. *operator_id*es **int**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Cualquier *operator_id* o *operator_name* debe especificarse, pero no pueden especificarse ambos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Número de identificación del operador.|  
|**Nombre**|**sysname**|Nombre del operador.|  
|**enabled**|**tinyint**|El operador está disponible para recibir notificaciones:<br /><br /> **1** = Sí<br /><br /> **0** = No|  
|**email_address**|**nvarchar (100)**|Dirección de correo electrónico del operador.|  
|**last_email_date**|**int**|Fecha de la última notificación al operador mediante correo electrónico.|  
|**last_email_time**|**int**|Hora de la última notificación al operador mediante correo electrónico.|  
|**pager_address**|**nvarchar (100)**|Dirección del buscapersonas del operador.|  
|**last_pager_date**|**int**|Fecha de la última notificación al operador mediante buscapersonas.|  
|**last_pager_time**|**int**|Hora de la última notificación al operador mediante buscapersonas.|  
|**weekday_pager_start_time**|**int**|Hora inicial a partir de la cual el operador está disponible para recibir notificaciones mediante buscapersonas durante los días laborables.|  
|**weekday_pager_end_time**|**int**|Hora en que el operador deja de estar disponible para recibir notificaciones mediante buscapersonas los días laborables.|  
|**saturday_pager_start_time**|**int**|Hora inicial a partir de la cual el operador está disponible para recibir notificaciones mediante buscapersonas los sábados.|  
|**saturday_pager_end_time**|**int**|Hora en que el operador deja de estar disponible para recibir notificaciones mediante buscapersonas los sábados.|  
|**sunday_pager_start_time**|**int**|Hora inicial a partir de la cual el operador está disponible para recibir notificaciones mediante buscapersonas los domingos.|  
|**sunday_pager_end_time**|**int**|Hora en que el operador deja de estar disponible para recibir notificaciones mediante buscapersonas los domingos.|  
|**pager_days**|**tinyint**|Una máscara de bits (**1** = el domingo, **64** = el sábado) de días de la semana que indica cuándo el operador está disponible para recibir notificaciones mediante localizador.|  
|**netsend_address**|**nvarchar (100)**|Dirección de red del operador para notificaciones por mensaje emergente de red.|  
|**last_netsend_date**|**int**|Fecha de la última notificación al operador mediante un mensaje emergente de red.|  
|**last_netsend_time**|**int**|Hora de la última notificación al operador mediante un mensaje emergente de red.|  
|**category_name**|**sysname**|Nombre de la categoría de operadores a la que pertenece este operador.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_operator** se debe ejecutar desde la **msdb** base de datos.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
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
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
