---
title: Restaurar base de datos (página Opciones) | Microsoft Docs
description: Al restaurar una base de datos en SQL Server, utilice la página Opciones del cuadro de diálogo Restaurar base de datos para modificar el comportamiento y el resultado de la operación de restauración.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoredb.options.f1
ms.assetid: 9a75d48b-c25f-40f3-8ea1-32cfa8211754
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f68337ee44e052c838b29d0051631c7be495a478
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85737718"
---
# <a name="restore-database-options-page"></a>Restaurar base de datos (página Opciones)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Utilice la página **Opciones** del cuadro de diálogo **Restaurar base de datos** para modificar el comportamiento y el resultado de la operación de restauración.  
  
 **Para utilizar SQL Server Management Studio a fin de restaurar una copia de seguridad de base de datos**  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  Cuando se especifica una tarea de restauración mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede generar el script de [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondiente que contenga las instrucciones RESTORE para esta operación de restauración. Para generar el script, haga clic en **Script** y seleccione un destino para este. Para obtener más información sobre la sintaxis de RESTORE, vea [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
## <a name="options"></a>Opciones  
  
### <a name="restore-options"></a>Opciones de restauración  
 Para modificar aspectos del comportamiento de la operación de restauración, utilice las opciones del panel **Opciones de restauración** .  
  
 **Sobrescribir la base de datos existente [WITH REPLACE]**  
 La operación de restauración sobrescribirá los archivos de cualquier base de datos que use en ese momento el nombre de base de datos especificado en el campo **Restaurar en**en la página [General](../../relational-databases/backup-restore/restore-database-general-page.md) del cuadro de diálogo **Restaurar base de datos** . Los archivos de la base de datos existente se sobrescribirán aunque restaure copias de seguridad de una base de datos diferente al nombre de base de datos existente. La selección de esta opción equivale a usar la opción REPLACE en una instrucción [RESTORE](../../t-sql/statements/restore-statements-arguments-transact-sql.md) ([!INCLUDE[tsql](../../includes/tsql-md.md)]).  
  
> [!CAUTION]  
>  Utilice esta opción después de haberlo pensado detenidamente. Para obtener más información, vea [RESTORE &#40;argumentos, Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 **Conservar la configuración de replicación [WITH KEEP_REPLICATION]**  
 Conserva la configuración de replicación cuando se restaura una base de datos publicada en un servidor distinto de aquel en que se creó. Esta opción solo es pertinente si la base de datos se replicó cuando se creó la copia de seguridad.  
  
 Esta opción solo está disponible con la opción **Dejar la base de datos lista para su uso revirtiendo las transacciones no confirmadas** (descrita más adelante en esta tabla), que equivale a restaurar una copia de seguridad con la opción RECOVERY.  
  
 La elección de esta opción equivale a usar la opción KEEP_REPLICATION en una instrucción [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) .  
  
 Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).  
  
 **Restringir el acceso a la base de datos restaurada [WITH RESTRICTED_USER]**  
 Hace que la base de datos restaurada esté disponible solo para los miembros de **db_owner**, **dbcreator**o **sysadmin**.  
  
 La selección de esta opción equivale al uso de la opción RESTRICTED_USER en una instrucción RESTORE.  
  
### <a name="recovery-state"></a>Estado de recuperación  
 Para determinar el estado de la base de datos después de la operación de restauración, debe seleccionar una de las opciones del panel **Estado de recuperación** .  
  
 **RESTORE WITH RECOVERY**  
 Recupera la base de datos después de restaurar la copia de seguridad final seleccionada en la cuadrícula **Conjuntos de copia de seguridad para restaurar**de la [página General](../../relational-databases/backup-restore/restore-database-general-page.md). Esta es la opción predeterminada y es equivalente a especificar WITH RECOVERY en una instrucción [RESTORE](../../t-sql/statements/restore-statements-arguments-transact-sql.md) ([!INCLUDE[tsql](../../includes/tsql-md.md)]).  
  
> [!NOTE]  
>  En el modelo de recuperación completa o en el modelo de recuperación optimizado para cargas masivas de registros, elija esta opción solo si va a restaurar todos los archivos de registro ahora.  
  
 **RESTORE WITH NORECOVERY**  
 Deja la base de datos en estado de restauración. Esto permite restaurar copias de seguridad adicionales en la ruta de recuperación actual. Para recuperar la base de datos, debe realizar una operación de restauración con la opción RESTORE WITH RECOVERY (vea la opción anterior).  
  
 Esta opción es equivalente a especificar WITH NORECOVERY en una instrucción RESTORE.  
  
 Si selecciona esta opción, no estará disponible la opción **Conservar la configuración de replicación** .  
  
 **RESTORE WITH STANDBY**  
 Deja la base de datos en un estado de espera, en el que la base de datos está disponible para acceso limitado de solo lectura. Esta opción es equivalente a especificar WITH STANDBY en una instrucción RESTORE.  
  
 Si elige esta opción, debe especificar un archivo en espera en el cuadro de texto **Archivo en espera** . El archivo en espera permite deshacer los efectos de la recuperación.  
  
 **Archivo en espera**  
 Especifica un archivo en espera. Puede buscar el archivo en espera o escribir su ruta de acceso directamente en el cuadro de texto.  
  
### <a name="tail-log-backup"></a>Copia del final del registro  
 Permite indicar que se realice una copia del final del registro junto con la restauración de la base de datos.  
  
 **Realizar copia del final del registro antes de restaurar**  
 Active esta casilla para indicar que debe realizarse una copia del final del registro.  
  
> [!NOTE]  
>  Si el momento seleccionado en el cuadro de diálogo [Escala de tiempo de la copia de seguridad](../../relational-databases/backup-restore/backup-timeline.md) requiere una copia del final del registro, esta casilla se activará y no podrá modificarse.  
  
 **Archivo de copia de seguridad**  
 Especifica un archivo de copia de seguridad del final del registro. Puede buscar el archivo de copia de seguridad o escribir su nombre directamente en el cuadro de texto.  
  
### <a name="server-connections"></a>Conexiones con el servidor  
 Permite cerrar las conexiones de base de datos existentes.  
  
 **Cerrar conexiones existentes**  
 Puede haber errores en las operaciones de restauración si hay conexiones activas con la base de datos. Active la opción **Cerrar conexiones existentes** para asegurarse de que se cierren todas las conexiones activas entre [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y la base de datos. Esta casilla establece la base de datos en modo de usuario único antes de realizar las operaciones de restauración, y establece la base de datos en modo multiusuario una vez completadas.  
  
### <a name="prompt"></a>Prompt  
 **Preguntar antes de restaurar cada copia de seguridad**  
 Especifica que, después de que se restaure cada copia de seguridad, se mostrará el cuadro de diálogo **Continuar con la restauración** para preguntar si quiere continuar con la secuencia de restauración. En este cuadro de diálogo se muestra el nombre del siguiente conjunto de medios (si se conoce) junto con el nombre y la descripción del siguiente conjunto de copia de seguridad.  
  
 Esta opción permite pausar una secuencia de restauración después de restaurar cualquier copia de seguridad. Esta opción es especialmente útil cuando hay que intercambiar cintas para distintos conjuntos de medios, por ejemplo, cuando el servidor dispone de un solo dispositivo de cinta. Cuando esté listo para continuar, haga clic en **Aceptar**.  
  
 Puede interrumpir una secuencia de restauración si hace clic en **No**. De este modo, la base de datos se quedará en estado de restauración. Para mayor comodidad, puede continuar más tarde con la secuencia de restauración mediante la reanudación de la copia de seguridad siguiente descrita en el cuadro de diálogo **Continuar con la restauración** . El procedimiento de restauración de la siguiente copia de seguridad depende de si contiene un registro de transacciones o datos, de esta forma:  
  
-   Si la siguiente copia de seguridad es una copia de seguridad de datos completa o diferencial, vuelva a utilizar la tarea **Restaurar base de datos** .  
  
-   Si la copia de seguridad siguiente es la de un archivo, utilice la tarea **Restaurar archivos y grupos de archivos**. Para obtener más información, vea [Restaurar archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md).  
  
-   Si la siguiente copia de seguridad es una copia de seguridad de registros, utilice la tarea **Restaurar registro de transacciones** . Para obtener más información sobre cómo reanudar una secuencia de restauración por medio de la restauración de un registro de transacciones, vea [Restaurar una copia de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md).  
  
## <a name="see-also"></a>Consulte también  
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Restaurar una copia de seguridad desde un dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)   
 [Restaurar una copia de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Restaurar la base de datos &#40;página General&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)  
  
  
