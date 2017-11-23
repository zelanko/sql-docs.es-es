---
title: sp_update_notification (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_update_notification_TSQL
- sp_update_notification
dev_langs: TSQL
helpviewer_keywords: sp_updatenotification
ms.assetid: 3e1c3d40-8c24-46ce-a68e-ce6c6a237fda
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 44b2755dca0a8d3cd2dae7d11e12cc16a708fe1e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spupdatenotification-transact-sql"></a>sp_update_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Actualiza el método de notificación de una notificación de alerta.  

  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_update_notification  
          [@alert_name =] 'alert' ,  
     [@operator_name =] 'operator' ,  
     [@notification_method =] notification  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@alert_name =**] **'***alerta***'**  
 Nombre de la alerta asociada a esta notificación. *alerta* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@operator_name =**] **'***operador***'**  
 Operador que notificará el momento de producirse la alerta. *operador* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@notification_method =**] *notificación*  
 Método que se utilizará para notificar al operador. *notificación*es **tinyint**, no tiene ningún valor predeterminado y puede tener uno o varios de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Correo electrónico|  
|**2**|Buscapersonas|  
|**4**|**net send**|  
|**7**|Todos los métodos|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_update_notification** se debe ejecutar desde la **msdb** base de datos.  
  
 Puede actualizar una notificación para un operador que no tiene la información de dirección necesaria mediante especificado *notification_method*. Si se produce algún error al enviar un mensaje de correo electrónico o una notificación por buscapersonas, el error se refleja en el registro de errores del Agente SQL Server.  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar este procedimiento almacenado, deben concederse a los usuarios la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se modifica el método de notificación para las notificaciones enviadas a `François Ajenstat`de la alerta `Test Alert`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_notification  
   @alert_name = N'Test Alert',  
   @operator_name = N'François Ajenstat',  
   @notification_method = 7;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_notification &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
