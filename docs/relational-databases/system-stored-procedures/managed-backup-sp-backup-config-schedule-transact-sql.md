---
title: managed_backup.sp_backup_config_schedule (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_backup_config_schedule_TSQL
- managed_backup.sp_backup_config_schedule
- managed_backup.sp_backup_config_schedule_TSQL
- sp_backup_config_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_schedule
- sp_backup_config_schedule
ms.assetid: 82541160-d1df-4061-91a5-6868dd85743a
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8ebeca4b0a1c9079f8786303207bcbae4dfe74c3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33238835"
---
# <a name="managedbackupspbackupconfigschedule-transact-sql"></a>managed_backup.sp_backup_config_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura las opciones de programación automatizadas o personalizadas para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
    
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
EXEC managed_backup.sp_backup_config_schedule   
    [@database_name = ] 'database_name'
    ,[@scheduling_option = ] {'Custom' | 'System'}  
    ,[@full_backup_freq_type = ] {'Daily' | 'Weekly'}  
    ,[@days_of_week = ] 'days_of_the_week'  
    ,[@backup_begin_time = ] 'begin time of the backup window'  
    ,[@backup_duration = ] 'backup window length'  
    ,[@log_backup_freq = ] 'frequency of log backup'  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @database_name  
 El nombre de la base de datos para habilitar la copia de seguridad administrada en una base de datos. Si es NULL o *, esta copia de seguridad administrada se aplica a todas las bases de datos en el servidor.  
  
 @scheduling_option  
 Especifique 'Sistema' para la programación de copia de seguridad controlado por el sistema. Especifique 'Custom' para una programación personalizada definida por los otros parámetros.  
  
 @full_backup_freq_type  
 El tipo de frecuencia de la operación de copia de seguridad administrada, que se puede establecer en 'Daily' o 'Semanal'.  
  
 @days_of_week  
 Los días de la semana para las copias de seguridad cuando @full_backup_freq_type está establecida en semanal. Especificar nombres de cadena completa como "Lunes".  También puede especificar más de nombre de un día, separado por barras verticales. Por ejemplo N'Monday | El miércoles | El viernes '.  
  
 @backup_begin_time  
 La hora de inicio de la ventana de copia de seguridad. No se iniciarán las copias de seguridad fuera del período de tiempo, que se define mediante una combinación de @backup_begin_time y @backup_duration.  
  
 @backup_duration  
 La duración del intervalo de tiempo de copia de seguridad. Tenga en cuenta que no hay ninguna garantía de que las copias de seguridad se completará durante el período de tiempo definido por @backup_begin_time y @backup_duration. No se cancelarán las operaciones de copia de seguridad que se inician en este período pero superan la duración de la ventana.  
  
 @log_backup_freq  
 Esto determina la frecuencia de las copias de seguridad del registro de transacciones. Estas copias de seguridad se realizan a intervalos regulares, en lugar de en la programación especificada para las copias de seguridad de base de datos. @log_backup_freq puede ser en minutos u horas y 0 es válido, lo que indica que no hay copias de seguridad del registro. Deshabilitar las copias de seguridad de registro solo sea adecuado para las bases de datos con un modelo de recuperación simple.  
  
> [!NOTE]  
>  Si cambia el modelo de recuperación de simple a full, debe volver a configurar el log_backup_freq de 0 a un valor distinto de cero.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere la pertenencia a **db_backupoperator** rol, la base de datos con **ALTER ANY CREDENTIAL** permisos, y **EXECUTE** permisos **sp_delete_ backuphistory** procedimiento almacenado.  
  
## <a name="see-also"></a>Vea también  
 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
