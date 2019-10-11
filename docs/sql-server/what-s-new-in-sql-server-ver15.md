---
title: Novedades de SQL Server 2019 | Microsoft Docs
ms.date: 08/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e85461ef0a6395904b0f80590a01f035eb51dc3a
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952759"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>Novedades de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] se basa en versiones anteriores para potenciar SQL Server como una plataforma que proporciona diversas opciones de lenguajes de desarrollo, tipos de datos, entornos locales o en la nube, y sistemas operativos.

En este artículo se resumen las nuevas características y mejoras de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Para obtener más información y problemas conocidos, vea [Notas de la versión de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-ver15-release-notes.md).

**Use las [herramientas más recientes](what-s-new-in-sql-server-ver15-prerelease.md#tools) para obtener la mejor experiencia con [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].**

>[!NOTE]
>El contenido se publica para la versión candidata para lanzamiento [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. La versión candidata para lanzamiento es software de versión preliminar. La información está sujeta a cambios. Para obtener información sobre los escenarios de soporte técnico, consulte [Soporte técnico](#support).
>
>Esta versión incluye las mejoras que se anunciaron anteriormente en las versiones Community Technology Preview (CTP). Las mejoras agregaron características, errores corregidos, seguridad mejorada y rendimiento optimizado. Para obtener una lista de las características introducidas o mejoradas en las versiones anteriores a la versión candidata para lanzamiento de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], consulte [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Archivo de anuncios de CTP](what-s-new-in-sql-server-ver15-prerelease.md).

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] presenta [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] para [!INCLUDE[sql-server](../includes/ssnoversion-md.md)]. También proporciona funciones y mejoras adicionales para el motor de base de datos de SQL Server, SQL Server Analysis Services, SQL Server Machine Learning Services, SQL Server en Linux y SQL Server Master Data Services.

En las secciones siguientes se proporciona información general sobre estas características.

## <a name="data-virtualization-and-includebig-data-clusters-2019includesssbigdataclusters-ver15md"></a>Virtualización de datos y [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]

Hoy en día, las empresas son propietarias de ingentes cantidades de datos que constan de una amplia gama de conjuntos de datos en constante crecimiento hospedados en orígenes de datos almacenados en toda la empresa. Obtenga información casi en tiempo real de todos los datos con [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)], que proporcionan un entorno completo para trabajar con grandes conjuntos de datos, incluidas funciones de inteligencia artificial y aprendizaje automático.

| Nueva característica o actualización | Detalles |
|:---|:---|
| Solución de macrodatos escalable | [Implementación de clústeres escalables](../big-data-cluster/deploy-get-started.md) de contenedores de SQL Server, Spark y HDFS que se ejecutan en Kubernetes <br/><br/> Lectura, escritura y procesamiento de macrodatos desde Transact-SQL o Spark<br/><br/> Combinación y análisis de forma sencilla de datos relacionales de alto valor con macrodatos de gran volumen<br/><br/>Consulta de orígenes de datos externos<br/><br/>Almacenamiento de macrodatos en HDFS administrados mediante SQL Server<br/><br/>Consulta de datos de varios orígenes de datos externos a través del clúster<br/><br/> Uso de los datos para tareas de inteligencia artificial, aprendizaje automático y otras tareas de análisis<br/><br/> [Implementación y ejecución de aplicaciones](../big-data-cluster/concept-application-deployment.md) en [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] <br/><br/> La instancia maestra de SQL Server proporciona alta disponibilidad y recuperación ante desastres para todas las bases de datos mediante la tecnología de grupos de disponibilidad AlwaysOn<br/>|
|Virtualización de datos con PolyBase | Consulte datos de orígenes de datos externos de SQL Server, Oracle, Teradata, MongoDB y ODBC con tablas externas, ahora [compatibles con la codificación UTF-8](../relational-databases/collations/collation-and-unicode-support.md). Vea [Qué es PolyBase](../relational-databases/polybase/polybase-guide.md) para más información.|
| &nbsp; | &nbsp; |

Para obtener más información, consulte [Qué son [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] de SQL Server](../big-data-cluster/big-data-cluster-overview.md).

El [Archivo de anuncios de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] (CTP)](what-s-new-in-sql-server-ver15-prerelease.md) contiene una lista de características anunciadas y modificadas para las versiones anteriores de CTP de esta característica.

## <a name="intelligent-database"></a>Base de datos inteligente

### <a name="intelligent-query-processing"></a>Procesamiento de consultas inteligentes

|Nueva característica o actualización | Detalles |
|:---|:---|
|Comentarios de concesión de memoria del modo de fila |Se expande en la característica de comentarios de concesión de memoria de modo de proceso por lotes al ajustar los tamaños de concesión de memoria tanto para los operadores del modo de proceso por lotes como del modo de fila. Esto puede corregir automáticamente las concesiones excesivas que dan lugar a la pérdida de memoria y a una reducción de la simultaneidad, y corregir las concesiones de memoria insuficientes que causan derrames costosos en el disco. Consulte [Comentarios de concesión de memoria del modo de fila](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback). |
|Compilación diferida de variables de tabla|Mejora la calidad del plan y el rendimiento general de las consultas que hacen referencia a las variables de tabla. Durante la optimización y la compilación inicial, esta característica propaga las estimaciones de cardinalidad que se basan en los recuentos de filas de variables de tabla reales. Esta información precisa del recuento de filas optimiza las operaciones del plan de bajada. Consulte [Compilación diferida de variables de tabla](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation). |
|Procesamiento de consultas aproximado con `APPROX_COUNT_DISTINCT `|En escenarios en los que la precisión absoluta no es importante, pero la capacidad de respuesta es crítica, se agrega `APPROX_COUNT_DISTINCT` en grandes conjuntos de datos con menos recursos que `COUNT(DISTINCT())` para obtener una simultaneidad superior. Consulte [Procesamiento de consultas aproximado](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing).|
|Modo por lotes en el almacén de filas|El modo por lotes en el almacén de filas permite la ejecución en modo por lotes sin necesidad de índices de almacén de columnas. La ejecución en modo por lotes utiliza la CPU de manera más eficaz durante las cargas de trabajo analíticas, pero hasta [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] solo se usó cuando una consulta incluía operaciones con índices de almacén de columnas. Pero algunas aplicaciones pueden usar características que no son compatibles con los índices de almacén de columnas y, por lo tanto, no pueden aprovechar el modo por lotes. A partir de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], el modo por lotes está habilitado en las cargas de trabajo analíticas válidas cuyas consultas incluyan operaciones con cualquier tipo de índice (almacén de filas o almacén de columnas). Consulte [Modo por lotes en el almacén de filas](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore). |
|Inserción de UDF escalares|Transforma automáticamente las UDF escalares en expresiones relacionales y las inserta en la consulta SQL de llamada. Esta transformación mejora el rendimiento de las cargas de trabajo que aprovechan las UDF escalares. Vea [Inserción de UDF escalar](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining).|
| &nbsp; | &nbsp; |


### <a name="in-memory-database"></a>Base de datos en memoria

|Nueva característica o actualización | Detalles |
|:---|:---|
|Grupo de búferes híbrido| Nueva característica del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)], en que se accede directamente a las páginas de base de datos ubicadas en archivos de base de datos presentes en un dispositivo de memoria persistente (PMEM) cuando sea necesario. Vea [Grupo de búferes híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md).|
|Metadatos `tempdb` optimizados para memoria| [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduce una nueva característica que forma parte de la familia de características [Base de datos en memoria](../relational-databases/in-memory-database.md), metadatos `tempdb` optimizados para memoria, que quita este cuello de botella de forma eficaz y desbloquea un nuevo nivel de escalabilidad para cargas de trabajo intensivas de `tempdb`. En [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], las tablas del sistema implicadas en la administración de metadatos de la tabla temporal del sistema se pueden mover a tablas optimizadas para memoria no duraderas y sin bloqueos temporales. Consulte [Metadatos `tempdb` optimizados para memoria](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata).|
| Compatibilidad de OLTP en memoria para instantáneas de base de datos | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduce compatibilidad para crear [instantáneas de base de datos](../relational-databases/databases/database-snapshots-sql-server.md) de bases de datos que incluyen grupos de archivos optimizados para memoria. |
| &nbsp; | &nbsp; |

### <a name="intelligent-performance"></a>Rendimiento inteligente

|Nueva característica o actualización | Detalles |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|Activa una optimización en el [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que ayuda a mejorar el rendimiento de las inserciones de alta simultaneidad en el índice. Esta opción está diseñada para los índices que son propensos a la contención de inserción de la última página, que suele darse con índices que tienen una clave secuencial, como una columna de identidad, de secuencia o de fecha y hora. Para más información, consulte [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys).|
|Forzado de cursores estáticos y de avance rápido | Plan de Almacén de consultas para forzar la compatibilidad con cursores estáticos y de avance rápido. Vea [Plan para forzar la compatibilidad con cursores estáticos y de avance rápido](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23).|
|Regulación de recursos| El tipo de datos del valor configurable para la opción `REQUEST_MAX_MEMORY_GRANT_PERCENT` de `CREATE WORKLOAD GROUP` y `ALTER WORKLOAD GROUP` se ha cambiado de "integer" a "float" para permitir un mayor control granular de los límites de la memoria. Consulte [ALTER WORKLOAD GROUP](../t-sql/statements/alter-workload-group-transact-sql.md) y [CREATE WORKLOAD GROUP](../t-sql/statements/create-workload-group-transact-sql.md).|
|Recompilaciones reducidas para cargas de trabajo| Mejora el uso de tablas temporales en varios ámbitos. Vea [Recompilaciones reducidas para cargas de trabajo](../relational-databases/tables/tables.md#ctp23). |
|Escalabilidad de puntos de control indirectos |Vea [Escalabilidad mejorada de puntos de control indirectos](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23).|
|Actualizaciones de PFS simultáneas|[Las páginas PFS](https://techcommunity.microsoft.com/t5/SQL-Server/Under-the-covers-GAM-SGAM-and-PFS-pages/ba-p/383125) son páginas especiales dentro de un archivo de base de datos que SQL Server usa para ayudar a localizar espacio libre al asignar espacio para un objeto. La contención de bloqueos temporales de página en las páginas PFS es algo que normalmente se asocia con [`tempdb`](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d), pero también se puede producir en las bases de datos de usuario cuando hay muchos subprocesos de asignación de objetos simultáneos. Esta mejora cambia la manera en que se administra la simultaneidad con las actualizaciones de PFS para que puedan actualizarse en un bloqueo temporal compartido, en lugar de un bloqueo exclusivo. Este comportamiento está activado de forma predeterminada en todas las bases de datos (incluida `tempdb`) a partir de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].|
| &nbsp; | &nbsp; |

### <a name="monitoring"></a>Supervisión

|Nueva característica o actualización | Detalles |
|:---|:---|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | Nuevo tipo de espera en la vista de administración dinámica `sys.dm_os_wait_stats`. Muestra el tiempo de nivel de instancia acumulado empleado en las operaciones de actualización de estadísticas sincrónicas. Vea [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|
|Directiva de captura personalizada para el Almacén de consultas|Cuando se habilita, una nueva configuración de la directiva de captura del Almacén de consultas incluye más configuraciones del Almacén de consultas para ajustar la recopilación de datos en un servidor específico. Para obtener más información, vea [Opciones de ALTER DATABASE SET](../t-sql/statements/alter-database-transact-sql-set-options.md).|
|`LIGHTWEIGHT_QUERY_PROFILING`|Nueva configuración de ámbito de base de datos. Vea [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp). |
|`command` columna `sys.dm_exec_requests` | Muestra `SELECT (STATMAN)` si un elemento `SELECT` está esperando a que finalice una operación de actualización de estadísticas sincrónica para continuar con la ejecución de la consulta. Vea [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|
|`sys.dm_exec_query_plan_stats` |La nueva DMF devuelve el equivalente del último plan de ejecución real conocido para la mayoría de las consultas. Vea [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md).|
|`LAST_QUERY_PLAN_STATS` | Nueva configuración de ámbito de base de datos para habilitar `sys.dm_exec_query_plan_stats`. Vea [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|`query_post_execution_plan_profile` | El evento extendido recopila el equivalente de un plan de ejecución real en función de la generación de perfiles ligera, a diferencia de `query_post_execution_showplan`, que utiliza la generación de perfiles estándar. Vea [Infraestructura de generación de perfiles de consultas](../relational-databases/performance/query-profiling-infrastructure.md).|
|`sys.dm_db_page_info(database_id, file_id, page_id, mode)` | La nueva DMF devuelve información sobre una página de una base de datos. Consulte [sys.dm_db_page_info (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md).|
| &nbsp; | &nbsp; |

## <a name="developer-experience"></a>Experiencia del desarrollador

### <a name="graph"></a>Gráfico

|Nueva característica o actualización | Detalles |
|:---|:---|
|Acciones de eliminación en cascada de restricción perimetral |Definir acciones de eliminación en cascada en una restricción perimetral de una base de datos del gráfico. Consulte [Restricciones perimetrales](../relational-databases/tables/graph-edge-constraints.md). |
|Nueva función de grafo: `SHORTEST_PATH` | Use `SHORTEST_PATH` dentro de `MATCH` para encontrar la ruta más corta entre dos nodos en un grafo o para realizar recorridos de longitud arbitraria.|
|Índices y tablas de particiones| Los datos de tablas e índices con particiones se dividen en unidades que pueden propagarse por más de un grupo de archivos de una base de datos de grafos. |
|Uso de alias de vista o tabla derivada en una consulta de coincidencia del grafo. |Vea [Consulta de coincidencia de grafos](../t-sql/queries/match-sql-graph.md). |
| &nbsp; | &nbsp; |

### <a name="unicode-support"></a>Compatibilidad con Unicode

|Nueva característica o actualización | Detalles |
|:---|:---|
|Compatibilidad con la codificación de caracteres UTF-8 |Se admite el carácter UTF-8 para la codificación de importación y exportación, y como intercalación de nivel de base de datos o de columna para los datos de cadena. Esto permite que las aplicaciones se extiendan a una escala global, en que el requisito de proporcionar servicios y aplicaciones de bases de datos multilingües mundiales es fundamental para satisfacer las demandas de los clientes y las normativas de mercado específicas. Vea [Compatibilidad con la intercalación y Unicode](../relational-databases/collations/collation-and-unicode-support.md).<br/><br/> La versión candidata para lanzamiento de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] habilita la compatibilidad con UTF-8 para las tablas externas de Polybase y Always Encrypted.|
| &nbsp; | &nbsp; |

### <a name="language-extensions"></a>Extensiones de lenguaje

|Nueva característica o actualización | Detalles |
|:---|:---|
|Nuevo SDK del lenguaje Java | Simplifica el desarrollo de los programas Java que se pueden ejecutar desde SQL Server. Vea [SDK de extensibilidad de Microsoft para Java para SQL Server](../language-extensions/how-to/extensibility-sdk-java-sql-server.md). |
|El SDK del lenguaje Java está en código abierto |El [SDK de extensibilidad de Microsoft para Java para Microsoft SQL Server](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) está ahora en código abierto y [disponible en GitHub](https://github.com/microsoft/sql-server-language-extensions).|
|Compatibilidad con tipos de datos de Java|Vea [Java data types](../language-extensions/how-to/java-to-sql-data-types.md) (Tipo de datos Java).|
|Nuevo runtime de Java predeterminado | Ahora, SQL Server incluye Zulu Embedded de Azul Systems para agregar compatibilidad con Java en todo el producto. Para obtener más información, vea [Compatibilidad gratuita con Java en SQL Server 2019 ya está disponible](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/). |
|Extensiones de lenguaje de SQL Server| Ejecute código externo con el marco de extensibilidad. Consulte [Extensiones de lenguaje de SQL Server](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview).
|Registrar lenguajes externos|La nueva instrucción DDL `CREATE EXTERNAL LANGUAGE` registra lenguajes externos, como Java, en SQL Server. Vea [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) (CREAR UN LENGUAJE EXTERNO). |
| &nbsp; | &nbsp; |

### <a name="spatial"></a>Espacial

|Nueva característica o actualización | Detalles |
|:---|:---|
| Nuevos identificadores de referencia espacial (SRID) |La [australiana GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) proporciona datos más sólidos y precisos, más estrechamente alineados con sistemas de posicionamiento global. Los nuevos SRID son:<br/><br/> - 7843 para 2D geográfico<br/> - 7844 para 3D geográfico <br/><br/>La vista [sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) contiene las definiciones de nuevos SRID. |
| &nbsp; | &nbsp; |

### <a name="error-messages"></a>Mensajes de error

|Nueva característica o actualización | Detalles |
|:---|:---|
|Advertencias de truncamiento detalladas | Valores predeterminados del mensaje de error de truncamiento para incluir los nombres de tabla y columna, así como el valor truncado. Vea [VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation).|
| &nbsp; | &nbsp; |

## <a name="mission-critical-security"></a>Seguridad crítica

|Nueva característica o actualización | Detalles |
|:---|:---|
|Always Encrypted con enclaves seguros|Expande Always Encrypted con cifrado en contexto y cálculos enriquecidos mediante la habilitación de cálculos en los datos de texto no cifrado dentro de un enclave seguro del lado servidor. El cifrado en contexto mejora el rendimiento y la confiabilidad de las operaciones criptográficas (cifrado de columnas, rotación de las claves de cifrado de columnas, etc.), ya que evita mover los datos fuera de la base de datos. La compatibilidad con cálculos enriquecidos (operaciones de coincidencia y comparación de patrones) abre Always Encrypted a un conjunto mucho más amplio de escenarios y aplicaciones que demandan protección de datos confidenciales, a la vez que requieren funciones más enriquecidas en las consultas de Transact-SQL. [Always Encrypted con enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md).|
|Administración de certificados en el Administrador de configuración de SQL Server|Vea [Administración de certificados (Administrador de configuración de SQL Server)](../database-engine/configure-windows/manage-certificates.md).|
| &nbsp; | &nbsp; |

## <a name="high-availability"></a>Alta disponibilidad

### <a name="availability-groups"></a>Grupos de disponibilidad

|Nueva característica o actualización | Detalles |
|:---|:---|
|Hasta cinco réplicas sincrónicas|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] aumenta el número máximo de réplicas sincrónicas a 5, de las 3 que eran en [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Puede configurar este grupo de cinco réplicas para habilitar la conmutación automática por error dentro del grupo. Hay una réplica principal, además de cuatro réplicas secundarias sincrónicas.|
|Redireccionamiento de la conexión de réplicas de secundaria a principal| Permite que las conexiones de las aplicaciones cliente se dirijan a la réplica principal, independientemente del servidor de destino especificado en la cadena de conexión. Para obtener más información, consulte [Secondary to primary replica read/write connection redirection (Always On Availability Groups)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md) (Redireccionamiento de la conexión de lectura/escrita de réplicas de secundaria a principal [Grupos de disponibilidad Always On]).|
| &nbsp; | &nbsp; |

### <a name="recovery"></a>Recuperación

|Nueva característica o actualización | Detalles |
|:---|:---|
|Recuperación acelerada de bases de datos. | Habilitación de la recuperación de base de datos acelerada por base de datos. Vea [Recuperación acelerada de bases de datos](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr).|
| &nbsp; | &nbsp; |

### <a name="resumable-operations"></a>Operaciones reanudables

|Nueva característica o actualización | Detalles |
|:---|:---|
|Compilación y recompilación en línea de índices de almacén de columnas en clúster | Vea [Realización de operaciones de índice en línea](../relational-databases/indexes/perform-index-operations-online.md). |
|Compilación reanudable en línea de índices de almacén de filas | Vea [Realización de operaciones de índice en línea](../relational-databases/indexes/perform-index-operations-online.md). |
|Suspensión y reanudación del examen inicial del Cifrado de datos transparente (TDE)|Vea [Análisis del Cifrado de datos transparente (TDE): suspensión y reanudación](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume).|
| &nbsp; | &nbsp; |

## <a name="setup"></a>Configurar 

|Nueva característica o actualización | Detalles | 
|:---|:---| 
|Nuevas opciones de configuración de memoria | Durante la instalación, establece las configuraciones de servidor *memoria de servidor mínima (MB)* y *memoria de servidor máxima (MB)* . Para obtener más información, consulte [Configuración del motor de base de datos: página de memoria](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#memory) y los parámetros `USESQLRECOMMENDEDMEMORYLIMITS`, `SQLMINMEMORY` y `SQLMAXMEMORY` en [Instalar SQL Server desde el símbolo del sistema](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install). El valor propuesto se alineará con las directrices de configuración de memoria en [Opciones de configuración de memoria del servidor](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually).| 
|Opciones de configuración de nuevo paralelismo | Durante la instalación, establece la configuración del servidor *Grado máximo de paralelismo*. Para obtener más información, consulte [Configuración del motor de base de datos: página MaxDOP](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#maxdop) y el parámetro `SQLMAXDOP` en [Instalar SQL Server desde el símbolo del sistema](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install). El valor predeterminado se alineará con las directrices sobre el grado máximo de paralelismo en [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines).| 
| &nbsp; | &nbsp; |

## <a name="platform-choice"></a>Elección de la plataforma

### <a id="sql-server-on-linux"></a>Linux

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Nuevo registro de contenedor|[Empezar a trabajar con contenedores de SQL Server con Docker](../linux/quickstart-install-connect-docker.md) |
|Compatibilidad con la replicación |[Replicación de SQL Server en Linux](../linux/sql-server-linux-replication.md)
|Compatibilidad con el Coordinador de transacciones distribuidas de Microsoft (MSDTC) |[Cómo configurar el Coordinador de transacciones distribuidas de Microsoft (MSDTC) en Linux](../linux/sql-server-linux-configure-msdtc.md) |
|Compatibilidad de OpenLDAP con proveedores terceros de AD |[Tutorial: Usar la autenticación de Active Directory con SQL Server en Linux](../linux/sql-server-linux-active-directory-authentication.md) |
|Machine Learning en Linux |[Instalar Machine Learning en Linux](../linux/sql-server-linux-setup-machine-learning.md) |
|Mejoras de `tempdb` | De forma predeterminada, una nueva instalación de SQL Server en Linux crea varios archivos de datos `tempdb` en función del número de núcleos lógicos (con un máximo de 8 archivos de datos). Esto no es aplicable a actualizaciones de versión principal o secundaria en contexto. Cada archivo `tempdb` es de 8 MB con un crecimiento automático de 64 MB. Este comportamiento es similar a la instalación de SQL Server predeterminada en Windows. |
| PolyBase en Linux | [Instale PolyBase](../relational-databases/polybase/polybase-linux-setup.md) en Linux para conectores que no son Hadoop.<br/><br/>[Asignación del tipo de PolyBase](../relational-databases/polybase/polybase-type-mapping.md). |
| Compatibilidad con Captura de datos modificados (CDC) | Captura de datos modificados (CDC) ahora es compatible con Linux para SQL Server 2019. |
| &nbsp; | &nbsp; |

### <a name="containers"></a>Contenedores

|Nueva característica o actualización | Detalles |
|:---|:---|
| Registro de contenedor de Microsoft | Ahora [Registro de contenedor de Microsoft](https://www.ntweekly.com/2019/09/23/microsoft-container-registry-to-replace-docker-hub-for-new-images/) reemplaza a Docker Hub para nuevas imágenes de contenedor de Microsoft oficiales, incluido [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. |
| Contenedores no raíz | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] presenta la capacidad de crear contenedores más seguros mediante el inicio del proceso de [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] como un usuario no raíz de forma predeterminada. Vea [Compilación y ejecución de contenedores de SQL Server como un usuario no raíz](../linux/sql-server-linux-configure-docker.md#buildnonrootcontainer) para más información. |
| &nbsp; | &nbsp; |

## <a id="ml"></a> Machine Learning Services de SQL Server

|Nueva característica o actualización | Detalles |
|:---|:---|
|Modelos basados en particiones|Procese scripts externos por partición de los datos mediante los nuevos parámetros agregados a `sp_execute_external_script`. Esta funcionalidad admite el aprendizaje de muchos modelos pequeños (un modelo por cada partición de datos) en lugar de uno grande. Vea [Creación de modelos basados en particiones](../advanced-analytics/tutorials/r-tutorial-create-models-per-partition.md).|
|Clúster de conmutación por error de Windows Server| Configure la alta disponibilidad de Machine Learning Services en un clúster de conmutación por error de Windows Server.|
| &nbsp; | &nbsp; |

## [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]

| Nueva característica o actualización | Detalles |
|:---|:---|
|Admite las bases de datos de instancias administradas de Azure SQL Database.| Hospeda [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] en una instancia administrada. Vea [Instalación y configuración de [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]](../master-data-services/master-data-services-installation-and-configuration.md#SetUpWeb).|
|Nuevos controles HTML| Los controles HTML reemplazan a los componentes anteriores de Silverlight. Quitada la dependencia de Silverlight.|
| &nbsp; | &nbsp; |

## <a name="sql-server-analysis-services"></a>SQL Server Analysis Services

| Nueva característica o actualización | Detalles |
|:---|:---|
|Intercalación de consultas| Consulte [Intercalación de consultas](https://docs.microsoft.com/analysis-services/tabular-models/query-interleaving) |
|Compatibilidad de la consulta MDX para los modelos tabulares con grupos de cálculo | Vea [Grupos de cálculo](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). |
|Grupos de cálculo en el modelo tabular| [Grupos de cálculo en el modelo tabular](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24) |
|Compatibilidad de la consulta MDX para los modelos tabulares con grupos de cálculo | Vea [Grupos de cálculo](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). |
|Formato dinámico de medidas con grupos de cálculo |Esta característica le permite cambiar condicionalmente las cadenas de formato para las medidas con [grupos de cálculo](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). Por ejemplo, con la conversión de moneda, se puede mostrar una medida con divisas en diferentes formatos.|
|Relaciones varios a varios en modelos tabulares|[Relaciones varios a varios en modelos tabulares](what-s-new-in-sql-server-ver15-prerelease.md#many-to-many-ctp24)|
|Configuración de propiedad para la gobernanza de recursos|[Configuración de propiedad para la gobernanza de recursos](what-s-new-in-sql-server-ver15-prerelease.md#property-ctp24)|
| Configuración de gobernanza para las actualizaciones de la caché de Power BI.  | El servicio Power BI almacena en caché los datos del icono del panel y los datos del informe para la carga inicial del informe de Live Connect, lo que provoca un número excesivo de consultas de caché que se envían a SSAS y, en casos extremos, la sobrecarga del servidor. En esta versión se incluye la propiedad **ClientCacheRefreshPolicy**. Esta propiedad permite invalidar este comportamiento en el nivel de servidor. Para obtener más información, vea [Propiedades generales](https://docs.microsoft.com/analysis-services/server-properties/general-properties). |
| Adjunto en línea  | Esta característica ofrece la posibilidad de adjuntar un modelo tabular como una operación en línea. Adjunto en línea se puede usar para la sincronización de réplicas de solo lectura en entornos locales de escalabilidad horizontal de consultas. Para obtener más información, en Detalles vea [Adjunto en línea](what-s-new-in-sql-server-ver15-prerelease.md#online-attach-ctp32). |
| &nbsp; | &nbsp; |

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

Para consultar las características específicas que se excluyen del soporte técnico, vea las [notas de la versión](sql-server-ver15-release-notes.md).

Además, se han incorporado o mejorado las características siguientes de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2.

## <a name="see-also"></a>Vea también

- [`SqlServer` Módulo de PowerShell](https://www.powershellgallery.com/packages/Sqlserver)
- [Documentación de SQL Server PowerShell](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>Pasos siguientes

- Notas de la versión de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-ver15-release-notes.md).

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]: Notas técnicas del producto](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />Publicado en septiembre de 2018. Se aplica a Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0 para Windows, Linux y contenedores de Docker.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
