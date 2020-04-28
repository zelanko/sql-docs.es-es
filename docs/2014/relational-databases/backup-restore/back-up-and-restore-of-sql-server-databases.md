---
title: Realizar copias de seguridad y restaurar bases de datos de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], see restoring [SQL Server]
- backups [SQL Server]
- restoring databases [SQL Server]
- backup [SQL Server], see backing up [SQL Server]
- databases [SQL Server], restoring
- backing up databases [SQL Server]
- restore [SQL Server], see restoring [SQL Server]
- disaster recovery [SQL Server], see backing up [SQL Server]
- backing up [SQL Server]
- Database Engine [SQL Server], backups
- databases [SQL Server], backups
ms.assetid: 570a21b3-ad29-44a9-aa70-deb2fbd34f27
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a94ec756e86cb814d0e3b3f624b4a9b3eb180533
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "70176026"
---
# <a name="back-up-and-restore-of-sql-server-databases"></a>Realizar copias de seguridad y restaurar bases de datos de SQL Server
  Este tema describe las ventajas de realizar copias de seguridad de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , los términos de copias de seguridad y restauración básicos, y presenta las estrategias de copias de seguridad y restauración para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , así como consideraciones de seguridad para las copias de seguridad y restauración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 El componente de copias de seguridad y restauración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece una protección esencial para los datos críticos almacenados en las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para minimizar el riesgo de una pérdida de datos catastrófica, debe realizar de forma periódica copias de seguridad de las bases de datos para conservar las modificaciones realizadas en los datos. Una estrategia bien diseñada de copia de seguridad y restauración le ayuda a proteger las bases de datos frente a la pérdida de datos provocada por diversos errores. Pruebe su estrategia con la restauración de un conjunto de copias de seguridad y, después, recupere la base de datos para prepararse para dar una respuesta eficaz en caso de desastre.  
  
 Además del almacenamiento local para almacenar las copias de seguridad, SQL Server también admite la copia de seguridad y la restauración en el servicio Azure Blob Storage. Para obtener más información, vea [Copia de seguridad y restauración de SQL Server con el servicio Azure Blob Storage](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  

  
##  <a name="benefits"></a><a name="Benefits"></a>Privilegios  
  
-   La copia de seguridad de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la ejecución de procedimientos de restauración de prueba de las copias de seguridad y el almacenamiento de las copias en una ubicación segura y fuera del sitio contribuyen a protegerse ante una pérdida de datos catastrófica.  
  
    > [!IMPORTANT]  
    >  Esta es la única forma de proteger de forma confiable los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Con las copias de seguridad válidas de una base de datos puede recuperar los datos en caso de que se produzcan errores, por ejemplo:  
  
    -   Errores de medios.  
  
    -   Errores de usuario, por ejemplo, quitar una tabla por error.  
  
    -   Errores de hardware, por ejemplo, una unidad de disco dañada o la pérdida permanente de un servidor.  
  
    -   Desastres naturales. El uso de la copia de seguridad de SQL Server en el servicio Azure Blob Storage le permite crear una copia de seguridad externa en una región diferente de la ubicación local, con lo que podrá utilizarla en caso de que un desastre natural afecte a su ubicación.  
  
-   Además, las copias de seguridad de una base de datos son útiles para fines administrativos habituales, como copiar una base de datos de un servidor a otro, configurar [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] o la creación de reflejo de la base de datos y el archivo.  
  

  
##  <a name="components-and-concepts"></a><a name="TermsAndDefinitions"></a> Componentes y conceptos  
 realizar copia de seguridad [verbo]  
 Copia los datos o las entradas de registro de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o de su registro de transacciones en un dispositivo de copia de seguridad, como un disco, para crear una copia de seguridad de datos o de registros.  
  
 copia de seguridad [nombre]  
 Copia de los datos que se puede usar para restaurar y recuperar los datos después de un error. Las copias de seguridad de una base de datos también se pueden usar para restaurar una copia de la base de datos en una nueva ubicación.  
  
 dispositivo de copia de seguridad  
 Disco o dispositivo de cinta en el que se escriben las copias de seguridad de SQL Server del que se pueden restaurar. Las copias de seguridad de SQL Server también se pueden escribir en un servicio Azure Blob Storage, y el formato de **URL** se usa para especificar el destino y el nombre del archivo de copia de seguridad. Para obtener más información, vea [Copia de seguridad y restauración de SQL Server con el servicio Azure Blob Storage](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 medio de copia de seguridad  
 Una o varias cintas o archivos de disco en los que se han escrito una o varias copias de seguridad.  
  
 copia de seguridad de datos  
 Copia de seguridad de datos en una base de datos completa (copia de seguridad de base de datos), una base de datos parcial (copia de seguridad parcial) o un conjunto de archivos de datos o grupos de archivos (copia de seguridad de archivos).  
  
 copia de seguridad de base de datos  
 Copia de seguridad de una base de datos. Las copias de seguridad completas representan la base de datos completa en el momento en que finalizó la copia de seguridad. Las copias de seguridad diferenciales solo contienen los cambios realizados en la base de datos desde la copia de seguridad completa más reciente.  
  
 copia de seguridad diferencial  
 Copia de seguridad de datos basada en la última copia de seguridad completa de una base de datos completa o parcial o de un conjunto de archivos de datos o grupos de archivos (base diferencial) y que solo incluye los datos que han cambiado desde dicha base.  
  
 copia de seguridad completa  
 Copia de seguridad completa que incluye todos los datos de una base de datos determinada o un conjunto de grupos de archivos o archivos, así como una cantidad suficiente del registro como para permitir la recuperación de datos.  
  
 copia de seguridad de registros  
 Copia de seguridad de los registros de transacciones que incluye todos los registros no guardados en una copia de seguridad de registros anterior. (modelo de recuperación completa)  
  
 recover  
 Devolver una base de datos a un estado estable y coherente.  
  
 recovery  
 Fase de inicio de una base de datos o de una restauración con recuperación que pone la base de datos en un estado de transacción coherente.  
  
 modelo de recuperación  
 Propiedad de la base de datos que controla el mantenimiento del registro de transacciones de una base de datos. Existen tres modelos de recuperación: simple, completa y por medio de registros de operaciones masivas. El modelo de recuperación de la base de datos determina sus requisitos de copias de seguridad y restauración.  
  
 Restauración  
 Proceso de varias fases que copia todos los datos y páginas del registro desde una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada a una base de datos especificada y, a continuación, pone al día todas las transacciones registradas en la copia de seguridad mediante la aplicación de los cambios registrados para poner los datos al día.  
  

  
##  <a name="introduction-to-backup-and-restore-strategies"></a><a name="BnrStrategies"></a>Introducción a las estrategias de copia de seguridad y restauración  
 Las operaciones de copia de seguridad y restauración deben personalizarse para un entorno concreto y funcionar con los recursos disponibles. Por tanto, un uso confiable del proceso de copia de seguridad y restauración para la recuperación de datos requiere una estrategia de copia de seguridad y restauración. Una estrategia bien diseñada maximiza la disponibilidad de los datos y minimiza la pérdida de los mismos, teniendo en cuenta los requisitos concretos de su empresa.  
  
> [!IMPORTANT]  
>  Coloque la base de datos y las copias de seguridad en dispositivos separados. De lo contrario, si se produce un error en el dispositivo que contiene la base de datos, las copias de seguridad no estarán disponibles. El hecho de colocar la base de datos y las copias de seguridad en dispositivos separados también mejora el rendimiento de E/S de la escritura de las copias de seguridad y el uso para producción de la base de datos.  
  
 Una estrategia de copia de seguridad y restauración contiene una parte de copia de seguridad y una parte de restauración. La parte de copia de seguridad de la estrategia define el tipo y la frecuencia de las copias de seguridad, la naturaleza y la velocidad del hardware necesario, cómo se prueban las copias de seguridad, y dónde y cómo se almacenan los medios de copia de seguridad (incluidas las consideraciones de seguridad). La parte de restauración de la estrategia define quién es responsable de llevar a cabo las operaciones de restauración y cómo se deben realizar para satisfacer sus objetivos de disponibilidad de la base de datos y minimizar la pérdida de datos. Se recomienda documentar los procedimientos de copia de seguridad y restauración, y mantener una copia de la documentación en su libro de documentación de procesos.  
  
 Diseñar una estrategia de copia de seguridad y restauración eficaz requiere mucho cuidado en el planeamiento, la implementación y las pruebas. Es necesario realizar pruebas. No tendrá una estrategia de copia de seguridad hasta que haya restaurado correctamente las copias de seguridad en todas las combinaciones incluidas en su estrategia de restauración. Debe tener en cuenta varios factores. Entre ellas se incluyen las siguientes:  
  
-   Los objetivos de producción de la organización para las bases de datos, especialmente los requisitos de disponibilidad y protección de datos frente a pérdidas.  
  
-   La naturaleza de cada una de las bases de datos: el tamaño, los patrones de uso, la naturaleza del contenido, los requisitos de los datos, etc.  
  
-   Restricciones de los recursos, como hardware, personal, espacio para almacenar los medios de copia de seguridad, seguridad física de los medios almacenados, etc.  
  
    > [!NOTE]  
    >  El formato de almacenamiento en disco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el mismo en los entornos de 64 bits y 32 bits. Por lo tanto, la operación de copia de seguridad y restauración funciona en entornos de 32 bits y de 64 bits. Una copia de seguridad creada en una instancia del servidor que se ejecute en un entorno puede restaurarse en una instancia del servidor que se ejecute en otro entorno.  
  

  
### <a name="impact-of-the-recovery-model-on-backup-and-restore"></a>Impacto del modelo de recuperación en copias de seguridad y restauración  
 Las operaciones de copias de seguridad y restauración se producen en el contexto de un modelo de recuperación. El modelo de recuperación es una propiedad de la base de datos que controla la forma en que se administra el registro de transacciones. Además, el modelo de recuperación de una base de datos determina qué tipos de copias de seguridad y qué escenarios de restauración se admiten para la base de datos. Normalmente, en las bases de datos se usa el modelo de recuperación simple o el modelo de recuperación completa. El modelo de recuperación completa puede complementarse cambiando al modelo de recuperación optimizado para cargas masivas de registros antes de las operaciones masivas. Para ver una introducción sobre estos modelos de recuperación y cómo afectan a la administración del registro de transacciones, vea [El registro de transacciones &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md).  
  
 La mejor elección de modelo de recuperación para la base de datos depende de sus requisitos empresariales. Para evitar la administración del registro de transacciones y simplificar la realización de copias de seguridad y restauración, utilice el modelo de recuperación simple. Para minimizar el riesgo de pérdida de trabajo, a costa de una sobrecarga de trabajo administrativo, utilice el modelo de recuperación completa. Para obtener información sobre el efecto de los modelos de recuperación en las copias de seguridad y restauración, vea [Información general de copia de seguridad &#40;SQL Server&#41;](backup-overview-sql-server.md).  
  
### <a name="design-the-backup-strategy"></a>Diseñar la estrategia de copias de seguridad  
 Una vez seleccionado un modelo de recuperación que cumpla los requisitos de su empresa para una base de datos específica, debe planear e implementar una estrategia de copias de seguridad. La estrategia de copias de seguridad óptima depende de distintos factores, de entre los cuales destacan los siguientes:  
  
-   ¿Cuántas horas al día requieren las aplicaciones acceso a la base de datos?  
  
     Si prevé un período de poca actividad, se recomienda programar las copias de seguridad de bases de datos completas en dicho período.  
  
-   ¿Cuál es la probabilidad de que se produzcan cambios y actualizaciones?  
  
     Si se realizan cambios frecuentes, tenga en cuenta los siguientes aspectos:  
  
    -   Con el modelo de recuperación simple, considere la posibilidad de programar copias de seguridad diferenciales entre copias de seguridad de bases de datos completas. Una copia de seguridad diferencial solo incluye los cambios desde la última copia de seguridad de base de datos completa.  
  
    -   Con el modelo de recuperación completa, debe programar copias de seguridad de registros frecuentes. La programación de copias de seguridad diferenciales entre copias de seguridad completas puede reducir el tiempo de restauración al disminuir el número de copias de seguridad del registro que se deben restaurar después de restaurar los datos.  
  
-   ¿Es probable que los cambios tengan lugar solo en una pequeña parte de la base de datos o en una grande?  
  
     Para una base de datos grande en la que los cambios se concentran en una parte de los archivos o grupos de archivos, las copias de seguridad parciales o de archivos pueden ser útiles. Para obtener más información, vea [Copias de seguridad parciales &#40;SQL Server&#41;](partial-backups-sql-server.md) y [Copias de seguridad de archivos completas &#40;SQL Server&#41;](full-file-backups-sql-server.md).  
  
-   ¿Cuánto espacio en disco necesitará una copia de seguridad completa de la base de datos?  
  
     Para obtener más información, vea [Calcular el tamaño de una copia de seguridad completa de base de datos](#EstimateDbBuSize) más adelante en este tema.  
  
####  <a name="estimate-the-size-of-a-full-database-backup"></a><a name="EstimateDbBuSize"></a>Calcular el tamaño de una copia de seguridad completa de la base de datos  
 Antes de implementar una estrategia de copias de seguridad y restauración, es necesario calcular cuánto espacio en disco usará la copia de seguridad completa. La operación de copia de seguridad copia los datos de la base de datos a un archivo de copia de seguridad. La copia de seguridad contiene solo los datos reales de la base de datos y no el espacio no utilizado. Por tanto, la copia de seguridad es normalmente más pequeña que la propia base de datos. Para calcular el tamaño de la copia de seguridad completa de la base de datos, use el procedimiento almacenado del sistema **sp_spaceused** . Para obtener más información, vea [sp_spaceused &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql).  
  
### <a name="schedule-backups"></a>Programar copias de seguridad  
 La realización de una operación de copia de seguridad tiene un efecto mínimo en las transacciones que se están ejecutando, por lo que se puede efectuar al mismo tiempo que otras operaciones periódicas. Puede realizar una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un efecto mínimo en las cargas de trabajo de producción.  
  
> [!NOTE]  
>  Para obtener información sobre las restricciones de simultaneidad durante la copia de seguridad, vea [Información general de copia de seguridad &#40;SQL Server&#41;](backup-overview-sql-server.md).  
  
 Una vez decididos los tipos de copias de seguridad necesarios y la frecuencia de realización de cada tipo de copia, se recomienda programar copias de seguridad regulares como parte de un plan de mantenimiento de la base de datos. Para obtener información acerca de los planes de mantenimiento y de cómo crearlos para las copias de seguridad de bases de datos y las copias de seguridad de registros, vea [Use the Maintenance Plan Wizard](../maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
### <a name="test-your-backups"></a>Comprobar las copias de seguridad  
 No tendrá una estrategia de restauración hasta que compruebe las copias de seguridad. Es muy importante comprobar cuidadosamente la estrategia de copia de seguridad de cada una de las bases de datos restaurando una copia de la base de datos en un sistema de prueba. Debe comprobar la restauración de cada tipo de copia de seguridad que pretenda utilizar.  
  
 Se recomienda mantener un manual de operaciones para cada base de datos. Este manual de operaciones debe documentar la ubicación de las copias de seguridad, los nombres de dispositivos de copia de seguridad (si los hay) y el tiempo necesario para restaurar las copias de seguridad de prueba.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
  
### <a name="scheduling-backup-jobs"></a>Programar trabajos de copia de seguridad  
  
-   [Crear un plan de mantenimiento](../maintenance-plans/create-a-maintenance-plan.md)  
  
-   [Crear un trabajo](../../ssms/agent/create-a-job.md)  
  
-   [Programar un trabajo](../../ssms/agent/schedule-a-job.md)  
  
### <a name="working-with-backup-devices-and-backup-media"></a>Trabajar con dispositivos de copia de seguridad y medios de copia de seguridad  
  
-   [Definir un dispositivo lógico de copia de seguridad para un archivo de disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Especificar un disco o una cinta como destino de copia de seguridad &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Eliminar un dispositivo de copia de seguridad &#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
-   [Establecer la fecha de expiración de una copia de seguridad &#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Ver el contenido de una cinta o un archivo de copia de seguridad &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Ver los archivos de datos y de registro en un conjunto de copia de seguridad &#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Restaurar una copia de seguridad desde un dispositivo &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
### <a name="creating-backups"></a>Crear copias de seguridad  
  
> [!NOTE]  
>  En el caso de copias de seguridad parciales o de solo copia, debe usar la instrucción [BACKUP](/sql/t-sql/statements/backup-transact-sql) de [!INCLUDE[tsql](../../includes/tsql-md.md)] con la opción PARTIAL o COPY_ONLY, respectivamente.  
  
 **Usar SQL Server Management Studio**  
  
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [Realizar copias de seguridad de archivos y grupos de archivos &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
 **Usar Transact-SQL**  
  
-   [Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad &#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [Realizar una copia de seguridad del registro de transacciones cuando la base de datos está dañada &#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [Habilitar o deshabilitar sumas de comprobación de copia de seguridad durante copia de seguridad o restauración &#40;SQL Server&#41;](enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [Especificar si una operación de copia de seguridad o restauración continúa o se detiene después de encontrar un error &#40;SQL Server&#41;](specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  

  
### <a name="restoring-data-backups"></a>Restaurar copias de seguridad de datos  
 **Usar SQL Server Management Studio**  
  
-   [Restaurar una copia de seguridad de base de datos &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
-   [Restaurar una copia de seguridad diferencial de la base de datos &#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)  
  
-   [Restaurar archivos y grupos de archivos &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
 **Usar Transact-SQL**  
  
-   [Restaurar una copia de seguridad de base de datos en el modelo de recuperación simple &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Restaurar una base de datos según el punto de error en el modelo de recuperación completa &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar archivos y grupos de archivos en archivos existentes &#40;SQL Server&#41;](restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Restaurar archivos en una nueva ubicación &#40;SQL Server&#41;](restore-files-to-a-new-location-sql-server.md)  
  
-   [Restaurar la base de datos maestra &#40;Transact-SQL&#41;](restore-the-master-database-transact-sql.md)  
  

  
### <a name="restoring-transaction-logs-full-recovery-model"></a>Restaurar registros de transacciones (modelo de recuperación completa)  
 **Usar SQL Server Management Studio**  
  
-   [Restaurar una base de datos en una transacción marcada &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Restaurar una copia de seguridad de registros de transacciones &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
-   [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
 **Usar Transact-SQL**  
  
-   [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  

  
### <a name="additional-restore-tasks"></a>Tareas adicionales de restauración  
 **Usar Transact-SQL**  
  
-   [Reiniciar una operación de restauración interrumpida &#40;Transact-SQL&#41;](restart-an-interrupted-restore-operation-transact-sql.md)  
  
-   [Recuperar una base de datos sin restaurar los datos &#40;Transact-SQL&#41;](recover-a-database-without-restoring-data-transact-sql.md)  
  

  
## <a name="see-also"></a>Consulte también  
 [Información general de copia de seguridad &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)   
 [Realizar copias de seguridad de los catálogos de texto completo y restaurarlos](../search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [Hacer copias de seguridad y restaurar bases de datos replicadas](../replication/administration/back-up-and-restore-replicated-databases.md)   
 [El registro de transacciones &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [Modelos de recuperación &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
