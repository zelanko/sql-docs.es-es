---
title: Actualizar el trasvase de registros a SQL Server 2014 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], upgrading
ms.assetid: b1289cc3-f5be-40bb-8801-0e3eed40336e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 19eae2e3ace3859d61048536be9b70bf58ad66f5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775422"
---
# <a name="upgrade-log-shipping-to-sql-server-2014-transact-sql"></a>Actualizar el trasvase de registros a SQL Server 2014 (Transact-SQL)
  Es posible conservar las configuraciones de trasvase de registros al actualizar de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. En este tema se describen escenarios alternativos y prácticas recomendadas para actualizar la configuración de trasvase de registros.  
  
> [!NOTE]  
>  La[compresión de copia de seguridad](../../relational-databases/backup-restore/backup-compression-sql-server.md) se incluyó en [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]. Una configuración de trasvase de registros actualizada usa la opción de configuración de nivel de seguridad **Compresión de copia de seguridad predeterminada** para controlar si se emplea la compresión de copia de seguridad para los archivos de copia de seguridad del registro de transacciones. El comportamiento de la compresión de las copias de seguridad de registros se puede especificar para cada configuración de trasvase de registros. Para obtener más información, vea [Configurar el trasvase de registros &#40;SQL Server&#41;](configure-log-shipping-sql-server.md).  
  
  
##  <a name="ProtectData"></a> Proteger los datos antes de la actualización  
 Como práctica recomendada, es aconsejable que proteja sus datos antes de realizar una actualización del trasvase de registros.  
  
 **Para proteger los datos**  
  
1.  Realice una copia de seguridad completa de cada base de datos principal.  
  
     Para obtener más información, vea [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
2.  Ejecute el comando [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) en cada base de datos principal.  
  
##  <a name="UpgradeMonitor"></a> Actualizar la instancia de servidor de supervisión  
 La instancia del servidor de supervisión, si existe, se puede actualizar en cualquier momento.  
  
 Mientras se actualiza el servidor de supervisión, la configuración de trasvase de registros continúa funcionando, pero su estado no se registra en las tablas del monitor. Cualquier alerta que se haya configurado no se desencadenará mientras el servidor de supervisión se esté actualizando. Después de la actualización, puede actualizar la información de las tablas del monitor ejecutando el procedimiento almacenado del sistema [sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql).  
  
##  <a name="UpgradeSingleSecondary"></a> Actualizar las configuraciones con un único servidor secundario de trasvase de registros  
 El proceso de actualización descrito en esta sección supone una configuración que consta del servidor principal y de un único servidor secundario. Esta configuración se representa en la ilustración siguiente, que muestra una instancia del servidor principal, A, y una única instancia del servidor secundario, B.  
  
 ![Un servidor secundario y ningún servidor supervisor](../media/ls-2-wayconfig-nomonitor.gif "un servidor secundario y ningún servidor supervisor")  
  
 Para obtener información sobre cómo actualizar varios servidores secundarios, vea [Actualizar varias instancias de servidores secundarios](#MultipleSecondaries), más adelante en este tema.  
 
  
###  <a name="UpgradeSecondary"></a> Actualizar la instancia del servidor secundario  
 El proceso de actualización implica actualizar las instancias de los servidores secundarios de una configuración de trasvase de registros de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] antes de actualizar la instancia del servidor principal. Actualice siempre la instancia del servidor secundario en primer lugar. Si el servidor principal se actualizara antes que un servidor secundario, se produciría un error en el trasvase de registros porque una copia de seguridad creada en una versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede restaurar en una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El trasvase de registros continúa a lo largo del proceso de actualización porque los servidores secundarios actualizados continúan restaurando las copias de seguridad de registros a partir del servidor principal de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versiones posteriores. El proceso para actualizar las instancias de los servidores secundarios depende en parte de si la configuración de trasvase de registros posee varios servidores secundarios. Para obtener más información, vea [Actualizar varias instancias del servidor secundario](#MultipleSecondaries), posteriormente en este tema.  
  
 Mientras se actualiza la instancia del servidor secundario, no se ejecutan los trabajos de copia y restauración del trasvase de registros, por lo que se acumularán las copias de seguridad de registros de transacciones sin restaurar. El grado de acumulación depende de la frecuencia de la copia de seguridad programada en el servidor principal. Además, si se ha configurado un servidor de supervisión independiente, se podrían generar alertas que indiquen que no se han realizado restauraciones durante más tiempo que el intervalo configurado.  
  
 Una vez actualizado el servidor secundario, los trabajos de los agentes de trasvase de registros se reanudan y continúan copiando y restaurando las copias de seguridad de registros a partir de la instancia del servidor principal, el servidor A. La cantidad de tiempo requerida para que el servidor secundario ponga al día la base de datos secundaria varía, dependiendo del tiempo que se tarde en actualizar el servidor secundario y la frecuencia de las copias de seguridad en el servidor principal.  
  
> [!NOTE]  
>  Durante la actualización del servidor, la base de datos secundaria no se actualiza a una base de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Solo se actualizará si se pone en conexión.  
  
> [!IMPORTANT]  
>  La opción RESTORE WITH STANDBY no se admite para una base de datos que requiere actualizarse. Si una base de datos secundaria actualizada se ha configurado utilizando RESTORE WITH STANDBY, los registros de transacciones ya no se pueden restaurar después de la actualización. Para reanudar el trasvase de registros en esa base de datos secundaria, tendrá que configurarlo de nuevo en ese servidor de reserva. Para obtener más información acerca de la opción STANDBY, vea [argumentos de RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql).  
  
###  <a name="UpgradePrimary"></a> Actualizar la instancia del servidor principal  
 Al planear una actualización, es importante tener en cuenta la cantidad de tiempo que la base de datos dejará de estar disponible. El escenario de actualización más sencillo implica que la base de datos no esté disponible mientras se actualiza el servidor principal (escenario 1, a continuación).  
  
 A costa de un proceso de actualización más complicado, puede obtener la máxima disponibilidad de la base de datos conmutando por error el servidor principal de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior al servidor secundario de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] antes de actualizar el servidor principal original (escenario 2, a continuación). Hay dos variantes del escenario de conmutación por error. Puede volver al servidor principal original y mantener la configuración de trasvase de registros original. O bien, puede quitar la configuración de trasvase de registros original antes de actualizar el servidor principal original y después crear una configuración nueva usando el servidor principal nuevo. En esta sección se describen ambos escenarios.  
  
> [!IMPORTANT]  
>  Asegúrese de actualizar la instancia del servidor secundario antes de actualizar la instancia del servidor principal. Para obtener más información, vea [Actualizar la instancia del servidor secundario](#UpgradeSecondary), anteriormente en este tema.  
  
  
####  <a name="Scenario1"></a> Escenario 1: Actualizar la instancia del servidor principal sin conmutación por error  
 Este es el escenario más sencillo, pero ocasiona más tiempo de inactividad que la conmutación por error. Simplemente se actualiza la instancia del servidor principal y la base de datos no está disponible durante la actualización.  
  
 Una vez actualizado el servidor, la base de datos se vuelve a poner en línea automáticamente, lo que hace que se actualice. Una vez actualizada la base de datos, los trabajos de trasvase de registros se reanudan.  
  
#### <a name="scenario-2-upgrade-primary-server-instance-with-failover"></a>Escenario 2: Actualizar la instancia del servidor principal con conmutación por error  
 En este escenario se obtiene la máxima disponibilidad y se reduce al mínimo el tiempo de inactividad. Utiliza una conmutación por error controlada a la instancia del servidor secundario, lo que mantiene la base de datos disponible mientras se actualiza la instancia del servidor principal original. El tiempo de inactividad se limita al tiempo relativamente corto que se requiere para la conmutación por error, en lugar del tiempo exigido para actualizar la instancia del servidor principal.  
  
 Actualizar la instancia del servidor principal con conmutación por error implica tres procedimientos generales: realizar una conmutación por error controlada al servidor secundario, actualizar la instancia del servidor principal original a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]y configurar el trasvase de registros en una instancia del servidor principal de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Estos procedimientos se describen en esta sección.  
  
> [!IMPORTANT]  
>  Si piensa tener la instancia del servidor secundario como instancia del nuevo servidor principal, tiene que quitar la configuración de trasvase de registros. Una vez actualizada la instancia del servidor principal original, será preciso reconfigurar el trasvase de registros desde el nuevo servidor principal hasta el nuevo servidor secundario. Para obtener más información, consulte [Quitar trasvase de registros &#40;SQL Server&#41;](remove-log-shipping-sql-server.md).  
  
  
#####  <a name="Procedure1"></a> Procedimiento 1: Realizar una conmutación por error controlada al servidor secundario  
 Conmutación por error controlada al servidor secundario:  
  
1.  Realice manualmente una [copia del final del registro](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) del registro de transacciones en la base de datos principal especificando WITH NORECOVERY. Esta copia de seguridad de registros captura cualquier entrada del registro que todavía no se haya incluido en la copia de seguridad y deja la base de datos sin conexión. Tenga en cuenta que mientras la base de datos esté sin conexión, se producirá un error en el trabajo de copia de seguridad del trasvase de registros.  
  
     En el ejemplo siguiente se crea una copia del final del registro de la base de datos `AdventureWorks` en el servidor principal. El archivo de copia de seguridad se denomina `Failover_AW_20080315.trn`:  
  
    ```  
    BACKUP LOG AdventureWorks   
      TO DISK = N'\\FileServer\LogShipping\AdventureWorks\Failover_AW_20080315.trn'   
       WITH NORECOVERY;  
    GO  
    ```  
  
     Se recomienda que utilice una convención de nomenclatura de archivos distinta para diferenciar el archivo de copia de seguridad creado manualmente de los que crea el trabajo de copia de seguridad de trasvase de registros.  
  
2.  En el servidor secundario:  
  
    1.  Asegúrese de que se han aplicado todas las copias de seguridad realizadas automáticamente por los trabajos de copia de seguridad de trasvase de registros. Para comprobar qué trabajos de copia de seguridad se han aplicado, use el procedimiento almacenado del sistema [sp_help_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql) en el servidor de supervisión o en los servidores principal y secundario. El mismo archivo debe aparecer en las columnas **last_backup_file**, **last_copied_file**y **last_restored_file** . Si alguno de los archivos de copia de seguridad no se ha copiado y restaurado, invoque manualmente los trabajos de restauración y copia del agente para la configuración de trasvase de registros.  
  
         Para obtener información sobre cómo iniciar un trabajo, vea [Start a Job](../../ssms/agent/start-a-job.md).  
  
    2.  Copie el archivo de copia de seguridad del final del registro que creó en el paso 1 desde el recurso compartido de archivos en la ubicación local usada por el trasvase de registros del servidor secundario.  
  
    3.  Restaure la copia de seguridad del final del registro especificando WITH RECOVERY para poner en línea la base de datos. Al ponerse en línea, la base de datos se actualizará a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
         En el ejemplo siguiente se restaura la copia del final del registro de la base de datos `AdventureWorks` en la base de datos secundaria. En el ejemplo se usa la opción WITH RECOVERY, que pone en línea la base de datos:  
  
        ```  
        RESTORE LOG AdventureWorks   
          FROM DISK = N'c:\logshipping\Failover_AW_20080315.trn'   
           WITH RECOVERY;  
        GO  
        ```  
  
        > [!NOTE]  
        >  En una configuración que contenga más de un servidor secundario, hay consideraciones adicionales. Para obtener más información, vea [Actualizar varias instancias del servidor secundario](#MultipleSecondaries), posteriormente en este tema.  
  
    4.  Realice la conmutación por error de la base de datos redirigiendo a los clientes del servidor principal original (servidor A) al servidor secundario (servidor B) en línea.  
  
    5.  Tenga cuidado de que el registro de transacciones de la base de datos secundaria no se llene mientras la base de datos está en línea. Para evitar que el registro de transacciones se llene, puede que sea necesario realizar una copia de seguridad del mismo. En ese caso, se recomienda que ponga la copia de seguridad en una ubicación compartida, un *recurso compartido de copia de seguridad*, de modo que las copias de seguridad estén disponibles para restaurarse en la otra instancia del servidor.  
  
#####  <a name="Procedure2"></a> Procedimiento 2: Actualice la instancia de servidor principal Original a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Después de actualizar la instancia del servidor principal original a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la base de datos todavía estará sin conexión y en el formato.  
  
#####  <a name="Procedure3"></a> Procedimiento 3: Configuración de trasvase de registros en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 El resto del proceso de actualización depende de si el trasvase de registros sigue estando configurado, como se explica a continuación:  
  
-   Si ha conservado la configuración de trasvase de registros de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]o posterior, vuelva a la instancia del servidor principal original. Para obtener más información, vea [Para volver a la instancia del servidor principal original](#SwitchToOrigPrimary), más adelante en esta sección.  
  
-   Si quitó la configuración de trasvase de registros antes de la conmutación por error, cree una nueva configuración de trasvase de registros en la que la instancia del servidor secundario original sea la instancia del nuevo servidor principal. Para obtener más información, vea [Para mantener la instancia del servidor secundario anterior como instancia del nuevo servidor principal](#KeepOldSecondaryAsNewPrimary), posteriormente en esta sección.  
  
######  <a name="SwitchToOrigPrimary"></a> Para volver a la instancia del servidor principal Original  
  
1.  En el servidor principal provisional (servidor B), haga una copia de seguridad del final del registro usando WITH NORECOVERY para crear una copia del final del registro y dejar la base de datos sin conexión. La copia de seguridad del final del registro se denomina `Switchback_AW_20080315.trn`. Por ejemplo:  
  
    ```  
    BACKUP LOG AdventureWorks   
      TO DISK = N'\\FileServer\LogShipping\AdventureWorks\Switchback_AW_20080315.trn'   
       WITH NORECOVERY;  
    GO  
    ```  
  
2.  Si se realizó alguna copia de seguridad de registros de transacciones en la base de datos principal provisional exceptuando la copia de seguridad del final del registro que creó en el paso 1, restaure esas copias de seguridad del registro usando WITH NORECOVERY en la base de datos sin conexión del servidor principal original (servidor A). La base de datos se actualiza al formato de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] cuando se restaura la primera copia de seguridad de registros.  
  
3.  Restaure la copia del final del registro, `Switchback_AW_20080315.trn`, en la base de datos principal original (en servidor A) usando WITH RECOVERY para poner en línea la base de datos.  
  
4.  Conmute por error de nuevo a la base de datos principal original (en el servidor A) redirigiendo a los clientes del servidor secundario en línea al servidor principal original.  
  
 Una vez que la base de datos se ponga en línea, se reanudará la configuración de trasvase de registros original.  
  
######  <a name="KeepOldSecondaryAsNewPrimary"></a> Para mantener la instancia de servidor secundario anterior como la nueva instancia de servidor principal  
 Establezca una nueva configuración de trasvase de registros utilizando la instancia del servidor secundario anterior, B, como servidor principal y la instancia del servidor principal anterior, A, como nuevo servidor secundario, de la forma siguiente:  
  
> [!IMPORTANT]  
>  La configuración de trasvase de registros anterior se debería haber quitado del servidor principal original al principio del proceso, antes de realizar la copia de seguridad manual del registro de transacciones que puso sin conexión la base de datos.  
  
1.  Para evitar realizar una copia de seguridad y restauración completa de la base de datos en el nuevo servidor secundario (servidor A), aplique las copias de seguridad de registros desde la nueva base de datos principal hasta la nueva base de datos secundaria. En la configuración del ejemplo, esto implica restaurar las copias de seguridad de registros tomadas en el servidor B a la base de datos del servidor A.  
  
2.  Haga una copia de seguridad de registros desde la nueva base de datos principal (en el servidor B).  
  
3.  Restaure las copias de seguridad de registros en la instancia del nuevo servidor secundario (servidor A) usando WITH NORECOVERY. La primera operación de restauración actualiza la base de datos a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
4.  Configure el trasvase de registros con el servidor secundario antiguo (servidor B) como instancia del servidor principal.  
  
    > [!IMPORTANT]  
    >  Si usa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], especifique que la base de datos secundaria ya está inicializada.  
  
     Para obtener más información, vea [Configurar el trasvase de registros &#40;SQL Server&#41;](configure-log-shipping-sql-server.md).  
  
5.  Realice la conmutación por error de la base de datos redirigiendo a los clientes del servidor principal original (servidor A) al servidor secundario (servidor B) en línea.  
  
    > [!IMPORTANT]  
    >  Cuando realice la conmutación por error a una nueva base de datos primaria, debe asegurarse de que sus metadatos sean coherentes con los de la base de datos principal original. Para obtener más información, vea [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
##  <a name="MultipleSecondaries"></a> Actualizar varias instancias del servidor secundario  
 Esta configuración se representa en la ilustración siguiente, que muestra una instancia del servidor principal, A, y dos instancias de servidores secundarios, B y C.  
  
 ![Dos servidores secundarios y ningún servidor supervisor](../media/ls-3-wayconfig-nomonitor.gif "dos servidores secundarios y ningún servidor supervisor")  
  
 En esta sección se explica cómo actualizar con una conmutación por error y después volver al servidor principal original. Al actualizar la instancia principal con conmutación por error, el proceso es más complejo si hay varias instancias de servidores secundarios. En el procedimiento siguiente, una vez actualizados todos los servidores secundarios, el servidor principal conmuta por error a una de las bases de datos secundarias actualizadas. Se actualiza el servidor principal original y el trasvase de registros conmuta por error a él.  
  
> [!IMPORTANT]  
>  Actualice siempre todas las instancias de los servidores secundarios antes de actualizar el servidor principal.  
  
 **Para actualizar mediante una conmutación por error y volver al servidor principal original**  
  
1.  Actualice todas las instancias de los servidores secundarios (servidor B y servidor C).  
  
2.  Obtenga el final del registro de transacciones de la base de datos principal (en el servidor A) y ponga la base de datos sin conexión, haciendo una copia de seguridad de registros de transacciones usando WITH NORECOVERY.  
  
3.  En el servidor secundario hacia el que planea realizar la conmutación por error (servidor B), ponga la base de datos secundaria en línea, restaurando la copia de seguridad de registros usando WITH RECOVERY.  
  
4.  En el otro servidor secundario (servidor C), deje la base de datos secundaria sin conexión restaurando la copia de seguridad de registros usando WITH NORECOVERY.  
  
    > [!NOTE]  
    >  Los trabajos de copia y restauración del trasvase de registros y se ejecutarán en los servidores secundarios, pero no harán nada porque los nuevos archivos de copia de seguridad de registros no se colocarán en el recurso compartido de copia de seguridad.  
  
5.  Realice la conmutación por error de la base de datos redirigiendo a los clientes del servidor principal original (servidor A) al servidor secundario (servidor B) en línea. La base de datos en línea se convierte en el servidor principal provisional y se mantiene disponible mientras el servidor principal original está sin conexión (servidor A).  
  
6.  Actualice el servidor principal original (servidor A).  
  
7.  Error en la principal base de datos provisional (en el servidor B), manualmente la base de datos realizar copias de seguridad del registro de transacciones usando WITH NORECOVERY. De esta forma se deja la base de datos sin conexión.  
  
8.  Restaure todas las copias de seguridad de registros de transacciones que creó en la base de datos principal provisional (en el servidor B) en la otra base de datos secundaria (en el servidor C) usando WITH NORECOVERY. Esto permite al trasvase de registros continuar a partir de la base de datos principal original después de su actualización, sin requerir una restauración de la base de datos completa en cada base de datos secundaria.  
  
9. Restaure el registro de transacciones a partir del servidor principal provisional (servidor B) en la base de datos principal original (en el servidor A) usando WITH RECOVERY.  
  
##  <a name="Redeploying"></a> Volver a implementar el trasvase de registros  
 Si no desea migrar la configuración de trasvase de registros mediante uno de los procedimientos antes indicados, puede volver a implementar el trasvase de registros desde el principio reinicializando la base de datos secundaria con una copia de seguridad y restauración completa de la base de datos principal. Esta opción puede ser adecuada si tiene una base de datos pequeña o si no es crucial una alta disponibilidad durante el procedimiento de actualización.  
  
 Para obtener información acerca de cómo habilitar el trasvase de registros, vea [configuración del trasvase de registros &#40;SQL Server&#41;](configure-log-shipping-sql-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Tablas y procedimientos almacenados de trasvase de registros](log-shipping-tables-and-stored-procedures.md)  
