---
title: Tablas y procedimientos almacenados de trasvase de registros | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- secondary servers [SQL Server]
- monitor servers [SQL Server]
- log shipping [SQL Server], system tables
- log shipping [SQL Server], stored procedures
- primary servers [SQL Server]
ms.assetid: 03420810-4c38-4c0c-adf0-913eb044c50a
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ea92eb3a991a21232bf2df110a04bb5bb25baeab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103600"
---
# <a name="log-shipping-tables-and-stored-procedures"></a>Log Shipping Tables and Stored Procedures
  En este tema se describen todas las tablas y los procedimientos almacenados asociados con una configuración de trasvase de registros. Todas las tablas de trasvase de registros se almacenan en **msdb** en cada servidor. En las tablas siguientes se describe qué tablas y procedimientos almacenados se utilizan en qué servidores en una configuración de trasvase de registros.  
  
## <a name="primary-server-tables"></a>Tablas de servidor principal  
  
|Table|Descripción|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|Almacena el Id. del trabajo de alerta. Esta tabla solo se usa en el servidor principal si no se ha configurado ningún servidor de supervisión remoto.|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|Almacena los detalles de error de los trabajos de trasvase de registros asociados con este servidor principal.|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|Almacena los detalles de historial de los trabajos de trasvase de registros asociados con este servidor principal.|  
|[log_shipping_monitor_primary](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)|Almacena un registro de monitor para esta base de datos principal.|  
|[log_shipping_primary_databases](/sql/relational-databases/system-tables/log-shipping-primary-databases-transact-sql)|Incluye información de configuración de las bases de datos principales de un servidor determinado. Incluye una fila por base de datos principal.|  
|[log_shipping_primary_secondaries](/sql/relational-databases/system-tables/log-shipping-primary-secondaries-transact-sql)|Asigna bases de datos principales a las secundarias.|  
  
## <a name="primary-server-stored-procedures"></a>Procedimientos almacenados del servidor principal  
  
|Procedimiento almacenado|Descripción|  
|----------------------|-----------------|  
|[sp_add_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql)|Configura la base de datos principal de una configuración de trasvase de registros, incluido el trabajo de copia de seguridad, el registro de monitor local y el registro de monitor remoto.|  
|[sp_add_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql)|Agrega un nombre de base de datos secundaria a una base de datos principal existente.|  
|[sp_change_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql)|Cambia la configuración de la base de datos principal incluidos los registros de monitor local y remoto.|  
|[sp_cleanup_log_shipping_history](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql)|Limpia el historial localmente y en el monitor basándose en el período de retención.|  
|[sp_delete_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql)|Quita el trasvase de registros de la base de datos principal, incluido el trabajo de copia de seguridad así como el historial local y remoto.|  
|[sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql)|Quita el nombre de una base de datos secundaria de una principal.|  
|[sp_help_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql)|Recupera la configuración de la base de datos principal y muestra los valores de las tablas **log_shipping_primary_databases** y **log_shipping_monitor_primary** .|  
|[sp_help_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql)|Recupera nombres de las bases de datos secundarias para una base de datos principal.|  
|[sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql)|Actualiza el monitor con la información más reciente del agente de trasvase de registros especificado.|  
  
## <a name="secondary-server-tables"></a>Tablas de servidor secundario  
  
|Table|Descripción|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|Almacena el Id. del trabajo de alerta. Esta tabla solo se usa en el servidor secundario si no se ha configurado ningún servidor de supervisión remoto.|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|Almacena los detalles de error de los trabajos de trasvase de registros asociados con este servidor secundario.|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|Almacena los detalles de historial de los trabajos de trasvase de registros asociados con este servidor secundario.|  
|[log_shipping_monitor_secondary](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)|Almacena un registro de monitor por cada base de datos secundaria asociada con este servidor secundario.|  
|[log_shipping_secondary](/sql/relational-databases/system-tables/log-shipping-secondary-transact-sql)|Incluye información de configuración de las bases de datos secundarias de un servidor determinado. Incluye una fila por Id. secundario.|  
|[log_shipping_secondary_databases](/sql/relational-databases/system-tables/log-shipping-secondary-databases-transact-sql)|Almacena información de configuración de una base de datos secundaria determinada. Incluye una fila por base de datos secundaria.|  
  
> [!NOTE]  
>  Las bases de datos secundarias del mismo servidor secundario de una base de datos principal comparten la configuración de la tabla **log_shipping_secondary** . Si se modifica un valor compartido de una base de datos secundaria, se modificará para todas ellas.  
  
## <a name="secondary-server-stored-procedures"></a>Procedimientos almacenados del servidor secundario  
  
|Procedimiento almacenado|Descripción|  
|----------------------|-----------------|  
|[sp_add_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql)|Configura una base de datos secundaria para el trasvase de registros.|  
|[sp_add_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-primary-transact-sql)|Configura información principal, agrega vínculos al monitor local y remoto y crea trabajos de copia y restauración en el servidor secundario de la base de datos principal especificada.|  
|[sp_change_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql)|Cambia la configuración de la base de datos secundaria incluidos los registros de monitor local y remoto.|  
|[sp_change_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-primary-transact-sql)|Cambia la configuración de la base de datos secundaria como el directorio de origen y destino o el período de retención de los archivos.|  
|[sp_cleanup_log_shipping_history](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql)|Limpia el historial localmente y en el monitor basándose en el período de retención.|  
|[sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql)|Quita una base de datos secundaria y los historiales local y remoto.|  
|[sp_delete_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-primary-transact-sql)|Quita la información acerca del servidor principal especificado del servidor secundario.|  
|[sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql)|Recupera la configuración de la base de datos secundaria de las tablas **log_shipping_secondary**, **log_shipping_secondary_databases**y **log_shipping_monitor_secondary** .|  
|[sp_help_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql)|Este procedimiento almacenado recupera la configuración de una base de datos principal determinada en el servidor secundario.|  
|[sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql)|Actualiza el monitor con la información más reciente del agente de trasvase de registros especificado.|  
  
## <a name="monitor-server-tables"></a>Tablas de servidor de supervisión  
  
|Table|Descripción|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|Almacena el Id. del trabajo de alerta.|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|Almacena los detalles de errores de los trabajos de trasvase de registros.|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|Almacena los detalles de historial de los trabajos de trasvase de registros.|  
|[log_shipping_monitor_primary](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)|Almacena un registro de monitor por cada base de datos principal asociada con este servidor de supervisión.|  
|[log_shipping_monitor_secondary](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)|Almacena un registro de monitor por cada base de datos secundaria asociada con este servidor de supervisión.|  
  
## <a name="monitor-server-stored-procedures"></a>Procedimientos almacenados del servidor de supervisión  
  
|Procedimiento almacenado|Descripción|  
|----------------------|-----------------|  
|[sp_add_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-alert-job-transact-sql)|Crea un trabajo de alerta de trasvase de registros si aún no se ha creado ninguno.|  
|[sp_delete_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql)|Quita un trabajo de alerta de trasvase de registros si no hay ninguna base de datos principal asociada.|  
|[sp_help_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-alert-job-transact-sql)|Devuelve el Id. del trabajo de alerta.|  
|[sp_help_log_shipping_monitor_primary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql)|Devuelve registros de supervisión para la base de datos principal especificada desde la tabla **log_shipping_monitor_primary** .|  
|[sp_help_log_shipping_monitor_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql)|Devuelve registros de supervisión para la base de datos secundaria especificada desde la tabla **log_shipping_monitor_secondary** .|  
  
  
