---
title: sp_help_notification (Transact-SQL) | Documentos de Microsoft
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
- sp_help_notification
- sp_help_notification_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_notification
ms.assetid: 0273457f-9d2a-4a6f-9a16-6a6bf281cba0
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c779b314553c1895071ab04b5131d998c029cc94
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpnotification-transact-sql"></a>sp_help_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Presenta una lista de alertas de un operador dado o una lista de operadores para una alerta dada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_notification  
     [ @object_type = ] 'object_type' ,  
     [ @name = ] 'name' ,  
     [ @enum_type = ] 'enum_type' ,   
     [ @notification_method = ] notification_method   
     [ , [ @target_name = ] 'target_name' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@object_type =**] **'***object_type***'**  
 Tipo de información que se va a devolver. *object_type*es **char (9)**, no tiene ningún valor predeterminado. *object_type* puede ser ALERTS, que presenta las alertas asignadas al nombre del operador especificado*,* u OPERATORS, que presenta los operadores responsables del nombre de alerta especificado*.*  
  
 [  **@name =**] **'***nombre***'**  
 Un nombre de operador (si *object_type* es OPERATORS) o un nombre de la alerta (si *object_type* es ALERTS). *nombre* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@enum_type =**] **'***enum_type***'**  
 El *object_type*información que se devuelve. *enum_type* es ACTUAL en la mayoría de los casos. *enum_type*es **char (10)**, no tiene ningún valor predeterminado y puede ser uno de estos valores.  
  
|Value|Description|  
|-----------|-----------------|  
|ACTUAL|Muestra sólo el *tipos de objetos* asociada *nombre*.|  
|ALL|Enumera todos los*tipos de objetos* incluidos aquellos que no están asociados con *nombre*.|  
|TARGET|Muestra sólo el *tipos de objetos* coincidencia proporcionado *target_name*, independientemente de la asociación con*nombre*.|  
  
 [  **@notification_method =**] *notification_method*  
 Valor numérico que determina las columnas del método de notificación que se van a devolver. *notification_method* es **tinyint**, y puede tener uno de los siguientes valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Correo electrónico: devuelve solamente el **use_email** columna.|  
|**2**|Buscapersonas: devuelve solamente el **use_pager** columna.|  
|**4**|NetSend: devuelve solamente el **use_netsend** columna.|  
|**7**|Todas: devuelve todas las columnas.|  
  
 [  **@target_name =**] **'***target_name***'**  
 Para buscar un nombre de la alerta (si *object_type* es ALERTS) o un nombre de operador que se busca (si *object_type* es OPERATORS). *target_name* solo es necesario si *enum_type* es el destino. *target_name* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-valves"></a>Código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si *object_type* es **alertas**, el conjunto de resultados enumera todas las alertas de un operador determinado.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|Número de identificador de la alerta.|  
|**alert_name**|**sysname**|Nombre de la alerta.|  
|**use_email**|**int**|Se utiliza el correo electrónico para notificar al operador:<br /><br /> **1** = Sí<br /><br /> **0** = No|  
|**use_pager**|**int**|Se utiliza un buscapersonas para notificar al operador:<br /><br /> **1** = Sí<br /><br /> **0** = No|  
|**use_netsend**|**int**|Se utiliza un mensaje de red para notificar al operador:<br /><br /> **1** = Sí<br /><br /> **0** = No|  
|**has_email**|**int**|Número de notificaciones por correo electrónico enviadas para esta alerta.|  
|**has_pager**|**int**|Número de notificaciones por buscapersonas enviadas para esta alerta.|  
|**has_netsend**|**int**|Número de **mediante net send** notificaciones enviadas para esta alerta.|  
  
 Si **object_type** es **operadores**, el conjunto de resultados presenta todos los operadores de una alerta dada.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**operator_id**|**int**|Número de identificación del operador.|  
|**operator_name**|**sysname**|Nombre del operador.|  
|**use_email**|**int**|Para enviar la notificación al operador se utiliza el correo electrónico:<br /><br /> **1** = Sí<br /><br /> **0** = No|  
|**use_pager**|**int**|Para enviar la notificación al operador se utiliza un buscapersonas:<br /><br /> **1** = Sí<br /><br /> **0** = No|  
|**use_netsend**|**int**|Para enviar la notificación al operador se utiliza un mensaje de red:<br /><br /> **1** = Sí<br /><br /> **0** = No|  
|**has_email**|**int**|El operador tiene una dirección de correo electrónico:<br /><br /> **1** = Sí<br /><br /> **0** = No|  
|**has_pager**|**int**|El operador tiene una dirección de buscapersonas:<br /><br /> **1** = Sí<br /><br /> **0** = No|  
|**has_netsend**|**int**|El operador tiene configurada la notificación mediante net send.<br /><br /> **1** = Sí<br /><br /> **0** = No|  
  
## <a name="remarks"></a>Comentarios  
 Este procedimiento almacenado se debe ejecutar desde la **msdb** base de datos.  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar este procedimiento almacenado, un usuario debe ser miembro del rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-alerts-for-a-specific-operator"></a>A. Presentar las alertas de un operador específico  
 En el ejemplo siguiente se devuelven todas las alertas para las que el operador `François Ajenstat` recibe algún tipo de notificación.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_notification   
    @object_type = N'ALERTS',  
    @name = N'François Ajenstat',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
### <a name="b-listing-operators-for-a-specific-alert"></a>B. Presentar los operadores de una alerta específica  
 En el ejemplo siguiente se devuelven todos los operadores que reciben algún tipo de notificación de la alerta `Test Alert`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_notification  
    @object_type = N'OPERATORS',  
    @name = N'Test Alert',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_update_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
