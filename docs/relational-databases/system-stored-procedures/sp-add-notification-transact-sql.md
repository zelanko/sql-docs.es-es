---
title: sp_add_notification (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_notification_TSQL
- sp_add_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_notification
ms.assetid: 0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a79b98fb3f44f3c69e7b4108502a3e6ea14e5c09
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spaddnotification-transact-sql"></a>sp_add_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Establece una notificación para una alerta.  
  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_notification [ @alert_name = ] 'alert' ,   
    [ @operator_name = ] 'operator' ,   
    [ @notification_method = ] notification_method  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@alert_name=** ] **'***alerta***'**  
 Alerta de esta notificación. *alerta* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@operator_name=** ] **'***operador***'**  
 Operador al que se notificará cuando se produzca la alerta. *operador* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@notification_method=** ] *notification_method*  
 Método que se utilizará para notificar al operador. *notification_method* es **tinyint**, no tiene ningún valor predeterminado. *notification_method* puede tener uno o varios de estos valores, combinados con un **OR** operador lógico.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Correo electrónico|  
|**2**|Buscapersonas|  
|**4**|**net send**|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **sp_add_notification** se debe ejecutar desde la **msdb** base de datos.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] proporciona una sencilla forma gráfica de administrar todo el sistema de alertas. Se recomienda utilizar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para configurar la infraestructura de alertas.  
  
 Para enviar una notificación como respuesta a una alerta, primero debe configurar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el envío de correo.  
  
 Si se produce algún error al enviar un mensaje de correo electrónico o una notificación por buscapersonas, el error se comunica en el registro de errores de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_add_notification**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se agrega una notificación de correo electrónico para la alerta especificada (`Test Alert`).  
  
> **Nota:** en este ejemplo se da por supuesto que `Test Alert` ya existe y que `François Ajenstat` es un nombre de operador válido.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_notification  
 @alert_name = N'Test Alert',  
 @operator_name = N'François Ajenstat',  
 @notification_method = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_delete_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [sp_update_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
