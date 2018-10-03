---
title: log_shipping_monitor_history_detail (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_history_detail_TSQL
- log_shipping_monitor_history_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_history_detail system table
ms.assetid: 7080c888-323b-4206-a1ab-e6c51f9e2579
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f8968661442adabe4c04608ca5a5bb5362341c4b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804113"
---
# <a name="logshippingmonitorhistorydetail-transact-sql"></a>log_shipping_monitor_history_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Almacena los detalles del historial para los trabajos de trasvase de registros. Esta tabla se almacena en el **msdb** base de datos.  
  
 Las tablas relacionadas con el historial y la supervisión también se utilizan en el servidor principal y los servidores secundarios.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**valor de agent_id**|**uniqueidentifier**|Id. principal de la copia de seguridad o Id. secundario de la copia o restauración.|  
|**agent_type**|**tinyint**|Es el tipo de trabajo de trasvase de registros.<br /><br /> 0 = Copia de seguridad.<br /><br /> 1 = Copia.<br /><br /> 2 = Restauración.|  
|**session_id**|**int**|Id. de sesión para el trabajo de copia de seguridad, copia o restauración.|  
|**database_name**|**sysname**|Nombre de la base de datos asociada a este registro. Base de datos principal para copia de seguridad, base de datos secundaria para restauración o vacío para copia.|  
|**session_status**|**tinyint**|Estado de la sesión.<br /><br /> 0 = Iniciada.<br /><br /> 1 = En ejecución.<br /><br /> 2 = Correcta.<br /><br /> 3 = Error.<br /><br /> 4 = Advertencia.|  
|**log_time**|**datetime**|Fecha y hora en que se creó el registro.|  
|**log_time_utc**|**datetime**|Fecha y hora en que se creó el registro en hora universal coordinada.|  
|**message**|**nvarchar(max)**|Texto del mensaje.|  
  
## <a name="remarks"></a>Comentarios  
 Esta tabla contiene los detalles del historial para los agentes de trasvase de registros. Para identificar una sesión de agente, use columnas **agent_id**, **agent_type**, y **session_id**. Para ver los detalles del historial de la sesión del agente, ordene por **log_time**.  
  
 Además de almacenarse en el servidor de supervisión remota, la información relacionada con el servidor principal se almacena en el servidor principal en su **log_shipping_monitor_history_detail** tabla e información relacionada con una base de datos secundaria servidor también se almacena en el servidor secundario en su **log_shipping_monitor_history_detail** tabla.  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [Las tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [log_shipping_monitor_error_detail &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)  
  
  
