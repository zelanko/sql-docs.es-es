---
title: Novedades de Motor de base de datos de Microsoft SQL Server 2016 | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
- SQL2016_rc1
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
caps.latest.revision: 431
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 687bddd3ce51c60e286cfa0e2634790a8a492500
ms.contentlocale: es-es
ms.lasthandoff: 10/18/2017

---
# <a name="whats-new-in-database-engine---sql-server-2016"></a>Novedades de Motor de base de datos de Microsoft SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

En este tema se resumen las mejoras presentadas en la versión [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)].  Las nuevas características y mejoras aumentan la eficacia y la productividad de los arquitectos, desarrolladores y administradores que diseñan, desarrollan y mantienen sistemas de almacenamiento de datos.

Si quiere revisar las novedades de los otros componentes de SQL Server, vea [Novedades de SQL Server 2016 Release Candidate (RC2)](../sql-server/what-s-new-in-sql-server-2016.md).

> [!NOTE]
>  [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] es una aplicación de 64 bits. La instalación de 32 bits está descontinuada, a pesar de que algunos de los elementos se ejecutan como componentes de 32 bits.

#### <a name="try-it-out"></a>Pruébelo

- Para descargar [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], vaya al **[Centro de evaluación](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**![descargar](../analysis-services/media/download.png "descargar").

- ¿Tiene una cuenta de Azure?  Si es así, haga clic **[aquí](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** para poner en marcha una máquina virtual con [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] ya instalado.

> [!NOTE]
> Para obtener las notas de la versión actuales, vea [Notas de la versión de SQL Server 2016](../sql-server/sql-server-2016-release-notes.md).
  
## <a name="sql-server-2016-service-pack-1-sp1"></a>SQL Server 2016 Service Pack 1 (SP1)  
-  Ahora, la sintaxis `CREATE OR ALTER <object>` está disponible para los [procedimientos](../t-sql/statements/create-procedure-transact-sql.md), [vistas](../t-sql/statements/create-view-transact-sql.md), [ funciones](../t-sql/statements/create-function-transact-sql.md) y [desencadenadores](../t-sql/statements/create-trigger-transact-sql.md).
-   Se ha agregado compatibilidad para un modelo de sugerencias de consultas más genérico: `OPTION (USE HINT('<hint1>', '<hint2>'))`. Para obtener más información, consulte [Sugerencias de consulta (Transact-SQL)](../t-sql/queries/hints-transact-sql-query.md).  
- Se ha agregado la DMV [sys.dm_exec_valid_use_hints](../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md) a las sugerencias de lista.  
- Se ha agregado la DMV [sys.dm_exec_query_statistics_xml](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) para devolver estadísticas transitorias de planes de presentación XML.  
- Se ha agregado la DMV [sys.dm_db_incremental_stats_properties](../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md) a las estadísticas incrementales para la tabla especificada.  
- Se ha agregado la columna `instant_file_initialization_enabled`a [sys.dm_server_services](../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md).  
- Se ha agregado la columna `estimated_read_row_count` a [sys.dm_exec_query_profiles](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md).  
-  Se han agregado las columnas `sql_memory_model` y `sql_memory_model_desc` a [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) para proporcionar información sobre el modelo de bloqueo de las páginas de memoria.
-  Se han ampliado las ediciones que admiten una serie de características. Esto incluye agregar seguridad a nivel de fila, Always Encrypted, enmascaramiento de datos dinámicos, auditoría de base de datos, OLTP en memoria y otras características para todas las ediciones. Para obtener más información, consulte [Características compatibles con las ediciones de SQL Server 2016](../sql-server/editions-and-supported-features-for-sql-server-2016.md).   
-  [sp_refresh_parameter_encryption](../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) permite que el cifrado Always On actualice los metadatos cuando se redefinen los objetos cifrados con Always On.  


##  <a name="Feature"></a> SQL Server 2016 RTM
Esta sección contiene las siguientes subsecciones:

-   [Índices de almacén de columnas](#columnstore)
-   [Configuraciones con ámbito de base de datos](#scopedconfiguration)
-   [OLTP en memoria](#InMemory)
-   [Optimizador de consultas](#QueryOptimizer)
-   [Estadísticas de consultas activas](#LiveStats)
-   [Almacén de consultas](#QueryStore)
-   [Tablas temporales](#TT)
-   [Copias de seguridad seccionadas en Microsoft Azure Blob Storage](#StripedBackupToAzure)
-   [Copias de seguridad de instantánea de archivos en Microsoft Azure Blob Storage](#FileSnapshotBackup)
-   [Copia de seguridad administrada](#ManagedBackup)
-   [Base de datos TempDB](#multipleTempDB)
-   [Compatibilidad de JSON integrada](#ForJson)
-   [PolyBase](#bkPolyBase)
-   [Stretch Database](#stretch)
-   [Compatibilidad con UTF-8](#UTF8)
-   [Nuevo tamaño de base de datos predeterminada y valores de crecimiento automático](#DefaultDB)
-   [Mejoras de Transact-SQL](#TSQL)
-   [Mejoras de la vista del sistema](#SystemTable)
-   [Mejoras de seguridad](#Security)
-   [Mejoras de alta disponibilidad](#HighAvailability)
-   [Mejoras en la replicación](#Repl)
-   [Mejoras de las herramientas](#Tools)

####  <a name="columnstore"></a> Índices de almacén de columnas

Esta versión ofrece mejoras en los índices de almacén de columnas, que incluyen índices de almacén de columnas no agrupados actualizables, índices de almacén de columnas en tablas en memoria y muchas características nuevas más para el análisis operativo.

- Se puede actualizar un índice de almacén de columnas no agrupado después de la actualización.  No es necesario recompilar el índice para poder actualizarlo.

- Hay mejoras de rendimiento para las consultas de análisis que existen en los índices de almacén de columnas, en especial para agregados y predicados de cadena.

- Hay mejoras en la compatibilidad de los XEvents y DMV.

Para obtener más información, vea estos temas en la sección de la [Guía de índices de almacén de columnas](../relational-databases/indexes/columnstore-indexes-overview.md) de los Libros en pantalla:

- [Resumen de las características de los índices de almacén de columnas para cada versión](~/relational-databases/indexes/columnstore-indexes-what-s-new.md) incluye las novedades.

- [Carga de datos de índices de almacén de columnas](../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)

- [Rendimiento de las consultas de índices de almacén de columnas](~/relational-databases/indexes/columnstore-indexes-query-performance.md)

- [Introducción al almacén de columnas para análisis operativos en tiempo real](../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)

- [Índices de almacén de columnas para el almacenamiento de datos](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

- [Desfragmentación de índices de almacén de columnas](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)


####  <a name="scopedconfiguration"></a> Configuraciones con ámbito de base de datos


La nueva instrucción [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) le proporciona el control de determinadas configuraciones de la base de datos. Las opciones de configuración afectan al comportamiento de la aplicación.

La nueva instrucción está disponible tanto en [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] como en [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)].



####  <a name="InMemory"></a> OLTP en memoria


##### <a name="storage-format-change"></a>Cambio de formato de almacenamiento

El formato de almacenamiento para tablas con optimización para memoria cambia entre SQL Server 2014 y 2016. Para actualizar y adjuntar o restaurar desde SQL Server 2014, el nuevo formato de almacenamiento se serializa y la base de datos se reinicia una vez durante la recuperación de la misma.

- [Actualizar a SQL Server 2016](../database-engine/install-windows/upgrade-sql-server.md)


##### <a name="alter-table-is-log-optimized-and-runs-in-parallel"></a>ALTER TABLE tiene optimización para registro y se ejecuta en paralelo

Ahora, cuando se ejecuta una instrucción ALTER TABLE en una tabla con optimización para memoria, solo los cambios de metadatos se escriben en el registro. Esto reduce en gran medida el E/S de registro. Además, la mayoría de los escenarios de ALTER TABLE se ejecutan ahora en paralelo, lo que puede reducir considerablemente la duración de la instrucción.

- Para las excepciones no paralelas, incluidos los LOB, vea [Modificar tablas con optimización para memoria](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md).



##### <a name="statistics"></a>Estadísticas

[Las estadísticas de las tablas con optimización para memoria](../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md) ahora se actualizan automáticamente. Además, ahora el muestreo es un método que se admite para recopilar estadísticas, lo que le permite evitar el método fullscan que es más costoso.


##### <a name="parallel-and-heap-scan-for-memory-optimized-tables"></a>Examen paralelo y de montón para tablas con optimización para memoria

Las tablas con optimización para memoria y los índices en tablas con optimización para memoria ahora son compatibles con el examen paralelo. Esto mejora el rendimiento de las consultas de análisis.

Además, se admite el examen de montón y se puede realizar en paralelo. En el caso de una tabla con optimización para memoria, un examen de montón hace referencia al examen de todas las filas de una tabla mediante la estructura de datos de montón en memoria usada para almacenar las filas. Para un examen de tabla completo, el examen de montón es más eficaz que usar un índice.

##### <a name="transact-sql-improvements-for-memory-optimized-tables"></a>Mejoras de Transact-SQL para tablas con optimización para memoria

Hay varios elementos de Transact-SQL que no se admitían para las tablas con optimización para memoria en SQL Server 2014, que ahora se admiten en SQL Server 2016:


- Se admiten índices y restricciones UNIQUE.


- Se admiten referencias FOREIGN KEY entre tablas con optimización para memoria.
  - Estas claves externas solo pueden hacer referencia a una clave principal y no pueden hacer referencia a una clave única.


- Se admiten las restricciones CHECK.

- Un índice no único puede permitir valores NULL en su clave.

- Los desencadenadores se admiten en las tablas con optimización para memoria.
  - Solo se admiten desencadenadores AFTER. No se admiten desencadenadores INSTEADOF.
  - Cualquier desencadenador de una tabla con optimización para memoria debe usar WITH NATIVE_COMPILATION.

- Compatibilidad total para todas las intercalaciones y páginas de códigos de SQL Server con índices y otros artefactos en tablas con optimización para memoria y módulos T-SQL compilados de forma nativa.


- Compatibilidad con [Modificar tablas con optimización para memoria](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md):
  - Índices ADD y DROP. Cambiar bucket_count de índices hash.
  - Realizar cambios de esquema: agregar, quitar o modificar columnas; agregar o quitar restricción.

- Una tabla con optimización para memoria ahora puede tener varias columnas cuyas longitudes combinadas son superiores a la longitud de la página de 8060 bytes. Un ejemplo es una tabla con tres columnas de tipo `nvarchar(4000)`. En estos ejemplos, algunas columnas ahora se almacenan de manera no consecutiva. Las consultas ignoran completamente si una columna se encuentra de manera consecutiva o no consecutiva.

- [Tipos de LOB (objeto grande)](../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) `varbinary(max)`, `nvarchar(max)` y `varchar(max)` ahora se admiten en tablas con optimización para memoria.


Para obtener información general, vea:

- [Construcciones Transact-SQL no admitidas por OLTP en memoria](../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)
- [Características de SQL Server no admitidas para OLTP en memoria](~/relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)


##### <a name="transact-sql-improvements-for-natively-compiled-modules"></a>Mejoras de Transact-SQL para los módulos compilados de manera nativa

Hay algunos elementos de Transact-SQL que no se admitían para los módulos compilados de manera nativa en SQL Server 2014, que ahora se admiten en SQL Server 2016:


- Construcciones de consulta:
  - UNION y UNION ALL
  - SELECT DISTINCT
  - OUTER JOIN
  - Subconsultas en SELECT


- Las instrucciones INSERT, UPDATE y DELETE ahora pueden incluir la [cláusula OUTPUT](../t-sql/queries/output-clause-transact-sql.md).

- Ahora, los LOB pueden usarse de las siguientes maneras en un procedimiento nativo:
  - Declaración de variables.
  - Parámetros de entrada recibidos.
  - Los parámetros se pasan a las funciones de cadena, como LTrim o Substring, en un procedimiento nativo.


- Las funciones con valores de tabla (TVF) insertadas (instrucción única) ahora pueden compilarse de manera nativa.

- Las funciones escalares definidas por el usuario (UDF) ahora pueden compilarse de manera nativa.

- Mayor compatibilidad para llamar a un procedimiento nativo:
  - [Funciones de seguridad](../t-sql/functions/security-functions-transact-sql.md) integradas.
  - [Funciones matemáticas](../t-sql/functions/mathematical-functions-transact-sql.md) integradas.
  - Función integrada `@@SPID`.


- Ahora se admite EXECUTE AS CALLER, lo que significa que la cláusula EXECUTE AS ya no es necesaria cuando se crea un módulo T-SQL compilado de forma nativa.


Para obtener información general, vea:

- [Características admitidas en los módulos T-SQL compilados de forma nativa](../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)
- [Altering Natively Compiled T-SQL Modules](../relational-databases/in-memory-oltp/altering-natively-compiled-t-sql-modules.md)


##### <a name="performance-and-scaling-improvements"></a>Mejoras de rendimiento y escalado

- Ya no hay ninguna limitación en el tamaño de los datos. Consulte [Estimar los requisitos de memoria para las tablas con optimización para memoria](~/relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md).

- Ahora, existen varios subprocesos simultáneos responsables de [conservar los cambios en tablas con optimización para memoria en disco](../relational-databases/in-memory-oltp/scalability.md).

- Compatibilidad de planes paralelos para [Acceso a tablas con optimización para memoria mediante Transact-SQL interpretado](../relational-databases/in-memory-oltp/accessing-memory-optimized-tables-using-interpreted-transact-sql.md).


##### <a name="enhancements-in-sql-server-management-studio"></a>Mejoras en SQL Server Management Studio

- [Determinar si una tabla o un procedimiento almacenado se debe pasar a OLTP en memoria](../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) ya no requiere la configuración de recopiladores de datos ni el almacén de administración de datos. Ahora el informe se puede ejecutar directamente en una base de datos de producción.

- [Cmdlet de PowerShell para la evaluación de la migración](../relational-databases/in-memory-oltp/powershell-cmdlet-for-migration-evaluation.md) para evaluar la idoneidad de migración de varios objetos en una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

- Genere listas de comprobación de las migraciones. Para ello, haga clic con el botón derecho en una base de datos y seleccione Tareas > Generar listas de comprobación de migración de OLTP en memoria.

##### <a name="cross-feature-support"></a>Compatibilidad entre características

- Compatibilidad para usar el control de versiones del sistema temporal con OLTP en memoria. Para obtener más información, vea [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md).

- Compatibilidad del Almacén de consultas con el código compilado de manera nativa desde cargas de trabajo de OLTP en memoria. Para obtener más información, vea [Uso del almacén de consultas con OLTP en memoria](../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md).

- [Seguridad de nivel de fila en tablas con optimización para memoria](../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md#rls)

- Las conexiones de [Usar conjuntos de resultados activos múltiples &#40;MARS&#41;](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) ahora pueden tener acceso a tablas con optimización para memoria y a procedimientos almacenados compilados de manera nativa.

- Compatibilidad del [Cifrado de datos transparente (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md). Si una base de datos está configurada para ENCRYPTION, los archivos del [grupo de archivos con optimización para memoria](../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md) ahora también se cifran.

Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).


####  <a name="QueryOptimizer"></a> Optimizador de consultas
##### <a name="compatibility-level-guarantees"></a>Garantías de nivel de compatibilidad
Cuando actualiza la base de datos a SQL Server 2016, no habrá ningún cambio de plan visto si permanece en los niveles de compatibilidad anteriores que estaba utilizando (por ejemplo, 120 o 110). Las nuevas características y mejoras relacionadas con el optimizador de consultas solo estarán disponibles en el nivel de compatibilidad más reciente. 
##### <a name="trace-flag-4199"></a>Marca de seguimiento 4199
En términos generales, no es necesario usar la marca de seguimiento 4199 en SQL Server 2016, ya que la mayoría de los comportamientos del optimizador de consultas que controla esta marca de seguimiento están habilitados sin condiciones bajo el nivel de compatibilidad más reciente (130) en SQL Server 2016 .
##### <a name="new-referential-integrity-operator"></a>Nuevo operador de integridad referencial
Una tabla puede hacer referencia a otras 253 tablas y columnas como claves externas (referencias de salida) como máximo. [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] aumenta el límite para la cantidad de otras tablas y columnas que pueden hacer referencia a las columnas de una sola tabla (referencias de entrada) de 253 a 10 000. Para ver las restricciones, vea [Create Foreign Key Relationships](../relational-databases/tables/create-foreign-key-relationships.md). Se incorpora un nuevo operador de integridad referencial (en el nivel de compatibilidad 130), que realiza las comprobaciones de integridad referencial. Esto mejora el rendimiento global de las operaciones UPDATE y DELETE, en tablas que tienen un gran número de referencias entrantes, por lo que resulta posible tener gran número de referencias entrantes. Para obtener más información, consulte [Query Optimizer Additions in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/23/query-optimizer-additions-in-sql-server/)(Incorporaciones del optimizador de consultas en SQL Server 2016).
##### <a name="parallel-update-of-sampled-statistics"></a>Actualización paralela de estadísticas muestreadas
El muestreo de datos para generar estadísticas ahora se realiza en paralelo (en el nivel de compatibilidad 130) para mejorar el rendimiento de recopilación de estadísticas. Para más información, vea [Update Statistics](../t-sql/statements/update-statistics-transact-sql.md) (Actualización de estadísticas).
#### <a name="sublinear-threshold-for-update-of-statistics"></a>Umbral infralineal para la actualización de estadísticas
La actualización automática de estadísticas es ahora más agresiva en tablas grandes (nivel de compatibilidad 130). El umbral para desencadenar la actualización automática de estadísticas es 20 %, a partir de SQL Server 2016, para tablas más grandes, este umbral comenzará a reducirse (todavía en forma de porcentaje) a medida que el número de filas aumenta en la tabla. Ya no necesitará establecer la marca de seguimiento 2371 para reducir el umbral. 
##### <a name="other-enhancements"></a>Otras mejoras
La instrucción Insert in an Insert-select es multiproceso o puede tener un plan paralelo (en el nivel de compatibilidad 130). Para obtener un plan paralelo, INSERT... La instrucción SELECT debe utilizar la sugerencia TABLOCK. Para más información, consulte [Parallel Insert Select](https://blogs.msdn.microsoft.com/sqlcat/2016/07/06/sqlsweet16-episode-3-parallel-insert-select/)(Insert Select en paralelo)

####  <a name="LiveStats"></a> Estadísticas de consultas activas
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] ofrece la posibilidad de ver el plan de ejecución de una consulta activa. Este plan de consulta activa ofrece conocimientos en tiempo real sobre el proceso de ejecución de consulta a medida que los controles fluyen desde un operador de plan de consulta a otro. Para obtener más información, consulte [Live Query Statistics](../relational-databases/performance/live-query-statistics.md).

####  <a name="QueryStore"></a> Almacén de consultas
Almacén de consultas es una característica nueva que ofrece a los administradores de base de datos los conocimientos sobre el rendimiento y la elección del plan de consulta. Esta característica simplifica la solución de problemas de rendimiento al permitirle encontrar rápidamente diferencias de rendimiento provocadas por cambios en los planes de consulta. Captura automáticamente un historial de consultas, planes y estadísticas en tiempo de ejecución, y los conserva para su revisión. Separa los datos por ventanas de tiempo, lo que permite ver patrones de uso la base de datos y comprender cuándo se produjeron cambios del plan de consultas en el servidor. El Almacén de consultas presenta la información mediante un cuadro de diálogo de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] y le permite forzar la consulta a uno de los planes de consultas seleccionados. Para obtener más información, consulte [Monitoring Performance By Using the Query Store](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).


####  <a name="TT"></a> Tablas temporales
[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] ahora es compatible con las tablas temporales con versiones del sistema. Una tabla temporal es un tipo de tabla nuevo que brinda información correcta sobre los hechos almacenados en cualquier momento determinado. Cada tabla temporal consta, en realidad, de dos tablas, una para los datos actuales y otra, para los históricos. El sistema garantiza que, cuando cambian los datos de la tabla con los datos actuales, los valores anteriores se almacenan en la tabla de datos históricos. Se proporcionan construcciones de consultas para que los usuarios no sepan de esta complejidad. Para obtener más información, consulte [Temporal Tables](../relational-databases/tables/temporal-tables.md).

####  <a name="StripedBackupToAzure"></a> Copias de seguridad seccionadas en Microsoft Azure Blob Storage
En [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], la copia de seguridad de SQL Server en una dirección URL mediante el uso del servicio de Almacenamiento de blobs de Microsoft Azure, ahora es compatible con los conjuntos de copias de seguridad seccionadas que usan blobs en bloques para admitir un tamaño máximo de copia de seguridad de 12,8 TB. Para obtener ejemplos, vea [Code Examples](../relational-databases/backup-restore/sql-server-backup-to-url.md#Examples).

####  <a name="FileSnapshotBackup"></a> Copias de seguridad de instantánea de archivos en Microsoft Azure Blob Storage
 En [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], la copia de seguridad de SQL Server en una dirección URL ahora es compatible con el uso de instantáneas de Azure para crear copias de seguridad de bases de datos en las que todos los archivos de base de datos se almacenan con el servicio de Almacenamiento de blobs de Microsoft Azure. Para obtener más información, vea [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).

####  <a name="ManagedBackup"></a> Copia de seguridad administrada
En [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], la copia de seguridad administrada de SQL Server en Microsoft Azure usa el nuevo almacenamiento de blobs en bloques para los archivos de copia de seguridad. También hay varios cambios y mejoras en Copia de seguridad administrada.

-   Compatibilidad con la programación, tanto automatizada como personalizada, de las copias de seguridad.

-   Compatibilidad de las copias de seguridad con bases de datos del sistema.

-   Compatibilidad con las bases de datos que usan el modelo de recuperación simple.

 Para obtener más información, consulte [SQL Server Managed Backup to Microsoft Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).

> [!NOTE]
>  Para [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], estas características nuevas de copia de seguridad administrada todavía no cuentan con la compatibilidad de interfaz de usuario correspondiente en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].

####  <a name="multipleTempDB"></a> Base de datos TempDB
 Hay varias mejoras en TempDB:

-   Las marcas de seguimiento 1117 y 1118 ya no son necesarias para tempdb. Si hay varios archivos de base de datos tempdb, todos crecerán al mismo tiempo en función de la configuración de crecimiento. Además, todas las asignaciones de tempdb usarán extensiones uniformes.

-   De manera predeterminada, la configuración agrega archivos tempdb según el valor que sea más bajo, ya sea 8 o la cantidad de CPU.

-   Durante la configuración, puede configurar la cantidad de archivos de base de datos tempdb, el tamaño inicial, el crecimiento automático y la colocación de directorio a través del nuevo control de entrada de IU en la sección Configuración del motor de base de datos - TempDB del Asistente para la instalación de SQL Server.

-   El tamaño inicial predeterminado es de 8 MB y el crecimiento automático predeterminado es de 64 MB.

-   Puede especificar varios volúmenes para los archivos de base de datos tempdb. Si se especifican varios directorios, los archivos de datos tempdb se distribuirán por turnos entre los directorios.

####  <a name="ForJson"></a> Compatibilidad de JSON integrada
SQL Server 2016 agrega compatibilidad integrada para la importación y exportación de JSON y el funcionamiento con cadenas JSON. Esta compatibilidad integrada incluye las siguientes instrucciones y funciones.

-   Para aplicar el formato JSON a los resultados de la consulta, o exportar JSON, agregue la cláusula **FOR JSON** a una instrucción **SELECT** . Use la cláusula **FOR JSON**, por ejemplo, para delegar en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] la aplicación de formato a los resultados de JSON procedentes de aplicaciones cliente. Para obtener más información, vea [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Aplicar el formato JSON a los resultados de la consulta con FOR JSON &#40;SQL Server&#41;)](../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).

-   Convertir datos JSON en filas y columnas, o importar JSON, mediante una llamada a la función de proveedor del conjunto de filas **OPENJSON**. Use **OPENJSON** para importar datos JSON a SQL Server o convertir datos JSON en filas y columnas para una aplicación o servicio que en este momento no puede usar directamente JSON. Para obtener más información, vea [Convert JSON Data to Rows and Columns with OPENJSON &#40;SQL Server&#41; (Convertir datos JSON en filas y columnas con OPENJSON &#40;SQL Server&#41;)](../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md).

-   La función **ISJSON** prueba si una cadena contiene un valor JSON válido. Para obtener más información, vea [ISJSON &#40;Transact-SQL&#41;](../t-sql/functions/isjson-transact-sql.md).

-   La función **JSON_VALUE** extrae un valor escalar de una cadena JSON. Para obtener más información, vea [JSON_VALUE &#40;Transact-SQL&#41;](../t-sql/functions/json-value-transact-sql.md).

-   La función **JSON_QUERY** extrae un objeto o una matriz de una cadena JSON. Para obtener más información, vea [JSON_QUERY &#40;Transact-SQL&#41;](../t-sql/functions/json-query-transact-sql.md).

-   La función **JSON_MODIFY** actualiza el valor de una propiedad en una cadena JSON y devuelve la cadena JSON actualizada. Para obtener más información, vea [JSON_MODIFY &#40;Transact-SQL&#41;](../t-sql/functions/json-modify-transact-sql.md).

####  <a name="bkPolyBase"></a> PolyBase
 PolyBase le permite usar instrucciones T-SQL para tener acceso a los datos almacenados en Hadoop o en Azure Blog Storage y consultarlos de manera ad hoc. También le permite consultar datos semiestructurados y combinar los resultados con los conjuntos de datos relacionales almacenados en SQL Server. PolyBase está optimizado para las cargas de trabajo de almacenamiento de datos y está dirigido a los escenarios de consultas de análisis.

 Para obtener más información, vea [PolyBase Guide (Guía de PolyBase)](../relational-databases/polybase/polybase-guide.md).

####  <a name="stretch"></a> Stretch Database
 Stretch Database es una nueva característica de [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] que migra los datos históricos de forma clara y segura a la nube de Microsoft Azure. Puede tener acceso a los datos de SQL Server sin problemas, independientemente de si están almacenados localmente o extendidos a la nube. Solo tiene que establecer la directiva que defina dónde se almacenan los datos y SQL Server se encargará del movimiento de datos en segundo plano. La tabla entera estará siempre en línea y lista para consultarse. Además, Stretch Database no requiere ningún cambio en las consultas o aplicaciones existentes: la ubicación de los datos es completamente clara para la aplicación. Para obtener más información, vea [Stretch Database](../sql-server/stretch-database/stretch-database.md).
 
####  <a name="UTF8"></a> Compatibilidad con UTF-8
[Utilidad BCP](../tools/bcp-utility.md), [BULK INSERT](../t-sql/statements/bulk-insert-transact-sql.md) y [OPENROWSET](../t-sql/functions/openrowset-transact-sql.md) ahora admiten la página de códigos UTF-8. Para obtener más información, vea esos temas y [Crear un archivo de formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md).

####  <a name="DefaultDB"></a> Nuevo tamaño de base de datos predeterminada y valores de crecimiento automático
Valores nuevos para la base de datos modelo y valores predeterminados para las bases de datos nuevas (que se basan en el modelo). El tamaño inicial de los datos y los archivos de registro ahora es de 8 MB. El crecimiento automático predeterminado de los datos y los archivos de registro ahora es de 64 MB.


###  <a name="TSQL"></a> Mejoras de Transact-SQL
Varias mejoras permiten admitir las características descritas en las demás secciones de este tema. Se encuentran disponibles las siguientes mejoras adicionales.
- La instrucción TRUNCATE TABLE ahora permite truncar particiones especificadas. Para obtener más información, vea [TRUNCATE TABLE &#40;Transact-SQL&#41;](../t-sql/statements/truncate-table-transact-sql.md).
- [ALTER TABLE &#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md) ahora permite realizar numerosas acciones de alteración de columna mientras la tabla sigue estando disponible.
- El índice de texto completo DMV [sys.dm_fts_index_keywords_position_by_document &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-position-by-document-transact-sql.md) devuelve la ubicación de las palabras clave en los documentos. Este DMV también se agregó en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP2 y [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP1.
- Una sugerencia de consulta nueva **NO_PERFORMANCE_SPOOL** puede evitar que se agregue un operador de cola de impresión a los planes de consulta. Esto puede mejorar el rendimiento cuando se ejecutan muchas consultas concurrentes con operaciones de cola de impresión. Para obtener más información, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-query.md).
- La instrucción [FORMATMESSAGE &#40;Transact-SQL&#41;](../t-sql/functions/formatmessage-transact-sql.md) está mejorada para aceptar argumentos msg_string.
- El tamaño de clave de índice máximo para los índices NONCLUSTERED se ha aumentado a 1700 bytes.
- Se agrega la nueva sintaxis DROP IF para las instrucciones DROP relacionadas con AGGREGATE, ASSEMBLY, COLUMN, CONSTRAINT, DATABASE, DEFAULT, FUNCTION, INDEX, PROCEDURE, ROLE, RULE, SCHEMA, SECURITY POLICY, SEQUENCE, SYNONYM, TABLE, TRIGGER, TYPE, USER y VIEW. Vea los temas de sintaxis individual para conocer la sintaxis.
- Se ha agregado una opción MAXDOP a [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checktable-transact-sql.md), [DBCC CHECKDB &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) y [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md) para especificar el grado de paralelismo.
- Ahora se puede establecer SESSION_CONTEXT. Incluye la función [SESSION_CONTEXT &#40;Transact-SQL&#41;](../t-sql/functions/session-context-transact-sql.md), la función [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../t-sql/functions/current-transaction-id-transact-sql.md) y el procedimiento [sp_set_session_context &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md).
- Las Extensiones de análisis avanzado permiten a los usuarios ejecutar scripts escritos en un lenguaje compatible, como R. [!INCLUDE[tsql](../includes/tsql-md.md)] admite R mediante la introducción del procedimiento almacenado [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) y la [Opción de configuración de servidor Scripts externos habilitados](../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md). Para obtener más información, vea [SQL Server R Services](../advanced-analytics/r-services/sql-server-r-services.md).
- Compatibilidad adicional con R: la capacidad de crear un grupo de recursos externo. Para obtener más información, vea [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/create-external-resource-pool-transact-sql.md).  Nuevas vistas de catálogo y DMV ([sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) y [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)). Se encuentran disponibles argumentos adicionales para [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) y [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-workload-group-transact-sql.md). Se agregan columnas adicionales a algunas de las vistas de catálogo existentes del regulador de recursos y DMV.
- La sintaxis [CREATE USER](../t-sql/statements/create-user-transact-sql.md) se mejora con la opción ALLOW_ENCRYPTED_VALUE_MODIFICATIONS para admitir la característica Always Encrypted. Para obtener más información, vea [Migración de información confidencial protegida mediante Always Encrypted](../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).
- Las funciones [COMPRESS &#40;Transact-SQL&#41;](../t-sql/functions/compress-transact-sql.md) y [DECOMPRESS &#40;Transact-SQL&#41;](../t-sql/functions/decompress-transact-sql.md) convierten valores en y desde el algoritmo GZIP.
- Las funciones [DATEDIFF_BIG &#40;Transact-SQL&#41;](../t-sql/functions/datediff-big-transact-sql.md) y [AT TIME ZONE &#40;Transact-SQL&#41;](../t-sql/queries/at-time-zone-transact-sql.md) y la vista [sys.time_zone_info &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) se agregan para admitir las interacciones de fecha y hora.
- Ahora se puede crear una credencial en el nivel de base de datos (además de la credencial de nivel de servidor que estaba disponible anteriormente). Para obtener más información, vea [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md).
- Se agregan ocho propiedades nuevas a [SERVERPROPERTY &#40;Transact-SQL&#41;](../t-sql/functions/serverproperty-transact-sql.md): InstanceDefaultDataPath, InstanceDefaultLogPath, ProductBuild, ProductBuildType, ProductMajorVersion, ProductMinorVersion, ProductUpdateLevel y ProductUpdateReference.
- Se quita el límite de longitud de entrada de 8000 bytes para la función [HASHBYTES &#40;Transact-SQL&#41;](../t-sql/functions/hashbytes-transact-sql.md).
- Se agregan nuevas funciones de cadena ([STRING_SPLIT &#40;Transact-SQL&#41;](../t-sql/functions/string-split-transact-sql.md) y [STRING_ESCAPE &#40;Transact-SQL&#41;](../t-sql/functions/string-escape-transact-sql.md)).
- Opciones de crecimiento automático: la marca de seguimiento 1117 se ha reemplazado por las opciones AUTOGROW_SINGLE_FILE y AUTOGROW_ALL_FILES de ALTER DATABASE y la marca de seguimiento 1117 no tiene ningún efecto. Para obtener más información, vea [Opciones File y Filegroup de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) y la nueva columna is_autogrow_all_files de [sys.filegroups &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md).
- Asignación de extensiones combinadas: para las bases de datos de usuario, la asignación predeterminada para las 8 primeras páginas de un objeto pasarán de usar extensiones de página combinadas a usar extensiones uniformes. La marca de seguimiento 1118 se reemplaza por la opción SET MIXED_PAGE_ALLOCATION de ALTER DATABASE y la marca de seguimiento 1118 no tiene efecto. Para obtener más información, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-set-options.md), y la nueva columna `is_mixed_page_allocation_on` de [sys.databases &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-databases-transact-sql.md).


###  <a name="SystemTable"></a> Mejoras de la vista del sistema
- Dos vistas nuevas admiten la seguridad de nivel de fila. Para obtener más información, vea [sys.security_predicates &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md) y [sys.security_policies &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md).
- Siete vistas nuevas admiten la característica Almacén de consultas. Para obtener más información, vea [Query Store Catalog Views &#40;Transact-SQL&#41; (Vistas de catálogo del almacén de consultas &#40;Transact-SQL&#41;)](../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md).
- Se agregan 24 nuevas columnas a [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) para proporcionar información sobre concesiones de memoria.
- Se agregan dos sugerencias de consulta nuevas (MIN_GRANT_PERCENT y MAX_GRANT_PERCENT) para especificar las concesiones de memoria. Vea [Sugerencias de consulta &#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-query.md).
- [sys.dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) proporciona un informe por sesión similar a todo el servidor [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).
- [sys.dm_exec_function_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-function-stats-transact-sql.md) proporciona estadísticas sobre la ejecución relacionadas con funciones con valores escalares.
- A partir de [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], las entradas de [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md) se conservan tal y como estaban antes de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].
- Se puede devolver información sobre las instrucciones enviadas a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante la nueva función de administración dinámica [sys.dm_exec_input_buffer &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md).
- Dos nuevas vistas admiten [SQL Server R Services](../advanced-analytics/r-services/sql-server-r-services.md): [sys.dm_external_script_requests](../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) y [sys.dm_external_script_execution_stats](../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 


###  <a name="Security"></a> Mejoras de seguridad

####  <a name="RLS"></a> Seguridad de nivel de fila
La seguridad de nivel de fila presenta el control de acceso basado en predicados. Ofrece una evaluación flexible, centralizada y basada en predicados que puede tener en cuenta metadatos (como etiquetas) o cualquier otro criterio que el administrador determine como apropiado. El predicado se usa como un criterio para determinar si el usuario tiene o no el acceso adecuado a los datos según los atributos del usuario. El control de acceso basado en etiquetas se puede implementar con el control de acceso basado en predicados. Para obtener más información, vea [Seguridad de nivel de fila](../relational-databases/security/row-level-security.md).


####  <a name="TCE"></a> Always Encrypted
Con Always Encrypted, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] puede realizar operaciones sobre datos cifrados y, lo mejor de todo, es que la clave de cifrado reside con la aplicación dentro del entorno de confianza del cliente y no en el servidor. Always Encrypted protege los datos de cliente para que los administradores de base de datos no tengan acceso a los datos de texto sin formato. El cifrado y descifrado de datos se produce sin problemas en el nivel de controlador, lo que minimiza los cambios que se deben realizar en las aplicaciones existentes. Para obtener más información, vea [Always Encrypted &#40;motor de base de datos&#41;](../relational-databases/security/encryption/always-encrypted-database-engine.md).


####  <a name="Masking"></a> Enmascaramiento de datos dinámicos
El enmascaramiento dinámico de datos limita la exposición de información confidencial ocultándolos a los usuarios sin privilegios. El enmascaramiento dinámico de datos evita el acceso no autorizado a información confidencial permitiendo que los clientes designen la cantidad de información confidencial que se debe revelar, con un impacto mínimo en la capa de aplicación. Se trata de una característica de protección de datos que oculta la información confidencial del conjunto de resultados de una consulta de campos designados de una base de datos, sin modificar los datos de esta última. Para obtener más información, vea [Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md).


####  <a name="Perms"></a> Nuevos permisos
- El permiso **ALTER ANY SECURITY POLICY** está disponible como parte de la implementación de la seguridad de nivel de fila.
- Los permisos **ALTER ANY MASK** y **UNMASK** están disponibles como parte de la implementación del enmascaramiento dinámico de datos.
- Los permisos **ALTER ANY COLUMN ENCRYPTION KEY**, **VIEW ANY COLUMN ENCRYPTION KEY**, **ALTER ANY COLUMN MASTER KEY DEFINITION**y **VIEW ANY COLUMN MASTER KEY DEFINITION** están disponibles como parte de la implementación de la característica Always Encrypted.
- Los permisos **ALTER ANY EXTERNAL DATA SOURCE** y **ALTER ANY EXTERNAL FILE FORMAT** se encuentran visibles en [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] pero solo se aplican en [!INCLUDE[ssAPS](../includes/ssaps-md.md)] ([!INCLUDE[ssDW](../includes/ssdw-md.md)]).
- Los permisos **EXECUTE ANY EXTERNAL SCRIPT** están disponibles como parte de la compatibilidad con los scripts de R.
 - Los permisos **ALTER ANY DATABASE SCOPED CONFIGURATION** están disponibles para autorizar el uso de la instrucción [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

####  <a name="TDE"></a> Cifrado de datos transparente
- Se ha agregado al Cifrado de datos transparente la compatibilidad con la aceleración de hardware Intel AES-NI de cifrado. Esto disminuirá la sobrecarga de CPU que surge cuando se activa Cifrado de datos transparente.

###  <a name="AES"></a> Cifrado AES para puntos de conexión
- El cifrado predeterminado para los puntos de conexión cambia de RC4 a AES.

####  <a name="newcredentialtype"></a> Tipo de credencial nuevo
- Ahora se puede crear una credencial en el nivel de base de datos (además de la credencial de nivel de servidor que estaba disponible anteriormente). Para obtener más información, vea [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md).


###  <a name="HighAvailability"></a> Mejoras de alta disponibilidad
SQL Server 2016 Standard Edition ahora admite los grupos de disponibilidad básica AlwaysOn. Los grupos de disponibilidad básica brindan compatibilidad con una réplica principal y una réplica secundaria. Esta funcionalidad reemplaza la tecnología obsoleta de Creación de reflejo de la base de datos para lograr una alta disponibilidad. Para obtener más información sobre las diferencias entre los grupos de disponibilidad básica y avanzada, vea [Basic Availability Groups &#40;Always On Availability Groups&#41; (Grupos de disponibilidad básica &#40;grupos de disponibilidad AlwaysOn&#41;)](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).

El equilibrio de carga de las solicitudes de conexión de lectura ahora se admite para todo un conjunto de réplicas de solo lectura. El comportamiento anterior siempre dirigía las conexiones a la primera réplica de solo lectura disponible en la lista de enrutamiento. Para obtener más información, vea [Configuración del equilibrio de carga entre réplicas de solo lectura](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing).

 La cantidad de réplicas que admiten la conmutación automática por error subió de dos a tres.

 Ahora se admiten las cuentas de servicio administradas de grupo para los clústeres de conmutación por error de AlwaysOn. Para obtener más información, vea [Cuentas de servicio administradas de grupo](https://technet.microsoft.com/library/hh831782.aspx). En el caso de Windows Server 2012 R2, se requiere una actualización para evitar estar fuera de servicio de manera temporal después de cambiar una contraseña. Para obtener la actualización, vea [Los servicios basados en gMSA no pueden iniciar sesión después de un cambio de contraseña en un dominio de Windows Server 2012 R2](https://support.microsoft.com/kb/2998082/).

 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] admite transacciones distribuidas y DTC en Windows Server 2016. Para obtener más información, vea [Support for distributed transactions (Compatibilidad con las transacciones distribuidas)](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md#dtcsupport).

 Ahora puede configurar [!INCLUDE[ssHADR](../includes/sshadr-md.md)] para realizar una conmutación por error cuando una base de datos queda sin conexión. Este cambio requiere la configuración de la opción **DB_FAILOVER** en **ON** en las instrucciones [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md) o [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md).

AlwaysOn ahora es compatible con bases de datos cifradas. Los asistentes para los grupos de disponibilidad ahora le solicitan ingresar una contraseña para todas las bases de datos que contienen una clave maestra de base de datos cuando crea un grupo de disponibilidad nuevo o cuando agrega bases de datos o réplicas a un grupo de disponibilidad existente.

Ahora se pueden combinar dos grupos de disponibilidad de dos clústeres de conmutación por error de Windows Server (WSFC) en un grupo de disponibilidad distribuida. Para obtener más información, vea [Distributed Availability Groups &#40;Always On Availability Groups&#41; (Grupos de disponibilidad distribuida &#40;grupos de disponibilidad AlwaysOn&#41;)](../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md).

La propagación directa permite propagar automáticamente una réplica secundaria a través de la red (en lugar de una propagación manual que requiere que una copia de seguridad física de la base de datos de destino se restaure en la réplica secundaria). La propagación directa se especifica mediante la configuración de **SEEDING_MODE=AUTOMATIC** en las instrucciones [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md) o [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md). También debe especificar **GRANT CREATE ANY DATABASE** con [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md) en cada réplica secundaria que se use con la propagación directa.

**Mejoras en el rendimiento**: el rendimiento de la sincronización de los grupos de disponibilidad ha aumentado aproximadamente 10 veces mediante la compresión más rápida y en paralelo de los bloques de registros de la réplica principal, mediante un protocolo de sincronización optimizado y al rehacer y descomprimir en paralelo las entradas del registro en la réplica secundaria. Esto aumenta la actualización de las secundarias legibles y reduce el tiempo de recuperación de la base de datos en caso de conmutación por error. Tenga en cuenta que la opción de rehacer para las tablas con optimización para memoria no se encuentra todavía en paralelo en SQL Server 2016.

###  <a name="Repl"></a> Mejoras en la replicación
- Ahora se admite la replicación de tablas con optimización para memoria. Para obtener más información, vea [Replicación para los suscriptores de tablas con optimización para memoria](../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).
- Ahora se admite la replicación en [!INCLUDE[ssSDSFull](../includes/sssdsfull-md.md)]. Para obtener más información, vea [Replication to SQL Database](../relational-databases/replication/replication-to-sql-database.md).

###  <a name="Tools"></a> Mejoras de las herramientas

####  <a name="SSMS"></a> Management Studio
Descargar la versión más reciente de [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] admite la Biblioteca de autenticación de Active Directory (ADAL) que se encuentra en desarrollo para conectarse a Microsoft Azure. Esto reemplaza la autenticación basada en certificados que se usa en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].
- Un requisito previo de la instalación de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] es tener instalado .NET 4.6. .NET 4.6 se instalará automáticamente a través de la configuración cuando se instale [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] .
- Una nueva opción de cuadrícula de resultados de consulta admite conservar el retorno de carro o avance de línea (caracteres de línea nueva) cuando se copia o se guarda texto de la cuadrícula de resultados. Puede definir esto en el menú Herramientas/Opciones.
- Las Herramientas de administración de SQL Server ya no se instalan desde el árbol de características principales; para obtener más detalles, vea [Instalar las Herramientas de administración de SQL Server con SSMS](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381).
- Un requisito previo de la instalación de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] es tener instalado .NET 4.6.1. .NET 4.6.1 se instalará automáticamente a través de la configuración cuando se instale [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] .

####  <a name="UA"></a> Asesor de actualizaciones
La vista previa del Asesor de actualizaciones de SQL Server 2016 es una herramienta independiente que permite que los usuarios de versiones anteriores ejecuten un conjunto de reglas de actualización en su base de datos SQL Server para identificar los cambios principales y de comportamiento y las características en desuso, además de prestar ayuda para la adopción de características nuevas, como Stretch Database.

 Puede descargar la vista previa del Asesor de actualizaciones [aquí](https://www.microsoft.com/en-us/download/details.aspx?id=48119) o puede instalarla con el Instalador de plataforma web.

## <a name="see-also"></a>Vea también
[Novedades de SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)
 
[Notas de la versión de SQL Server 2016](../sql-server/sql-server-2016-release-notes.md) 
 
[Instalar las Herramientas de administración de SQL Server con SSMS](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)









