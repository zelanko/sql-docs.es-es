---
title: sp_help_log_shipping_secondary_database (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_secondary_database
- sp_help_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_secondary_database
ms.assetid: 11ce42ca-d3f1-44c8-9cac-214ca8896b9a
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e2a943234d835d1f78cf57c096fd8492849bfa0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259605"
---
# <a name="sphelplogshippingsecondarydatabase-transact-sql"></a>sp_help_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este procedimiento almacenado recupera la configuración de una o más bases de datos secundarias.  
  

  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database' OR  
[ @secondary_id = ] 'secondary_id'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@secondary_database =** ] '*secondary_database*'  
 Es el nombre de la base de datos secundaria. *secondary_database* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@secondary_id =** ] '*secondary_id*'  
 Id. del servidor secundario en la configuración del trasvase de registros. *secondary_id* es **uniqueidentifier** y no puede ser NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Description|  
|-----------------|-----------------|  
|**secondary_id**|Id. del servidor secundario en la configuración del trasvase de registros.|  
|**primary_server**|El nombre de la instancia principal de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] en la configuración de trasvase de registros.|  
|**primary_database**|Nombre de la base de datos principal en la configuración del trasvase de registros.|  
|**backup_source_directory**|Directorio donde se almacenan los archivos de copia de seguridad de registros de transacciones del servidor principal.|  
|**backup_destination_directory**|Directorio del servidor secundario donde se copian los archivos de copia de seguridad.|  
|**file_retention_period**|Tiempo, en minutos, durante el que un archivo de copia de seguridad se retiene en el servidor secundario antes de eliminarse.|  
|**copy_job_id**|Id. asociado al trabajo de copia en el servidor secundario.|  
|**restore_job_id**|Id. asociado al trabajo de restauración en el servidor secundario.|  
|**monitor_server**|Nombre de la instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que se utiliza como servidor de supervisión en la configuración del trasvase de registros.|  
|**monitor_server_security_mode**|Modo de seguridad utilizado para conectarse al servidor de supervisión.<br /><br /> 1 = Autenticación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.|  
|**secondary_database**|Nombre de la base de datos secundaria en la configuración del trasvase de registros.|  
|**restore_delay**|Cantidad de tiempo, en minutos, que espera el servidor secundario antes de restaurar un archivo de copia de seguridad dado. El valor predeterminado es 0 minutos.|  
|**restore_all**|Si se establece en 1, el servidor secundario restaura todas las copias de seguridad disponibles del registro de transacciones cuando se ejecuta el trabajo de restauración. De lo contrario, se detiene tras haber restaurado un archivo.|  
|**restore_mode**|Modo de restauración para la base de datos secundaria.<br /><br /> 0 = Restaurar registro con NORECOVERY.<br /><br /> 1 = Restaurar registro con STANDBY.|  
|**disconnect_users**|Si se establece en 1, los usuarios están desconectados de la base de datos secundaria cuando se realiza una operación de restauración. Valor predeterminado = 0.|  
|**block_size**|Tamaño, en bytes, que se utiliza como tamaño de bloque para el dispositivo de copia de seguridad.|  
|**buffer_count**|Número total de búferes utilizados por la operación de copia de seguridad o restauración.|  
|**max_transfer_size**|Tamaño, en bytes, de la solicitud de entrada o salida máxima emitida por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al dispositivo de copia de seguridad.|  
|**restore_threshold**|Número de minutos permitido entre las operaciones de restauración antes de que se genere una alerta.|  
|**threshold_alert**|Alerta que se generará cuando se sobrepase el umbral de restauración.|  
|**threshold_alert_enabled**|Determina si las alertas de umbral de restauración están habilitadas.<br /><br /> 1 = Habilitada.<br /><br /> 0 = Deshabilitada.|  
|**last_copied_file**|Nombre del último archivo de copia de seguridad copiado en el servidor secundario.|  
|**last_copied_date**|Fecha y hora de la última operación de copia en el servidor secundario.|  
|**last_copied_date_utc**|Fecha y hora de la última operación de copia en el servidor secundario, expresadas en hora universal coordinada (UTC).|  
|**last_restored_file**|Nombre del último archivo de copia de seguridad restaurado en la base de datos secundaria.|  
|**last_restored_date**|Fecha y hora de la última operación de restauración en la base de datos secundaria.|  
|**last_restored_date_utc**|Fecha y hora de la última operación de restauración en la base de datos secundaria, expresadas en hora universal coordinada (UTC).|  
|**history_retention_period**|Cantidad de tiempo, en minutos, durante la que los registros de historial del trasvase de registros se mantienen en una base de datos secundaria determinada antes de ser eliminados.|  
|**last_restored_latency**|Período de tiempo, en minutos, transcurrido desde que se creó la copia de seguridad de registros en el servidor primario hasta que se restauró en el servidor secundario.<br /><br /> El valor inicial es NULL.|  
  
## <a name="remarks"></a>Comentarios  
 Si incluye el *secondary_database* parámetro, el conjunto de resultados contendrá información acerca de la base de datos secundaria; si incluye el *secondary_id* parámetro, que contendrá el conjunto de resultados obtener información sobre todas las bases de datos secundarias asociadas con ese Id. secundario.  
  
 **sp_help_log_shipping_secondary_database** se debe ejecutar desde la **maestro** base de datos en el servidor secundario.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar este procedimiento.  
  
## <a name="see-also"></a>Vea también  
 [sp_help_log_shipping_secondary_primary &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql.md)   
 [Acerca del trasvase de registros & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
