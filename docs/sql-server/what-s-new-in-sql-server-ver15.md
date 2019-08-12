---
title: Novedades de SQL Server 2019 | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: caf8b23b823d7863e1bd7c8abd01ef43b0b8ec20
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702892"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>Novedades de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] se basa en versiones anteriores para potenciar SQL Server como una plataforma que proporciona diversas opciones de lenguajes de desarrollo, tipos de datos, entornos locales o en la nube, y sistemas operativos.

En este artículo se resumen las nuevas características y mejoras de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Para obtener más información y problemas conocidos, vea [Notas de la versión de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-ver15-release-notes.md).

**Use las [herramientas más recientes](what-s-new-in-sql-server-ver15-prerelease.md#tools) para obtener la mejor experiencia con [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].**

## <a name="ctp-32-july-2019"></a>CTP 3.2, julio de 2019

Community Technology Preview (CTP) 3.2 es la versión pública más reciente de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Esta versión incluye mejoras respecto a versiones anteriores de CTP para corregir errores, mejorar la seguridad y optimizar el rendimiento. Para obtener una lista de las características introducidas o mejoradas en cada una de las versiones anteriores a [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2, vea [Archivo de anuncios de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP](what-s-new-in-sql-server-ver15-prerelease.md).

### <a name="new-in-big-data-clusters"></a>Novedades de los clústeres de macrodatos

|Nueva característica o actualización | Detalles |
|:---|:---|
|Versión preliminar pública |Antes de CTP 3.2, el clúster de macrodatos de SQL Server estaba disponible para los usuarios pioneros registrados. Esta versión permite a todo el mundo experimentar las características de los clústeres de macrodatos de SQL Server. <br/><br/> Vea [Introducción a los clústeres de macrodatos de SQL Server](../big-data-cluster/deploy-get-started.md).|
|`azdata` |CTP 3.2 presenta `azdata`: una utilidad de línea de comandos escrita en Python que permite a los administradores de clústeres arrancar y administrar el clúster de macrodatos mediante las API REST. `azdata` reemplaza a `mssqlctl`. Vea [Instalación de `azdata`](../big-data-cluster/deploy-install-azdata.md). |
|PolyBase |Los nombres de las columnas de la tabla externa ahora se usan para consultar orígenes de datos de ODBC, SQL Server, Oracle, Teradata y MongoDB. En versiones anteriores de CTP, las columnas se enlazaban solo según el ordinal en el destino y los nombres de las columnas de la definición de tabla externa no se usaban.|
|Actualización de niveles de HDFS |Presentamos la funcionalidad de actualización de niveles de HDFS, gracias a la que se puede actualizar un montaje existente a la instantánea más reciente de los datos remotos. Vea [Niveles de HDFS](../big-data-cluster/hdfs-tiering.md). |
|Solución de problemas basada en cuadernos |CTP 3.2 presenta cuadernos de Jupyter para ayudar con la [implementación](../big-data-cluster/deploy-notebooks.md) y la [detección, el diagnóstico y la solución de problemas](../big-data-cluster/manage-notebooks.md) de componentes en un clúster de macrodatos de SQL Server. |
| &nbsp; | &nbsp; |

### <a name="new-in-analysis-services"></a>Novedades de Analysis Services

| Nueva característica o actualización | Detalles |
|:---|:---| 
| Configuración de gobernanza para las actualizaciones de la caché de Power BI.  | El servicio Power BI almacena en caché los datos del icono del panel y los datos del informe para la carga inicial del informe de Live Connect, lo que provoca un número excesivo de consultas de caché que se envían a SSAS y, en casos extremos, la sobrecarga del servidor. En esta versión se incluye la propiedad **ClientCacheRefreshPolicy**. Esta propiedad permite invalidar este comportamiento en el nivel de servidor. Para obtener más información, vea [Propiedades generales](../analysis-services/server-properties/general-properties.md). |
| Adjunto en línea  | Esta característica ofrece la posibilidad de adjuntar un modelo tabular como una operación en línea. Adjunto en línea se puede usar para la sincronización de réplicas de solo lectura en entornos locales de escalabilidad horizontal de consultas. Para obtener más información, en Detalles vea [Adjunto en línea](what-s-new-in-sql-server-ver15-prerelease.md#online-attach-ctp32). |
| &nbsp; | &nbsp; |

### <a name="new-in-language-extensions"></a>Novedades de Extensiones de lenguaje

|Nueva característica o actualización | Detalles |
|:---|:---|
| Nuevo runtime de Java predeterminado  | SQL Server ahora incluye Zulu Embedded de Azul System para agregar compatibilidad con Java en todo el producto. Para obtener más información, vea [Compatibilidad gratuita con Java en SQL Server 2019 ya está disponible](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/). |

### <a name="new-in-sql-server-on-linux"></a>Novedades de SQL Server en Linux

|Nueva característica o actualización | Detalles |
|:---|:---|
| Compatibilidad con Captura de datos modificados (CDC) | Captura de datos modificados (CDC) ahora es compatible con Linux para SQL Server 2019. |

## <a name="includesql-server-2019includessssqlv15-mdmd-features-by-component"></a>Características de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] por componente

En las secciones siguientes se resaltan los nuevos componentes y características que se mejoraron en versiones anteriores de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## <a name="big-data-clusters"></a>Clústeres de macrodatos

| Nueva característica o actualización | Detalles |
|:---|:---|
| Solución de macrodatos escalable | [Implementación de clústeres escalables](../big-data-cluster/deploy-get-started.md) de contenedores de SQL Server, Spark y HDFS que se ejecutan en Kubernetes <br/><br/> Lectura, escritura y procesamiento de macrodatos desde Transact-SQL o Spark<br/><br/> Combinación y análisis de forma sencilla de datos relacionales de alto valor con macrodatos de gran volumen<br/><br/>Consulta de orígenes de datos externos<br/><br/>Almacenamiento de macrodatos en HDFS administrados mediante SQL Server<br/><br/>Consulta de datos de varios orígenes de datos externos a través del clúster<br/><br/> Uso de los datos para tareas de inteligencia artificial, aprendizaje automático y otras tareas de análisis<br/><br/> Implementación y ejecución de aplicaciones en clústeres de macrodatos <br/>|
| &nbsp; | &nbsp; |

Para obtener más información, vea [¿Qué son los clústeres de macrodatos de SQL Server?](../big-data-cluster/big-data-cluster-overview.md)

El [Archivo de anuncios de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] (CTP)](what-s-new-in-sql-server-ver15-prerelease.md) contiene una lista de características anunciadas y modificadas para las versiones anteriores de CTP de esta característica.

## <a name="database-engine"></a>Motor de base de datos

### <a name="security"></a>Seguridad

|Nueva característica o actualización | Detalles |
|:---|:---|
|Restricciones de características| Impida que algunas formas de inyección de SQL filtren información sobre la base de datos, incluso cuando la inyección de SQL se realice correctamente. Vea [Restricciones de características](../relational-databases/security/feature-restrictions.md)|
|Indexación de columnas cifradas|Cree índices en columnas cifradas mediante cifrado aleatorio y claves habilitadas para enclave, a fin de mejorar el rendimiento de consultas enriquecidas (con `LIKE` y operadores de comparación). [Always Encrypted con enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md).
|Suspensión y reanudación del examen inicial del Cifrado de datos transparente (TDE)|Vea [Análisis del Cifrado de datos transparente (TDE): suspensión y reanudación](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)|
|Administración de certificados en el Administrador de configuración de SQL Server|Vea [Administración de certificados (Administrador de configuración de SQL Server)](../database-engine/configure-windows/manage-certificates.md)
| &nbsp; | &nbsp; |


### <a name="graph"></a>Gráfico

|Nueva característica o actualización | Detalles |
|:---|:---|
|Acciones de eliminación en cascada de restricción perimetral |Definir acciones de eliminación en cascada en una restricción perimetral de una base de datos del gráfico. Vea [Restricciones perimetrales](../relational-databases/tables/graph-edge-constraints.md). |
|Nueva función de grafo: `SHORTEST_PATH` | Use `SHORTEST_PATH` dentro de `MATCH` para encontrar la ruta más corta entre dos nodos en un grafo o para realizar recorridos de longitud arbitraria.|
|Índices y tablas de particiones| Los datos de tablas e índices con particiones se dividen en unidades que pueden propagarse por más de un grupo de archivos de una base de datos de grafos. |
|Uso de alias de vista o tabla derivada en una consulta de coincidencia del grafo. |Vea [Restricciones perimetrales del grafo](../relational-databases/tables/graph-edge-constraints.md). |
| &nbsp; | &nbsp; |

### <a name="indexes"></a>Índices

|Nueva característica o actualización | Detalles |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|Activa una optimización en el motor de base de datos que ayuda a mejorar el rendimiento de las inserciones de alta simultaneidad en el índice. Esta opción está diseñada para los índices que son propensos a la contención de inserción de la última página, que suele darse con índices que tienen una clave secuencial, como una columna de identidad, de secuencia o de fecha y hora. Para más información, consulte [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys).|
|Compilación y recompilación en línea de índices de almacén de columnas en clúster | Vea [Realización de operaciones de índice en línea](../relational-databases/indexes/perform-index-operations-online.md). |
| &nbsp; | &nbsp; |

### <a name="in-memory-databases"></a>En bases de datos de memoria

|Nueva característica o actualización | Detalles |
|:---|:---|
|Control de DDL para el grupo de búferes híbrido |Con el [grupo de búferes híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md), se accede directamente a las páginas de base de datos ubicadas en archivos de base de datos presentes en un dispositivo de memoria persistente (PMEM) cuando sea necesario.|
|Metadatos tempdb optimizados para memoria|Vea [Metadatos tempdb optimizados para memoria](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata).|
| &nbsp; | &nbsp; |

### <a name="linked-servers"></a>Servidores vinculados

|Nueva característica o actualización | Detalles |
|:---|:---|
|Los servidores vinculados admiten la codificación de caracteres UTF-8. |[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md) |
| &nbsp; | &nbsp; |

### <a name="polybase"></a>PolyBase

|Nueva característica o actualización | Detalles |
|:---|:---|
|PolyBase |Los nombres de las columnas de la tabla externa ahora se usan para consultar orígenes de datos de ODBC, SQL Server, Oracle, Teradata y MongoDB. |
| &nbsp; | &nbsp; |

### <a name="collation"></a>Intercalación

|Nueva característica o actualización | Detalles |
|:---|:---|
|Compatibilidad con la codificación de caracteres UTF-8 |Habilitada para una intercalación BIN2 (`Latin1_General_100_BIN2_UTF8`). Vea [Compatibilidad con la intercalación y Unicode](../relational-databases/collations/collation-and-unicode-support.md). |
|Selección de la intercalación de UTF-8 como valor predeterminado durante la configuración | Vea [Compatibilidad con la intercalación y Unicode](../relational-databases/collations/collation-and-unicode-support.md#ctp23). |
| &nbsp; | &nbsp; |

### <a name="server-settings"></a>Configuración del servidor

|Nueva característica o actualización | Detalles |
|:---|:---|
|Establecer los valores de memoria del servidor `MIN` y `MAX` en la instalación |Durante la instalación, puede establecer los valores de memoria del servidor. Use los valores predeterminados (los valores calculados recomendados) o especifique manualmente sus propios valores una vez que haya elegido la opción **recomendada**[Opciones de configuración del servidor de memoria](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually).|
|La instalación de SQL Server habilita la configuración de MAXDOP |Las nuevas recomendaciones siguen las directrices documentadas. [Configure la opción de configuración del servidor grado máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)|
|Grupo de búferes híbrido| Característica nueva del motor de base de datos de SQL Server donde se accederá directamente a las páginas de base de datos ubicadas en archivos de base de datos presentes en un dispositivo de memoria persistente (PMEM) cuando sea necesario. Vea [Grupo de búferes híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md).|
| &nbsp; | &nbsp; |

### <a name="performance-monitoring"></a>Supervisión de rendimiento

|Nueva característica o actualización | Detalles |
|:---|:---|
|Inserción de UDF escalar |Transforma automáticamente funciones definidas por el usuario (UDF) escalares en expresiones relacionales y las inserta en la consulta SQL de llamada. Vea [Inserción de UDF escalar](../relational-databases/user-defined-functions/scalar-udf-inlining.md). |
| `command` columna `sys.dm_exec_requests` | Muestra `SELECT (STATMAN)` si un elemento `SELECT` está esperando a que finalice una operación de actualización de estadísticas sincrónica para continuar con la ejecución de la consulta. Vea [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | Nuevo tipo de espera en la vista de administración dinámica `sys.dm_os_wait_stats`. Muestra el tiempo de nivel de instancia acumulado empleado en las operaciones de actualización de estadísticas sincrónicas. Vea [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|
|Directiva de captura personalizada para el Almacén de consultas|Cuando se habilita, una nueva configuración de la directiva de captura del Almacén de consultas incluye más configuraciones del Almacén de consultas para ajustar la recopilación de datos en un servidor específico. Para obtener más información, vea [Opciones de ALTER DATABASE SET](../t-sql/statements/alter-database-transact-sql-set-options.md).|
|`sys.dm_exec_query_plan_stats` |La nueva DMF devuelve el equivalente del último plan de ejecución real conocido para la mayoría de las consultas. Vea [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md).|
|`LAST_QUERY_PLAN_STATS` | Nueva configuración de ámbito de base de datos para habilitar `sys.dm_exec_query_plan_stats`. Vea [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|`LIGHTWEIGHT_QUERY_PROFILING`|Nueva configuración de ámbito de base de datos. Vea [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp). |
|`query_post_execution_plan_profile` | El evento extendido recopila el equivalente de un plan de ejecución real en función de la generación de perfiles ligera, a diferencia de `query_post_execution_showplan`, que utiliza la generación de perfiles estándar. Vea [Infraestructura de generación de perfiles de consultas](../relational-databases/performance/query-profiling-infrastructure.md).|
|Comentarios de concesión de memoria del modo de fila. |[Comentarios de concesión de memoria del modo de fila](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback) |
|Compilación diferida de variables de tabla.|[Compilación diferida de variables de tabla](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation) |
|Aproximadamente `COUNT DISTINCT`.|[Procesamiento de consultas aproximado](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing)|
|Modo por lotes en el almacén de filas.|[Modo por lotes en el almacén de filas](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore) |

### <a name="language-extensions"></a>Extensiones de lenguaje

|Nueva característica o actualización | Detalles |
|:---|:---|
|Nuevo SDK del lenguaje Java | Simplifica el desarrollo de los programas Java que se pueden ejecutar desde SQL Server. Vea [Novedades de SQL Server Machine Learning Services](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md). |
|Extensiones de lenguaje de SQL Server: [extensión del lenguaje Java](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)|El [SDK de extensibilidad de Microsoft para Java para Microsoft SQL Server](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) está ahora en código abierto y [disponible en GitHub](https://github.com/microsoft/sql-server-language-extensions).|
|Registrar lenguajes externos|La nueva instrucción DDL `CREATE EXTERNAL LANGUAGE` registra lenguajes externos, como Java, en SQL Server. Vea [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) (CREAR UN LENGUAJE EXTERNO). |
|Compatibilidad con tipos de datos de Java|Vea [Java data types](../language-extensions/how-to/java-to-sql-data-types.md) (Tipo de datos Java).|

### <a name="spatial"></a>Espacial

|Nueva característica o actualización | Detalles |
|:---|:---|
| Nuevos identificadores de referencia espacial (SRID) |La [australiana GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) proporciona datos más sólidos y precisos, más estrechamente alineados con sistemas de posicionamiento global. Los nuevos SRID son:<br/><br/> - 7843: 2D geográfico<br/> - 7844: 3D geográfico <br/><br/>La vista [sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) contiene las definiciones de nuevos SRID. |
| &nbsp; | &nbsp; |

### <a name="performance"></a>Rendimiento

|Nueva característica o actualización | Detalles |
|:---|:---|
|Recuperación acelerada de bases de datos. | Habilitación de la recuperación de base de datos acelerada por base de datos. Vea [Recuperación acelerada de bases de datos](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr).|
|Forzado de cursores estáticos y de avance rápido | Plan de Almacén de consultas para forzar la compatibilidad con cursores estáticos y de avance rápido. Vea [Plan para forzar la compatibilidad con cursores estáticos y de avance rápido](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23).|
|Recompilaciones reducidas para cargas de trabajo| Mejora el uso de tablas temporales en varios ámbitos. Vea [Recompilaciones reducidas para cargas de trabajo](../relational-databases/tables/tables.md#ctp23). |
|Escalabilidad de puntos de control indirectos |Vea [Escalabilidad mejorada de puntos de control indirectos](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23).|
| &nbsp; | &nbsp; |

### <a name="availability-groups"></a>Grupos de disponibilidad

|Nueva característica o actualización | Detalles |
|:---|:---|
|Hasta cinco réplicas sincrónicas|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] aumenta el número máximo de réplicas sincrónicas a 5, de las 3 que eran en [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Puede configurar este grupo de cinco réplicas para habilitar la conmutación automática por error dentro del grupo. Hay una réplica principal, además de cuatro réplicas secundarias sincrónicas.|
|Redireccionamiento de la conexión de réplicas de secundaria a principal| Permite que las conexiones de las aplicaciones cliente se dirijan a la réplica principal, independientemente del servidor de destino especificado en la cadena de conexión. Para obtener más información, consulte [Secondary to primary replica read/write connection redirection (Always On Availability Groups)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md) (Redireccionamiento de la conexión de lectura/escrita de réplicas de secundaria a principal [Grupos de disponibilidad Always On]).|
| &nbsp; | &nbsp; |

### <a name="error-messages"></a>Mensajes de error

|Nueva característica o actualización | Detalles |
|:---|:---|
|Advertencias de truncamiento detalladas | Valores predeterminados del mensaje de error de truncamiento para incluir los nombres de tabla y columna, así como el valor truncado. Vea [VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation).|
| &nbsp; | &nbsp; |

## <a name="sql-server-on-linux"></a>SQL Server en Linux

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Nuevo registro de contenedor|[Empezar a trabajar con contenedores de SQL Server con Docker](../linux/quickstart-install-connect-docker.md) |
|Grupo de disponibilidad Always On en contenedores de Docker con Kubernetes |[Grupos de disponibilidad Always On para contenedores](../linux/sql-server-ag-kubernetes.md) |
|Compatibilidad con la replicación |[Replicación de SQL Server en Linux](../linux/sql-server-linux-replication.md)
|Compatibilidad con el Coordinador de transacciones distribuidas de Microsoft (MSDTC) |[Cómo configurar el Coordinador de transacciones distribuidas de Microsoft (MSDTC) en Linux](../linux/sql-server-linux-configure-msdtc.md) |
|Compatibilidad de OpenLDAP con proveedores terceros de AD |[Tutorial: Usar la autenticación de Active Directory con SQL Server en Linux](../linux/sql-server-linux-active-directory-authentication.md) |
|Machine Learning en Linux |[Instalar Machine Learning en Linux](../linux/sql-server-linux-setup-machine-learning.md) |
|Mejoras de tempdb | De forma predeterminada, una nueva instalación de SQL Server en Linux crea varios archivos de datos tempdb en función del número de núcleos lógicos (con un máximo de 8 archivos de datos). Esto no es aplicable a actualizaciones de versión principal o secundaria en contexto. Cada archivo tempdb es de 8 MB con un crecimiento automático de 64 MB. Este comportamiento es similar a la instalación de SQL Server predeterminada en Windows. |
| PolyBase en Linux | [Instale PolyBase](../relational-databases/polybase/polybase-linux-setup.md) en Linux para conectores que no son Hadoop.<br/><br/>[Asignación del tipo de PolyBase](../relational-databases/polybase/polybase-type-mapping.md). |
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

## <a name="analysis-services"></a>Analysis Services

| Nueva característica o actualización | Detalles |
|:---|:---|
|Grupos de cálculo en el modelo tabular| [Grupos de cálculo en el modelo tabular](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24) |
|Compatibilidad de la consulta MDX para los modelos tabulares con grupos de cálculo | Vea [Grupos de cálculo](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). |
|Formato dinámico de medidas con grupos de cálculo |Esta característica le permite cambiar condicionalmente las cadenas de formato para las medidas con [grupos de cálculo](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). Por ejemplo, con la conversión de moneda, se puede mostrar una medida con divisas en diferentes formatos.|
|Relaciones varios a varios en modelos tabulares|[Relaciones varios a varios en modelos tabulares](what-s-new-in-sql-server-ver15-prerelease.md#many-to-many-ctp24)|
|Configuración de propiedad para la gobernanza de recursos|[Configuración de propiedad para la gobernanza de recursos](what-s-new-in-sql-server-ver15-prerelease.md#property-ctp24)|
| &nbsp; | &nbsp; |

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

Para consultar las características específicas que se excluyen del soporte técnico, vea las [notas de la versión](sql-server-ver15-release-notes.md).

Además, se han incorporado o mejorado las características siguientes de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2.

## <a name="see-also"></a>Vea también

- [`SqlServer` Módulo de PowerShell](https://www.powershellgallery.com/packages/Sqlserver)
- [Documentación de SQL Server PowerShell](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>Pasos siguientes

- [Notas de la versión de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-ver15-release-notes.md).

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]: Notas técnicas del producto](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />Publicado en septiembre de 2018. Se aplica a Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0 para Windows, Linux y contenedores de Docker.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
