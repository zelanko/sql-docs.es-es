---
title: log_shipping_monitor_error_detail (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_error_detail_TSQL
- log_shipping_monitor_error_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_error_detail system table
ms.assetid: 0c38a625-60d2-4ee2-bcf3-2ba367914220
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff9a5a08e0b74a4cba9582b49b5224a801209130
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="logshippingmonitorerrordetail-transact-sql"></a>log_shipping_monitor_error_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Almacena los detalles de errores de los trabajos de trasvase de registros. Esta tabla se almacena en la **msdb** base de datos.  
  
 Las tablas relacionadas con el historial y la supervisión también se utilizan en el servidor principal y los servidores secundarios.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|Id. principal de la copia de seguridad o Id. secundario de la copia o restauración.|  
|**agent_type**|**tinyint**|Es el tipo de trabajo de trasvase de registros.<br /><br /> 0 = Copia de seguridad.<br /><br /> 1 = Copia.<br /><br /> 2 = Restauración.|  
|**session_id**|**int**|Id. de sesión para el trabajo de copia de seguridad, copia o restauración.|  
|**database_name**|**sysname**|Nombre de la base de datos asociada a este registro de errores. Base de datos principal para copia de seguridad, base de datos secundaria para restauración o vacío para copia.|  
|**sequence_number**|**int**|Número incremental que indica el orden correcto de la información para los errores que ocupan varios registros.|  
|**log_time**|**datetime**|Fecha y hora en que se creó el registro.|  
|**log_time_utc**|**datetime**|Fecha y hora en que se creó el registro en hora universal coordinada.|  
|**message**|**nvarchar**|Texto del mensaje.|  
|**origen**|**nvarchar**|Origen del evento o mensaje de error.|  
|**help_url**|**nvarchar**|Dirección URL (si está disponible) donde se puede encontrar más información acerca del error.|  
  
## <a name="remarks"></a>Comentarios  
 Esta tabla contiene los detalles de los errores de los agentes de trasvase de registros. Cada error se registra como una secuencia de excepciones. Puede haber varios errores (secuencias) para cada sesión de agente.  
  
 Además de almacenarse en el servidor de supervisión remota, la información relacionada con el servidor principal se almacena en el servidor principal en su **log_shipping_monitor_error_detail** tabla e información relacionada con un servidor secundario También se almacena en el servidor secundario en su **log_shipping_monitor_error_detail** tabla.  
  
 Para identificar una sesión de agente, use columnas **agent_id**, **agent_type**, y **session_id**. Ordenar por **log_time** para ver los errores en el orden en el que se registraron.  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_monitor_history_detail &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
