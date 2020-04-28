---
title: SQL Server copia de seguridad administrada en Azure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: afa01165-39e0-4efe-ac0e-664edb8599fd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ab44323dfabd389113351e413751b7a230c176e6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "70175756"
---
# <a name="sql-server-managed--backup-to-azure"></a>SQL Server de la copia de seguridad administrada en Azure
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]administra y automatiza las copias de seguridad de SQL Server en el servicio de almacenamiento de blobs de Azure. La estrategia de copia de seguridad que usa [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] se basa en el período de retención y en la carga de trabajo de transacciones en la base de datos. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] admite la restauración a un momento dado para el período de retención especificado.   
[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] se puede habilitar en el nivel de base de datos o en el de instancia para administrar todas las bases de datos en la instancia de SQL Server. El SQL Server se puede ejecutar de forma local o en entornos hospedados como la máquina virtual de Azure. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]se recomienda para SQL Server que se ejecutan en Azure Virtual Machines.  
  
## <a name="benefits-of-automating-sql-server-backup-using-ss_smartbackup"></a>Ventajas de la automatización de la copia de seguridad de SQL Server mediante [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
-   Actualmente, para automatizar las copias de seguridad de varias bases de datos, se requiere desarrollar una estrategia de copia de seguridad, escribir código personalizado y programar copias de seguridad. Mediante [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], solo tiene que proporcionar la configuración del período de retención y la ubicación de almacenamiento. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]programa, realiza y mantiene las copias de seguridad.  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] se puede configurar en el nivel de base de datos o con la configuración predeterminada para una instancia de SQL Server. La automatización de la [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] copia de seguridad mediante ofrece las siguientes ventajas:  
  
    -   Al establecer los valores predeterminados en el nivel de instancia, puede aplicar esta configuración en cualquier base de datos creada después, con lo que se evita el riesgo de no realizar la copia de seguridad de las bases de datos nuevas y así como la pérdida de datos.  
  
    -   La opción de habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] y establecer el período de retención en el nivel de base de datos le permite invalidar la configuración predeterminada establecida en el nivel de instancia. Esto permite un control más específico sobre la capacidad de recuperación de una base de datos concreta.  
  
-   Con [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], no es necesario especificar el tipo o la frecuencia de las copias de seguridad de una base de datos.  Especifique el período de retención y [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] determinará el tipo y la frecuencia de las copias de seguridad de una base de datos para almacenar las copias de seguridad en el servicio de almacenamiento de blobs de Azure. Para obtener más detalles sobre el conjunto de criterios [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] que usa para crear la estrategia de copia de seguridad, consulte la sección [componentes y conceptos](#Concepts) de este tema.  
  
-   Cuando se configura para utilizar el cifrado, debe tener seguridad adicional para los datos de copia de seguridad. Para obtener más información, vea [cifrado de copia de seguridad](backup-encryption.md)  
  
 Para más información sobre las ventajas de usar el almacenamiento de blobs de Azure para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las copias de seguridad, consulte [SQL Server copias de seguridad y restauración con Azure BLOB Storage servicio](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
## <a name="terms-and-definitions"></a>Términos y definiciones  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
 Una característica de SQL Server que automatiza la copia de seguridad de la base de datos y mantiene las copias de seguridad según el período de retención.  
  
 Período de retención  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usa el período de retención para determinar qué archivos de copia de seguridad se deben conservar en el almacenamiento para recuperar una base de datos hasta un momento dado en el intervalo de tiempo especificado.  Los valores admitidos están en el intervalo de 1 a 30 días.  
  
 Cadena de registros  
 Una secuencia continua de copias de seguridad de registros se denomina cadena de registros. Una cadena de registros empieza con una copia de seguridad completa de la base de datos.  
  
##  <a name="requirements-concepts-and-components"></a><a name="Concepts"></a>Requisitos, conceptos y componentes  
  
  
###  <a name="permissions"></a><a name="Security"></a> Permisos  
 Transact-SQL es la interfaz principal que se utiliza para configurar y supervisar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. En general, para ejecutar los procedimientos almacenados de configuración, **db_backupoperator** rol de base de datos con permisos **ALTER any Credential** , y `EXECUTE` se requieren permisos en **sp_delete_backuphistory** procedimiento almacenado.  Los procedimientos almacenados y las funciones que se usan para revisar la información normalmente requieren permisos `Execute` en el procedimiento almacenado y `Select` en la función, respectivamente.  
  
###  <a name="prerequisites"></a><a name="Prereqs"></a> Requisitos previos  
 **Requisitos previos**  
  
 Utiliza **Azure Storage servicio** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para almacenar los archivos de copia de seguridad.    Los conceptos, la estructura y los requisitos para crear una cuenta de almacenamiento de Azure se explican en detalle en la sección [Introducción a los componentes y conceptos clave](sql-server-backup-to-url.md#intorkeyconcepts) del tema **SQL Server copia de seguridad en dirección URL** .  
  
 La **credencial SQL** se usa para almacenar la información necesaria para autenticarse en la cuenta de almacenamiento de Azure. El objeto Credencial de SQL almacena la información del nombre de cuenta y de las claves de acceso. Para obtener más información, consulte la sección [Introduction to Key components and Concepts](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) del tema **SQL Server Backup to URL** . Para ver un tutorial sobre cómo crear una credencial de SQL para almacenar Azure Storage información de autenticación, vea [Lección 2: crear una credencial de SQL Server](../../tutorials/lesson-2-create-a-sql-server-credential.md).  
  
###  <a name="concepts-and-key-components"></a><a name="Concepts_Components"></a>Conceptos y componentes clave  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] es una característica que administra las operaciones de copia de seguridad. Almacena los metadatos en la base de datos **msdb** y usa trabajos del sistema para escribir copias de seguridad completas de las bases de datos y del registro de transacciones.  
  
#### <a name="components"></a>Componentes  
 Transact-SQL es la interfaz principal para interactuar con [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Los procedimientos almacenados del sistema se utilizan para habilitar, configurar y supervisar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Las funciones del sistema se utilizan para recuperar la configuración, los valores de parámetros y la información del archivo de copia de seguridad existentes. Los eventos extendidos se utilizan para exponer los errores y advertencias. Los mecanismos de alerta se habilitan mediante los trabajos del Agente SQL y la administración basada en directivas de SQL Server. La siguiente es una lista de los objetos y una descripción de su funcionalidad en relación con [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 Los cmdlets de PowerShell también están disponibles para configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. SQL Server Management Studio permite restaurar las copias de seguridad creadas por [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] mediante la tarea **Restaurar base de datos**  
  
|||  
|-|-|  
|Objeto del sistema|Descripción|  
|**MSDB**|Almacena los metadatos y el historial de copias de seguridad de todas las copias de seguridad creadas por [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|[smart_admin. set_db_backup &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/dn451013(v=sql.120).aspx)|Procedimiento almacenado del sistema para habilitar y configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para una base de datos.|  
|[smart_admin. set_instance_backup &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/dn451009(v=sql.120).aspx)|Procedimiento almacenado del sistema para habilitar y configurar los [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] valores predeterminados para la instancia de SQL Server.|  
|[smart_admin. sp_ backup_master_switch &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql)|Procedimiento almacenado del sistema para pausar y reanudar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|[smart_admin. sp_set_parameter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql)|Procedimiento almacenado del sistema para habilitar y configurar la supervisión de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Ejemplos: habilitar eventos extendidos, configuración de correo para las notificaciones.|  
|[smart_admin. sp_backup_on_demand &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)|Procedimiento almacenado del sistema que se utiliza para realizar una copia de seguridad ad hoc de una base de datos que [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitada para usar sin interrumpir la cadena de registros.|  
|[smart_admin. fn_backup_db_config &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-backup-db-config-transact-sql)|Función del sistema que devuelve el [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] estado actual y los valores de configuración de una base de datos, o para todas las bases de datos de la instancia.|  
|[smart_admin. fn_is_master_switch_on &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-is-master-switch-on-transact-sql)|Función del sistema que devuelve el estado del modificador principal.|  
|[smart_admin. sp_get_backup_diagnostics &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-get-backup-diagnostics-transact-sql)|Procedimiento almacenado del sistema que se utiliza para devolver los eventos registrados por Eventos extendidos.|  
|[smart_admin. fn_get_parameter &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql)|Función del sistema que devuelve los valores actuales de la configuración del sistema de copia de seguridad como la supervisión y la configuración del correo para las alertas.|  
|[smart_admin. fn_available_backups &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql)|Procedimiento almacenado utilizado para recuperar las copias de seguridad disponibles para una base de datos especificada o para todas las bases de datos de una instancia.|  
|[smart_admin. fn_get_current_xevent_settings &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql)|Función del sistema que devuelve la configuración actual de Eventos extendidos.|  
|[smart_admin. fn_get_health_status &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-health-status-transact-sql)|Función del sistema que devuelve los recuentos agregados de los errores registrados por Eventos extendidos durante un período específico.|  
|[Supervisión de copia de seguridad administrada de SQL Server en Azure](sql-server-managed-backup-to-microsoft-azure.md)|Eventos extendidos para la supervisión, la notificación por correo electrónico de errores y las advertencias, la administración basada en directivas de SQL Server para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
  
#### <a name="backup-strategy"></a>Estrategia de copia de seguridad  
 **Estrategia de copia de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]seguridad utilizada por:**  
  
 Determina el tipo de copias de seguridad programadas y la frecuencia de copia de seguridad en función de la carga de trabajo de la base de datos. La configuración del período de retención se utiliza para determinar el tiempo que un archivo de copia de seguridad debe conservarse en el almacenamiento y la capacidad de recuperar la base de datos hasta un momento dado dentro del período de retención.  
  
 **Convenciones de nomenclatura de los archivos y del contenedor de copia de seguridad:**  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]asigna un nombre al contenedor de almacenamiento de Azure mediante el nombre de la instancia de SQL Server para todas las bases de datos, excepto las bases de datos de disponibilidad.  En el caso de las bases de datos de disponibilidad, se usa el GUID del grupo de disponibilidad para asignar un nombre al contenedor de almacenamiento de Azure.  
  
 El archivo de copia de seguridad para las bases de datos que no son de disponibilidad se denomina con la Convención siguiente: el nombre se crea con los primeros 40 caracteres del nombre de la base de datos, el GUID de la base de datos sin '-' y la marca de tiempo. El carácter de subrayado se inserta entre los segmentos como separadores. La extensión de archivo **.bak** se usa en el caso de que la copia de seguridad sea completa y **.log** se usa para las copias de seguridad de registros. En las bases de datos del grupo de disponibilidad, además de la convención de nomenclatura de archivos descrita anteriormente, se agrega el GUID de la base de datos del grupo de disponibilidad después de los 40 caracteres del nombre de la base de datos. El GUID de la base de datos del grupo de disponibilidad es el valor de group_database_id de sys.databases.  
  
 **Copia de seguridad completa de base de datos:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] el agente programa una copia de seguridad completa de la base de datos si se cumple alguna de las siguientes condiciones.  
  
-   Una base de datos se habilita para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] por primera vez o cuando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] se habilita con la configuración predeterminada en el nivel de instancia.  
  
-   El crecimiento del registro desde la última copia de seguridad completa de la base de datos es igual o mayor que 1 GB.  
  
-   Ha transcurrido el intervalo de tiempo máximo de una semana desde la última copia de seguridad completa de la base de datos.  
  
-   La cadena de registros se interrumpe. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] comprueba periódicamente si la cadena de registros está intacta comparando el primer y el último LSN de los archivos de copia de seguridad. Si se interrumpe la cadena de registros por cualquier motivo, [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] programa una copia de seguridad completa de la base de datos. La razón más común para la interrupción de la cadena de registros es, probablemente, un comando de copia de seguridad emitido con Transact-SQL o con la tarea de copia de seguridad en SQL Server Management Studio.  Otros escenarios comunes incluyen la eliminación accidental de los archivos de registro de copia de seguridad o la sobrescritura accidental de las copias de seguridad.  
  
 **Copia de seguridad del registro de transacciones:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] programa una copia de seguridad de registros si se cumple alguna de las siguientes condiciones:  
  
-   No se encuentra el historial de copias de seguridad de registros. Normalmente esto es así cuando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] se habilita por primera vez.  
  
-   El espacio del registro de transacciones utilizado es de 5 MB o más.  
  
-   Se alcanza el intervalo de tiempo máximo de 2 horas desde la última copia de seguridad de registros.  
  
-   En cualquier momento, la copia de seguridad del registro de transacciones se retrasa después de una copia de seguridad completa de la base de datos. El objetivo es mantener la cadena de registros por delante de la copia de seguridad completa.  
  
#### <a name="retention-period-settings"></a>Configuración del período de retención  
 Al habilitar la copia de seguridad, debe establecer el período de retención en días: el mínimo es 1 día y el máximo es 30 días.  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] según la configuración del período de retención evalúa la capacidad de recuperar a un momento dado en el tiempo especificado para determinar qué archivos de copia de seguridad mantener e identificar los que hay que eliminar. El backup_finish_date de la copia de seguridad se utiliza para determinar y hacer coincidir el tiempo especificado por la configuración del período de retención.  
  
#### <a name="important-considerations"></a>Consideraciones importantes  
 Hay algunas consideraciones que son importantes para comprender su efecto en las operaciones de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Se enumeran a continuación:  
  
-   Para las bases de datos, si hay un trabajo de copia de seguridad completa de la base de datos en ejecución, [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] espera a que el trabajo actual se complete antes de hacer otra copia de seguridad completa de la misma base de datos. Asimismo, solo una copia de seguridad del registro de transacciones se puede ejecutar en un momento dado. Sin embargo, una copia de seguridad completa y una copia de seguridad del registro de transacciones pueden ejecutarse simultáneamente. Los errores se registran como Eventos extendidos.  
  
-   Si se programan más de 10 copias de seguridad completas simultáneas de la base de datos, se emitirá una advertencia a través del canal de depuración de Eventos extendidos. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] mantiene entonces una cola de prioridad para las bases de datos restantes que requieren una copia de seguridad hasta que se programen y completen todas.  
  
###  <a name="support-limitations"></a>Limitaciones de compatibilidad de <a name="support_limits"></a>  
 A continuación se indican algunas limitaciones específicas de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   El agente [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] solo admite copias de seguridad de la base de datos: copias de seguridad completas y de registros.  La automatización de la copia de seguridad de archivos no se admite.  
  
-   Las operaciones de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] se admiten actualmente mediante Transact-SQL. La supervisión y la solución de problemas se puede llevar a cabo con Eventos extendidos. El soporte técnico de SMO y PowerShell se limita a la configuración del almacenamiento, a la configuración predeterminada del periodo de retención para una instancia de SQL Server y a la supervisión del estado de la copia de seguridad y del estado general según las directivas de administración basada en directivas de SQL Server.  
  
-   Las bases de datos del sistema no se admiten.  
  
-   Azure Blob Storage servicio es la única opción de almacenamiento de copia de seguridad admitida. Las copias de seguridad en disco o cinta no se admiten.  
  
-   Actualmente, el tamaño de archivo máximo permitido para un BLOB en páginas en Azure Storage es 1 TB. Los archivos de copia de seguridad mayores que 1 TB mayor producirán un error. Para evitar esta situación, se recomienda usar la compresión para las bases de datos grandes y se pruebe el tamaño del archivo de copia de seguridad antes de configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Puede realizar una prueba realizando una copia de seguridad en un disco local o realizando una copia de seguridad `BACKUP TO URL` manual en Azure Storage mediante la instrucción TRANSACT-SQL. Para más información, consulte [SQL Server Backup to URL](sql-server-backup-to-url.md).  
  
-   Modelos de recuperación: solo se admiten las bases de datos establecidas para el modelo de registro masivo o completo.  Las bases de datos establecidas en el modelo de recuperación simple no se admiten.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] puede tener algunas limitaciones cuando se configura con otras tecnologías que admiten la copia de seguridad, la alta disponibilidad o la recuperación de desastres. Para obtener más información, vea [SQL Server copia de seguridad administrada en Azure: interoperabilidad y coexistencia](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
  
|||  
|-|-|  
|**Descripciones de tareas**|**Tema**|  
|Las tareas básicas como la configuración de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para una base de datos, la configuración predeterminada en el nivel de instancia, la deshabilitación de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en la instancia o base de datos, la pausa y el reinicio de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|[Copia de seguridad administrada de SQL Server en Azure: configuración de la retención y el almacenamiento](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)|  
|**Tutorial:** Instrucciones paso a paso para configurar y supervisar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|[Configuración de copia de seguridad administrada de SQL Server en Azure](enable-sql-server-managed-backup-to-microsoft-azure.md)|  
|**Tutorial:** Instrucciones paso a paso para configurar y supervisar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] bases de datos en el grupo de disponibilidad.|[Configuración de copia de seguridad administrada de SQL Server para Azure para grupos de disponibilidad](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)|  
|Herramientas, conceptos y tareas relacionadas con la supervisión de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|[Supervisión de copia de seguridad administrada de SQL Server en Azure](sql-server-managed-backup-to-microsoft-azure.md)|  
|Herramientas y pasos para solucionar problemas de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|[Solución de problemas de la copia de seguridad administrada de SQL Server en Azure](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)|  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server copias de seguridad y restauración con Azure Blob Storage servicio](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [SQL Server copia de seguridad en URL](sql-server-backup-to-url.md)   
 [SQL Server copia de seguridad administrada en Azure: interoperabilidad y coexistencia](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)   
 [Solución de problemas de la copia de seguridad administrada de SQL Server en Azure](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)  
  
  
