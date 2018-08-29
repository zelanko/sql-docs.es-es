---
title: sp_help_log_shipping_monitor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_TSQL
- sp_help_log_shipping_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor
ms.assetid: a4e96c45-6dcd-471a-a494-b5c619459855
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e1f51b575ff8ee40db402fe48cacf8396b89ac45
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43027083"
---
# <a name="sphelplogshippingmonitor-transact-sql"></a>sp_help_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve un conjunto de resultados que contiene el estado y otra información de bases de datos primarias y secundarias registradas en un servidor primario, secundario o de supervisión.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_log_shipping_monitor  
```  
  
## <a name="arguments"></a>Argumentos  
 Ninguno.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**status**|**bit**|Estado colectivo de los agentes de la base de datos de trasvase de registros:<br /><br /> **0** = errores sin agente y en buen Estados.<br /><br /> **1** = lo contrario.|  
|**is_primary**|**bit**|Indica si esta fila es para una base de datos principal:: <br /><br /> **1** = la fila es para una base de datos principal.<br /><br /> **0** = la fila es para una base de datos secundaria.|  
|**servidor**|**sysname**|Nombre del servidor primario o secundario en el que reside esta base de datos.|  
|**database_name**|**sysname**|Nombre de la base de datos.|  
|**time_since_last_backup**|**int**|Período de tiempo, en minutos, transcurrido desde la última copia de seguridad de registros.<br /><br /> NULL = La información no está disponible o no es relevante.|  
|**last_backup_file**|**nvarchar(500)**|Nombre del último archivo de copia de seguridad de registros correcto.<br /><br /> NULL = La información no está disponible o no es relevante.|  
|**backup_threshold**|**int**|Período de tiempo, en minutos, que puede transcurrir después de la última copia de seguridad antes de que se genere un error threshold_alert. **backup_threshold** es **int**, su valor predeterminado es **60 minutos**.<br /><br /> NULL = La información no está disponible o no es relevante.<br /><br /> Este valor puede cambiarse mediante [sp_add_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md).|  
|**is_backup_alert_enabled**|**bit**|Especifica si va a una alerta se genera cuando **backup_threshold** se supera. El valor de uno (**1**), el valor predeterminado, significa que se generará la alerta.<br /><br /> NULL = La información no está disponible o no es relevante.<br /><br /> Este valor puede cambiarse mediante [sp_add_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md).|  
|**time_since_last_copy**|**int**|Período de tiempo, en minutos, transcurrido desde que se copió la última copia de seguridad de registros.<br /><br /> NULL = La información no está disponible o no es relevante.|  
|**last_copied_file**|**nvarchar(500)**|Nombre del último archivo de copia de seguridad de registros que se copió correctamente.<br /><br /> NULL = La información no está disponible o no es relevante.|  
|**time_since_last_restore**|**int**|Período de tiempo, en minutos, transcurrido desde que se restauró la última copia de seguridad de registros.<br /><br /> NULL = La información no está disponible o no es relevante.|  
|**last_restored_file**|**nvarchar (500).**|Nombre del último archivo de copia de seguridad de registros que se restauró correctamente.<br /><br /> NULL = La información no está disponible o no es relevante.|  
|**last_restored_latency**|**int**|Período de tiempo, en minutos, transcurrido desde que se creó la última copia de seguridad hasta que se restauró.<br /><br /> NULL = La información no está disponible o no es relevante.|  
|**restore_threshold**|**int**|Número de minutos permitido entre las operaciones de restauración antes de que se genere una alerta. **restore_threshold** no puede ser NULL.|  
|**is_restore_alert_enabled**|**bit**|Especifica si se generará una alerta cuando **restore_threshold** se supera. El valor de uno (**1**), el valor predeterminado, significa que se generará la alerta.<br /><br /> NULL = La información no está disponible o no es relevante.<br /><br /> Para establecer el umbral de restauración, utilice [sp_add_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md).|  
  
## <a name="remarks"></a>Notas  
 **sp_help_log_shipping_monitor** se debe ejecutar desde la **maestro** base de datos del servidor de supervisión.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
