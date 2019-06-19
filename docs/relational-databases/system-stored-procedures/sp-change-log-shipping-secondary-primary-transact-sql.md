---
title: sp_change_log_shipping_secondary_primary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_primary
- sp_change_log_shipping_secondary_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_primary
ms.assetid: 5bcb4df7-6df3-4f2b-9207-b97b5addf2a6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a84ed0105558772752f4d9871ad28a5bffde6bec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62997132"
---
# <a name="spchangelogshippingsecondaryprimary-transact-sql"></a>sp_change_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la configuración de la base de datos secundaria.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_change_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server',  
[ @primary_database = ] 'primary_database',  
[, [ @backup_source_directory = ] 'backup_source_directory']  
[, [ @backup_destination_directory = ] 'backup_destination_directory']  
[, [ @file_retention_period = ] file_retention_period]  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @primary_server = ] 'primary_server'` El nombre de la instancia principal de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] en la configuración de trasvase de registros. *primary_server* es **sysname** y no puede ser NULL.  
  
`[ @primary_database = ] 'primary_database'` Es el nombre de la base de datos en el servidor principal. *primary_database* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @backup_source_directory = ] 'backup_source_directory'` El directorio donde se almacenan los archivos de copia de seguridad del registro de transacciones desde el servidor principal. *backup_source_directory* es **nvarchar (500)** y no puede ser NULL.  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'` El directorio en el servidor secundario que se copiarán los archivos de copia de seguridad. *backup_destination_directory* es **nvarchar (500)** y no puede ser NULL.  
  
`[ @file_retention_period = ] 'file_retention_period'` Es el período de tiempo en minutos en el que se retendrá el historial. *history_retention_period* es **int**, su valor predeterminado es null. Si se especifica ninguno, se usará un valor de 14420.  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` Modo de seguridad utilizado para conectarse al servidor de supervisión.  
  
 1 = Autenticación de Windows;  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. *monitor_server_security_mode* es **bit** y no puede ser NULL.  
  
`[ @monitor_server_login = ] 'monitor_server_login'` Es el nombre de usuario de la cuenta utilizada para tener acceso el servidor de supervisión.  
  
`[ @monitor_server_password = ] 'monitor_server_password'` Es la contraseña de la cuenta utilizada para tener acceso el servidor de supervisión.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **sp_change_log_shipping_secondary_primary** se debe ejecutar desde la **maestro** base de datos en el servidor secundario. Este procedimiento almacenado hace lo siguiente:  
  
1.  Cambia la configuración de la **log_shipping_secondary** registra según sea necesario.  
  
2.  Si el servidor de supervisión es diferente del servidor secundario, los cambios de registro de supervisión de **log_shipping_monitor_secondary** en el monitor de servidor con los argumentos proporcionados, si es necesario.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar este procedimiento.  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
