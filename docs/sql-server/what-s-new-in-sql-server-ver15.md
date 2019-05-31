---
title: Novedades de SQL Server 2019 | Microsoft Docs
ms.date: 05/22/2019
ms.prod: sql-server-2019
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ad10f03e426298d3785feeba132979e647cb1a98
ms.sourcegitcommit: 209fa6dafe324f606c60dda3bb8df93bcf7af167
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2019
ms.locfileid: "66198190"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>Novedades de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] se basa en versiones anteriores para potenciar SQL Server como una plataforma que proporciona diversas opciones de lenguajes de desarrollo, tipos de datos, entornos locales o en la nube, y sistemas operativos. En este artículo se resumen las novedades de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

En este artículo se resumen las características de cada versión y se ofrecen más detalles de cada característica. En la sección [Detalles](#details) se proporcionan detalles técnicos sobre las características que quizá no estén disponibles en la documentación principal. Las demás secciones de este artículo proporcionan detalles sobre todas las características publicadas hasta la fecha para [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Para obtener más información y problemas conocidos, vea [Notas de la versión de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-ver15-release-notes.md).

**Use las [herramientas más recientes](#tools) para obtener la mejor experiencia con [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].**

## <a name="ctp-30-may-2019"></a>CTP 3.0, mayo de 2019

Community Technology Preview (CTP) 3.0 es la versión pública más reciente de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Esta versión incluye mejoras respecto a versiones anteriores de CTP para corregir errores, mejorar la seguridad y optimizar el rendimiento.

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

Para consultar las características específicas que se excluyen del soporte técnico, vea las [notas de la versión](sql-server-ver15-release-notes.md).

Además, se han incorporado o mejorado las características siguientes de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] en CTP 3.0.

### <a name="big-data-clusters"></a>Clústeres de macrodatos

| Nueva característica o actualización | Detalles |
|:---|:---|
| Actualizaciones de **mssqlctl** | Varias [actualizaciones de comandos y parámetros](../big-data-cluster/reference-mssqlctl.md) de **mssqlctl**. Esto incluye una actualización del comando **mssqlctl login**, que ahora se dirige al punto de conexión y al nombre de usuario del controlador. |
| Mejoras en el almacenamiento | Compatibilidad con distintas configuraciones de almacenamiento para registros y datos. Además, se ha reducido el número de notificaciones de volumen persistentes para un clúster de macrodatos. |
| Varias instancias de grupos de procesos | Compatibilidad con varias instancias de grupos de procesos. |
| Nuevas características y nuevo comportamiento del grupo | Ahora, el grupo de procesos se utiliza de forma predeterminada para las operaciones de grupo de almacenamiento y grupo de datos solo en distribución **ROUND_ROBIN**. Ahora, el grupo de datos puede utilizar un nuevo tipo de distribución, **REPLICATED**, lo que significa que los mismos datos están presentes en todas las instancias del grupo de datos. |
| Mejoras en la tabla externa | Las tablas externas de tipo origen de datos HADOOP ahora admiten la lectura de filas de hasta 1 MB. Ahora, las tablas externas (ODBC, bloque de almacenamiento, grupo de datos) admiten filas tan anchas como las tablas de SQL Server. |
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motor de base de datos

| Nueva característica o actualización | Detalles |
|:---|:---|
|Registrar lenguajes externos|La nueva instrucción DDL `CREATE EXTERNAL LANGUAGE` registra lenguajes externos, como Java, en SQL Server. Vea [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) (CREAR UN LENGUAJE EXTERNO). |
|Compatibilidad con más tipos de datos para Java|Vea [Java data types](../language-extensions/how-to/java-to-sql-data-types.md) (Tipo de datos Java).|
|Directiva de captura personalizada para el Almacén de consultas|Cuando se habilita, una nueva configuración de la directiva de captura del Almacén de consultas incluye más configuraciones del Almacén para optimizar la recopilación de datos en un servidor específico. Para obtener más información, vea [Opciones de ALTER DATABASE SET](../t-sql/statements/alter-database-transact-sql-set-options.md).|
|[Base de datos en memoria](../relational-databases/in-memory-database.md) agrega la nueva sintaxis DDL para controlar el grupo de búferes híbrido. <sup>2</sup>|Con el [grupo de búferes híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md), se accede directamente a las páginas de base de datos ubicadas en archivos de base de datos presentes en un dispositivo de memoria persistente (PMEM) cuando sea necesario.|
|Incorporación de una nueva característica de base de datos en memoria: metadatos tempdb optimizados para memoria.|Vea [Metadatos tempdb optimizados para memoria](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata).|
|Los servidores vinculados admiten la codificación de caracteres UTF-8. |[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md) |
|`sys.dm_exec_query_plan_stats` devuelve información sobre el grado de paralelismo y la concesión de memoria para planes de consulta. |[sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)<sup>1</sup>|
| &nbsp; | &nbsp; |

><sup>1</sup> Se trata de una característica opcional que requiere que la [marca de seguimiento](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451 esté habilitada.
>
><sup>2</sup> Ya no se requiere una marca de seguimiento para habilitar el grupo de búferes híbrido.

### [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]

| Nueva característica o actualización | Detalles |
|:---|:---|
|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] admite las bases de datos de instancias administradas de Azure SQL Database.| Hospeda [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] en una instancia administrada. Vea [Instalación y configuración de [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]](../master-data-services/master-data-services-installation-and-configuration.md#SetUpWeb).
| &nbsp; | &nbsp; |

### <a name="analysis-services"></a>Analysis Services

| Nueva característica o actualización | Detalles |
|:---|:---|
|Compatibilidad de la consulta MDX para los modelos tabulares con grupos de cálculo. |Esta versión quita una limitación que anteriormente se aplicaba a los [grupos de cálculo](#calc-ctp24). |
|Formato dinámico de medidas con grupos de cálculo. |Esta característica le permite cambiar condicionalmente las cadenas de formato para las medidas con [grupos de cálculo](#calc-ctp24). Por ejemplo, con la conversión de moneda, se puede mostrar una medida con divisas en diferentes formatos.|

## <a name="ctp-25-april-2019"></a>CTP 2.5, abril de 2019

### <a name="big-data-clusters"></a>Clústeres de macrodatos

| Nueva característica o actualización | Detalles |
|:---|:---|
| Perfiles de implementación | Utiliza los [archivos JSON de configuración de la implementación](../big-data-cluster/deployment-guidance.md#configfile) predeterminados y personalizados para las implementaciones de clústeres de macrodatos en lugar de las variables de entorno. |
| Implementaciones solicitadas | `mssqlctl cluster create` ahora le pide los valores necesarios para realizar implementaciones predeterminadas. |
| Cambios de nombre de punto de conexión de servicio y pod | Para obtener más información, vea las [notas de versión del clúster de macrodatos](../big-data-cluster/release-notes-big-data-cluster.md). |
| Mejoras de **mssqlctl** | Use **mssqlctl** para [enumerar los puntos de conexión externos](../big-data-cluster/deployment-guidance.md#endpoints) y compruebe la versión de **mssqlctl** con el parámetro `--version`. |
| Instalación sin conexión | [Instrucciones para las implementaciones del clúster de macrodatos sin conexión](../big-data-cluster/deploy-offline.md). |
| Mejoras en los niveles de HDFS | Niveles de HDFS frente a almacenamiento de Amazon S3. Compatibilidad de OAuth con ADLS Gen2. Funcionalidad de almacenamiento en caché para un mejor rendimiento. Para obtener más información, vea [Niveles de HSDFS](../big-data-cluster/hdfs-tiering.md). |
| Conector de Spark a SQL Server | [Leer y escribir en SQL Server de Spark con el conector MSSQL JDBC](../big-data-cluster/spark-mssql-connector.md) |
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motor de base de datos

| Nueva característica o actualización | Detalles |
|:---|:---|
| PolyBase en Linux. | [Instale PolyBase](../relational-databases/polybase/polybase-linux-setup.md) en Linux para conectores que no son Hadoop.<br/><br/>[Asignación del tipo de PolyBase](../relational-databases/polybase/polybase-type-mapping.md). |
| Nuevo SDK del lenguaje de programación Java para SQL Server. | Simplifica el desarrollo de los programas Java que se pueden ejecutar desde SQL Server. Vea [Novedades de SQL Server Machine Learning Services](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md). |
| Se ha ampliado el ámbito de los planes disponibles en `sys.dm_exec_query_plan_stats` de DMF. |Vea [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)<sup>1</sup>.|
| Nueva configuración de ámbito de la base de datos `LAST_QUERY_PLAN_STATS` para habilitar `sys.dm_exec_query_plan_stats`. |Vea [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
| Nuevos identificadores de referencia espacial (SRID). |La [australiana GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) proporciona datos más sólidos y precisos, más estrechamente alineados con sistemas de posicionamiento global. Los nuevos SRID son:<br/><br/> - 7843: 2D geográfico<br/> - 7844: 3D geográfico <br/><br/>La vista [sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) contiene las definiciones de nuevos SRID. |
| &nbsp; | &nbsp; |

><sup>1</sup> Esta es una característica opcional y requiere que la [marca de seguimiento](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451 esté habilitada o establecer la configuración de ámbito de base de datos de `LAST_QUERY_PLAN_STATS` en ON.

## <a name="ctp-24-march-2019"></a>CTP 2.4, marzo de 2019

### <a name="big-data-clusters"></a>Clústeres de macrodatos

| Nueva característica o actualización | Detalles |
|:---|:---|
| Orientación sobre la compatibilidad de GPU para la ejecución de aprendizaje profundo con TensorFlow en Spark. | [Implementa un clúster de macrodatos con compatibilidad con GPU y ejecuta TensorFlow](../big-data-cluster/spark-gpu-tensorflow.md). |
| Los orígenes de datos **SqlDataPool** y **SqlStoragePool** ya no se crean de forma predeterminada. | Puede crearlos manualmente según sea necesario. Consulte los [problemas conocidos](../big-data-cluster/release-notes-big-data-cluster.md#externaltablesctp24). |
| Compatibilidad de `INSERT INTO SELECT` con el grupo de datos. | Para obtener un ejemplo, vea [Tutorial: Introducir datos en un grupo de datos de SQL Server con Transact-SQL](../big-data-cluster/tutorial-data-pool-ingest-sql.md). |
| Opción `FORCE SCALEOUTEXECUTION` y `DISABLE SCALEOUTEXECUTION`. | Consulte [Notas de la versión para clústeres de macrodatos](../big-data-cluster/release-notes-big-data-cluster.md#whats-new).|
| Recomendaciones actualizadas para implementar AKS. | Al evaluar los clústeres de macrodatos en AKS, ahora se recomienda utilizar un único nodo del tamaño **Standard_L8s**. |
| Actualización del entorno de ejecución de Spark a Spark 2.4. | |
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motor de base de datos

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Valores predeterminados del mensaje de error de truncamiento para incluir los nombres de tabla y columna, así como el valor truncado.|[VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation)|
|La nueva DMF `sys.dm_exec_query_plan_stats` devuelve el equivalente del último plan de ejecución real conocido para la mayoría de las consultas. |[sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)<sup>1</sup>|
|El nuevo evento extendido `query_post_execution_plan_profile` recopila el equivalente de un plan de ejecución real en función de la generación de perfiles ligera, a diferencia de `query_post_execution_showplan`, que utiliza la generación de perfiles estándar. |[Infraestructura de generación de perfiles de consultas](../relational-databases/performance/query-profiling-infrastructure.md)|
|Análisis del cifrado de datos transparente (TDE): suspensión y reanudación.|[Análisis del cifrado de datos transparente (TDE): suspensión y reanudación](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)|
| &nbsp; | &nbsp; |

><sup>1</sup> Se trata de una característica opcional que requiere que la [marca de seguimiento](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451 esté habilitada.

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Relaciones varios a varios en modelos tabulares.|[Relaciones varios a varios en modelos tabulares](#many-to-many-ctp24)|
|Configuración de propiedad para la gobernanza de recursos.|[Configuración de propiedad para la gobernanza de recursos](#property-ctp24)|
| &nbsp; | &nbsp; |

## <a name="ctp-23-february-2019"></a>CTP 2.3, febrero de 2019

### <a name="big-data-clusters"></a>Clústeres de macrodatos

| Nueva característica o actualización | Detalles |
| :---------- | :------ |
| Envío de trabajos de Spark en clústeres de macrodatos en IntelliJ. | [Envío de trabajos de Spark en clústeres de macrodatos de SQL Server en IntelliJ](../big-data-cluster/spark-submit-job-intellij-tool-plugin.md) |
| CLI comunes para la implementación de la aplicación y la administración de clústeres. | [Cómo implementar una aplicación en un clúster de macrodatos de SQL Server 2019 (versión preliminar)](../big-data-cluster/big-data-cluster-create-apps.md) |
| Extensión de VS Code para implementar aplicaciones en un clúster de macrodatos. | [Cómo utilizar VS Code para implementar aplicaciones en clústeres de macrodatos de SQL Server](../big-data-cluster/app-deployment-extension.md) |
| Cambios en el uso del comando de la herramienta **mssqlctl**. | Para obtener más información, vea los [problemas conocidos con mssqlctl](../big-data-cluster/release-notes-big-data-cluster.md#mssqlctlctp23). |
| Uso de Sparklyr en clústeres de macrodatos. | [Uso de Sparklyr en clústeres de macrodatos de SQL Server 2019](../big-data-cluster/sparklyr-from-RStudio.md) |
| Montaje de almacenamiento externo compatible con HDFS en clústeres de macrodatos con **niveles de HDFS**. | Vea [Niveles de HDFS](../big-data-cluster/hdfs-tiering.md). |
| Nueva experiencia de conexión unificada para la instancia principal de SQL Server y la puerta de enlace de Spark o HDFS. | Consulte la [instancia principal de SQL Server y la puerta de enlace de Spark o HDFS](../big-data-cluster/connect-to-big-data-cluster.md). |
| Al eliminar un clúster con la función **eliminar clúster mssqlctl** ahora solo se eliminan los objetos en el espacio de nombres que formaban parte del clúster de macrodatos. | El espacio de nombres no se elimina. Sin embargo, en versiones anteriores, este comando sí que eliminaba todo el espacio de nombres. |
| Los nombres de punto de conexión de _seguridad_ se han cambiado y consolidado. | **service-security-lb** y **service-security-nodeport** se han consolidado en el punto de conexión **endpoint-security**. |
| Los nombres de punto de conexión de _proxy_ se han cambiado y consolidado. | **service-proxy-lb** y **service-proxy-nodeport** se han consolidado en el punto de conexión **endpoint-sevice-proxy**. |
| Los nombres de punto de conexión de _controller_ se han cambiado y consolidado. | **service-mssql-controller-lb** y **service-mssql-controller-nodeport** se han consolidado en el punto de conexión **endpoint-controller**. |
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motor de base de datos

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Habilitar la recuperación acelerada de bases de datos se puede activar a nivel de la base de datos.| [Recuperación acelerada de bases de datos](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr)|
|Plan de Almacén de consultas para forzar la compatibilidad con cursores estáticos y de avance rápido.|[Plan para forzar la compatibilidad con cursores estáticos y de avance rápido](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23) |
|Recompilaciones reducidas para cargas de trabajo mediante tablas temporales en varios ámbitos. |[Recompilaciones reducidas para cargas de trabajo](../relational-databases/tables/tables.md#ctp23) |
|Escalabilidad mejorada de puntos de control indirectos. |[Escalabilidad mejorada de puntos de control indirectos](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23)|
|agrega la posibilidad de usar la codificación de caracteres UTF-8 con una replicación de BIN2 (`UTF8_BIN2`). |[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md) |
|Definir acciones de eliminación en cascada en una restricción perimetral de una base de datos del gráfico. |[Restricciones perimetrales](../relational-databases/tables/graph-edge-constraints.md) |
|Habilitar o deshabilitar `LIGHTWEIGHT_QUERY_PROFILING` con la nueva configuración de ámbito de base de datos. |[`VERBOSE_TRUNCATION_WARNINGS`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation) |
| &nbsp; | &nbsp; |

### <a name="tools"></a>Herramientas

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Azure Data Studio es compatible con Azure Active Directory. |[Azure Data Studio](../azure-data-studio/what-is.md) |
|La interfaz de usuario de la vista de Notebook se ha movido al núcleo de Azure Data Studio. |[Cómo se administran los cuadernos en Azure Data Studio](../big-data-cluster/notebooks-how-to-manage.md) |
|Se ha agregado un asistente nuevo para crear orígenes de datos externos desde Hadoop Distributed File System (HDFS) en clústeres de macrodatos de SQL Server. | [Herramientas](#tools-ctp23)|
|Se ha mejorado la interfaz de usuario de Notebook. | [Herramientas](#tools-ctp23) |
|Se han agregado nuevas API de Notebook.| [Herramientas](#tools-ctp23) |
|Se ha agregado el comando "Reinstall Notebook dependencies" (Reinstalar dependencias de Notebook) para ayudar con las actualizaciones de paquetes Python. | [Herramientas](#tools-ctp23) |
|Inicio de Azure Data Studio desde SSMS.| [Herramientas](#tools-ctp23) |
| &nbsp; | &nbsp; |

### <a name="analysis-services"></a>Analysis Services

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Grupos de cálculo en el modelo tabular.| [Grupos de cálculo en el modelo tabular](#calc-ctp24) |
| &nbsp; | &nbsp; |

## <a name="ctp-22-december-2018"></a>CTP 2.2, diciembre de 2018

### <a name="big-data-clusters"></a>Clústeres de macrodatos

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Use SparkR desde Azure Data Studio en un clúster de macrodatos. | |
|Implementación de aplicaciones de Python y R.|[Implementar aplicaciones con mssqlctl](../big-data-cluster/big-data-cluster-create-apps.md) |
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motor de base de datos

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Agrega la posibilidad de usar la codificación de caracteres UTF-8 con la replicación de SQL Server. |[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md#ctp23) |
| &nbsp; | &nbsp; |


### <a name="sql-server-on-linux"></a>SQL Server en Linux

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Grupo de disponibilidad Always On en contenedores de Docker con Kubernetes. |[Grupos de disponibilidad Always On para contenedores](../linux/sql-server-ag-kubernetes.md) |
| &nbsp; | &nbsp; |

## <a name="ctp-21-november-2018"></a>CTP 2.1, noviembre de 2018

### <a name="database-engine"></a>Motor de base de datos

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Agrega la posibilidad de seleccionar la intercalación de UTF-8 como valor predeterminado. Configuración de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. |[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md#ctp23) |
|La inserción de UDF escalar transforma automáticamente funciones definidas por el usuario (UDF) escalares en expresiones relacionales y las inserta en la consulta SQL de llamada. |[Inserción de UDF escalar](../relational-databases/user-defined-functions/scalar-udf-inlining.md) |
|La vista de administración dinámica `sys.dm_exec_requests`, columna `command`, muestra `SELECT (STATMAN)` si un `SELECT` está esperando a que finalice una operación de actualización de estadísticas sincrónica para proseguir con la ejecución de la consulta. | [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) |
|Además, el nuevo tipo de espera `WAIT_ON_SYNC_STATISTICS_REFRESH` aparece en la vista de administración dinámica `sys.dm_os_wait_stats`. Muestra el tiempo de nivel de instancia acumulado empleado en las operaciones de actualización de estadísticas sincrónicas.|[`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) |
|El grupo de búferes híbrido es una característica nueva del motor de base de datos de Microsoft SQL Server donde se accederá directamente a las páginas de base de datos ubicadas en archivos de base de datos presentes en un dispositivo de memoria persistente (PMEM) cuando sea necesario.|[Grupo de búferes híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md) |
|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] presenta el enmascaramiento de datos estáticos. Puede usar el enmascaramiento de datos estático para sanear los datos confidenciales en las copias de bases de datos de SQL Server.|[Enmascaramiento estático de datos](../relational-databases/security/static-data-masking.md) |
|Uso de alias de vista o tabla derivada en una consulta de coincidencia del grafo. |[Restricciones perimetrales del grafo](../relational-databases/tables/graph-edge-constraints.md) |
| &nbsp; | &nbsp; |

### <a name="sql-server-on-linux"></a>SQL Server en Linux

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Nuevo registro de contenedor para SQL Server. |[Empezar a trabajar con contenedores de SQL Server con Docker](../linux/quickstart-install-connect-docker.md) |
| &nbsp; | &nbsp; |

### <a name="tools"></a>Herramientas

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|[Azure Data Studio](../azure-data-studio/what-is.md) admite la conexión y administración de clústeres de macrodatos de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. | |
| &nbsp; | &nbsp; |

## <a name="ctp-20-october-2018"></a>CTP 2.0, octubre de 2018

### <a name="big-data-clusters"></a>Clústeres de macrodatos

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Implementación de un clúster de macrodatos con contenedores [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y Spark Linux en Kubernetes. | |
|Acceso a los macrodatos desde HDFS. | |
|Ejecución de análisis avanzado y aprendizaje automático con Spark. | |
|Uso de Spark Streaming en grupos de datos a datos de SQL. | |
|Ejecuta libros de consulta que proporcionan una experiencia de cuadernos en **Azure Data Studio**.|[Ingeniería de datos](../azure-data-studio/what-is.md#data-engineering)|
| &nbsp; | &nbsp; |

### <a name="database-engine"></a>Motor de base de datos

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Se agregó el nivel de compatibilidad **COMPATIBILITY_LEVEL 150** de base de datos. |[Nivel de compatibilidad de ALTER DATABASE (Transact-SQL)](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) |
|Característica Resumable online index create.|[CREATE INDEX (Transact-SQL)](../t-sql/statements/create-index-transact-sql.md#resumable-indexes) |
|Comentarios de concesión de memoria del modo de fila. |[Comentarios de concesión de memoria del modo de fila](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback) |
|Aproximadamente `COUNT DISTINCT`.|[Procesamiento de consultas aproximado](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing)|
|Modo por lotes en el almacén de filas.|[Modo por lotes en el almacén de filas](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore) |
|Compilación diferida de variables de tabla.|[Compilación diferida de variables de tabla](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation) |
|Extensión del lenguaje Java.|[Extensión del lenguaje Java](../advanced-analytics/java/extension-java.md) |
|Combine los datos de gráfico actuales de las tablas perimetrales o de nodo con nuevos datos mediante los predicados `MATCH` en la instrucción `MERGE`. | |
|Restricciones perimetrales.|[Restricciones perimetrales del grafo](../relational-databases/tables/graph-edge-constraints.md) |
|Configuración predeterminada de ámbito de base de datos para operaciones DDL en línea y reanudables.| |
|Los grupos de disponibilidad admiten hasta 5 réplicas secundarias sincrónicas.|[Grupos de disponibilidad](../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) |
|Redireccionamiento de la conexión de lectura/escritura de réplicas de secundaria a principal|[Redireccionamiento de la conexión de lectura/escritura de réplicas de secundaria a principal (grupos de disponibilidad AlwaysOn)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md) |
|Clasificación y detección de datos de SQL.| [Clasificación y detección de datos de SQL](../relational-databases/security/sql-data-discovery-and-classification.md) |
|Compatibilidad ampliada con los dispositivos de memoria persistente.|[Grupo de búferes híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md) |
|Compatibilidad con las estadísticas de almacén de columnas en `DBCC CLONEDATABASE`|[Blob de estadísticas para los índices de almacén de columnas](../t-sql/database-console-commands/dbcc-clonedatabase-transact-sql.md#ctp23)|
|`sp_estimate_data_compression_savings` presenta `COLUMNSTORE` y `COLUMNSTORE_ARCHIVE`.|[Consideraciones para los índices de almacén de columnas](../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md#considerations-for-columnstore-indexes)|
|Machine Learning Services se admite en el clúster de conmutación de Windows Server. |[Novedades: ¿Qué es SQL Server Machine Learning Services?](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)|
|Machine Learning admite el modelo basado en particiones.|[Novedades: SQL Server Machine Learning Services](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md) |
|Infraestructura de generación de perfiles ligera de consultas habilitada de forma predeterminada |[Infraestructura de generación de perfiles de estadísticas de ejecución de consultas ligera v3](../relational-databases/performance/query-profiling-infrastructure.md#lightweight-query-execution-statistics-profiling-infrastructure-v3) |
|Nuevos conectores de PolyBase para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata y MongoDB. |[¿Qué es PolyBase?](../relational-databases/polybase/polybase-guide.md) |
|`sys.dm_db_page_info(database_id, file_id, page_id, mode)` devuelve información sobre una página de una base de datos. |[sys.dm_db_page_info (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)|
|Always Encrypted con enclaves seguros. |[Always Encrypted con enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md) |
|Compilación y recompilación en línea de índices de almacén de columnas en clúster. |[Realizar operaciones de índice en línea](../relational-databases/indexes/perform-index-operations-online.md) |
| &nbsp; | &nbsp; |

### <a name="sql-server-on-linux"></a>SQL Server en Linux

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Compatibilidad con la replicación |[Replicación de SQL Server en Linux](../linux/sql-server-linux-replication.md)
|Compatibilidad con el Coordinador de transacciones distribuidas de Microsoft (MSDTC) |[Cómo configurar el Coordinador de transacciones distribuidas de Microsoft (MSDTC) en Linux](../linux/sql-server-linux-configure-msdtc.md) |
|Compatibilidad de OpenLDAP con proveedores terceros de AD |[Tutorial: Usar la autenticación de Active Directory con SQL Server en Linux](../linux/sql-server-linux-active-directory-authentication.md) |
|Machine Learning en Linux |[Instalar Machine Learning en Linux](../linux/sql-server-linux-setup-machine-learning.md) |
| &nbsp; | &nbsp; |

### <a name="master-data-services"></a>Master Data Services

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|El portal de Master Data Services (MDS) ya no depende de Silverlight.| Todos los componentes de Silverlight anteriores se han reemplazado por controles HTML.|
| &nbsp; | &nbsp; |

### <a name="security"></a>Seguridad

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Administración de certificados en el Administrador de configuración de SQL Server|[Administración de certificados (Administrador de configuración de SQL Server)](../database-engine/configure-windows/manage-certificates.md)
| &nbsp; | &nbsp; |

### <a name="tools"></a>Herramientas

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|[Azure Data Studio](../azure-data-studio/what-is.md) admite la conexión y administración de clústeres de macrodatos de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. |[Qué es Azure Data Studio](../azure-data-studio/what-is.md)|
|Admite escenarios que usen clústeres de macrodatos de SQL Server. |[Extensión de SQL Server 2019 (versión preliminar)](../azure-data-studio/sql-server-2019-extension.md)|
|[**SQL Server Management Studio (SSMS) 18.0 (versión preliminar)** ](../ssms/sql-server-management-studio-ssms.md): admite [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].| |
|Compatibilidad con Always Encrypted con enclaves seguros |[Always Encrypted con enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md)|
| &nbsp; | &nbsp; |


## <a name="other-services"></a>Otros servicios

A partir de CTP 2.4, [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] no presenta características nuevas para los servicios siguientes:

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS)

## <a name="details"></a>Detalles

### <a id="bigdatacluster"></a>Clústeres de macrodatos

Los [clústeres de macrodatos](../big-data-cluster/big-data-cluster-overview.md) de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] habilitan nuevos escenarios, como los siguientes:

- [Compatibilidad de GPU para la ejecución de aprendizaje profundo con TensorFlow en Spark.](../big-data-cluster/spark-gpu-tensorflow.md) (CTP 2.4)
- Actualización del entorno de ejecución de Spark a Spark 2.4. (CTP 2.4)
- Compatibilidad de `INSERT INTO SELECT` con el grupo de datos. (CTP 2.4)
- Cláusula de opción `FORCE SCALEOUTEXECUTION` y `DISABLE SCALEOUTEXECUTION` para las consultas de tabla externa. (CTP 2.4)
- [Envío de trabajos de Spark en clústeres de macrodatos de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] en IntelliJ](../big-data-cluster/spark-submit-job-intellij-tool-plugin.md). (CTP 2.3)
- [Experiencia de administración e implementación de aplicaciones](../big-data-cluster/big-data-cluster-create-apps.md) para diversas aplicaciones relacionadas con los datos, incluida la operacionalización de modelos de aprendizaje automático mediante R y Python, la ejecución de trabajos de SQL Server Integration Services (SSIS) y mucho más. (CTP 2.3)
- [Uso de Sparklyr en clústeres de macrodatos de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](../big-data-cluster/sparklyr-from-RStudio.md). (CTP 2.3)
- Montaje de almacenamiento externo compatible con HDFS en clústeres de macrodatos con [niveles de HDFS](../big-data-cluster/hdfs-tiering.md). (CTP 2.3)
- Use SparkR desde Azure Data Studio en un clúster de macrodatos. (CTP 2.2)
- [Implementación de aplicaciones de Python y R](../big-data-cluster/big-data-cluster-create-apps.md) (CTP 2.2)
- Implementación de un clúster de macrodatos con contenedores [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y Spark Linux en Kubernetes. (CTP 2.0)
- Acceso a los macrodatos desde HDFS. (CTP 2.0)
- Ejecución de análisis avanzado y aprendizaje automático con Spark. (CTP 2.0)
- Uso de Spark Streaming en grupos de datos a datos de SQL. (CTP 2.0)
- Ejecución de libros de consulta que proporcionan una experiencia de cuadernos en [**Azure Data Studio**](../sql-operations-studio/what-is.md) (CTP 2.0)
 
[!INCLUDE [Big data clusters preview](../includes/big-data-cluster-preview-note.md)]

### <a id="databaseengine"></a> Motor de base de datos

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] presenta o mejora las siguientes características nuevas para [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)].

#### <a name="new-querypostexecutionplanprofile-extended-event-ctp-24"></a>Nuevo evento extendido query_post_execution_plan_profile (CTP 2.4)

El nuevo evento extendido `query_post_execution_plan_profile` recopila el equivalente de un plan de ejecución real en función de la generación de perfiles ligera, a diferencia de `query_post_execution_showplan`, que utiliza la generación de perfiles estándar. Para obtener más información, vea [Infraestructura de generación de perfiles de consultas](../relational-databases/performance/query-profiling-infrastructure.md).

##### <a name="example-1---extended-event-session-using-standard-profiling"></a>Ejemplo 1: Sesión de eventos extendidos mediante la generación de perfiles estándar

```sql
CREATE EVENT SESSION [QueryPlanOld] ON SERVER 
ADD EVENT sqlserver.query_post_execution_showplan(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename = N'C:\Temp\QueryPlanStd.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

##### <a name="example-2---extended-event-session-using-lightweight-profiling"></a>Ejemplo 2: Sesión de eventos extendidos mediante la generación de perfiles ligera

```sql
CREATE EVENT SESSION [QueryPlanLWP] ON SERVER 
ADD EVENT sqlserver.query_post_execution_plan_profile(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename=N'C:\Temp\QueryPlanLWP.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

#### <a name="new-dmf-sysdmexecqueryplanstats-ctp-24"></a>Nueva DMF sys.dm_exec_query_plan_stats (CTP 2.4) 

La nueva DMF `sys.dm_exec_query_plan_stats` devuelve el equivalente del último plan de ejecución real conocido para la mayoría de las consultas de acuerdo con la generación de perfiles ligera. Para obtener más información, vea [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md) e [Infraestructura de generación de perfiles de consulta](../relational-databases/performance/query-profiling-infrastructure.md). Vea el siguiente script como ejemplo:

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

Se trata de una característica opcional que requiere que la [marca de seguimiento](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451 esté habilitada.

#### <a name="transparent-data-encryption-tde-scan---suspend-and-resume-ctp-24"></a>Análisis del cifrado de datos transparente (TDE): suspensión y reanudación (CTP 2.4)

Con el fin de habilitar el [cifrado de datos transparente (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md) en una base de datos, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] debe realizar un análisis de cifrado que lea cada página de archivos de datos en el grupo de búferes y, a continuación, escriba las páginas cifradas de nuevo en el disco. Para proporcionar al usuario más control sobre el análisis de cifrado, [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] presenta la sintaxis del análisis de TDE de suspensión y reanudación para que el análisis se pueda poner en pausa aunque la carga de trabajo en el sistema sea intensa, o durante el horario crítico para la empresa, y reanudar luego.

Use la siguiente sintaxis para poner en pausa el análisis de cifrado TDE:

```sql
ALTER DATABASE <db_name> SET ENCRYPTION SUSPEND;
```

De forma similar, la siguiente sintaxis reanuda el análisis de cifrado TDE:

```sql
ALTER DATABASE <db_name> SET ENCRYPTION RESUME;
```

Para mostrar el estado actual del análisis de cifrado, `encryption_scan_state` se ha agregado a la vista de administración dinámica `sys.dm_database_encryption_keys`. También hay una nueva columna denominada `encryption_scan_modify_date` que contendrá la fecha y la hora del último cambio de estado de análisis de cifrado. Observe también que, si la instancia [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se reinicia mientras el análisis de cifrado se encuentra en un estado suspendido, se registrará un mensaje en el registro de errores durante el inicio que indicará que hay un análisis existente que se ha puesto en pausa.

#### <a name="accelerated-database-recovery-ctp-23"></a>Recuperación acelerada de bases de datos (CTP 2.3)

La [recuperación acelerada de bases de datos](/azure/sql-database/sql-database-accelerated-database-recovery/) mejora considerablemente la disponibilidad de la base de datos, especialmente en presencia de transacciones de larga duración, al volver a diseñar el proceso de recuperación del motor de base de datos de SQL Server. La [recuperación de base de datos](../relational-databases/logs/the-transaction-log-sql-server.md?#recovery-of-all-incomplete-transactions-when--is-started) es el proceso que usa SQL Server para cada base de datos con el fin de empezar en un estado transaccionalmente coherente o limpio. Una base de datos con la recuperación acelerada de base de datos habilitada completa la recuperación más rápidamente después de una conmutación por error o de otro apagado que no haya sido limpio. A partir de CTP 2.3, la recuperación acelerada de la base de datos se puede habilitar en cada base de datos mediante la sintaxis siguiente:

```sql
ALTER DATABASE <db_name> SET ACCELERATED_DATABASE_RECOVERY = {ON | OFF}
```

> [!NOTE]
> Esta sintaxis no es necesaria para aprovechar las ventajas de esta característica de Azure SQL DB, donde se [habilita por solicitud durante la versión preliminar pública](/azure/sql-database/sql-database-accelerated-database-recovery#to-enable-adr-during-this-preview-period). Una vez habilitada, la característica está activada de forma predeterminada.

Si tiene bases de datos críticas propensas a transacciones de gran tamaño, experimente con esta característica durante la versión preliminar. Proporcione comentarios al [equipo de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](<https://aka.ms/sqlfeedback>).

#### <a name="query-store-plan-forcing-support-for-fast-forward-and-static-cursors-ctp-23"></a>Plan de Almacén de consultas para forzar la compatibilidad con cursores estáticos y de avance rápido (CTP 2.3)

Ahora en Almacén de consultas se admite la capacidad de forzar planes de ejecución de consulta para los cursores de T-SQL y API estáticos y de avance rápido. Forzar los planes ahora se admite a través de `sp_query_store_force_plan` o informes de Almacén de consultas de SQL Server Management Studio.

#### <a name="reduced-recompilations-for-workloads-using-temporary-tables-across-multiple-scopes-ctp-23"></a>Recompilaciones reducidas para cargas de trabajo mediante tablas temporales en varios ámbitos (CTP 2.3)

Antes de esta característica, al hacer referencia a una tabla temporal con una instrucción de lenguaje de manipulación de datos DML (`SELECT`, `INSERT`, `UPDATE` o `DELETE`), si la tabla temporal se había creado mediante un lote de ámbito externo, el resultado era una recompilación de la instrucción DML en cada ejecución. Con esta mejora, SQL Server realiza comprobaciones ligeras adicionales para evitar recompilaciones innecesarias:

- Se comprueba si el módulo de ámbito externo que se usa para crear la tabla temporal en tiempo de compilación es el mismo que el de las ejecuciones consecutivas. 
- Se realiza el seguimiento de los cambios de lenguaje de definición de datos (DDL) realizados en la compilación inicial y se comparan con las operaciones DDL para ejecuciones consecutivas. 

El resultado final es una reducción de las recompilaciones extrañas y la sobrecarga de la CPU.

#### <a name="improved-indirect-checkpoint-scalability-ctp-23"></a>Escalabilidad mejorada de puntos de control indirectos (CTP 2.3)

En versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], es posible que los usuarios experimenten errores de programador que no rinde cuando hay una base de datos que genera un gran número de páginas desfasadas, como tempdb. En [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] se presenta una mejor escalabilidad para los puntos de control indirectos, lo que debería evitar estos errores en las bases de datos con una gran carga de trabajo de operaciones UPDATE o INSERT.

#### <a name="utf-8-support-ctp-23"></a>Compatibilidad con UTF-8 (CTP 2.3)

Compatibilidad total para utilizar la ampliamente utilizada codificación de caracteres UTF-8 como codificación de importación o exportación, o bien como intercalación columna o base de datos para datos de texto. UTF-8 se permite en los tipos de datos `CHAR` y `VARCHAR`, y se habilita al crear o cambiar la intercalación de un objeto a una intercalación con el sufijo `UTF8`. 

Por ejemplo, de `LATIN1_GENERAL_100_CI_AS_SC` a `LATIN1_GENERAL_100_CI_AS_SC_UTF8`. UTF-8 solo está disponible para las intercalaciones de Windows que admiten caracteres adicionales, tal y como se presentó en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. `NCHAR` y `NVARCHAR` solo permiten la codificación UTF-16 y no se han realizado cambios.

Esta característica puede proporcionar ahorros significativos de almacenamiento, según el juego de caracteres que se esté usando. Por ejemplo, si se cambia un tipo de datos de columna existente con cadenas ASCII (latinas) de `NCHAR(10)` a `CHAR(10)` utilizando una intercalación habilitada para UTF-8, se reducen a la mitad los requisitos de almacenamiento. Esto se debe a que `NCHAR(10)` requiere 20 bytes para el almacenamiento, mientras que `CHAR(10)` necesita 10 bytes para la misma cadena Unicode.

Para más información, consulte [Compatibilidad con la intercalación y Unicode](../relational-databases/collations/collation-and-unicode-support.md).

**CTP 2.1** agrega la posibilidad de seleccionar la intercalación de UTF-8 como valor predeterminado durante la configuración de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

**CTP 2.2** agrega la posibilidad de usar la codificación de caracteres UTF-8 con la replicación de SQL Server.

**CTP 2.3** agrega la posibilidad de usar la codificación de caracteres UTF-8 con una replicación de BIN2 (UTF8_BIN2).

#### <a name="scalar-udf-inlining-ctp-21"></a>Inserción de UDF escalar (CTP 2.1)

La inserción de UDF escalar transforma automáticamente funciones definidas por el usuario (UDF) escalares en expresiones relacionales y las inserta en la consulta SQL de llamada, lo que mejora el rendimiento de las cargas de trabajo que aprovechan las UDF escalares. La inserción de UDF escalar facilita la optimización basada en costos de las operaciones dentro de las UDF, y da como resultado planes eficaces paralelos y orientados a conjuntos en lugar de planes de ejecución ineficaces, iterativos y en serie. Esta característica está habilitada de forma predeterminada en el nivel de compatibilidad de base de datos 150.

Para obtener más información, vea [Inserción de UDF escalares](../relational-databases/user-defined-functions/scalar-udf-inlining.md).

#### <a name="a-nametruncation-truncation-error-message-improved-to-include-table-and-column-names-and-truncated-value-ctp-21"></a><a name="truncation" />Mejora del mensaje de error de truncamiento para incluir los nombres de tabla y columna, así como el valor truncado (CTP 2.1)

El mensaje de error ID 8152 `String or binary data would be truncated` resulta familiar a muchos desarrolladores y administradores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que desarrollan o mantienen las cargas de trabajo de movimiento de datos; el error se produce durante las transferencias de datos entre un origen y un destino con distintos esquemas cuando los datos de origen son demasiado grandes para caber en el tipo de datos de destino. Se puede tardar mucho tiempo en solucionar el error que indica este mensaje. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] presenta un mensaje de error nuevo y más específico (2628) para este escenario:  

`String or binary data would be truncated in table '%.*ls', column '%.*ls'. Truncated value: '%.*ls'.`

El nuevo mensaje de error 2628 proporciona más contexto para el problema de truncamiento de datos, lo que simplifica el proceso de solución de problemas. 

**CTP 2.1 y CTP 2.2** Se trata de un mensaje de error opcional que requiere que la [marca de seguimiento](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460 esté habilitada.

**CTP 2.4** El mensaje de error 2628 pasa a ser el mensaje de truncamiento predeterminado y reemplaza el mensaje de error 8152 bajo el nivel de compatibilidad de base de datos 150. Se ha introducido una nueva configuración de ámbito de base de datos `VERBOSE_TRUNCATION_WARNINGS` para alternar entre los mensajes de error 2628 y 8152 cuando el nivel de compatibilidad de base de datos es 150. Para obtener más información, vea [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).
Para el nivel de compatibilidad de base de datos 140 o inferior, el mensaje de error 2628 sigue siendo un mensaje de error opcional que requiere que la [marca de seguimiento](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460 esté habilitada.

#### <a name="improved-diagnostic-data-for-stats-blocking-ctp-21"></a>Mejora de datos de diagnóstico para el bloqueo de estadísticas (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] ofrece datos de diagnóstico mejorados para las consultas de larga ejecución que esperan en las operaciones de actualización de estadísticas sincrónicas. La vista de administración dinámica `sys.dm_exec_requests`, columna `command`, muestra `SELECT (STATMAN)` si un `SELECT` está esperando a que finalice una operación de actualización de estadísticas sincrónica para proseguir con la ejecución de la consulta. Además, el nuevo tipo de espera `WAIT_ON_SYNC_STATISTICS_REFRESH` aparece en la vista de administración dinámica `sys.dm_os_wait_stats`. Muestra el tiempo de nivel de instancia acumulado empleado en las operaciones de actualización de estadísticas sincrónicas.

#### <a name="hybrid-buffer-pool-ctp-21"></a>Grupo de búferes híbrido (CTP 2.1)

El grupo de búferes híbrido es una característica nueva del motor de base de datos de Microsoft SQL Server donde se accederá directamente a las páginas de base de datos ubicadas en archivos de base de datos presentes en un dispositivo de memoria persistente (PMEM) cuando sea necesario. Puesto que los dispositivos PMEM proporcionan una latencia muy baja para el acceso a datos, el motor puede renunciar a la realización de una copia de los datos en un área de "páginas limpias" del grupo de búferes y simplemente acceder a la página directamente en PMEM. El acceso se realiza mediante la E/S asignada a la memoria, como sucede con la habilitación. Esto aporta ventajas de rendimiento al evitar una copia de la página en DRAM y que la pila de E/S del sistema operativo tenga acceso a la página en el almacenamiento persistente. Esta característica está disponible en SQL Server en Windows y SQL Server en Linux.

Para obtener más información, consulte [Hybrid buffer pool](../database-engine/configure-windows/hybrid-buffer-pool.md) (Grupo de búferes híbrido).

#### <a name="static-data-masking-ctp-21"></a>Enmascaramiento de datos estático (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] presenta el enmascaramiento de datos estáticos. Puede usar el enmascaramiento de datos estático para sanear los datos confidenciales en las copias de bases de datos de SQL Server. El enmascaramiento de datos estático ayuda a crear una copia saneada de bases de datos donde se ha modificado toda la información confidencial de una manera tal que la copia se puede compartir con usuarios que no son de producción. El enmascaramiento de datos estático se puede usar con fines de desarrollo, pruebas, informes empresariales y analíticos, cumplimiento, solución de problemas y cualquier otro escenario donde no se puedan copiar datos específicos en distintos entornos.

El enmascaramiento de datos estático funciona a nivel de columna. Seleccione las columnas que desea enmascarar y, para cada columna seleccionada, especifique la función de enmascaramiento. El enmascaramiento de datos estático copia la base de datos y, a continuación, aplica a las funciones de enmascaramiento especificadas a las columnas.

##### <a name="static-data-masking-vs-dynamic-data-masking"></a>Enmascaramiento de datos estático frente a enmascaramiento de datos dinámico

El enmascaramiento de datos es el proceso de aplicar una máscara a una base de datos para ocultar información confidencial y reemplazarla por datos nuevos o limpios. Microsoft ofrece dos opciones de enmascaramiento: el enmascaramiento de datos estático y el enmascaramiento de datos dinámico. El enmascaramiento de datos dinámico se incluyó por primera vez en [!INCLUDE[ssSQL16](../includes/sssql16-md.md)]. La tabla siguiente compara estas dos soluciones:

|Enmascaramiento de datos estático |Enmascaramiento de datos dinámicos|
|:----|:----|
|Se produce en una copia de la base de datos <br/><br/>Datos originales no recuperables<br/><br/>El enmascaramiento se produce a nivel de almacenamiento<br/><br/>Todos los usuarios tienen acceso a los mismos datos enmascarados<br/><br/>Se destina a un acceso continuo de todo el equipo|Ocurre en la base de datos original<br/><br/>Datos originales intactos<br/><br/>El enmascaramiento se produce sobre la marcha en el momento de la consulta<br/><br/>El enmascaramiento varía en función de los permisos de usuario <br/><br/>Se destina a un acceso puntual específico de un usuario|

#### <a name="database-compatibility-level-ctp-20"></a>Nivel de compatibilidad de la base de datos (CTP 2.0)

Se agregó el nivel de compatibilidad **COMPATIBILITY_LEVEL 150** de base de datos. Si quiere habilitarlo para una base de datos de usuario específica, ejecute lo siguiente:

   ```sql
   ALTER DATABASE database_name SET COMPATIBILITY_LEVEL =  150;
   ```

#### <a name="resumable-online-index-create-ctp-20"></a>Característica Resumable online index create (CTP 2.0)

La característica **Resumable online index create** permite que una operación de creación de índices se pause y se reanude más adelante desde el punto en que la operación se pausó o falló, en lugar de tener que reiniciarla desde el principio.

Resumable online index create admite los escenarios siguientes:
- Reanudar una operación de creación de índices después de un error de creación de índices, por ejemplo, después de una conmutación por error de base de datos o de quedarse sin espacio en disco.
- Pausar una operación de creación de índices en curso y reanudarla más adelante permitiendo que temporalmente se liberen los recursos del sistema según sea necesario, y reanudar esta operación más tarde.
- Crear índices grandes sin usar tanto espacio de registro y una transacción de larga ejecución que bloquea otras actividades de mantenimiento truncando el registro.

En el caso de que se produzca un error de creación de índices, sin esta característica, debe ejecutarse de nuevo una operación de creación de índices en línea y reiniciarla desde el principio.

Con esta versión, se amplía la funcionalidad reanudable agregando esta característica a las [recompilaciones de índices en línea reanudables](http://azure.microsoft.com/blog/modernize-index-maintenance-with-resumable-online-index-rebuild/).

Además, esta característica se puede establecer como predeterminada en una base de datos específica mediante la [configuración predeterminada de ámbito de base de datos para operaciones DDL en línea y reanudables](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

Para obtener más información, consulte [Característica Resumable online index create](../t-sql/statements/create-index-transact-sql.md#resumable-indexes).

#### <a name="build-and-rebuild-clustered-columnstore-indexes-online-ctp-20"></a>Compilación y recompilación de índices en línea de almacén de columnas en clúster (CTP 2.0)

Convierta tablas de almacén de filas en formato de almacén de columnas. El proceso de creación de índices de almacén de columnas en clúster (CCI) se realizaba sin conexión en las versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], y había que detener todos los cambios mientras se creaban estos índices CCI. Con [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] y [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] puede crear o volver a crear índices CCI en línea. La carga de trabajo no se bloqueará y todos los cambios realizados en los datos subyacentes se agregan de forma transparente en la tabla de almacén de columnas de destino. Estos son algunos ejemplos de nuevas instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] que se pueden usar:

  ```sql
  CREATE CLUSTERED COLUMNSTORE INDEX cci
    ON <tableName>
    WITH (ONLINE = ON);
  ```

  ```sql
  ALTER INDEX cci
    ON <tableName>
    REBUILD WITH (ONLINE = ON);
  ```

#### <a name="always-encrypted-with-secure-enclaves-ctp-20"></a>Always Encrypted con enclaves seguros (CTP 2.0)

Expande Always Encrypted con cifrado in situ y cálculos enriquecidos. Las expansiones se producen por la habilitación de los cálculos en datos de texto simple, dentro de un enclave seguro en el servidor.

Las operaciones criptográficas incluyen el cifrado de columnas y la rotación de claves de cifrado de columna. Estas operaciones ahora se pueden emitir utilizando [!INCLUDE[tsql](../includes/tsql-md.md)] y no requieren que los datos se mueven fuera de la base de datos. Los enclaves seguros proporcionan Always Encrypted a un conjunto más amplio de escenarios que tienen los dos siguientes requisitos:  

- La demanda de que la información confidencial esté protegida de los usuarios con privilegios elevados, pero no autorizados, como los administradores de base de datos, los administradores del sistema, los operadores en la nube o el malware.
- El requisito de que se admitan cálculos enriquecidos en datos protegidos dentro del sistema de base de datos.

Para obtener más información, consulte [Always Encrypted con enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md).

> [!NOTE]
> Always Encrypted con enclaves seguros solo está disponible en el sistema operativo Windows.

#### <a name="intelligent-query-processing-ctp-20"></a>Procesamiento de consultas inteligentes (CTP 2.0)

- Los **comentarios de concesión de memoria del modo de fila** se expanden en la característica de comentarios de concesión de memoria presentada en [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] al ajustar los tamaños de concesión de memoria tanto para los operadores del modo de proceso por lotes como del modo de fila. En el caso de una condición de concesión de memoria excesiva, si la memoria concedida es más de dos veces el tamaño de la memoria usada real, los comentarios de concesión de memoria volverán a calcular la concesión de memoria. Por tanto, las ejecuciones consecutivas solicitarán menos memoria. En el caso de las concesiones de memoria de tamaño insuficiente que provocan un desbordamiento en disco, los comentarios de concesión de memoria desencadenarán un nuevo cálculo de la concesión de memoria. Por tanto, las ejecuciones consecutivas solicitarán más memoria. Esta característica está habilitada de forma predeterminada en el nivel de compatibilidad de base de datos 150.

- La función **Approximate COUNT DISTINCT**devuelve el número aproximado de valores no nulos únicos de un grupo. Esta función está diseñada para usarse en escenarios de macrodatos. Además, está optimizada para las consultas donde se cumplen todas las condiciones siguientes:
   - Tiene acceso a conjuntos de datos de, al menos, millones de filas.
   - Agrega una columna o varias columnas con muchos valores distintos.
   - La capacidad de respuesta es más importante que la precisión absoluta.
      - `APPROX_COUNT_DISTINCT` devuelve los resultados que se encuentran normalmente dentro del 2 % de la respuesta exacta.
      - Y también devuelve la respuesta aproximada en una pequeña fracción del tiempo necesario para la respuesta exacta.

- El **modo de proceso por lotes en el almacén de filas** ya no requiere que un índice de almacén de columnas procese una consulta por lotes. El modo de proceso por lotes permite a los operadores de consulta trabajar en un conjunto de filas, en lugar de fila por fila. Esta característica está habilitada de forma predeterminada en el nivel de compatibilidad de base de datos 150. El modo de proceso por lotes mejora la velocidad de las consultas que acceden a tablas de almacén de filas cuando se cumplen todas estas condiciones:
   - La consulta utiliza operadores analíticos como combinaciones u operadores de agregación.
   - La consulta implica 100 000 o más filas.
   - La consulta está enlazado a la CPU, en lugar de a los datos de entrada/salida.
   - La creación y el uso de un índice de almacén de columnas tendría una de las siguientes desventajas:
      - Agregaría demasiada sobrecarga a la consulta.
      - O bien, no sería factible porque la aplicación depende de una característica que no es compatible aún con los índices de almacén de columnas.

- La **compilación diferida de variables de tabla** mejora la calidad del plan y el rendimiento general de las consultas que hacen referencia a las variables de tabla. Durante la optimización y la compilación inicial, esta característica propagará las estimaciones de cardinalidad que se basan en los recuentos de filas de variables de tabla reales. Con la compilación diferida de variables de tabla, la compilación de una instrucción que hace referencia a una variable de tabla se difiere hasta la primera ejecución real de la instrucción. Esta característica está habilitada de forma predeterminada en el nivel de compatibilidad de base de datos 150.

Para usar el procesamiento de consultas inteligentes, establezca la base datos `COMPATIBILITY_LEVEL = 150`.

#### <a id="programmability"></a> Extensiones de programación del lenguaje Java (CTP 2.0)

- **Extensión del lenguaje Java (versión preliminar)** : Use la extensión del lenguaje Java para ejecutar código de Java en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. En [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], esta extensión está instalada cuando se agrega la característica "Machine Learning Services (en base de datos)" a la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

#### <a id="sqlgraph"></a> Características de SQL Graph (CTP 2.3)

- **Uso de alias de vista o tabla derivada en consultas de coincidencia del grafo (CTP 2.1)** Las consultas de grafo en la versión preliminar de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] admiten el uso de alias de vista o tabla derivada en la sintaxis de `MATCH`. Para usar estos alias en `MATCH`, las vistas y tablas derivadas deben crearse en un conjunto de nodos o un conjunto de tablas perimetrales, con el operador `UNION ALL`. Las tablas de nodos o perimetrales pueden o no contener filtros. La posibilidad de usar alias de vista o tabla derivada en consultas de `MATCH` pueden resultar muy útil en escenarios donde desea consultar entidades o conexiones heterogéneas entre dos o más entidades del grafo.

- La **compatibilidad de coincidencias en el DML (CTP 2.0)** `MERGE` permite especificar las relaciones de gráfico en una sola instrucción, en lugar de las instrucciones `INSERT`,`UPDATE` o `DELETE`. Combine los datos de gráfico actuales de las tablas perimetrales o de nodo con nuevos datos mediante los predicados `MATCH` en la instrucción `MERGE`. Esta característica permite escenarios `UPSERT` en tablas perimetrales. Los usuarios ahora pueden usar una instrucción merge única para insertar un borde nuevo o actualizar uno existente entre dos nodos.

- Las **restricciones perimetrales (CTP 2.0)** se presentaron para las tablas perimetrales en SQL Graph. Las tablas perimetrales pueden conectarse a cualquier otro nodo en la base de datos. Con la introducción de las restricciones perimetrales, ahora puede aplicar algunas restricciones en este comportamiento. La nueva restricción `CONNECTION` puede utilizarse para especificar el tipo de nodos a la que una tabla perimetral determinada podrá conectarse en el esquema. 

  **(CTP 2.3)** Ampliando aún más esta característica, se pueden definir acciones de eliminación en cascada en una restricción perimetral. Puede definir las acciones que realiza el motor de base de datos cuando un usuario elimina los nodos que conecta una tabla perimetral determinada.

#### <a name="database-scoped-default-setting-for-online-and-resumable-ddl-operations-ctp-20"></a>Configuración predeterminada de ámbito de base de datos para operaciones DDL en línea y reanudables (CTP 2.0)

- La **configuración predeterminada de ámbito de base de datos para las operaciones DDL en línea y reanudables** permite una configuración de comportamiento predeterminado en las operaciones de índice `ONLINE` y `RESUMABLE` en el nivel de base de datos, en lugar de definir estas opciones en cada instrucción DDL de índice, como recompilaciones o creaciones de índices.

- Establezca estos valores predeterminados mediante las opciones de configuración de ámbito de base de datos `ELEVATE_ONLINE` y `ELEVATE_RESUMABLE`. Ambas opciones harán que el motor eleve automáticamente las operaciones compatibles a la ejecución de índices ONLINE o RESUMABLE. Puede habilitar los siguientes comportamientos con estas opciones:

  - La opción `FAIL_UNSUPPORTED` permite todas las operaciones de índices en línea o reanudables y las operaciones de índices con errores que no se admiten para las opciones en línea o reanudables.
  - La opción `WHEN_SUPPPORTED` permite las operaciones admitidas en línea o reanudables y ejecutan operaciones no admitidas de índices sin conexión o no reanudables.
  - La opción `OFF` permite el comportamiento actual de la ejecución de todas las operaciones de índices sin conexión y no reanudables, salvo que se especifique explícitamente lo contrario en la instrucción DDL.

Para invalidar la configuración predeterminada, incluya la opción `ONLINE` o `RESUMABLE` en los comandos de recompilación y creación de índices. 

Sin esta característica, hay que especificar las opciones en línea y reanudables directamente en la instrucción DDL de índice, como la recompilación y la creación de índices.

Para obtener más información sobre las opciones reanudables de índices, vea [Característica Resumable online index create](https://azure.microsoft.com/blog/resumable-online-index-create-is-in-public-preview-for-azure-sql-db/).

#### <a id="ha"></a>Grupos de disponibilidad AlwaysOn: más réplicas sincrónicas (CTP 2.0)

- **Hasta cinco réplicas sincrónicas**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] aumenta el número máximo de réplicas sincrónicas a 5, de las 3 que eran en [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Puede configurar este grupo de cinco réplicas para habilitar la conmutación automática por error dentro del grupo. Hay una réplica principal, además de cuatro réplicas secundarias sincrónicas.

- **Redireccionamiento de la conexión de réplicas de secundaria a principal**: Permite que las conexiones de las aplicaciones cliente se dirijan a la réplica principal, independientemente del servidor de destino especificado en la cadena de conexión. Esta funcionalidad permite el redireccionamiento de la conexión sin un agente de escucha. Use el redireccionamiento de la conexión de réplicas de secundaria a principal en los casos siguientes:

  - La tecnología del clúster no ofrece una funcionalidad de agente de escucha.
  - Una configuración de múltiples subredes en la que el redireccionamiento se vuelve complejo.
  - Escenarios de escalado horizontal de lectura o de recuperación ante desastres en los que el tipo de clúster es `NONE`.

Para obtener más información, consulte [Secondary to primary replica read/write connection redirection (Always On Availability Groups)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md) (Redireccionamiento de la conexión de lectura/escrita de réplicas de secundaria a principal [Grupos de disponibilidad Always On]).

#### <a name="data-discovery-and-classification-ctp-20"></a>Clasificación y detección de datos (CTP 2.0)

La característica de clasificación y detección de datos proporciona funcionalidades avanzadas que se integran de forma nativa en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Clasificar y etiquetar la información más confidencial proporciona las siguientes ventajas:
- Ayuda a cumplir los requisitos de cumplimiento reglamentario y los estándares de privacidad de datos.
- Admite escenarios de seguridad, como la supervisión (auditoría) y las alertas por accesos anómalos a información confidencial.
- Resulta más fácil identificar donde reside la información confidencial de la empresa, para que los administradores pueden adoptar los pasos adecuados para proteger la base de datos.

Para obtener más información, consulte [Clasificación y detección de datos de SQL](../relational-databases/security/sql-data-discovery-and-classification.md).

La [auditoría](../relational-databases/security/auditing/sql-server-audit-database-engine.md) también se ha mejorado para incluir un nuevo campo en el registro de auditoría denominado `data_sensitivity_information`, que registra las clasificaciones de confidencialidad (etiquetas) de los datos reales que devuelve la consulta. Para obtener información detallada y ejemplos, vea [ADD SENSITIVITY CLASSIFICATION (Transact-SQL)](../t-sql/statements/add-sensitivity-classification-transact-sql.md).

>[!NOTE]
>No hay ningún cambio en cuanto a cómo se habilita la auditoría. Hay un nuevo campo en los registros de auditoría, `data_sensitivity_information`, que registra las clasificaciones de confidencialidad (etiquetas) de los datos reales que devuelve la consulta. Consulte [Auditoría del acceso a datos confidenciales](/azure/sql-database/sql-database-data-discovery-and-classification/#subheading-3).

#### <a name="expanded-support-for-persistent-memory-devices-ctp-20"></a>Compatibilidad ampliada con los dispositivos de memoria persistente (CTP 2.0)

Ahora, cualquier archivo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que se coloque en un dispositivo de memoria persistente puede usarse en el modo *habilitado*. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] accede directamente al dispositivo, de modo que ignora la pila de almacenamiento del sistema operativo mediante operaciones memcpy eficaces. Este modo mejora el rendimiento porque permite una entrada/salida de latencia baja en estos dispositivos.
    - Estos son algunos ejemplos de archivos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:
        - Archivos de base de datos
        - Archivos de registro de transacciones
        - Archivos de punto de control de OLTP en memoria
    - La memoria persistente también se denomina "memoria de la clase de almacenamiento".
    - A la memoria persistente se le conoce informalmente como *pmem* en algunos sitios web de terceros.

> [!NOTE]
> En esta versión preliminar, la habilitación de archivos en los dispositivos de memoria persistente solo está disponible en Linux. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Windows es compatible con los dispositivos de memoria persistente a partir de [!INCLUDE[ssSQL15](../includes/sssql15-md.md)].

#### <a name="support-for-columnstore-statistics-in-dbcc-clonedatabase-ctp-20"></a>Compatibilidad con las estadísticas de almacén de columnas en DBCC CLONEDATABASE (CTP 2.0)

`DBCC CLONEDATABASE` crea una copia de solo esquema de una base de datos que incluye todos los elementos necesarios para solucionar problemas de rendimiento de consultas sin copiar los datos. En versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el comando no copió las estadísticas necesarias para solucionar con precisión los problemas de las consultas del índice de almacén de columnas y se tuvieron que realizar pasos manuales para capturar esta información. Ahora, en [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], `DBCC CLONEDATABASE` captura automáticamente los blobs de estadísticas de índices de almacén de columnas, por lo que no será necesario realizar ningún paso manual.

#### <a name="new-options-added-to-spestimatedatacompressionsavings-ctp-20"></a>Nuevas opciones agregadas a sp_estimate_data_compression_savings (CTP 2.0)

`sp_estimate_data_compression_savings` devuelve el tamaño actual del objeto solicitado y calcula el tamaño del objeto para el estado de compresión solicitado. Actualmente, este procedimiento admite tres opciones: `NONE`, `ROW` y `PAGE`. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] presenta dos opciones nuevas: `COLUMNSTORE` y `COLUMNSTORE_ARCHIVE`. Estas nuevas opciones permiten estimar los ahorros de espacio si se crea un índice de almacén de columnas se crea la tabla mediante la compresión de almacén de columnas estándar o de archivo.

#### <a id="ml"></a> Modelado basado en particiones y clústeres de conmutación por error de Machine Learning Services en SQL Server (CTP 2.0)

- **Modelos basados en particiones**: Procese scripts externos por partición de los datos mediante los nuevos parámetros agregados a `sp_execute_external_script`. Esta funcionalidad admite el aprendizaje de muchos modelos pequeños (un modelo por cada partición de datos) en lugar de uno grande.

- **Clúster de conmutación por error de Windows Server**: Configure la alta disponibilidad de Machine Learning Services en un clúster de conmutación por error de Windows Server.

Para obtener más información, consulte [Novedades de SQL Server Machine Learning Services](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).

#### <a name="lightweight-query-profiling-infrastructure-enabled-by-default-ctp-20"></a>Infraestructura de generación de perfiles ligera de consultas habilitada de forma predeterminada (CTP 2.0)

La infraestructura de generación de perfiles ligera de consultas (LWP) proporciona datos de rendimiento de consulta de forma más eficaz que con los mecanismos de generación de perfiles estándar. La generación de perfiles ligera ahora está habilitada de forma predeterminada. Se presentó en [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. La generación de perfiles ligera ofrece un mecanismo de recopilación de estadísticas de ejecución de consultas con una sobrecarga esperada del 2 % de CPU, en comparación con una sobrecarga de hasta un 75 % de CPU con el mecanismo de generación de perfiles de consultas estándar. En versiones anteriores, estaba desactivada de forma predeterminada. Los administradores de base de datos pueden habilitarla con la función [trace flag 7412](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). 

Para obtener más información sobre la generación de perfiles de baja intensidad, vea [Infraestructura de generación de perfiles de consultas](../relational-databases/performance/query-profiling-infrastructure.md).

**CTP 2.3** incorpora una nueva configuración `LIGHTWEIGHT_QUERY_PROFILING` de ámbito de base de datos para habilitar o deshabilitar la infraestructura de generación ligera de perfiles de consulta.

#### <a id="polybase"></a>Nuevos conectores de PolyBase

- **Nuevos conectores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata y MongoDB**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] presenta nuevos conectores de datos externos para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata y MongoDB.

#### <a name="new-sysdmdbpageinfo-system-function-returns-page-information-ctp-20"></a>Nueva función del sistema sys.dm_db_page_info que devuelve información de la página (CTP 2.0)

`sys.dm_db_page_info(database_id, file_id, page_id, mode)` devuelve información sobre una página de una base de datos. La función devuelve una fila que contiene la información de encabezado en la página, incluidos `object_id`, `index_id` y `partition_id`. Esta función reemplaza la necesidad de usar `DBCC PAGE` en la mayoría de los casos. 

Para facilitar la solución de problemas de esperas relacionadas con la página, también se agregó una nueva columna denominada "page_resource" a `sys.dm_exec_requests` y `sys.sysprocesses`. Esta nueva columna permite unir `sys.dm_db_page_info` a estas vistas a través de otra nueva función del sistema: `sys.fn_PageResCracker`. Vea el siguiente script como ejemplo:

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d 
  CROSS APPLY sys.fn_PageResCracker(d.page_resource) AS r
  CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id,'DETAILED')
    AS page_info;
```

### <a id="sqllinux"></a> SQL Server en Linux

- **Grupo de disponibilidad Always On en contenedores de Docker con Kubernetes (CTP 2.2)** : Kubernetes puede organizar contenedores que ejecutan instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para proporcionar un conjunto de bases de datos de alta disponibilidad con grupos de disponibilidad Always On de SQL Server. Un operador de Kubernetes implementa un objeto StatefulSet incluyendo un contenedor con el **contenedor mssql-server** y un monitor de estado.

- **Nuevo registro de contenedor (CTP 2.1)** : Todas las imágenes de contenedor de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] y [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] ahora se encuentran en Microsoft Container Registry. Microsoft Container Registry es el registro de contenedor oficial para la distribución de los contenedores de producto de Microsoft. Además, ahora se publican imágenes certificadas basadas en RHEL.

  - Microsoft Container Registry: `mcr.microsoft.com/mssql/server:vNext-CTP2.0`
  - Imágenes de contenedor certificadas basadas en RHEL: `mcr.microsoft.com/mssql/rhel/server:vNext-CTP2.0`

- **Compatibilidad con la replicación (CTP 2.0)** : [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] admite la replicación de SQL Server en Linux. Una máquina virtual Linux con el Agente SQL puede ser un editor, distribuidor o suscriptor. 

  Cree los siguientes tipos de publicaciones:
  - Transaccional
  - Snapshot
  - Mezcla

  Configure la replicación [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o use [procedimientos almacenados de replicación](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

- **Compatibilidad con el Coordinador de transacciones distribuidas de Microsoft (MSDTC) (CTP 2.0)** : [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] en Linux es compatible con el Coordinador de transacciones distribuidas de Microsoft (MSDTC). Para obtener más información, consulte [How to configure MSDTC on Linux](../linux/sql-server-linux-configure-msdtc.md) (Cómo configurar el Coordinador de transacciones distribuidas de Microsoft (MSDTC) en Linux).

- **Compatibilidad de OpenLDAP con proveedores terceros de AD (CTP 2.0)** : [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] en Linux es compatible con OpenLDAP, que permite a los proveedores terceros unirse a Active Directory.

- **Machine Learning en Linux (CTP 2.0)** : Machine Learning Services (en base de datos) de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] ahora es compatible con Linux. Entre esta compatibilidad se encuentra el procedimiento almacenado `sp_execute_external_script`. Para obtener instrucciones sobre cómo instalar Machine Learning Services en Linux, vea [Instalar [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Machine Learning Services (R, Python y Java) en Linux](../linux/sql-server-linux-setup-machine-learning.md).

### <a id="mds"></a> Master Data Services 

- **Controles de Silverlight reemplazados con HTML (CTP 2.0)** : El portal de Master Data Services (MDS) ya no depende de Silverlight. Todos los componentes de Silverlight anteriores se han reemplazado por controles HTML.

### <a id="security"></a>Seguridad

- **Administración de certificados en el Administrador de configuración de SQL Server (CTP 2.0)** : El uso de certificados SSL/TLS para garantizar el acceso a instancias de SQL Server está generalizado. La administración de certificados ahora está integrada ahora en el Administrador de configuración de SQL Server, lo que simplifica tareas comunes como las siguientes:

  - Ver y validar los certificados instalados en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 
  - Ver certificados a punto de expirar
  - Implementar certificados en máquinas que participan en grupos de disponibilidad Always On (desde el nodo que contiene la réplica principal).
  - Implementar certificados en máquinas que participan en una instancia de clúster de conmutación por error (desde el nodo activo).

  > [!NOTE]
  > El usuario debe tener permisos de administrador en todos los nodos de clúster.

### <a id="tools"></a>Herramientas

- [**Azure Data Studio**](../azure-data-studio/what-is.md): Azure Data Studio, publicado anteriormente con el nombre en versión preliminar de SQL Operations Studio, es una herramienta de escritorio ligera, moderna, de código abierto y multiplataforma con la que se pueden llevar a cabo las tareas más comunes de administración y desarrollo de datos. Con Azure Data Studio y la [extensión de la versión preliminar de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](../azure-data-studio/sql-server-2019-extension.md) se puede conectar a SQL Server local y en la nube en Windows, macOS y Linux. Azure Data Studio permite realizar lo siguiente:

<a name = "tools-ctp23"></a>

  - Ahora se admite AAD. (CTP 2.3)
  - La interfaz de usuario de la vista de Notebook se ha movido al núcleo de Azure Data Studio. (CTP 2.3)
  - Se ha agregado un asistente nuevo para crear orígenes de datos externos desde Hadoop Distributed File System (HDFS) en clústeres de macrodatos de SQL Server. (CTP 2.3)
  - Se ha mejorado la interfaz de usuario de Notebook. (CTP 2.3)
  - Se han agregado nuevas API de Notebook. (CTP 2.3)
  - Se ha agregado el comando "Reinstall Notebook dependencies" (Reinstalar dependencias de Notebook) para ayudar con las actualizaciones de paquetes Python. (CTP 2.3)
  - Conexión y administración de clústeres de macrodatos de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. (CTP 2.1)
  - Editar y ejecutar consultas en un entorno de desarrollo moderno con la posibilidad de usar IntelliSense de forma sumamente rápida, con fragmentos de código y con integración del control de código fuente (CTP 2.0) 
  - Visualizar rápidamente datos con gráficos integrados de los conjuntos de resultados (CTP 2.0)
  - Crear paneles personalizados de los servidores y las bases de datos mediante widgets personalizables (CTP 2.0)  
  - Administrar fácilmente su entorno más amplio con el terminal integrado (CTP 2.0)
  - Analizar datos en una experiencia de cuadernos integrada basada en Jupyter (CTP 2.0)
  - Mejorar la experiencia con las extensiones y los temas personalizados (CTP 2.0)
  - Explorar los recursos de Azure con un explorador de recursos y una suscripción integrados. (CTP 2.0)
  - Admite escenarios que usen el clúster de macrodatos de SQL Server. (CTP 2.0)
  
  > [!TIP]
  > Para obtener las mejoras más recientes de Azure Data Studio, vea las [notas de la versión de Azure Data Studio](../azure-data-studio/release-notes-azure-data-studio.md).

- [**SQL Server Management Studio (SSMS) 18.0 (versión preliminar)** ](../ssms/sql-server-management-studio-ssms.md): admite [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

  - Inicio de Azure Data Studio desde SSMS. (CTP 2.3)
  - Compatibilidad con Always Encrypted con enclaves seguros (CTP 2.0)
  - Tamaño de descarga más pequeño (CTP 2.0)
  - Se basa ahora en el shell aislado de Visual Studio 2017 (CTP 2.0)
  - Para ver una lista completa, consulte el [registro de cambios de SSMS](../ssms/release-notes-ssms.md). (CTP 2.0)

- [**Módulo SQL Server PowerShell**](http://www.powershellgallery.com/packages/SqlServer/21.1.18080): El módulo SqlServer PowerShell permite a los desarrolladores, administradores y profesionales de inteligencia empresarial de SQL Server automatizar la implementación de bases de datos y la administración de servidores.

  - Actualización de 21.0 a 21.1 para admitir SMO v150.
  - Se ha actualizado el proveedor SQL Server (SQLRegistration) para mostrar los grupos IS, AS y RS.
  - Se ha corregido un problema en el cmdlet `New-SqlAvailabilityGroup` cuando el destino es SQL Server 2014.
  - Se ha agregado el parámetro `–LoadBalancedReadOnlyRoutingList` a `Set-SqlAvailabilityReplica` y `New-SqlAvailabilityReplica`.
  - Se ha actualizado el cmdlet `AnalysisService` para usar el token de inicio de sesión en caché de `Login-AzureAsAccount` para Azure Analysis Services.

### <a id="ssas"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Analysis Services (SSAS) 

#### <a name="many-to-many-ctp24"></a>Relaciones varios a varios en modelos tabulares (CTP 2.4)

Esta característica permite relaciones de varios a varios entre tablas donde las dos columnas no son únicas. Puede definirse una relación entre una tabla de hechos y dimensiones con una granularidad mayor que la columna clave de la dimensión. Esto evita tener que normalizar las tablas de dimensiones y puede mejorar la experiencia del usuario, dado que el modelo resultante tiene un menor número de tablas con columnas agrupadas lógicamente. Para esta versión de CTP 2.4, las relaciones de varios a varios son características de solo motor. 

Las relaciones de varios a varios requieren modelos en el nivel de compatibilidad 1470, que actualmente solo se admite en [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.3 y versiones posteriores. Para esta versión CTP 2.4, las relaciones de varios a varios se pueden crear con la API Modelo de objetos tabulares (TOM), el Lenguaje de scripting de modelos tabulares (TMSL) y la herramienta de código abierto Tabular Editor. El soporte en SQL Server Data Tools (SSDT) se incluirá en una versión futura, así como la documentación. En el blog de Analysis Services se proporcionará información adicional para esta y otras características de CTP.

#### <a name="property-ctp24"></a>Configuración de memoria para la gobernanza de recursos (CTP 2.4)

La configuración de memoria que se describe aquí ya está disponible en Azure Analysis Services. A partir de CTP 2.4, ahora también es compatible con [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Analysis Services. 

- **Memory\QueryMemoryLimit**: esta propiedad de la memoria puede utilizarse para limitar las colas de memoria generadas por las consultas DAX enviadas al modelo. 
- **DbpropMsmdRequestMemoryLimit**: esta propiedad de XMLA puede utilizarse para reemplazar el valor de la propiedad del servidor Memory\QueryMemoryLimit de una conexión.
- **OLAP\Query\RowsetSerializationLimit**: esta propiedad del servidor limita el número de filas devueltas en un conjunto de filas, lo cual protege los recursos del servidor frente a una exportación masiva de datos. Esta propiedad se aplica a las consultas DAX y a las consultas MDX.

Estas propiedades pueden establecerse mediante la última versión de SQL Server Management Studio (SSMS). En el blog de Analysis Services se proporcionará información adicional para esta característica.

#### <a name="calc-ctp24"></a>Grupos de cálculo en modelos tabulares (CTP 2.3) 

Los grupos de cálculo resuelven un problema común de los modelos complejos, donde puede haber una proliferación de medidas con los mismos cálculos, como la inteligencia de tiempo. Los grupos de cálculo se muestran en los clientes de informes como una tabla con una sola columna. Cada valor de la columna representa un cálculo reutilizable (o elemento de cálculo) que se puede aplicar a cualquiera de las medidas.  

Un grupo de cálculo puede tener cualquier número de elementos de cálculo. Cada elemento de cálculo se define mediante una expresión DAX. Se han introducido tres funciones DAX nuevas para trabajar con los grupos de cálculo: 

- `SELECTEDMEASURE()`: devuelve una referencia a la medida en el contexto actual.  

- `SELECTEDMEASURENAME()`: devuelve una cadena que contiene el nombre de la medida en el contexto actual.  

- `ISSELECTEDMEASURE(M1, M2, …)`: devuelve un valor booleano que indica si la medida en el contexto actual es una de las que se han especificado como argumento.

Además de las funciones DAX nuevas, se han presentado dos nuevas vistas de administración dinámica:

- `TMSCHEMA_CALCULATION_GROUPS`  
- `TMSCHEMA_CALCULATION_ITEMS`  

##### <a name="limitations-in-this-release"></a>Limitaciones de esta versión:

- Todavía no se admite la función `ALLSELECTED DAX`.
- Todavía no se admite la seguridad de nivel de fila definida en la tabla de grupos de cálculo.
- Todavía no se admite la seguridad de nivel de grupo definida en la tabla de grupos de cálculo.
- Todavía no se admiten las expresiones DetailsRows que hacen referencia a elementos de cálculo.
- Todavía no se admiten MDX.

##### <a name="known-issues-in-this-release"></a>Problemas conocidos de esta versión:

- La presencia de grupos de cálculo en un modelo puede provocar que las medidas devuelvan tipos de datos Variant, lo cual puede producir errores de actualización para las columnas calculadas y las tablas que hacen referencia a las medidas.

##### <a name="compatibility-level"></a>Nivel de compatibilidad

Los grupos de cálculo requieren modelos en el nivel de compatibilidad 1470, que actualmente solo se admite en [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.3 y versiones posteriores. En este momento, se pueden crear grupos de cálculo mediante la API Modelo de objetos tabulares (TOM), el Lenguaje de scripting de modelos tabulares (TMSL) y la herramienta Tabular Editor de código abierto. El soporte en SQL Server Data Tools (SSDT) se incluirá en una versión futura, así como la documentación. En el blog de Analysis Services se proporcionará información adicional para esta y otras características de CTP.

## <a name="see-also"></a>Vea también

- [`SqlServer` Módulo de PowerShell](https://www.powershellgallery.com/packages/Sqlserver)
- [Documentación de SQL Server PowerShell](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>Pasos siguientes

- [Notas de la versión de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-ver15-release-notes.md).

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]: Notas técnicas del producto](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />Publicado en septiembre de 2018. Se aplica a Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0 para Windows, Linux y contenedores de Docker.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
