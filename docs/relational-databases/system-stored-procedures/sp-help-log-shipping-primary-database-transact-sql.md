---
title: sp_help_log_shipping_primary_database (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
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
- sp_help_log_shipping_primary_database_TSQL
- sp_help_log_shipping_primary_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_primary_database
ms.assetid: e711b01c-ef29-4eb6-a016-0e647e337818
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 257d4310d46f757ab2d34760b99a394bba933330
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelplogshippingprimarydatabase-transact-sql"></a>sp_help_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Recupera parámetros de la base de datos principal.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_log_shipping_primary_database  
[ @database = ] 'database' OR  
[ @primary_id = ] 'primary_id'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@database =** ] '*base de datos*'  
 Es el nombre de la base de datos principal de trasvase de registros. *base de datos* es **sysname**, no tiene ningún valor predeterminado, y no puede ser NULL.  
  
 [  **@primary_id =** ] '*primary_id*'  
 Id. de la base de datos principal para la configuración del trasvase de registros. *primary_id* es **uniqueidentifier** y no puede ser NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Description|  
|-----------------|-----------------|  
|**primary_id**|Id. de la base de datos principal para la configuración del trasvase de registros.|  
|**primary_database**|Nombre de la base de datos principal en la configuración del trasvase de registros.|  
|**backup_directory**|Directorio donde se almacenan los archivos de copia de seguridad de registros de transacciones del servidor principal.|  
|**backup_share**|Ruta UNC o de red al directorio de copia de seguridad.|  
|**backup_retention_period**|Tiempo, en minutos, durante el que un archivo de copia de seguridad de registros se retiene en el directorio de copia de seguridad antes de eliminarse.|  
|**backup_compression**|Indica si se utiliza la configuración de trasvase de registros [compresión de copia de seguridad](../../relational-databases/backup-restore/backup-compression-sql-server.md).<br /><br /> **0** = deshabilitado. No se comprimen nunca las copias de seguridad de registros.<br /><br /> **1** = habilitado. Se comprimen siempre las copias de seguridad de registros.<br /><br /> **2** = utilizar la configuración de la [ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md). Es el valor predeterminado.<br /><br /> La compresión de copia de seguridad solo se admite en [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (o una versión posterior). En otras ediciones, el valor es 2 siempre.|  
|**backup_job_id**|El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Id. de trabajo de agente asociado con el trabajo de copia de seguridad en el servidor principal.|  
|**monitor_server**|Nombre de la instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que se utiliza como servidor de supervisión en la configuración del trasvase de registros.|  
|**monitor_server_security_mode**|Modo de seguridad utilizado para conectarse al servidor de supervisión.<br /><br /> 1 = Autenticación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.|  
|**backup_threshold**|Número de minutos permitido entre las operaciones de copia de seguridad antes de que se genere una alerta.|  
|**threshold_alert**|Alerta que se generará cuando se sobrepase el umbral de copia de seguridad.|  
|**threshold_alert_enabled**|Determina si las alertas de umbral de copia de seguridad están habilitadas.<br /><br /> **1** = habilitado.<br /><br /> **0** = deshabilitado.|  
|**last_backup_file**|Ruta de acceso absoluta de la copia de seguridad más reciente del registro de transacciones.|  
|**last_backup_date**|Fecha y hora de la última operación de copia de seguridad del registro.|  
|**last_backup_date_utc**|Fecha y hora de la última operación de copia de seguridad del registro de transacciones en la base de datos principal, expresadas en UTC (hora universal coordinada).|  
|**history_retention_period**|Cantidad de tiempo, en minutos, durante la que los registros de historial del trasvase de registros se mantienen en una base de datos principal determinada antes de ser eliminados.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_log_shipping_primary_database** se debe ejecutar desde la **maestro** base de datos en el servidor principal.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestra cómo utilizar **sp_help_log_shipping_primary_database** para recuperar la configuración de la base de datos principal de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC master.dbo.sp_help_log_shipping_primary_database @database=N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
