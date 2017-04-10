---
title: "Caracter&#237;sticas compatibles con las ediciones de SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
keywords: 
  - "Edición de SQL"
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
caps.latest.revision: 175
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
---
# Caracter&#237;sticas compatibles con las ediciones de SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tema proporciona información detallada de las características admitidas por las diversas ediciones de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 La edición de evaluación de SQL Server está disponible durante un período de prueba de 180 días.  
  
 Para leer las notas de la versión más reciente e información sobre las novedades, vea lo siguiente:
- [Notas de la versión de SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
- [Novedades de SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

    
 **Probar SQL Server 2016**    
    
 > [![Descargar desde el centro de evaluación](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Descargar SQL Server 2016 desde el centro de evaluación](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Máquina virtual de Azure pequeña ](../analysis-services/media/azure-virtual-machine-small.png)**[Poner en marcha una máquina virtual con SQL Server 2016 ya instalado](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    
    
  
 Para conocer las características admitidas por las ediciones Evaluation y Developer, consulte SQL Server Enterprise Edition.  
  
##  <a name="a-namecross-boxscalelimitsa-scale-limits"></a><a name="Cross-BoxScaleLimits"></a> Límites de escala  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|Capacidad máxima de cálculo que usa una sola instancia: [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Sistema operativo máximo|Limitada a menos de 4 sockets o 24 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos| 
|Capacidad máxima de cálculo que usa una sola instancia: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Sistema operativo máximo|Limitada a menos de 4 sockets o 24 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|  
|Memoria máxima para el grupo de búferes por cada instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Sistema operativo máximo|128 GB|64 GB|1410 MB|1410 MB|
|Cantidad máxima de memoria para la caché de segmento del almacén de columnas por cada instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memoria ilimitada| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 GB<sup>2</sup>| 352 GB<sup>2</sup>|  
|Tamaño máximo de datos con optimización para memoria por base de datos en [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memoria ilimitada| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 GB<sup>2</sup>| 352 GB<sup>2</sup>|  
|Memoria máxima usada por instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Sistema operativo máximo|Tabular: 16 GB<br /><br /> MOLAP: 64 GB|N/D|N/D|N/D|  
|Memoria máxima usada por instancia de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Sistema operativo máximo|64 GB|64 GB|4 GB|N/D|
|Tamaño máximo de la base de datos relacional|524 PB|524 PB|524 PB|10 GB|10 GB|  
  
 1. La licencia basada en Enterprise Edition con licencia de servidor y acceso de cliente (CAL) (no disponible para nuevos contratos) está limitada a un máximo de 20 núcleos por instancia de SQL Server. No hay ningún límite en el modelo de licencias de servidor basado en núcleos. Para obtener más información, consulte [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
<sup>2</sup> Se aplica a [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. 

##  <a name="a-namerdbmshaa-rdbms-high-availability"></a><a name="RDBMSHA"></a> Alta disponibilidad RDBMS  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Compatibilidad con Server Core <sup>1</sup>|Sí|Sí|Sí|Sí|Sí|  
|Trasvase de registros|Sí|Sí|Sí|No|No|  
|Creación de reflejo de base de datos|Sí|Sí<br /><br /> Solo seguridad completa|Solo testigo|Solo testigo|Solo testigo| 
|Compresión de copia de seguridad|Sí|Sí|No|No|No| 
|Instantáneas de base de datos|Sí|Sí <sup>3</sup>|Sí <sup>3</sup>|Sí <sup>3</sup>|Sí <sup>3</sup>|
|Instancias de clúster de conmutación por error de AlwaysOn|Sí<br /><br /> El número de nodos es el sistema operativo máximo|Sí<br /><br /> Compatibilidad con 2 nodos|No|No|No|  
|Grupos de disponibilidad AlwaysOn|Sí<br /><br /> Hasta 8 réplicas secundarias, incluidas 2 réplicas secundarias sincrónicas|No|No|No|No|
|Grupos de disponibilidad básica <sup>2</sup>|No|Sí<br /><br /> Compatibilidad con 2 nodos|No|No|No|
|Director de conexión|Sí|No|No|No|No|
|Restauración de archivos y páginas en línea|Sí|No|No|No|No|
|Índices en línea|Sí|No|No|No|No|
|Cambio de esquema en línea|Sí|No|No|No|No|
|Recuperación rápida|Sí|No|No|No|No|
|Copias de seguridad reflejadas|Sí|No|No|No|No|
|Agregar memoria y CPU sin interrupción|Sí|No|No|No|No|
|Asistente para la recuperación de base de datos|Sí|Sí|Sí|Sí|Sí|
|Copia de seguridad cifrada|Sí|Sí|No|No|No|
|Copia de seguridad híbrida en Windows Azure (copia de seguridad en dirección URL)|Sí|Sí|No|No|No|  
  
 <sup>1</sup> Para más información sobre cómo instalar SQL Server 2016 en Server Core, vea [Instalación de SQL Server 2016 en Server Core](../database-engine/install-windows/install-sql-server-2016-on-server-core.md). 

<sup>2</sup> Para más información sobre los grupos de disponibilidad básica, vea [Grupos de disponibilidad básica](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).  

<sup>3</sup> Se aplica a [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.
  
##  <a name="a-namerdbmsspa-rdbms-scalability-and-performance"></a><a name="RDBMSSP"></a> Escalabilidad y rendimiento RDBMS  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Almacén de columnas <sup>1</sup>|Sí|Sí <sup>2</sup>|Sí <sup>2</sup>|Sí<sup>2</sup>|Sí<sup>2</sup>|  
|OLTP en memoria <sup>1</sup>|Sí|Sí <sup>2</sup>|Sí <sup>2</sup>|Sí <sup>2</sup>, <sup>3</sup>|Sí <sup>2</sup>|
|Stretch Database|Sí|Sí|Sí|Sí|Sí|
|Memoria principal persistente|Sí|Sí|Sí|Sí|Sí|
|Compatibilidad con varias instancias|50|50|50|50|50|
|Particiones de tabla e índice|Sí|Sí <sup>2</sup>|Sí <sup>2</sup>|Sí <sup>2</sup>|Sí <sup>2</sup>|  
|Compresión de datos|Sí|Sí <sup>2</sup>|Sí <sup>2</sup>|Sí <sup>2</sup>|Sí <sup>2</sup>|
|Regulador de recursos|Sí|No|No|No|No|  
|Paralelismo de tabla con particiones|Sí|No|No|No|No|
|Varios contenedores de secuencias de archivo|Sí|Sí <sup>2</sup>|Sí <sup>2</sup>|Sí <sup>2</sup>|Sí <sup>2</sup>|
|Asignación de memoria de página grande habilitada para NUMA y matriz de búferes|Sí|No|No|No|No|
|Extensión del grupo de búferes|Sí|Sí|No|No|No|
|Regulación de recursos de E/S|Sí|No|No|No|No|  
|Perdurabilidad diferida|Sí|Sí|Sí|Sí|Sí|

<sup>1</sup> El tamaño de los datos de OLTP en memoria y la memoria caché del segmento del almacén de columnas se limitan a la cantidad de memoria especificada por edición en la sección Límites de escala. Los grados de paralelismo máximos están limitados. Los grados de paralelismo (DOP) para la compilación de un índice se limitan a 2 DOP para Standard Edition y 1 DOP para las ediciones Web y Express. Se refiere a los índices de almacén de columnas que se crean en tablas basadas en disco y en tablas con optimización para memoria.

<sup>2</sup> Se aplica a [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. 

<sup>3</sup> Esta característica no está incluida en la opción de instalación LocalDB.
##  <a name="a-namerdbmssa-rdbms-security"></a><a name="RDBMSS"></a> Seguridad RDBMS  
  
|Característica|Enterprise|Standard|Web|Express|Express con Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|Seguridad de nivel de fila|Sí|Sí|Sí <sup>1</sup>|Sí <sup>1</sup>|Sí <sup>1</sup>|  
|Always Encrypted|Sí|Sí <sup>1</sup>|Sí <sup>1</sup>|Sí <sup>1</sup>|Sí <sup>1</sup>| 
|Enmascaramiento de datos dinámicos|Sí|Sí|Sí <sup>1</sup>|Sí <sup>1</sup>|Sí <sup>1</sup>|   
|Auditoría básica|Sí|Sí|Sí|Sí|Sí| 
|Auditoría específica|Sí|Sí <sup>1</sup>|Sí <sup>1</sup>|Sí <sup>1</sup>|Sí <sup>1</sup>| 
|Cifrado de base de datos transparente|Sí|No|No|No|No|   
|Administración extensible de claves|Sí|No|No|No|No| 
|Roles definidos por el usuario|Sí|Sí|Sí|Sí|Sí| 
|Bases de datos independientes|Sí|Sí|Sí|Sí|Sí| 
|Cifrado para copias de seguridad|Sí|Sí|No|No|No|  

<sup>1</sup> Se aplica a [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.  
##  <a name="a-namereplicationa-replication"></a><a name="Replication"></a> Replicación  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Suscriptores heterogéneos|Sí|Sí|No|No|No|  
|Replicación de mezcla|Sí|Sí|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|   
|Publicación de Oracle|Sí|No|No|No|No| 
|Replicación transaccional punto a punto|Sí|No|No|No|No|   
|Replicación de instantáneas|Sí|Sí|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|   
|Seguimiento de cambios de SQL Server|Sí|Sí|Sí|Sí|Sí| 
|Replicación transaccional|Sí|Sí|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|   
|Replicación transaccional a Azure|Sí|Sí|Sí|No|No|   
|Suscripción actualizable a la replicación transaccional|Sí|No|No|No|No|  
  
##  <a name="a-namessmsa-management-tools"></a><a name="SSMS"></a> Herramientas de administración  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Objetos de administración de SQL (SMO)|Sí|Sí|Sí|Sí|Sí|  
|Administrador de configuración de SQL|Sí|Sí|Sí|Sí|Sí|   
|SQL CMD (herramienta del símbolo del sistema)|Sí|Sí|Sí|Sí|Sí|      
|Distributed Replay: herramienta de administración|Sí|Sí|Sí|Sí|No|  
|Distribute Replay: cliente|Sí|Sí|Sí|No|No|  
|Distributed Replay: controlador|Sí (hasta 16 clientes)|Sí (1 cliente)|Sí (1 cliente)|No|No|   
|SQL Profiler|Sí|Sí|No <sup>1</sup>|No <sup>1</sup>|No <sup>1</sup>|  
|Agente SQL Server|Sí|Sí|Sí|No|No| 
|Paquete de administración de Microsoft System Center Operations Manager|Sí|Sí|Sí|No|No|  
|Asistente para la optimización de motor de base de datos (DTA)|Sí|Sí <sup>2</sup>|Sí <sup>2</sup>|No|No|      
  
 <sup>1</sup> Se pueden generar perfiles de SQL Server Web, SQL Server Express, SQL Server Express con herramientas y SQL Server Express con Advanced Services mediante las ediciones SQL Server Standard y SQL Server Enterprise.  
  
 <sup>2</sup> La optimización se habilita solo en las características de la edición Standard  
  
##  <a name="a-namerdbmsma-rdbms-manageability"></a><a name="RDBMSM"></a> Capacidad de administración de RDBMS  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Instancias de usuario|No|No|No|Sí|Sí| 
|LocalDB|No|No|No|Sí|No| 
|Conexión de administración dedicada|Sí|Sí|Sí|Sí, con marca de seguimiento|Sí, con marca de seguimiento|   
|Compatibilidad con PowerShell scripting|Sí|Sí|Sí|Sí|Sí| 
|Compatibilidad con SysPrep <sup>1</sup>|Sí|Sí|Sí|Sí|Sí| 
|Compatibilidad con las operaciones de componentes de aplicación de capa de datos: extracción, implementación, actualización, eliminación|Sí|Sí|Sí|Sí|Sí| 
|Automatización de directivas (comprobar en la programación y cambio)|Sí|Sí|Sí|No|No|   
|Recopilador de datos de rendimiento|Sí|Sí|Sí|No|No| 
|Capacidad de inscribirse como instancia administrada en una administración de varias instancias|Sí|Sí|Sí|No|No|   
|Informes de rendimiento estándar|Sí|Sí|Sí|No|No| 
|Guías del plan y congelación del plan para las guías del plan|Sí|Sí|Sí|No|No|   
|Consulta directa de vistas indexadas (mediante la sugerencia NOEXPAND)|Sí|Sí|Sí|Sí|Sí| 
|Mantenimiento automático de vistas indexadas|Sí|Sí|Sí|No|No| 
|Vistas distribuidas con particiones|Sí|No|No|No|No| 
|Operaciones indizadas en paralelo|Sí|No|No|No|No|  
|Uso automático de vistas indexadas por el optimizador de consultas|Sí|No|No|No|No| 
|Comprobación de coherencia en paralelo|Sí|No|No|No|No| 
|Punto de control de la utilidad de SQL Server|Sí|No|No|No|No|    
|Extensión del grupo de búferes|Sí|Sí|No|No|No| 
  
 <sup>1</sup> Para más información, vea [Consideraciones acerca de la instalación de SQL Server con SysPrep](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
 
<sup>2</sup> Se aplica a [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1. 
  
##  <a name="a-namedevtoolsa-development-tools"></a><a name="DevTools"></a> Herramientas de desarrollo  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Integración de Microsoft Visual Studio|Sí|Sí|Sí|Sí|Sí| 
|IntelliSense (Transact-SQL y MDX)|Sí|Sí|Sí|Sí|Sí| 
|SQL Server Data Tools (SSDT)|Sí|Sí|Sí|Sí|No|    
|Herramientas de edición, depuración y diseño de MDX|Sí|Sí|No|No|No|   
  
##  <a name="a-nameprogrammabilitya-programmability"></a><a name="Programmability"></a> Programación  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Integración básica de R|Sí|Sí|Sí|Sí|No|   
|Integración avanzada de R|Sí|No|No|No|No| 
|R Server (Standalone)|Sí|No|No|No|No|   
|Nodo de ejecución de Polybase|Sí|Sí <sup>1</sup>|Sí <sup>1</sup>, <sup>2</sup>|Sí <sup>1</sup>, <sup>2</sup>|Sí <sup>1</sup>, <sup>2</sup>| 
|Nodo principal de Polybase|Sí|No|No|No|No| 
|JSON|Sí|Sí|Sí|Sí|Sí|   
|Almacén de consultas|Sí|Sí|Sí|Sí|Sí|   
|Temporal|Sí|Sí|Sí|Sí|Sí|   
|Integración de Common Language Runtime (CLR)|Sí|Sí|Sí|Sí|Sí|   
|Compatibilidad con XML nativo|Sí|Sí|Sí|Sí|Sí| 
|Índices XML|Sí|Sí|Sí|Sí|Sí| 
|Funciones MERGE y UPSERT|Sí|Sí|Sí|Sí|Sí|   
|compatibilidad con FILESTREAM|Sí|Sí|Sí|Sí|Sí| 
|FileTable|Sí|Sí|Sí|Sí|Sí| 
|Tipos de datos de fecha y hora|Sí|Sí|Sí|Sí|Sí|  
|Compatibilidad para internacionalización|Sí|Sí|Sí|Sí|Sí| 
|Búsqueda de texto completo y semántica|Sí|Sí|Sí|Sí|No| 
|Especificación de idioma en la consulta|Sí|Sí|Sí|Sí|No|   
|Service Broker (mensajería)|Sí|Sí|No (solo cliente)|No (solo cliente)|No (solo cliente)|   
|Transact-SQL, extremos|Sí|Sí|Sí|No|No| 

<sup>1</sup> El escalado horizontal con varios nodos de cálculo exige un nodo principal.

<sup>2</sup> Se aplica a [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.
  
## <a name="a-nameisa-integration-services"></a><a name="IS"></a> Integration Services

Para información sobre las características de Integration Services (SSIS) compatibles con las ediciones de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], consulte [Características de Integration Services compatibles con las ediciones de SQL Server 2016](Integration%20Services%20Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).

##  <a name="a-namemdsa-master-data-services"></a><a name="MDS"></a> Master Data Services  
 Para información sobre las características de [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] y Data Quality Services compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Master Data Services y Data Quality Services compatibles con las ediciones de SQL Server 2016](../master-data-services/master data services and data quality services features support.md). 

  
##  <a name="a-namedwa-data-warehouse"></a><a name="DW"></a> Almacenamiento de datos  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Crear cubos sin base de datos|Sí|Sí|No|No|No |   
|Ensayo de generación automática y esquema de almacenamiento de datos|Sí|Sí|No|No|No| 
|Captura de datos modificados|Sí|Sí <sup>1</sup>|Sí <sup>1</sup>|No|No| 
|Optimizaciones de consultas de combinación en estrella|Sí|No|No|No|No| 
|Configuración de solo lectura escalable de Analysis Services|Sí|No|No|No|No| 
|Procesamiento de consultas en paralelo en las tablas e índices con particiones|Sí|No|No|No|No|   
|Agregación global de lotes|Sí|No|No|No|No| 

<sup>1</sup> Se aplica a [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] SP1.  
##  <a name="a-namessasa-analysis-services"></a><a name="SSAS"></a> Analysis Services  
  
Para información sobre las características de Analysis Services compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Analysis Services compatibles con las ediciones de SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md). 
  
##  <a name="a-namebimda-bi-semantic-model-multi-dimensional"></a><a name="BIMD"></a> Modelo semántico BI (multidimensional)  
  
Para información sobre las características de Analysis Services compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Analysis Services compatibles con las ediciones de SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
   
##  <a name="a-namebita-bi-semantic-model-tabular"></a><a name="BIT"></a> Modelo semántico BI (tabular)  
  
Para información sobre las características de Analysis Services compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Analysis Services compatibles con las ediciones de SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="a-nameppspa-power-pivot-for-sharepoint"></a><a name="PPSP"></a> PowerPivot para SharePoint  
  
Para información sobre las características de Power Pivot para SharePoint compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Analysis Services compatibles con las ediciones de SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="a-namedma-data-mining"></a><a name="DM"></a> Minería de datos  
  
Para información sobre las características de minería de datos compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Analysis Services compatibles con las ediciones de SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="a-namessrsa-reporting-services"></a><a name="SSRS"></a> Reporting Services  
  
Para información sobre las características de Reporting Services compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Reporting Services compatibles con las ediciones de SQL Server 2016](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).

##  <a name="a-namebica-business-intelligence-clients"></a><a name="BIC"></a> Clientes de Business Intelligence  

Para información sobre las características del cliente de Business Intelligence compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Analysis Services compatibles con las ediciones de SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) o [Características de Reporting Services compatibles con las ediciones de SQL Server 2016](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="a-nameslsa-spatial-and-location-services"></a><a name="SLS"></a> Servicios espaciales y de ubicación  
  
|Nombre de la característica|Enterprise|Standard|Web|Express con Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Índices espaciales|Sí|Sí|Sí|Sí|Sí|   
|Tipos de datos planares y geodésicos|Sí|Sí|Sí|Sí|Sí| 
|Bibliotecas espaciales avanzadas|Sí|Sí|Sí|Sí|Sí|   
|Importación y exportación de formatos de datos espaciales estándar del sector|Sí|Sí|Sí|Sí|Sí|   
  
##  <a name="a-nameadsa-additional-database-services"></a><a name="ADS"></a> Servicios de bases de datos adicionales  
  
|Nombre de la característica|Enterprise|Standard|Web|Express con Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|Sí|Sí|Sí|Sí|Sí|   
|Correo electrónico de base de datos|Sí|Sí|Sí|No|No| 
  
##  <a name="a-nameothera-other-components"></a><a name="Other"></a> Otros componentes  
  
|Nombre de la característica|Enterprise|Standard|Web|Express con Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|No|No| 
|StreamInsight HA|StreamInsight Premium Edition|No|No|No|No|   
  
> [![Descargar SSMS](../analysis-services/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx)Descargar la versión más reciente de **[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**    
  
## <a name="see-also"></a>Vea también  
 [Especificaciones de producto de SQL Server 2016](../Topic/Product%20Specifications%20for%20SQL%20Server%202016.md)   
 [Instalación de SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)  
  
  