---
title: "Ediciones y características compatibles para SQL Server 2016 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "Edición de SQL"
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
caps.latest.revision: 175
author: sabotta
ms.author: carlasab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b9b9db3ca911b8fd8eed6304b9d3a8f51e9e9ba2
ms.lasthandoff: 04/11/2017

---
# <a name="editions-and-supported-features-for-sql-server-2016"></a>Características compatibles con las ediciones de SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tema proporciona información detallada de las características admitidas por las diversas ediciones de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 La edición de evaluación de SQL Server está disponible durante un período de prueba de 180 días.  
  
 Para leer las notas de la versión más reciente e información sobre las novedades, vea lo siguiente:
- [Notas de la versión de SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
- [Novedades de SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

    
 **Probar SQL Server 2016**    
    
 > [![Download from Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Download SQL Server 2016  from the Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Máquina virtual de Azure pequeña ](../analysis-services/media/azure-virtual-machine-small.png)**[Poner en marcha una máquina virtual con SQL Server 2016 ya instalado](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.SQL2016SP1-WS2016?tab=Overview?wt.mc_id=sqL16_vm)**    
    
**Ediciones Developer y Evaluation**  
 Para obtener las características compatibles con las ediciones Developer y Evaluation, vea las características enumeradas para SQL Server Enterprise Edition en las tablas siguientes.
Para obtener una lista de las características que se agregaron a la edición Developer de [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1, vea [SQL Server 2016 SP1 editions](https://aka.ms/uw6cw4) (Ediciones de SQL Server 2016 SP1).   
  
##  <a name="Cross-BoxScaleLimits"></a> Scale Limits  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|Capacidad máxima de cálculo que usa una sola instancia: [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Sistema operativo máximo|Limitada a menos de 4 sockets o 24 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos| 
|Capacidad máxima de cálculo que usa una sola instancia: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Sistema operativo máximo|Limitada a menos de 4 sockets o 24 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|  
|Memoria máxima para el grupo de búferes por cada instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Sistema operativo máximo|128 GB|64 GB|1410 MB|1410 MB|
|Cantidad máxima de memoria para la caché de segmento del almacén de columnas por cada instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memoria ilimitada| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 GB<sup>2</sup>| 352 GB<sup>2</sup>|  
|Tamaño máximo de datos con optimización para memoria por base de datos en [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memoria ilimitada| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 GB<sup>2</sup>| 352 GB<sup>2</sup>|  
|Memoria máxima usada por instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Sistema operativo máximo|Tabular: 16 GB<br /><br /> MOLAP: 64 GB|N/D|N/D|N/D|  
|Memoria máxima usada por instancia de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Sistema operativo máximo|64 GB|64 GB|4 GB|N/D|
|Tamaño máximo de la base de datos relacional|524 PB|524 PB|524 PB|10 GB|10 GB|  
  
<sup>1</sup> La licencia basada en Enterprise Edition con licencia de servidor y acceso de cliente (CAL) (no disponible para nuevos contratos) está limitada a un máximo de 20 núcleos por instancia de SQL Server. No hay ningún límite en el modelo de licencias de servidor basado en núcleos. Para obtener más información, consulte [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
<sup>2</sup> Se aplica a [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. 

##  <a name="RDBMSHA"></a> RDBMS High Availability  
  
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
|Restauración de archivos y páginas en línea|Sí|No|No|No|No|
|Índices en línea|Sí|No|No|No|No|
|Cambio de esquema en línea|Sí|No|No|No|No|
|Recuperación rápida|Sí|No|No|No|No|
|Copias de seguridad reflejadas|Sí|No|No|No|No|
|Agregar memoria y CPU sin interrupción|Sí|No|No|No|No|
|Asistente para la recuperación de base de datos|Sí|Sí|Sí|Sí|Sí|
|Copia de seguridad cifrada|Sí|Sí|No|No|No|
|Copia de seguridad híbrida en Windows Azure (copia de seguridad en dirección URL)|Sí|Sí|No|No|No|  
  
 <sup>1</sup> Para más información sobre cómo instalar SQL Server 2016 en Server Core, vea [Instalación de SQL Server 2016 en Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md). 

<sup>2</sup> Para más información sobre los grupos de disponibilidad básica, vea [Grupos de disponibilidad básica](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).  

<sup>3</sup> Se aplica a [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.
  
##  <a name="RDBMSSP"></a> RDBMS Scalability and Performance  
  
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
##  <a name="RDBMSS"></a> RDBMS Security  
  
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
##  <a name="Replication"></a> Replication  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Suscriptores heterogéneos|Sí|Sí|No|No|No|  
|Replicación de mezcla|Sí|Sí|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|   
|Publicación de Oracle|Sí|No|No|No|No| 
|Replicación transaccional punto a punto|Sí|No|No|No|No|   
|Replicación de instantáneas|Sí|Sí|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|   
|Seguimiento de cambios de SQL Server|Sí|Sí|Sí|Sí|Sí| 
|Replicación transaccional|Sí|Sí|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|   
|Replicación transaccional a Azure|Sí|Sí|No|No|No|   
|Suscripción actualizable a la replicación transaccional|Sí|No|No|No|No|  
  
##  <a name="SSMS"></a> Management Tools  
  
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
  
##  <a name="RDBMSM"></a> RDBMS Manageability  
  
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
  
##  <a name="DevTools"></a> Development Tools  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Integración de Microsoft Visual Studio|Sí|Sí|Sí|Sí|Sí| 
|IntelliSense (Transact-SQL y MDX)|Sí|Sí|Sí|Sí|Sí| 
|SQL Server Data Tools (SSDT)|Sí|Sí|Sí|Sí|No|    
|Herramientas de edición, depuración y diseño de MDX|Sí|Sí|No|No|No|   
  
##  <a name="Programmability"></a> Programmability  
  
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
  
## <a name="IS"></a> Integration Services

Para obtener información sobre las características de Integration Services (SSIS) compatibles con las ediciones de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], vea [Integration Services Features Supported by the Editions of SQL Server](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md) (Características de Integration Services compatibles con las ediciones de SQL Server).

##  <a name="MDS"></a> Master Data Services  
 Para información sobre las características de [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] y Data Quality Services compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Master Data Services y Data Quality Services compatibles con las ediciones de SQL Server 2016](../master-data-services/master-data-services-and-data-quality-services-features-support.md). 

  
##  <a name="DW"></a> Data Warehouse  
  
|Característica|Enterprise|Standard|Web|Express con Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Crear cubos sin base de datos|Sí|Sí|No|No|No |   
|Ensayo de generación automática y esquema de almacenamiento de datos|Sí|Sí|No|No|No| 
|Captura de datos modificados|Sí|Sí <sup>1</sup>|No|No|No| 
|Optimizaciones de consultas de combinación en estrella|Sí|No|No|No|No| 
|Configuración de solo lectura escalable de Analysis Services|Sí|No|No|No|No| 
|Procesamiento de consultas en paralelo en las tablas e índices con particiones|Sí|No|No|No|No|   
|Agregación global de lotes|Sí|No|No|No|No| 

<sup>1</sup> Se aplica a [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] SP1.  
##  <a name="SSAS"></a> Analysis Services  
  
Para información sobre las características de Analysis Services compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Analysis Services compatibles con las ediciones de SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md). 
  
##  <a name="BIMD"></a> BI Semantic Model (Multi Dimensional)  
  
Para información sobre las características de Analysis Services compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Analysis Services compatibles con las ediciones de SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
   
##  <a name="BIT"></a> BI Semantic Model (Tabular)  
  
Para información sobre las características de Analysis Services compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Analysis Services compatibles con las ediciones de SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="PPSP"></a> Power Pivot for SharePoint  
  
Para información sobre las características de Power Pivot para SharePoint compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Analysis Services compatibles con las ediciones de SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="DM"></a> Data Mining  
  
Para información sobre las características de minería de datos compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Analysis Services compatibles con las ediciones de SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="SSRS"></a> Reporting Services  
  
Para información sobre las características de Reporting Services compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Reporting Services compatibles con las ediciones de SQL Server 2016](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).

##  <a name="BIC"></a> Business Intelligence Clients  

Para información sobre las características del cliente de Business Intelligence compatibles con las ediciones de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Características de Analysis Services compatibles con las ediciones de SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) o [Características de Reporting Services compatibles con las ediciones de SQL Server 2016](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="SLS"></a> Spatial and Location Services  
  
|Nombre de la característica|Enterprise|Standard|Web|Express con Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Índices espaciales|Sí|Sí|Sí|Sí|Sí|   
|Tipos de datos planares y geodésicos|Sí|Sí|Sí|Sí|Sí| 
|Bibliotecas espaciales avanzadas|Sí|Sí|Sí|Sí|Sí|   
|Importación y exportación de formatos de datos espaciales estándar del sector|Sí|Sí|Sí|Sí|Sí|   
  
##  <a name="ADS"></a> Additional Database Services  
  
|Nombre de la característica|Enterprise|Standard|Web|Express con Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|Sí|Sí|Sí|Sí|Sí|   
|Correo electrónico de base de datos|Sí|Sí|Sí|No|No| 
  
##  <a name="Other"></a> Other Components  
  
|Nombre de la característica|Enterprise|Standard|Web|Express con Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|No|No| 
|StreamInsight HA|StreamInsight Premium Edition|No|No|No|No|   
  
> [![Download SSMS](../analysis-services/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx) **[Download the latest version of SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**    
  
## <a name="see-also"></a>Vea también  
 [Especificaciones de producto para SQL Server 2016](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [Instalación de SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)  
  
  

