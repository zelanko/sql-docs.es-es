---
title: log_shipping_monitor_secondary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_secondary_TSQL
- log_shipping_monitor_secondary
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_secondary system table
ms.assetid: afbe1bb7-89a7-4020-9408-0af64a043c2e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b29942520092a39f218cf7673930682afe78f660
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62719346"
---
# <a name="logshippingmonitorsecondary-transact-sql"></a>log_shipping_monitor_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Almacena un registro de supervisión por cada base de datos secundaria en una configuración de trasvase de registros. Esta tabla se almacena en el **msdb** base de datos.  
  
 Las tablas relacionadas con el historial y la supervisión también se utilizan en el servidor principal y los servidores secundarios.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**secondary_server**|**sysname**|El nombre de la instancia secundaria de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] en la configuración de trasvase de registros.|  
|**secondary_database**|**sysname**|Nombre de la base de datos secundaria en la configuración del trasvase de registros.|  
|**secondary_id**|**uniqueidentifier**|Id. del servidor secundario en la configuración del trasvase de registros.|  
|**primary_server**|**sysname**|Nombre de la instancia principal del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] en la configuración del trasvase de registros.|  
|**primary_database**|**sysname**|Nombre de la base de datos principal en la configuración del trasvase de registros.|  
|**restore_threshold**|**int**|Número de minutos permitido entre las operaciones de restauración antes de que se genere una alerta.|  
|**threshold_alert**|**int**|Alerta que se generará cuando se sobrepase el umbral de restauración.|  
|**threshold_alert_enabled**|**bit**|Determina si las alertas de umbral de restauración están habilitadas. 1 = Habilitada.<br /><br /> 0 = Deshabilitada.|  
|**last_copied_file**|**nvarchar(500)**|Nombre del último archivo de copia de seguridad copiado en el servidor secundario.|  
|**last_copied_date**|**datetime**|Fecha y hora de la última operación de copia en el servidor secundario.|  
|**last_copied_date_utc**|**datetime**|Fecha y hora de la última operación de copia en el servidor secundario, expresadas en hora universal coordinada (UTC).|  
|**last_restored_file**|**nvarchar(500)**|Nombre del último archivo de copia de seguridad restaurado en la base de datos secundaria.|  
|**last_restored_date**|**datetime**|Fecha y hora de la última operación de restauración en la base de datos secundaria.|  
|**last_restored_date_utc**|**datetime**|Fecha y hora de la última operación de restauración en la base de datos secundaria, expresadas en hora universal coordinada (UTC).|  
|**last_restored_latency**|**int**|Período de tiempo, en minutos, transcurrido desde que se creó la copia de seguridad de registros en el servidor primario hasta que se restauró en el servidor secundario.<br /><br /> El valor inicial es NULL.|  
|**history_retention_period**|**int**|Cantidad de tiempo, en minutos, durante la que los registros de historial del trasvase de registros se mantienen en una base de datos secundaria determinada antes de ser eliminados.|  
  
## <a name="remarks"></a>Comentarios  
 Además de almacenarse en el servidor de supervisión remota y la información relacionada con un servidor secundario también se almacena en el servidor secundario en su **log_shipping_monitor_secondary** tabla.  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_add_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_change_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_monitor_secondary &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
