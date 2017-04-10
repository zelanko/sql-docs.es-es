---
title: "Realizar copias de seguridad y restaurar bases de datos de SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "07/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "recuperación ante desastres [SQL Server], ver restauración [SQL Server]"
  - "copias de seguridad [SQL Server]"
  - "restaurar bases de datos [SQL Server]"
  - "copia de seguridad [SQL Server], ver copia de seguridad [SQL Server]"
  - "bases de datos [SQL Server], restaurar"
  - "hacer copia de seguridad de bases de datos [SQL Server]"
  - "restaurar [SQL Server], ver restauración [SQL Server]"
  - "recuperación ante desastres [SQL Server], ver copia de seguridad [SQL Server]"
  - "realizar copias de seguridad [SQL Server]"
  - "Motor de base de datos [SQL Server], copias de seguridad"
  - "bases de datos [SQL Server], copias de seguridad"
ms.assetid: 570a21b3-ad29-44a9-aa70-deb2fbd34f27
caps.latest.revision: 91
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 91
---
# Realizar copias de seguridad y restaurar bases de datos de SQL Server
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tema describe las ventajas de realizar copias de seguridad de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los términos de copias de seguridad y restauración básicos, y presenta las estrategias de copias de seguridad y restauración para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como consideraciones de seguridad para las copias de seguridad y restauración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
> **¿Busca instrucciones detalladas?** En este tema **no se entrega ningún paso específico sobre cómo crear una copia de seguridad**. Si desea obtener información sobre cómo crear una copia de seguridad, desplace esta página hacia abajo hasta la sección de vínculos, los que están organizados por tareas de copia de seguridad y si desea usar SSMS o T-SQL.  
  
 El componente de copia de seguridad y restauración de SQL Server ofrece una protección esencial para los datos críticos almacenados en las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para minimizar el riesgo de pérdida de datos catastrófica, debe realizar copias de seguridad de las bases de datos para conservar las modificaciones en los datos de forma periódica. Una estrategia de copias de seguridad y restauración correctamente planeada contribuye a la protección de las bases de datos de la pérdida de datos derivada de daños causados por diferentes errores. Pruebe la estrategia mediante la restauración de las copias de seguridad y la posterior recuperación de la base de datos para estar preparado y poder responder de forma eficaz ante un desastre.  
  
 Además del almacenamiento local para almacenar las copias de seguridad, SQL Server también admite la copia de seguridad y la restauración en el Servicio de almacenamiento Blob de Windows Azure. Para obtener más información, vea [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). Para archivos de base de datos almacenados mediante el servicio de almacenamiento de blobs de Microsoft Azure, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] proporciona la opción de usar instantáneas de Azure para copias de seguridad casi instantáneas y restauraciones más rápidas. Para obtener más información, vea [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
##  Por qué realizar copias de seguridad  
-   La copia de seguridad de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la ejecución de procedimientos de restauración de prueba de las copias de seguridad y el almacenamiento de las copias en una ubicación segura y fuera del sitio contribuyen a protegerse ante una pérdida de datos catastrófica. **Las copias de seguridad son la única forma de proteger los datos.**

     Con las copias de seguridad válidas de una base de datos puede recuperar los datos en caso de que se produzcan errores, por ejemplo:  
  
    -   Errores de medios.  
  
    -   Errores de usuario, por ejemplo, quitar una tabla por error.  
  
    -   Errores de hardware, por ejemplo, una unidad de disco dañada o la pérdida permanente de un servidor.  
  
    -   Desastres naturales. El uso de la copia de seguridad de SQL Server en el servicio de almacenamiento Blob de Windows Azure le permite crear una copia de seguridad externa en una región diferente de la ubicación local, con lo que podrá utilizarla en caso de que un desastre natural afecte a su ubicación.  
  
-   Además, las copias de seguridad de una base de datos son útiles para fines administrativos habituales, como copiar una base de datos de un servidor a otro, configurar [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] o la creación de reflejo de la base de datos y el archivo.  
  
##  Glosario de términos de copia de seguridad
 **realizar copia de seguridad** [forma verbal]  
 Copia los datos o las entradas de registro de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o de su registro de transacciones en un dispositivo de copia de seguridad, como un disco, para crear una copia de seguridad de datos o de registros.  
  
 **copia de seguridad** [forma nominal]  
 Copia de los datos que se puede usar para restaurar y recuperar los datos después de un error. Las copias de seguridad de una base de datos también se pueden usar para restaurar una copia de la base de datos en una nueva ubicación.  
  
dispositivo de **copia de seguridad**  
 Disco o dispositivo de cinta en el que se escriben las copias de seguridad de SQL Server del que se pueden restaurar. Las copias de seguridad de SQL Server también se pueden escribir en un servicio de Almacenamiento de blobs de Microsoft Azure y el formato de **URL** se usa para especificar el destino y el nombre del archivo de copia de seguridad. Para obtener más información, vea [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
**medio de copia de seguridad**  
 Una o varias cintas o archivos de disco en los que se han escrito una o varias copias de seguridad.  
  
**copia de seguridad de datos**  
 Copia de seguridad de datos en una base de datos completa (copia de seguridad de base de datos), una base de datos parcial (copia de seguridad parcial) o un conjunto de archivos de datos o grupos de archivos (copia de seguridad de archivos).  
  
**copia de seguridad de base de datos**  
 Copia de seguridad de una base de datos. Las copias de seguridad completas representan la base de datos completa en el momento en que finalizó la copia de seguridad. Las copias de seguridad diferenciales solo contienen los cambios realizados en la base de datos desde la copia de seguridad completa más reciente.  
  
**copia de seguridad diferencial**  
 Copia de seguridad de datos basada en la última copia de seguridad completa de una base de datos completa o parcial o de un conjunto de archivos de datos o grupos de archivos (base diferencial) y que solo incluye los datos que han cambiado desde dicha base.  
  
**copia de seguridad completa**  
 Copia de seguridad completa que incluye todos los datos de una base de datos determinada o un conjunto de grupos de archivos o archivos, así como una cantidad suficiente del registro como para permitir la recuperación de datos.  
  
**copia de seguridad de registros**  
 Copia de seguridad de los registros de transacciones que incluye todos los registros no guardados en una copia de seguridad de registros anterior. (modelo de recuperación completa)  
  
**recuperar**  
 Devolver una base de datos a un estado estable y coherente.  
  
**recovery**  
 Fase de inicio de una base de datos o de una restauración con recuperación que pone la base de datos en un estado de transacción coherente.  
  
**modelo de recuperación**  
 Propiedad de la base de datos que controla el mantenimiento del registro de transacciones de una base de datos. Existen tres modelos de recuperación: simple, completa y por medio de registros de operaciones masivas. El modelo de recuperación de la base de datos determina sus requisitos de copias de seguridad y restauración.  
  
**restaurar**  
 Proceso de varias fases que copia todos los datos y páginas del registro desde una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada a una base de datos especificada y, a continuación, pone al día todas las transacciones registradas en la copia de seguridad mediante la aplicación de los cambios registrados para poner los datos al día.  
  
 ##  Estrategias de copias de seguridad y restauración  
 Las operaciones de copia de seguridad y restauración deben personalizarse para un entorno concreto y funcionar con los recursos disponibles. Por tanto, un uso confiable del proceso de copia de seguridad y restauración para la recuperación de datos requiere una estrategia de copia de seguridad y restauración. Una estrategia bien diseñada maximiza la disponibilidad de los datos y minimiza la pérdida de los mismos, teniendo en cuenta los requisitos concretos de su empresa.  
  
#### Importante: 
**Coloque la base de datos y las copias de seguridad en dispositivos separados. De lo contrario, si se produce un error en el dispositivo que contiene la base de datos, las copias de seguridad no estarán disponibles. El hecho de colocar la base de datos y las copias de seguridad en dispositivos separados también mejora el rendimiento de E/S de la escritura de las copias de seguridad y el uso para producción de la base de datos.**  
  
 Una estrategia de copia de seguridad y restauración contiene una parte de copia de seguridad y una parte de restauración. La parte de copia de seguridad de la estrategia define el tipo y la frecuencia de las copias de seguridad, la naturaleza y la velocidad del hardware necesario, cómo se prueban las copias de seguridad, y dónde y cómo se almacenan los medios de copia de seguridad (incluidas las consideraciones de seguridad). La parte de restauración de la estrategia define quién es responsable de llevar a cabo las operaciones de restauración y cómo se deben realizar para satisfacer sus objetivos de disponibilidad de la base de datos y minimizar la pérdida de datos. Se recomienda documentar los procedimientos de copia de seguridad y restauración, y mantener una copia de la documentación en su libro de documentación de procesos.  
  
 Diseñar una estrategia de copia de seguridad y restauración eficaz requiere mucho cuidado en el planeamiento, la implementación y las pruebas. Es necesario realizar pruebas. No tendrá una estrategia de copia de seguridad hasta que haya restaurado correctamente las copias de seguridad en todas las combinaciones incluidas en su estrategia de restauración. Debe tener en cuenta varios factores. Entre ellas, figuran:  
  
-   Los objetivos de producción de la organización para las bases de datos, especialmente los requisitos de disponibilidad y protección de datos frente a pérdidas.  
  
-   La naturaleza de cada una de las bases de datos: el tamaño, los patrones de uso, la naturaleza del contenido, los requisitos de los datos, etc.  
  
-   Restricciones de los recursos, como hardware, personal, espacio para almacenar los medios de copia de seguridad, seguridad física de los medios almacenados, etc.  

### Impacto del modelo de recuperación en copias de seguridad y restauración  
 Las operaciones de copias de seguridad y restauración se producen en el contexto de un modelo de recuperación. El modelo de recuperación es una propiedad de la base de datos que controla la forma en que se administra el registro de transacciones. Además, el modelo de recuperación de una base de datos determina qué tipos de copias de seguridad y qué escenarios de restauración se admiten para la base de datos. Normalmente, en las bases de datos se usa el modelo de recuperación simple o el modelo de recuperación completa. El modelo de recuperación completa puede complementarse cambiando al modelo de recuperación optimizado para cargas masivas de registros antes de las operaciones masivas. Para ver una introducción sobre estos modelos de recuperación y cómo afectan a la administración del registro de transacciones, vea [El registro de transacciones (SQL Server)](https://msdn.microsoft.com/library/ms190925(SQL.130).aspx).  
  
 La mejor elección de modelo de recuperación para la base de datos depende de sus requisitos empresariales. Para evitar la administración del registro de transacciones y simplificar la realización de copias de seguridad y restauración, utilice el modelo de recuperación simple. Para minimizar el riesgo de pérdida de trabajo, a costa de una sobrecarga de trabajo administrativo, utilice el modelo de recuperación completa. Para obtener información sobre el efecto de los modelos de recuperación en las copias de seguridad y restauración, vea [Información general de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
### Diseñar la estrategia de copia de seguridad  
 Una vez seleccionado un modelo de recuperación que cumpla los requisitos de su empresa para una base de datos específica, debe planear e implementar una estrategia de copias de seguridad. La estrategia de copias de seguridad óptima depende de distintos factores, de entre los cuales destacan los siguientes:  
  
-   ¿Cuántas horas al día requieren las aplicaciones acceso a la base de datos?  
  
     Si prevé un período de poca actividad, se recomienda programar las copias de seguridad de bases de datos completas en dicho período.  
  
-   ¿Cuál es la probabilidad de que se produzcan cambios y actualizaciones?  
  
     Si se realizan cambios frecuentes, tenga en cuenta los siguientes aspectos:  
  
    -   Con el modelo de recuperación simple, considere la posibilidad de programar copias de seguridad diferenciales entre copias de seguridad de bases de datos completas. Una copia de seguridad diferencial solo incluye los cambios desde la última copia de seguridad de base de datos completa.  
  
    -   Con el modelo de recuperación completa, debe programar copias de seguridad de registros frecuentes. La programación de copias de seguridad diferenciales entre copias de seguridad completas puede reducir el tiempo de restauración al disminuir el número de copias de seguridad del registro que se deben restaurar después de restaurar los datos.  
  
-   ¿Es probable que los cambios tengan lugar solo en una pequeña parte de la base de datos o en una grande?  
  
     Para una base de datos grande en la que los cambios se concentran en una parte de los archivos o grupos de archivos, las copias de seguridad parciales o de archivos pueden ser útiles. Para obtener más información, vea [Copias de seguridad parciales &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md) y [Copias de seguridad de archivos completas &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md).  
  
-   ¿Cuánto espacio en disco necesitará una copia de seguridad completa de la base de datos?  
  
 ### Calcular el tamaño de una copia de seguridad completa de base de datos  
 Antes de implementar una estrategia de copias de seguridad y restauración, es necesario calcular cuánto espacio en disco usará la copia de seguridad completa. La operación de copia de seguridad copia los datos de la base de datos a un archivo de copia de seguridad. La copia de seguridad contiene solo los datos reales de la base de datos y no el espacio no utilizado. Por tanto, la copia de seguridad es normalmente más pequeña que la propia base de datos. Para calcular el tamaño de la copia de seguridad completa de la base de datos, use el procedimiento almacenado del sistema **sp_spaceused**. Para obtener más información, vea [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md).  
  
### Programar copias de seguridad  
 La realización de una operación de copia de seguridad tiene un efecto mínimo en las transacciones que se están ejecutando, por lo que se puede efectuar al mismo tiempo que otras operaciones periódicas. Puede realizar una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un efecto mínimo en las cargas de trabajo de producción.  
   
>  Para obtener información sobre las restricciones de simultaneidad durante la copia de seguridad, vea [Información general de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
 Una vez decididos los tipos de copias de seguridad necesarios y la frecuencia de realización de cada tipo de copia, se recomienda programar copias de seguridad regulares como parte de un plan de mantenimiento de la base de datos. Para obtener información acerca de los planes de mantenimiento y de cómo crearlos para las copias de seguridad de bases de datos y las copias de seguridad de registros, vea [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
### Probar las copias de seguridad  
 No tendrá una estrategia de restauración hasta que compruebe las copias de seguridad. Es muy importante comprobar cuidadosamente la estrategia de copia de seguridad de cada una de las bases de datos restaurando una copia de la base de datos en un sistema de prueba. Debe comprobar la restauración de cada tipo de copia de seguridad que pretenda utilizar.  
  
 Se recomienda mantener un manual de operaciones para cada base de datos. Este manual de operaciones debe documentar la ubicación de las copias de seguridad, los nombres de dispositivos de copia de seguridad (si los hay) y el tiempo necesario para restaurar las copias de seguridad de prueba.  
  
## Más información sobre las tareas de copia de seguridad  
-   [Crear un plan de mantenimiento](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
-   [Crear un trabajo](../../ssms/agent/create-a-job.md)  
  
-   [Programar un trabajo](../../ssms/agent/schedule-a-job.md)  
  
## Trabajar con dispositivos de copia de seguridad y medios de copia de seguridad  
-   [Definir un dispositivo lógico de copia de seguridad para un archivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Especificar un disco o una cinta como destino de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Eliminar un dispositivo de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [Establecer la fecha de expiración de una copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Ver el contenido de una cinta o un archivo de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Ver los archivos de datos y de registro en un conjunto de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Restaurar una copia de seguridad desde un dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## Crear copias de seguridad  
**Nota** En el caso de copias de seguridad parciales o de solo copia, debe usar la instrucción [BACKUP](../../t-sql/statements/backup-transact-sql.md) de [!INCLUDE[tsql](../../includes/tsql-md.md)] con la opción PARTIAL o COPY_ONLY, respectivamente.  
  
 ### Usar SSMS   
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Realizar copias de seguridad de archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 ### Usar T-SQL  
-   [Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [Realizar una copia de seguridad del registro de transacciones cuando la base de datos está dañada &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [Habilitar o deshabilitar sumas de comprobación de copia de seguridad durante copia de seguridad o restauración &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [Especificar si una operación de copia de seguridad o restauración continúa o se detiene después de encontrar un error &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify if backup or restore continues or stops after error.md)  
  
## Restaurar copias de seguridad de datos 
### Usar SSMS 
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
-   [Restaurar una copia de seguridad diferencial de la base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)  
  
-   [Restaurar archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
### Usar T-SQL
-   [Restaurar una copia de seguridad de base de datos en el modelo de recuperación simple &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Restaurar una base de datos según el punto de error en el modelo de recuperación completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore database to point of failure - full recovery.md)  
  
-   [Restaurar archivos y grupos de archivos en archivos existentes &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Restaurar archivos en una nueva ubicación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [Restaurar la base de datos maestra &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)  

## Restaurar registros de transacciones (modelo de recuperación completa)
### Usar SSMS  
-   [Restaurar una base de datos en una transacción marcada &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Restaurar una copia de seguridad de registros de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
 ### Usar T-SQL 
-   [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
 
-   [Reiniciar una operación de restauración interrumpida &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restart-an-interrupted-restore-operation-transact-sql.md)  
  
-   [Recuperar una base de datos sin restaurar los datos &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
 
## Más información y recursos
 [Información general de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)   
 [Realizar copias de seguridad de los catálogos de texto completo y restaurarlos](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [Hacer copias de seguridad y restaurar bases de datos replicadas](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  