---
title: managed_backup. sp_backup_config_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/20/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e7bb477901dee22c70bb47cd0eaf7da5eb163b7f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "77507542"
---
# <a name="managed_backupsp_backup_config_schedule-transact-sql"></a>managed_backup. sp_backup_config_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura opciones de programación automatizadas o personalizadas para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
    
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
  
##  <a name="arguments"></a><a name="Arguments"></a>Argumentos  
 @database_name  
 Nombre de la base de datos para habilitar la copia de seguridad administrada en una base de datos específica. Si es NULL o *, esta copia de seguridad administrada se aplica a todas las bases de datos del servidor.  
  
 @scheduling_option  
 Especifique ' System ' para la programación de copias de seguridad controlada por el sistema. Especifique ' Custom ' para una programación personalizada definida por el otro parámetros.  
  
 @full_backup_freq_type  
 El tipo de frecuencia de la operación de copia de seguridad administrada, que se puede establecer en ' Daily ' o ' Weekly '.  
  
 @days_of_week  
 Los días de la semana para las copias de seguridad @full_backup_freq_type cuando se establece en semanalmente. Especifique nombres de cadena completos como ' lunes '.  También puede especificar más de un nombre de día, separados por canalización. Por ejemplo N'Monday | Miércoles | Viernes '.  
  
 @backup_begin_time  
 La hora de inicio de la ventana de copia de seguridad. Las copias de seguridad no se iniciarán fuera de la ventana de tiempo, que se define mediante @backup_begin_time una @backup_durationcombinación de y.  
  
 @backup_duration  
 La duración del período de tiempo de copia de seguridad. Tenga en cuenta que no hay ninguna garantía de que las copias de seguridad se completen durante @backup_begin_time el @backup_durationperíodo de tiempo definido por y. Las operaciones de copia de seguridad que se inician en este período de tiempo pero superan la duración de la ventana no se cancelarán.  
  
 @log_backup_freq  
 Esto determina la frecuencia de las copias de seguridad del registro de transacciones. Estas copias de seguridad se producen a intervalos regulares, en lugar de a la programación especificada para las copias de seguridad de base de datos. @log_backup_freqpuede ser en minutos u horas y `0:00` es válido, lo que indica que no hay copias de seguridad de registros. Deshabilitar las copias de seguridad de registros solo sería adecuado para las bases de datos con un modelo de recuperación simple.  
  
> [!NOTE]  
>  Si el modelo de recuperación cambia de simple a completo, debe volver a configurar la log_backup_freq de `0:00` en un valor distinto de cero.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol de base de datos **db_backupoperator** , con permisos **ALTER any Credential** y permisos **Execute** en **sp_delete_backuphistory** procedimiento almacenado.  
  
## <a name="see-also"></a>Consulte también  
 [managed_backup. sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
