---
title: sp_change_log_shipping_primary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_primary_database
- sp_change_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_primary_database
ms.assetid: 8c9dce6b-d2a3-4ca7-a832-8f59a5adb214
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 244811989bd5ab58a3ab1f6ffdfcf82649af1916
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045820"
---
# <a name="spchangelogshippingprimarydatabase-transact-sql"></a>sp_change_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la configuración de la base de datos principal.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_change_log_shipping_primary_database [ @database = ] 'database'  
[, [ @backup_directory = ] 'backup_directory']   
[, [ @backup_share = ] 'backup_share']   
[, [ @backup_retention_period = ] 'backup_retention_period']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] 'backup_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
[, [ @backup_compression = ] backup_compression_option ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @database = ] 'database'` Es el nombre de la base de datos en el servidor principal. *primary_database* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @backup_directory = ] 'backup_directory'` Es la ruta de acceso a la carpeta de copia de seguridad en el servidor principal. *directorio_de_copia_de_seguridad* es **nvarchar (500)** , no tiene ningún valor predeterminado, y no puede ser NULL.  
  
`[ @backup_share = ] 'backup_share'` Es la ruta de acceso de red en el directorio de copia de seguridad en el servidor principal. *backup_share* es **nvarchar (500)** , no tiene ningún valor predeterminado, y no puede ser NULL.  
  
`[ @backup_retention_period = ] 'backup_retention_period'` Es el período de tiempo, en minutos, que se retiene el archivo de copia de seguridad de registro en el directorio de copia de seguridad en el servidor principal. *backup_retention_period* es **int**, no tiene ningún valor predeterminado, y no puede ser NULL.  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` Modo de seguridad utilizado para conectarse al servidor de supervisión.  
  
 1 = Autenticación de Windows.  
  
 0 = Autenticación de SQL Server.  
  
 *monitor_server_security_mode* es **bit** y no puede ser NULL.  
  
`[ @monitor_server_login = ] 'monitor_server_login'` Es el nombre de usuario de la cuenta utilizada para tener acceso el servidor de supervisión.  
  
`[ @monitor_server_password = ] 'monitor_server_password'` Es la contraseña de la cuenta utilizada para tener acceso el servidor de supervisión.  
  
`[ @backup_threshold = ] 'backup_threshold'` Es el período de tiempo, en minutos, tras la última copia de seguridad antes de un *threshold_alert* se genera el error. *backup_threshold* es **int**, su valor predeterminado es de 60 minutos.  
  
`[ @threshold_alert = ] 'threshold_alert'` La alerta que se genera cuando se supera el umbral de copia de seguridad. *threshold_alert* es **int** y no puede ser NULL.  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` Especifica si se generará una alerta cuando *backup_threshold* se supera.  
  
 1 = habilitada  
  
 0 = deshabilitada  
  
 *threshold_alert_enabled* es **bit** y no puede ser NULL.  
  
`[ @history_retention_period = ] 'history_retention_period'` Es el período de tiempo en minutos en el que se retiene el historial. *history_retention_period* es **int**. Si no se especifica ningún valor, se utiliza 14420.  
  
`[ @backup_compression = ] backup_compression_option` Especifica si se usa una configuración de trasvase de registros [compresión de copia de seguridad](../../relational-databases/backup-restore/backup-compression-sql-server.md). Este parámetro solo se admite en [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (o una versión posterior).  
  
 0 = Deshabilitada. No se comprimen nunca las copias de seguridad de registros.  
  
 1 = Habilitada. Se comprimen siempre las copias de seguridad de registros.  
  
 2 = use el valor de la [ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md). Este es el valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **sp_change_log_shipping_primary_database** se debe ejecutar desde la **maestro** base de datos en el servidor principal. Este procedimiento almacenado hace lo siguiente:  
  
1.  Cambia la configuración de la **log_shipping_primary_database** registrar, si es necesario.  
  
2.  Cambia el registro local en **log_shipping_monitor_primary** en el servidor principal con los argumentos proporcionados, si es necesario.  
  
3.  Si el servidor de supervisión es diferente del servidor principal, cambia el registro de **log_shipping_monitor_primary** en el monitor de servidor con los argumentos proporcionados, si es necesario.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestra el uso de **sp_change_log_shipping_primary_database** para actualizar la configuración asociada a la base de datos principal [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC master.dbo.sp_change_log_shipping_primary_database   
 @database = N'AdventureWorks'   
, @backup_directory = N'c:\LogShipping'   
, @backup_share = N'\\tribeca\LogShipping'   
, @backup_retention_period = 1440   
, @backup_threshold = 60   
, @threshold_alert = 0   
, @threshold_alert_enabled = 1   
, @history_retention_period = 1440   
,@monitor_server_security_mode = 1  
,@backup_compression = 1;  
```  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [log_shipping_primary_databases &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)  
  
  
