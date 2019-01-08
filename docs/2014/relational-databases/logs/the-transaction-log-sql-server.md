---
title: El registro de transacciones (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], about
- databases [SQL Server], transaction logs
- logs [SQL Server], transaction logs
ms.assetid: d7be5ac5-4c8e-4d0a-b114-939eb97dac4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1b4a175ad850ccbb0711a0997c3658cf01497686
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52807017"
---
# <a name="the-transaction-log-sql-server"></a>El registro de transacciones (SQL Server)
  Todas las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen un registro de transacciones que registra todas las transacciones y las modificaciones que cada transacción realiza en la base de datos. El registro de transacciones se debe truncar periódicamente para evitar que se llene. Sin embargo, algunos factores pueden retrasar el truncamiento del registro, por lo que es importante supervisar el tamaño del registro. Algunas operaciones se pueden registrar mínimamente para reducir su impacto sobre el tamaño del registro de transacciones.  
  
 El registro de transacciones es un componente esencial de la base de datos y, si se produce un error del sistema, podría ser necesario para volver a poner la base de datos en un estado coherente. El registro de transacciones nunca se debe eliminar o mover, a menos que se conozcan totalmente las implicaciones de esas acciones.  
  
> [!NOTE]  
>  Los puntos de comprobación crean puntos buenos conocidos a partir de los cuales se empiezan a aplicar los registros de transacciones durante la recuperación de base de datos. Para obtener más información, vea [Puntos de comprobación de base de datos &#40;SQL Server&#41;](database-checkpoints-sql-server.md).  
  
 **En este tema:**  
  
-   [Ventajas: Operaciones admitidas por el registro de transacciones](#Benefits)  
  
-   [Truncamiento del registro de transacciones](#Truncation)  
  
-   [Factores que pueden ralentizar el truncamiento del registro](#FactorsThatDelayTruncation)  
  
-   [Operaciones que pueden registrar mínimamente](#MinimallyLogged)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="Benefits"></a> Ventajas: Operaciones compatibles con el registro de transacciones  
 El registro de transacciones permite las siguientes operaciones:  
  
-   Recuperación de transacciones individuales.  
  
-   Recuperación de todas las transacciones incompletas cuando se inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Puesta al día de una base de datos, un archivo, un grupo de archivos o una página restaurados hasta el momento exacto del error.  
  
-   Permitir replicación transaccional.  
  
-   Compatibilidad con soluciones de alta disponibilidad y recuperación ante desastres: [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], creación de reflejo de la base de datos y trasvase de registros.  
  
##  <a name="Truncation"></a> Truncamiento del registro de transacciones  
 El truncamiento del registro libera el espacio en el archivo de registro para que lo pueda reutilizar el registro de transacciones. El truncamiento del registro es esencial para evitar que se llene. El truncamiento del registro elimina los archivos de registro virtuales inactivos del registro de transacciones lógico de una base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , liberando espacio en el registro lógico para que lo reutilice el registro de transacciones físico. Si no se truncara nunca un registro de transacciones, acabaría ocupando todo el espacio de disco asignado a sus archivo de registro físicos.  
  
 Para evitar este problema, a menos que el truncamiento del registro se retrase por algún motivo, el truncamiento se produciría automáticamente después de los siguientes eventos:  
  
-   En el modelo de recuperación simple, después de un punto de comprobación.  
  
-   En el modelo de recuperación completa o de recuperación optimizado para cargas masivas de registros, si se ha producido un punto de comprobación desde la copia de seguridad anterior, el truncamiento se produce después de una copia de seguridad de registros (a menos que sea una copia de seguridad de registros de solo copia).  
  
 Para obtener más información, vea [Factores que pueden ralentizar el truncamiento del registro](#FactorsThatDelayTruncation), más adelante en este tema.  
  
> [!NOTE]  
>  El truncamiento del registro no reduce el tamaño del archivo de registro físico. Para reducir el tamaño físico de un archivo de registro físico, se debe reducir el archivo de registro. Para obtener información sobre cómo reducir el tamaño de un archivo de registro físico, vea [Manage the Size of the Transaction Log File](manage-the-size-of-the-transaction-log-file.md).  
  
##  <a name="FactorsThatDelayTruncation"></a> Factores que pueden ralentizar el truncamiento del registro  
 Cuando las entradas de registro permanecen activas durante una transacción de larga duración, se retrasa el truncamiento del registro y es posible que se llene el registro de transacciones.  
  
> [!IMPORTANT]  
>  Para obtener más información sobre cómo actuar ante un registro de transacciones lleno, vea [Troubleshoot a Full Transaction Log &#40;SQL Server Error 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md).  
  
 El truncamiento del registro se puede retrasar por diferentes factores. Para averiguar qué es lo que impide el truncamiento del registro, si hay alguna causa, consulte las columnas **log_reuse_wait** y **log_reuse_wait_desc** de la vista de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) . En la tabla siguiente se describen los valores de estas columnas.  
  
|valor log_reuse_wait|valor log_reuse_wait_desc|Descripción|  
|----------------------------|----------------------------------|-----------------|  
|0|NOTHING|Hay actualmente uno o más archivos de registro virtual reutilizables.|  
|1|CHECKPOINT|No se ha producido ningún punto de comprobación desde el último truncamiento o el encabezado del registro no se ha movido más allá de un archivo de registro virtual. (Todos los modelos de recuperación)<br /><br /> Este es un motivo habitual para retrasar el truncamiento. Para obtener más información, vea [Database Checkpoints &#40;SQL Server&#41;](database-checkpoints-sql-server.md).|  
|2|LOG_BACKUP|Se requiere una copia de seguridad del registro para que se pueda truncar el registro de transacciones. (Solo modelos de recuperación completa u optimizada para cargas masivas de registros)<br /><br /> Cuando se completa la siguiente copia de seguridad de registros, es posible que se pueda reutilizar parte del espacio de registro.|  
|3|ACTIVE_BACKUP_OR_RESTORE|Existe una recuperación o copia de seguridad de datos en curso (todos los modelos de recuperación).<br /><br /> Si la copia de seguridad de una base de datos impide el truncamiento del registro, la cancelación de la operación de copia de seguridad podría ayudar a solucionar el problema inmediato.|  
|4|ACTIVE_TRANSACTION|Existe una transacción activa (todos los modelos de recuperación).<br /><br /> Podría existir una transacción de larga duración en el inicio de la copia de seguridad del registro. En este caso, para liberar espacio se podría requerir otra copia de seguridad del registro. Tenga en cuenta que un transacciones de larga ejecución impiden el truncamiento de registro en todos los modelos de recuperación, incluido el modelo de recuperación simple, en la que se suele truncar el registro de transacciones en cada punto de comprobación automático.<br /><br /> Una transacción está diferida. Una *transacción diferida* es efectivamente una transacción activa cuya reversión se bloquea debido a algún recurso no disponible. Para obtener más información sobre las causas de las transacciones diferidas y cómo sacarlas del estado diferido, vea [Transacciones diferidas &#40;SQL Server&#41;](../backup-restore/deferred-transactions-sql-server.md). <br /><br />Las transacciones de larga ejecución también podrían llenar el registro de transacciones de tempdb. Las transacciones de usuario usan implícitamente tempdb para objetos internos como tablas de trabajo para ordenar, archivos de trabajo para crear valores hash, tablas de trabajo de cursor y versiones de fila. Incluso si la transacción de usuario incluye datos (consultas SELECT) de solo lectura, los objetos internos se pueden crear y usar en las transacciones de usuario. Después, se puede rellenar el registro de transacciones de tempdb.|  
|5|DATABASE_MIRRORING|Se realiza una pausa en la creación de reflejo de la base de datos o, en el modo de alto rendimiento, la base de datos reflejada está notablemente detrás de la base de datos principal. (Solo para el modelo de recuperación completa)<br /><br /> Para obtener más información, vea [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|6|REPLICATION|Durante las replicaciones transaccionales, las transacciones pertinentes para las publicaciones no se han entregado aún a la base de datos de distribución. (Solo para el modelo de recuperación completa)<br /><br /> Para obtener información acerca de la replicación transaccional, vea [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md).|  
|7|DATABASE_SNAPSHOT_CREATION|Se está creando una instantánea de base de datos. (Todos los modelos de recuperación)<br /><br /> Este es un motivo habitual, por lo general breve, para retrasar el truncamiento del registro.|  
|8|LOG_SCAN|Se está realizando un examen de registro. (Todos los modelos de recuperación)<br /><br /> Este es un motivo habitual, por lo general breve, para retrasar el truncamiento del registro.|  
|9|AVAILABILITY_REPLICA|Una réplica secundaria de un grupo de disponibilidad está aplicando entradas del registro de transacciones de esta base de datos a una base de datos secundaria correspondiente. (Modelo de recuperación completa)<br /><br /> Para obtener más información, consulte [información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|10|-|Exclusivamente para uso interno.|  
|11|-|Exclusivamente para uso interno.|  
|12|-|Exclusivamente para uso interno.|  
|13|OLDEST_PAGE|Si una base de datos está configurada para usar puntos de comprobación indirectos, la página más antigua de la base de datos podría ser anterior al LSN del punto de comprobación. En este caso, la página más antigua puede retrasar el truncamiento del registro. (Todos los modelos de recuperación)<br /><br /> Para obtener más información sobre los puntos de comprobación indirectos, vea [Database Checkpoints &#40;SQL Server&#41;](database-checkpoints-sql-server.md).|  
|14|OTHER_TRANSIENT|No se utiliza este valor actualmente.|  
|16|XTP_CHECKPOINT|Cuando una base de datos tiene un grupo de archivos optimizados para memoria, el registro de transacciones no se puede truncar hasta que el punto de comprobación [!INCLUDE[hek_2](../../includes/hek-2-md.md)] automático se desencadena (lo que sucede cada 512 MB de crecimiento de los registros).<br /><br /> Nota: Para truncar el registro de transacción antes de un tamaño de 512 MB, activa el comando Checkpoint manualmente en la base de datos en cuestión.|  
  
##  <a name="MinimallyLogged"></a> Operaciones que pueden registrar mínimamente  
 El*registro mínimo* implica registrar únicamente la cantidad de información necesaria para recuperar la transacción sin permitir la recuperación a un momento dado. En este tema se identifican las operaciones que se registran mínimamente en el modelo de recuperación optimizado para cargas masivas de registros (y en el modelo de recuperación simple, excepto cuando se está ejecutando una copia de seguridad).  
  
> [!NOTE]  
>  Las tablas optimizadas para memoria no admiten el registro mínimo.  
  
> [!NOTE]  
>  Con el modelo de recuperación completa, todas las operaciones masivas se registran completamente. Sin embargo, puede usar el registro mínimo en un conjunto de operaciones masivas cambiando la base de datos temporalmente al modelo de recuperación optimizado para cargas masivas de registros para este tipo de operaciones. El registro mínimo resulta más eficaz que el registro completo y reduce la posibilidad de que una operación masiva a gran escala termine por ocupar todo el espacio del registro de transacciones durante una transacción masiva. Sin embargo, si la base de datos se daña o se pierde cuando el registro mínimo está activo, no se podrá recuperar la base de datos hasta el momento del error.  
  
 Las operaciones siguientes, que se registran completamente en el modelo de recuperación completa, se registran mínimamente en el modelo de recuperación simple y en el optimizado para cargas masivas de registros:  
  
-   Operaciones de importación en bloque ([bcp](../../tools/bcp-utility.md), [BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql) e [INSERT... SELECT](/sql/t-sql/statements/insert-transact-sql)). Para obtener más información sobre cuándo se registra mínimamente una importación masiva en una tabla, vea [Prerequisites for Minimal Logging in Bulk Import](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
    > [!NOTE]  
    >  Cuando la replicación transaccional está habilitada, las operaciones BULK INSERT se registran por completo en el modelo de recuperación optimizado para cargas masivas de registros.  
  
-   Operaciones SELECT [INTO](/sql/t-sql/queries/select-into-clause-transact-sql) .  
  
    > [!NOTE]  
    >  Cuando la replicación transaccional está habilitada, las operaciones SELECT INTO se registran por completo en el modelo de recuperación optimizado para cargas masivas de registros.  
  
-   Actualizaciones parciales de tipos de datos de valores grandes que usan la cláusula .WRITE de la instrucción [UPDATE](/sql/t-sql/queries/update-transact-sql) al insertar o anexar datos nuevos. Tenga en cuenta que el registro mínimo no se utiliza cuando se actualizan valores existentes. Para obtener más información sobre los tipos de datos de valores grandes, vea [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
-   [WRITETEXT](/sql/t-sql/queries/writetext-transact-sql) y [UPDATETEXT](/sql/t-sql/queries/updatetext-transact-sql) instrucciones al insertar o anexar datos nuevos en el `text`, `ntext`, y `image` columnas de tipo de datos. Tenga en cuenta que el registro mínimo no se utiliza cuando se actualizan valores existentes.  
  
    > [!NOTE]  
    >  Las instrucciones WRITETEXT y UPDATETEXT han quedado desusadas, por lo que debería evitar utilizarlas en las aplicaciones nuevas.  
  
-   Si la base de datos está establecida en el modelo de recuperación optimizado para cargas masivas de registros o simple, algunas operaciones DDL de índices se registran mínimamente con independencia de si la operación se ejecuta sin conexión o con conexión. Las operaciones de índice con registro mínimo son:  
  
    -   Operaciones[CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) (incluidas las vistas indexadas).  
  
    -   Operaciones[ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql) REBUILD o DBCC DBREINDEX.  
  
        > [!NOTE]  
        >  La instrucción DBCC DBREINDEX ha quedado desusada, por lo que debería evitar utilizarla en las aplicaciones nuevas.  
  
    -   Regeneración del nuevo montón DROP INDEX (si procede).  
  
        > [!NOTE]  
        >  La desasignación de páginas de índice durante una operación [DROP INDEX](/sql/t-sql/statements/drop-index-transact-sql) siempre se registra completamente.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 `Managing the transaction log`  
  
-   [Administrar el tamaño del archivo de registro de transacciones](manage-the-size-of-the-transaction-log-file.md)  
  
-   [Solucionar problemas de un registro de transacciones lleno &#40;Error 9002 de SQL Server&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
 **Realizar copia de seguridad de un registro de transacciones (modelo de recuperación completa)**  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **Restaurar el registro de transacciones (modelo de recuperación completa)**  
  
-  [Restaurar una copia de seguridad del registro de transacciones](../backup-restore/restore-a-transaction-log-backup-sql-server.md)   
  
## <a name="see-also"></a>Vea también  
 [Controlar la durabilidad de las transacciones](control-transaction-durability.md)   
 [Requisitos previos para el registro mínimo durante la importación en bloque](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Puntos de comprobación de base de datos &#40;SQL Server&#41;](database-checkpoints-sql-server.md)   
 [Ver o cambiar las propiedades de una base de datos](../databases/view-or-change-the-properties-of-a-database.md)   
 [Modelos de recuperación &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)  
  
  
