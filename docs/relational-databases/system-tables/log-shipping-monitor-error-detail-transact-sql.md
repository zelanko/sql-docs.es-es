---
title: log_shipping_monitor_error_detail (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_error_detail_TSQL
- log_shipping_monitor_error_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_error_detail system table
ms.assetid: 0c38a625-60d2-4ee2-bcf3-2ba367914220
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5e441e5165262a4455e34cb9a0adb55b9679578f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67990055"
---
# <a name="log_shipping_monitor_error_detail-transact-sql"></a>log_shipping_monitor_error_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Almacena los detalles de errores de los trabajos de trasvase de registros. Esta tabla se almacena en la base de datos **msdb** .  
  
 Las tablas relacionadas con el historial y la supervisión también se utilizan en el servidor principal y los servidores secundarios.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|Id. principal de la copia de seguridad o Id. secundario de la copia o restauración.|  
|**agent_type**|**tinyint**|Es el tipo de trabajo de trasvase de registros.<br /><br /> 0 = Copia de seguridad.<br /><br /> 1 = Copia.<br /><br /> 2 = Restauración.|  
|**session_id**|**int**|Id. de sesión para el trabajo de copia de seguridad, copia o restauración.|  
|**database_name**|**sysname**|Nombre de la base de datos asociada a este registro de errores. Base de datos principal para copia de seguridad, base de datos secundaria para restauración o vacío para copia.|  
|**sequence_number**|**int**|Número incremental que indica el orden correcto de la información para los errores que ocupan varios registros.|  
|**log_time**|**datetime**|Fecha y hora en que se creó el registro.|  
|**log_time_utc**|**datetime**|Fecha y hora en que se creó el registro en hora universal coordinada.|  
|**Mensaje**|**nvarchar**|Texto del mensaje.|  
|**fuentes**|**nvarchar**|Origen del evento o mensaje de error.|  
|**help_url**|**nvarchar**|Dirección URL (si está disponible) donde se puede encontrar más información acerca del error.|  
  
## <a name="remarks"></a>Observaciones  
 Esta tabla contiene los detalles de los errores de los agentes de trasvase de registros. Cada error se registra como una secuencia de excepciones. Puede haber varios errores (secuencias) para cada sesión de agente.  
  
 Además de almacenarse en el servidor de supervisión remoto, la información relacionada con el servidor principal se almacena en el servidor principal en la tabla de **log_shipping_monitor_error_detail** , y la información relacionada con un servidor secundario también se almacena en el servidor secundario de la tabla **log_shipping_monitor_error_detail** .  
  
 Para identificar una sesión del agente, utilice las columnas **agent_id**, **agent_type**y **session_id**. Ordenar por **log_time** para ver los errores en el orden en que se registraron.  
  
## <a name="see-also"></a>Consulte también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_monitor_history_detail &#40;&#41;de Transact-SQL](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
