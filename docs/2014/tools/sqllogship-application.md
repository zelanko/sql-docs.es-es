---
title: Aplicación sqllogship | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqllogship
ms.assetid: 8ae70041-f3d9-46e4-8fa8-31088572a9f8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 14b9cda05bca998bd113a316692c4c2c2111d091
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2019
ms.locfileid: "63035084"
---
# <a name="sqllogship-application"></a>sqllogship (aplicación)
  La aplicación **sqllogship** realiza una operación de copia de seguridad, copia o restauración y las tareas de limpieza asociadas en una configuración de trasvase de registros. La operación se realiza en una instancia específica de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para una base de datos determinada.  
  
 ![Icono de vínculo de tema](../../2014/database-engine/media/topic-link.gif "Icono de vínculo de tema") Para obtener las convenciones de sintaxis, vea [referencia &#40;de la&#41;utilidad de símbolo del sistema motor de base de datos](../tools/command-prompt-utility-reference-database-engine.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqllogship  
-server  
instance_name { -backupprimary_id | -copysecondary_id | -restoresecondary_id } [ -verboselevellevel ] [ -logintimeouttimeout_value ] [ -querytimeouttimeout_value ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-server** _instance_name_  
 Especifica la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] donde se ejecutará la operación. La instancia del servidor que se va a especificar depende de la operación de trasvase de registros indicada. Para **-backup**, *instance_name* debe ser el nombre del servidor principal en una configuración de trasvase de registros. Para **-copy** o **-restore**, *instance_name* debe ser el nombre de un servidor secundario en una configuración de trasvase de registros.  
  
 **-backup** _primary_id_  
 Realiza una operación de copia de seguridad de la base de datos principal cuyo identificador principal se especifica en *primary_id*. Para obtener este identificador, selecciónelo en la tabla del sistema [log_shipping_primary_databases](/sql/relational-databases/system-tables/log-shipping-primary-databases-transact-sql) o use el procedimiento almacenado [sp_help_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql) .  
  
 La operación de copia de seguridad crea la copia de seguridad del registro en el directorio de copia de seguridad. A continuación, la aplicación **sqllogship** limpia los archivos de copia de seguridad antiguos, basándose en el período de retención de archivos. Más tarde, la aplicación registra el historial de la operación de copia de seguridad en el servidor principal y en el servidor de supervisión. Por último, la aplicación ejecuta [sp_cleanup_log_shipping_history](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql), que limpia la información del historial antigua, basándose en el período de retención.  
  
 **-copy** _secondary_id_  
 Realiza una operación de copia para copiar copias de seguridad desde el servidor secundario especificado de la base de datos o bases de datos secundarias cuyo identificador secundario se indica en *secondary_id*. Para obtener este identificador, selecciónelo en la tabla del sistema [log_shipping_secondary](/sql/relational-databases/system-tables/log-shipping-secondary-transact-sql) o use el procedimiento almacenado [sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql) .  
  
 La operación copia los archivos de copia de seguridad desde el directorio de copia de seguridad al directorio de destino. A continuación, la aplicación **sqllogship** registra el historial de la operación de copia en el servidor secundario y en el servidor de supervisión.  
  
 **-restore** _secondary_id_  
 Realiza una operación de restauración en el servidor secundario especificado de la base de datos o bases de datos secundarias cuyo identificador secundario se indica en *secondary_id*. Para obtener este identificador, use el procedimiento almacenado **sp_help_log_shipping_secondary_database** .  
  
 Los archivos de copia de seguridad del directorio de destino creados después del punto de restauración más reciente se restauran en la base de datos o bases de datos secundarias. A continuación, la aplicación **sqllogship** limpia los archivos de copia de seguridad antiguos, basándose en el período de retención de archivos. Más tarde, la aplicación registra el historial de la operación de restauración en el servidor secundario y en el servidor de supervisión. Por último, la aplicación ejecuta **sp_cleanup_log_shipping_history**, que limpia la información del historial antigua, basándose en el período de retención.  
  
 **-verboselevel** _level_  
 Especifica el nivel de mensajes agregados al historial de trasvase de registros. *level* es uno de los siguientes enteros:  
  
|level|Descripción|  
|-----------|-----------------|  
|0|No se obtienen mensajes de depuración ni de seguimiento.|  
|1|Se obtienen mensajes de control de errores.|  
|2|Se obtienen mensajes de control de errores y advertencias.|  
|**3**|Se obtienen mensajes de control de errores, advertencias e informativos. Este es el valor predeterminado.|  
|4|Se obtienen todos los mensajes de depuración y traza.|  
  
 **-logintimeout** _timeout_value_  
 Especifica la cantidad de tiempo asignado al intento de iniciar sesión en la instancia del servidor antes de que se agote el tiempo de espera del intento. El valor predeterminado es 15 segundos. *timeout_value* es de tipo **int** _._  
  
 **-querytimeout** _timeout_value_  
 Especifica la cantidad de tiempo asignado para iniciar la operación especificada antes de que se agote el tiempo de espera. El valor predeterminado es sin tiempo de espera. *timeout_value* es de tipo **int** _._  
  
## <a name="remarks"></a>Comentarios  
 Se recomienda que use los trabajos de copia de seguridad, copia y restauración para realizar la copia de seguridad, copia y restauración cuando sea posible. Para iniciar estos trabajos desde una operación por lotes u otra aplicación, llame al procedimiento almacenado [sp_start_job](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql) .  
  
 El historial de trasvase de registros creado por **sqllogship** se combina con el historial creado por los trabajos de copia de seguridad, copia y restauración de trasvase de registros. Si tiene previsto usar **sqllogship** repetidamente para realizar operaciones de copia de seguridad, copia y restauración para una configuración de trasvase de registros, considere la posibilidad de deshabilitar los trabajos de trasvase de registros correspondientes. Para obtener más información, consulte [Disable or Enable a Job](../ssms/agent/disable-or-enable-a-job.md).  
  
 La aplicación **sqllogship** , sqllogship. exe, se instala en el directorio X:\Archivos de Programa\microsoft SQL Server\120\Tools\Binn  
  
## <a name="permissions"></a>Permisos  
 **sqllogship** usa la autenticación de Windows. La cuenta de la autenticación de Windows donde se ejecuta el comando requiere acceso al directorio de Windows y permisos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . El requisito depende de si el comando **sqllogship** especifica la opción **-backup**, **-copy**o **-restore** .  
  
|Opción|Acceso al directorio|Permisos|  
|------------|----------------------|-----------------|  
|**-backup**|Requiere acceso de lectura/escritura al directorio de copia de seguridad.|Requiere los mismos permisos que la instrucción BACKUP. Para obtener más información, vea [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).|  
|**-copy**|Requiere acceso de lectura al directorio de copia de seguridad y acceso de escritura al directorio de copia.|Requiere los mismos permisos que el procedimiento almacenado [sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql) .|  
|**-restore**|Requiere acceso de lectura/escritura al directorio de copia.|Requiere los mismos permisos que la instrucción RESTORE. Para obtener más información, vea [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).|  
  
> [!NOTE]  
>  Para conocer las rutas de acceso de los directorios de copia de seguridad y copia, puede ejecutar el procedimiento almacenado **sp_help_log_shipping_secondary_database** o examinar la tabla **log_shipping_secondary** en **msdb**. Las rutas de acceso al directorio de copia de seguridad y al de destino se encuentran en las columnas **backup_source_directory** y **backup_destination_directory** respectivamente.  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_primary_databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/log-shipping-primary-databases-transact-sql)   
 [log_shipping_secondary &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/log-shipping-secondary-transact-sql)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql)   
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql)   
 [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql)  
  
  
