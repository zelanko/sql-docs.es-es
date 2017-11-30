---
title: sp_change_log_shipping_secondary_primary (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_primary
- sp_change_log_shipping_secondary_primary_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_change_log_shipping_secondary_primary
ms.assetid: 5bcb4df7-6df3-4f2b-9207-b97b5addf2a6
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3971444d93a2cb9c57ecce4a278410135a9aaf32
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
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
 [  **@primary_server**  =] '*primary_server*'  
 El nombre de la instancia principal de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] en la configuración de trasvase de registros. *primary_server* es **sysname** y no puede ser NULL.  
  
 [  **@primary_database**  =] '*primary_database*'  
 Es el nombre de la base de datos en el servidor principal. *primary_database* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@backup_source_directory**  =] '*backup_source_directory*'  
 Directorio donde se almacenan los archivos de copia de seguridad de registros de transacciones del servidor principal. *backup_source_directory* es **nvarchar (500)** y no puede ser NULL.  
  
 [  **@backup_destination_directory**  =] '*backup_destination_directory*'  
 Directorio del servidor secundario donde se copian los archivos de copia de seguridad. *backup_destination_directory* es **nvarchar (500)** y no puede ser NULL.  
  
 [  **@file_retention_period**  =] '*file_retention_period*'  
 Es la cantidad de tiempo en minutos durante la que se retendrá el historial. *history_retention_period* es **int**, su valor predeterminado es null. Si no se especifica ninguno, se usará un valor de 14420.  
  
 [  **@monitor_server_security_mode**  =] '*monitor_server_security_mode*'  
 Modo de seguridad utilizado para conectarse al servidor de supervisión.  
  
 1 = Autenticación de Windows;  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. *monitor_server_security_mode* es **bits** y no puede ser NULL.  
  
 [  **@monitor_server_login**  =] '*monitor_server_login*'  
 Es el nombre de usuario de la cuenta utilizada para tener acceso al servidor de supervisión.  
  
 [  **@monitor_server_password**  =] '*monitor_server_password*'  
 Es la contraseña de la cuenta utilizada para tener acceso al servidor de supervisión.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Comentarios  
 **sp_change_log_shipping_secondary_primary** se debe ejecutar desde la **maestro** base de datos en el servidor secundario. Este procedimiento almacenado hace lo siguiente:  
  
1.  Cambia la configuración de la **log_shipping_secondary** registra según sea necesario.  
  
2.  Si el servidor de supervisión es diferente del servidor secundario, cambios de registro de supervisión de **log_shipping_monitor_secondary** en el monitor de servidor con los argumentos proporcionados, si es necesario.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar este procedimiento.  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
