---
title: sp_update_notification (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_notification_TSQL
- sp_update_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatenotification
ms.assetid: 3e1c3d40-8c24-46ce-a68e-ce6c6a237fda
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7282472dcb916d7122625534cb64f80ce9f4ea6a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827494"
---
# <a name="sp_update_notification-transact-sql"></a>sp_update_notification (Transact-SQL)
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
`[ @alert_name = ] 'alert'`El nombre de la alerta asociada a esta notificación. la *alerta* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @operator_name = ] 'operator'`Operador al que se notificará cuando se produzca la alerta. *Operator* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @notification_method = ] notification`Método por el que se notifica al operador. la *notificación*es de **tinyint**, no tiene ningún valor predeterminado y puede tener uno o varios de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Correo electrónico|  
|**2**|Buscapersonas|  
|**4**|**net send**|  
|**7**|Todos los métodos|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_update_notification** se debe ejecutar desde la base de datos **msdb** .  
  
 Puede actualizar una notificación para un operador que no tenga la información de dirección necesaria mediante el *notification_method*especificado. Si se produce algún error al enviar un mensaje de correo electrónico o una notificación por buscapersonas, el error se refleja en el registro de errores del Agente SQL Server.  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar este procedimiento almacenado, se debe conceder a los usuarios el rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se modifica el método de notificación para las notificaciones enviadas a `François Ajenstat` para la alerta `Test Alert` .  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_notification  
   @alert_name = N'Test Alert',  
   @operator_name = N'François Ajenstat',  
   @notification_method = 7;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_add_notification &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
