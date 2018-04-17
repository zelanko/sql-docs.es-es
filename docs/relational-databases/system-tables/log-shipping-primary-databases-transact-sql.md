---
title: log_shipping_primary_databases (Transact-SQL) | Documentos de Microsoft
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
- log_shipping_primary_databases
- log_shipping_primary_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_primary_databases system table
ms.assetid: 56888756-a798-42be-9b5e-0f9aa05a2cc6
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d3dfd38e9fa44dff09127c72e342223f3ae138c4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="logshippingprimarydatabases-transact-sql"></a>log_shipping_primary_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Almacena un registro para la base de datos principal en una configuración de trasvase de registros. Esta tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|Id. de la base de datos principal para la configuración del trasvase de registros.|  
|**primary_database**|**sysname**|Nombre de la base de datos principal en la configuración del trasvase de registros.|  
|**backup_directory**|**nvarchar(500)**|Directorio donde se almacenan los archivos de copia de seguridad de registros de transacciones del servidor principal.|  
|**backup_share**|**nvarchar(500)**|Ruta UNC o de red al directorio de copia de seguridad.|  
|**backup_retention_period**|**int**|Tiempo, en minutos, durante el que un archivo de copia de seguridad de registros se retiene en el directorio de copia de seguridad antes de eliminarse.|  
|**backup_job_id**|**uniqueidentifier**|El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Id. de trabajo de agente asociado con el trabajo de copia de seguridad en el servidor principal.|  
|**monitor_server**|**sysname**|El nombre de la instancia de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] está en uso como un servidor de supervisión en la configuración de trasvase de registros.|  
|**monitor_server_security_mode**|**bit**|Modo de seguridad utilizado para conectarse al servidor de supervisión.<br /><br /> 1 = Autenticación de Windows.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.|  
|**last_backup_file**|**nvarchar(500)**|Ruta de acceso absoluta de la copia de seguridad más reciente del registro de transacciones.|  
|**last_backup_date**|**datetime**|Fecha y hora de la última operación de copia de seguridad del registro.|  
|**user_specified_monitor**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **sp_help_log_shipping_primary_database** y **sp_help_log_shipping_secondary_primary** utilizar esta columna para controlar la visualización de la configuración del monitor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].<br /><br /> 0 = al invocar alguno de estos dos procedimientos almacenados, el usuario no especificó un valor explícito para la **@monitor_server** parámetro.<br /><br /> 1 = El usuario especificó un valor explícito.|  
|**backup_compression**|**tinyint**|Indica si la configuración de trasvase de registros invalida el comportamiento de compresión de copia de seguridad del nivel servidor.<br /><br /> 0 = Deshabilitada. Nunca se comprimen las copias de seguridad de registros, independientemente de la configuración de la compresión de copia de seguridad configurada por el servidor.<br /><br /> 1 = Habilitada. Las copias de seguridad de registros siempre se comprimen, independientemente de la configuración de la compresión de copia de seguridad configurada por el servidor.<br /><br /> 2 = usa la configuración del servidor para la [ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) opción de configuración del servidor. Es el valor predeterminado.<br /><br /> La compresión de copia de seguridad solo se admite en la edición Enterprise de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
