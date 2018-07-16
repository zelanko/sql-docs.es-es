---
title: Características compatibles con las ediciones de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- data-quality-services
- database-engine
- integration-services
- master-data-services
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
caps.latest.revision: 126
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dac6134987f8a6d3964d919d1aff7688b74da7fe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312315"
---
# <a name="features-supported-by-the-editions-of-sql-server-2014"></a>Características compatibles con las ediciones de SQL Server 2014
  Este tema proporciona información detallada de las características admitidas por las diversas ediciones de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
> **Nota:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está disponible en una edición de evaluación durante un período de prueba de 180 días. Para obtener más información, consulte el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [sitio Web de Software de prueba](http://go.microsoft.com/fwlink/?LinkId=190955).  
  
> **Nota:** para características compatibles con las ediciones Evaluation y Developer, consulte el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] conjunto de características de Enterprise.  
  
 Para navegar hasta la tabla de una tecnología de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , haga clic en su vínculo:  
  
 [Límites de escala entre cuadros](#CrossBoxScale)  
  
 [Alta disponibilidad](#High_availability)  
  
 [Escalabilidad y rendimiento](#Scalability)  
  
 [Seguridad](#Enterprise_security)  
  
 [Replicación](#Replication)  
  
 [Herramientas de administración](#Mgmt_Tools)  
  
 [Facilidad de uso RDBMS](#RDBMS_mgmt)  
  
 [Herramientas de desarrollo](#Dev_tools)  
  
 [Capacidad de programación](#Programmability)  
  
 [Integration Services](#SSIS)  
  
 [Integration Services: adaptadores avanzados](#SSIS_AA)  
  
 [Integration Services: transformaciones avanzadas](#SSIS_AT)  
  
 [Master Data Services](#MDS)  
  
 [Data Warehouse](#Data_warehouse)  
  
 [Analysis Services](#SSAS)  
  
 [Modelo semántico BI (Multidimensional)](#BISemModel_multi)  
  
 [Modelo semántico BI (Tabular)](#BISemModel_tabular)  
  
 [PowerPivot para SharePoint](#PowerPivot)  
  
 [Minería de datos](#DataMining)  
  
 [Reporting Services](#Reporting)  
  
 [Clientes de Business Intelligence](#BIClients)  
  
 [Espaciales y los servicios de ubicación](#Spatial)  
  
 [Servicios adicionales de la base de datos](#Add_DBServices)  
  
 [Otros componentes](#Other_Components)  
  
##  <a name="CrossBoxScale"></a> Límites de escala entre cuadros  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Capacidad máxima de cálculo utilizada por una instancia única ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] motor de base de datos)<sup>1</sup>|Sistema operativo máximo|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|  
|Capacidad máxima de cálculo utilizada por una instancia única (Analysis Services, Reporting Services) <sup>1</sup>|Sistema operativo máximo|Sistema operativo máximo|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|  
|Memoria máxima usada (por instancia del motor de base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)])|Sistema operativo máximo|128 GB|128 GB|64 GB|1 GB|1 GB|1 GB|  
|Memoria máxima usada (por instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)])|Sistema operativo máximo|Sistema operativo máximo|64 GB|N/A|N/D|N/D|N/D|  
|Memoria máxima usada (por instancia de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)])|Sistema operativo máximo|Sistema operativo máximo|64 GB|64 GB|4 GB|N/D|N/D|  
|Tamaño máximo de la base de datos relacional|524 PB|524 PB|524 PB|524 PB|10 GB|10 GB|10 GB|  
  
 <sup>1</sup> Enterprise Edition con el servidor y cliente acceso licencia (CAL) en función de licencias (no disponible para nuevos contratos) está limitada a un máximo de 20 núcleos por [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instancia. No hay ningún límite en el modelo de licencias de servidor basado en núcleos. Para obtener más información, consulte [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
##  <a name="High_availability"></a> Alta disponibilidad  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Compatibilidad con Server Core<sup>1</sup>|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Trasvase de registros|Sí|Sí|Sí|Sí||||  
|Creación de reflejo de base de datos|Sí|Sí (solo seguridad completa)|Sí (solo seguridad completa)|Solo testigo|Solo testigo|Solo testigo|Solo testigo|  
|Compresión de copia de seguridad|Sí|Sí|Sí|||||  
|Instantáneas de base de datos|Sí|||||||  
|Instancias de clúster de conmutación por error de AlwaysOn|Sí (soporte del nodo: sistema operativo máximo)|Sí (soporte del nodo: 2)|Sí (soporte del nodo: 2)|||||  
|Grupos de disponibilidad AlwaysOn|Sí (hasta 8 réplicas secundarias, incluidas 2 réplicas secundarias síncronas)|||||||  
|Connection Director|Sí|||||||  
|Restauración de archivos y páginas en línea|Sí|||||||  
|Índices en línea|Sí|||||||  
|Cambio de esquema en línea|Sí|||||||  
|Recuperación rápida|Sí|||||||  
|Copias de seguridad reflejadas|Sí|||||||  
|En caliente de memoria y CPU<sup>2</sup>|Sí|||||||  
|Asistente para recuperación de base de datos|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Copia de seguridad cifrada|Sí|Sí|Sí|||||  
|Copia de seguridad inteligente|Sí|Sí|Sí|no||||  
  
 <sup>1</sup>para obtener más información acerca de cómo instalar [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] en Server Core, vea [instalar SQL Server 2014 en Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md).  
  
 <sup>2</sup>esta característica solo está disponible para 64 bits [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="Scalability"></a> Escalabilidad y rendimiento  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Compatibilidad con varias instancias|50|50|50|50|50|50|50|  
|Particiones de tabla e índice|Sí|||||||  
|Compresión de datos|Sí|||||||  
|Regulador de recursos|Sí|||||||  
|Paralelismo de la tabla de particiones|Sí|||||||  
|Varios contenedores de secuencias de archivo|Sí|||||||  
|Asignación de memoria de página grande habilitada para NUMA y matriz de búferes|Sí|||||||  
|Extensión del grupo de búferes <sup>1</sup>|Sí|Sí|Sí|||||  
|Regulación de recursos de E/S|Sí|||||||  
|OLTP en memoria <sup>1</sup>|Sí|||||||  
|Durabilidad diferida|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
  
 <sup>1</sup> esta característica solo está disponible para 64 bits [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="Enterprise_security"></a> Seguridad  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Auditoría básica|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Auditoría específica|Sí|||||||  
|Cifrado de base de datos transparente|Sí|||||||  
|Administración extensible de claves|Sí|||||||  
|Roles definidos por el usuario|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Bases de datos independientes|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Cifrado para copias de seguridad|Sí|Sí|Sí|||||  
  
##  <a name="Replication"></a> Replication  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] seguimiento de cambios|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Replicación de mezcla|Sí|Sí|Sí|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|  
|Replicación transaccional|Sí|Sí|Sí|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|  
|Replicación de instantáneas|Sí|Sí|Sí|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|  
|Suscriptores heterogéneos|Sí|Sí|Sí|||||  
|Publicación de Oracle|Sí|||||||  
|Replicación transaccional punto a punto|Sí|||||||  
  
##  <a name="Mgmt_Tools"></a> Management Tools  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Objetos de administración de SQL (SMO)|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Administrador de configuración de SQL|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|SQL CMD (herramienta del símbolo del sistema)|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio|Sí|Sí|Sí|Sí|Sí|Sí||  
|Distributed Replay: herramienta de administración|Sí|Sí|Sí|Sí|Sí|Sí||  
|Distributed Replay: cliente|Sí|no|Sí|Sí||||  
|Distributed Replay: controlador|Sí (Enterprise admite hasta 16 clientes, Developer admite solo 1 cliente)|no|Sí (solo admite 1 cliente)|Sí (solo admite 1 cliente)||||  
|SQL Profiler|Sí|Sí|Sí|No<sup>2</sup>|No<sup>2</sup>|No<sup>2</sup>|No<sup>2</sup>|  
|e[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] |Sí|Sí|Sí|Sí||||  
|Paquete de administración de Microsoft System Center Operations Manager|Sí|Sí|Sí|Sí||||  
|Asistente para la optimización de motor de base de datos (DTA)|Sí|Sí|Sí<sup>3</sup>|Sí<sup>3</sup>||||  
|Asistente para implementar una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en una máquina virtual de Windows Azure|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Archivos de datos en Windows Azure|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
  
 <sup>2</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] web, [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] con herramientas, y [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] con Advanced Services se pueden personalizar con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] estándar y [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition.  
  
 <sup>3</sup> optimización se habilita solo en las características de Standard edition.  
  
##  <a name="RDBMS_mgmt"></a> RDBMS Manageability  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Instancias de usuario|||||Sí|Sí|Sí|  
|LocalDB|||||Sí|Sí||  
|Conexión de administración dedicada|Sí|Sí|Sí|Sí|Sí (bajo marca de seguimiento)|Sí (bajo marca de seguimiento)|Sí (bajo marca de seguimiento)|  
|Compatibilidad con PowerShell scripting|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Compatibilidad con SysPrep<sup>1</sup>|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Compatibilidad con las operaciones de componentes de aplicación de capa de datos: extracción, implementación, actualización, eliminación|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Automatización de directivas (comprobar en la programación y cambio)|Sí|Sí|Sí|Sí||||  
|Recopilador de datos de rendimiento|Sí|Sí|Sí|Sí||||  
|Capacidad de inscribirse como instancia administrada en una administración de varias instancias|Sí|Sí|Sí|Sí||||  
|Informes de rendimiento estándar|Sí|Sí|Sí|Sí||||  
|Guías del plan y congelación del plan para las guías del plan|Sí|Sí|Sí|Sí||||  
|Consulta directa de vistas indexadas (mediante la sugerencia NOEXPAND)|Sí|Sí|Sí|Sí||||  
|Mantenimiento automático de vistas indexadas|Sí|Sí|Sí|Sí||||  
|Vistas distribuidas con particiones|Sí|Parcial. Las vistas distribuidas con particiones no son actualizables|Parcial. Las vistas distribuidas con particiones no son actualizables|Parcial. Las vistas distribuidas con particiones no son actualizables|Parcial. Las vistas distribuidas con particiones no son actualizables|Parcial. Las vistas distribuidas con particiones no son actualizables|Parcial. Las vistas distribuidas con particiones no son actualizables|  
|Operaciones indizadas en paralelo|Sí|||||||  
|Uso automático de vistas indexadas por el optimizador de consultas|Sí|||||||  
|Comprobación de coherencia en paralelo|Sí|||||||  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Punto de control de utilidad|Sí|||||||  
|Bases de datos independientes|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Extensión del grupo de búferes<sup>2</sup>|Sí|Sí|Sí|||||  
  
 <sup>1</sup> Para más información, vea [Consideraciones acerca de la instalación de SQL Server con SysPrep](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
  
 <sup>2</sup> esta característica solo está disponible para 64 bits [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="Dev_tools"></a> Development Tools  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Integración de [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|IntelliSense ([!INCLUDE[tsql](../includes/tsql-md.md)] y MDX)|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Sí|Sí|Sí|Sí|Sí|||  
|Herramientas de edición y diseño de consultas de SQL<sup>1</sup>|Sí|Sí|Sí|||||  
|Compatibilidad de control de versiones<sup>1</sup>|Sí|Sí|Sí|||||  
|Edición MDX, depuración y las herramientas de diseño<sup>1</sup>|Sí|Sí|Sí|||||  
  
 <sup>1</sup> esta característica no está disponible para la versión de 64 bits de Standard edition.  
  
##  <a name="Programmability"></a> Programmability  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Integración de Common Language Runtime (CLR)|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Compatibilidad con XML nativo|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Índices XML|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Capacidades MERGE y UPSERT|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|compatibilidad con FILESTREAM|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|FileTable|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Tipos de datos de fecha y hora|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Compatibilidad para internacionalización|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Búsqueda de texto completo y semántica|Sí|Sí|Sí|Sí|Sí|||  
|Especificación de idioma en la consulta|Sí|Sí|Sí|Sí|Sí|||  
|Service Broker (mensajería)|Sí|Sí|Sí|No (solo cliente)|No (solo cliente)|No (solo cliente)|No (solo cliente)|  
|Extremos de [!INCLUDE[tsql](../includes/tsql-md.md)]|Sí|Sí|Sí|Sí||||  
  
##  <a name="SSIS"></a> Integration Services  
  
|Característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Conectores de origen de datos integrados|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Diseñador y tiempo de ejecución de SSIS|Sí|Sí|Sí|||||  
|Transformaciones básicas|Sí|Sí|Sí|||||  
|Herramientas de generación de perfiles de datos básicos|Sí|Sí|Sí|||||  
|Servicio de captura de datos modificados para Oracle de Attunity|Sí|||||||  
|Diseñador de captura de datos modificados para Oracle de Attunity|Sí|||||||  
  
###  <a name="SSIS_AA"></a> Integration Services: adaptadores avanzados  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Destino de Oracle de alto rendimiento|Sí|||||||  
|Destino de teradatos de alto rendimiento|Sí|||||||  
|Origen y destino de SAP BW|Sí|||||||  
|Adaptador de destino de entrenamiento del modelo de minería de datos|Sí|||||||  
|Adaptador de destino de procesamiento de dimensiones|Sí|||||||  
|Adaptador de destino de procesamiento de particiones|Sí|||||||  
|Componentes de Captura de datos modificados de Attunity|Sí|||||||  
|Conector de Conectividad abierta de base de datos (ODBC) de Attunity|Sí|||||||  
  
###  <a name="SSIS_AT"></a> Integration Services: transformaciones avanzadas  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Búsquedas persistentes (alto rendimiento)|Sí|||||||  
|Transformación de consulta de minería de datos|Sí|||||||  
|Transformaciones de búsqueda y agrupación aproximada|Sí|||||||  
|Transformaciones de búsqueda y extracción de términos|Sí|||||||  
  
##  <a name="MDS"></a> Master Data Services  
  
> [!NOTE]  
>  -   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] está disponible en las ediciones de 64 bits de Business Intelligence y Enterprise solo.  
  
|Característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|Sí|Sí||||||  
|Aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]|Sí|Sí||||||  
  
##  <a name="Data_warehouse"></a> Data Warehouse  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Crear cubos sin base de datos|Sí|Sí|Sí|||||  
|Ensayo de generación automática y esquema de almacenamiento de datos|Sí|Sí|Sí|||||  
|Captura de datos modificados|Sí|||||||  
|Optimizaciones de consultas de combinación en estrella|Sí|||||||  
|Configuración de solo lectura escalable de Analysis Services|Sí|||||||  
|Procesamiento de consultas en paralelo en las tablas e índices con particiones|Sí|||||||  
|índices de almacén de columnas optimizados de memoria xVelocity|Sí|||||||  
|Agregación global de lotes|Sí|||||||  
  
##  <a name="SSAS"></a> Analysis Services  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Bases de datos compartidas escalables (adjuntar y separar, leer solo las bases de datos)|Sí|Sí||||||  
|Copia de seguridad o restauración, adjuntar y separar bases de datos|Sí|Sí|Sí|||||  
|Sincronizar bases de datos|Sí|Sí||||||  
|Alta disponibilidad|Sí|Sí|Sí|||||  
|Programación (AMO, ADOMD.Net, OLEDB, XML/A, ASSL)|Sí|Sí|Sí|||||  
  
###  <a name="BISemModel_multi"></a> Modelo semántico BI (Multidimensional)  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Medidas de suma parcial|Sí|Sí|No<sup>1</sup>|||||  
|Jerarquías|Sí|Sí|Sí|||||  
|KPI|Sí|Sí|Sí|||||  
|perspectivas|Sí|Sí||||||  
|Acciones|Sí|Sí|Sí|||||  
|Inteligencia de cuentas|Sí|Sí|Sí|||||  
|Inteligencia de tiempo|Sí|Sí|Sí|||||  
|Resúmenes personalizados|Sí|Sí|Sí|||||  
|Reescritura de cubos|Sí|Sí|Sí|||||  
|Reescritura de dimensiones|Sí|Sí||||||  
|Reescritura de celdas|Sí|Sí|Sí|||||  
|Obtención de detalles|Sí|Sí|Sí|||||  
|Tipos de jerarquías avanzadas (jerarquías primarios-secundario, jerarquías desiguales)|Sí|Sí|Sí|||||  
|Dimensiones avanzadas (dimensiones de referencia, dimensiones de varios a varios)|Sí|Sí|Sí|||||  
|Medidas y dimensiones vinculadas|Sí|Sí||||||  
|Translations|Sí|Sí|Sí|||||  
|Agregaciones|Sí|Sí|Sí|||||  
|Varias particiones|Sí|Sí|Sí, hasta 3|||||  
|Almacenamiento en caché automático|Sí|Sí||||||  
|Ensamblados personalizados (procedimientos almacenados)|Sí|Sí|Sí|||||  
|Consultas MDX y scripts|Sí|Sí|Sí|||||  
|Consultas DAX|Sí|Sí||||||  
|Modelo de seguridad basada en roles|Sí|Sí|Sí|||||  
|Seguridad de dimensión y de nivel de celda|Sí|Sí|Sí|||||  
|Almacenamiento escalable de cadena|Sí|Sí|Sí|||||  
|Modos de almacenamiento MOLAP, ROLAP, HOLAP|Sí|Sí|Sí|||||  
|Transporte XML comprimido y binario|Sí|Sí|Sí|||||  
|Procesamiento de modo de inserción|Sí|Sí||||||  
|Reescritura directa|Sí|Sí||||||  
|Expresiones de medida|Sí|Sí||||||  
  
 <sup>1</sup>medida de suma parcial LastChild the se admite en standard edition, pero no lo son otras medidas de suma parcial, como None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren y ByAccount. En todas las ediciones se admiten medidas de suma, como Sum, Count, Min y Max, y medidas de no suma (DistinctCount).  
  
###  <a name="BISemModel_tabular"></a> BI Semantic Model (Tabular)  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Jerarquías|Sí|Sí||||||  
|KPI|Sí|Sí||||||  
|perspectivas|Sí|Sí||||||  
|Translations|Sí|Sí||||||  
|Cálculos de DAX, consultas de DAX, consultas MDX|Sí|Sí||||||  
|Seguridad de filas|Sí|Sí||||||  
|Particiones|Sí|Sí||||||  
|Modos de almacenamiento In-Memory y DirectQuery (solo tabulares)|Sí|Sí||||||  
  
###  <a name="PowerPivot"></a> Modelo de objetos de informe utilizado por las extensiones de representación.  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Integración de la granja de servidores de SharePoint según la arquitectura del servicio|Sí|Sí||||||  
|Informes de uso|Sí|Sí||||||  
|Reglas de seguimiento de estado|Sí|Sí||||||  
|Galería de PowerPivot|Sí|Sí||||||  
|Actualización de datos PowerPivot|Sí|Sí||||||  
|Fuentes de distribución de datos de PowerPivot|Sí|Sí||||||  
  
###  <a name="DataMining"></a> Data Mining  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Algoritmos estándar|Sí|Sí|Sí|||||  
|Herramientas de minería de datos (asistentes, editores, generadores de consultas)|Sí|Sí|Sí|||||  
|Validación cruzada|Sí|Sí||||||  
|Modelos de subconjuntos filtrados de datos de estructura de minería de datos|Sí|Sí||||||  
|Series temporales: mezcla personalizada entre métodos ARTXP y ARIMA|Sí|Sí||||||  
|Series horarias: predicción con nuevos datos|Sí|Sí||||||  
|Consultas de minería de datos simultáneas ilimitadas|Sí|Sí||||||  
|Configuración avanzada y opciones de optimización de algoritmos de minería de datos|Sí|Sí||||||  
|Compatibilidad con algoritmos de complemento|Sí|Sí||||||  
|Procesamiento de modelos en paralelo|Sí|Sí||||||  
|Series temporales: predicción de series cruzadas|Sí|Sí||||||  
|Atributos ilimitados para reglas de asociación|Sí|Sí||||||  
|Predicción de secuencias|Sí|Sí||||||  
|Varios destinos de predicción para Bayes naive, red neuronal y regresión logística|Sí|Sí||||||  
  
##  <a name="Reporting"></a> Reporting Services  
  
###  <a name="Reporting_features"></a> Características de Reporting Services  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Catálogo compatible con la edición DB [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Estándar o superior|Estándar o superior|Estándar o superior|Web|Express|||  
|Origen de datos compatibles con la edición [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Todas las ediciones de   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Web|Express|||  
|Servidor de informes|Sí|Sí|Sí|Sí|Sí|||  
|Diseñador de informes|Sí|Sí|Sí|Sí|Sí|||  
|Administrador de informes|Sí|Sí|Sí|Sí|Sí|||  
|Seguridad basada en roles|Sí|Sí|Sí|Sí|Sí|||  
|Compatibilidad con exportación de Word y texto enriquecido|Sí|Sí|Sí|Sí|Sí|||  
|Medidores y gráficos mejorados|Sí|Sí|Sí|Sí|Sí|||  
|Exportación a Excel, PDF e imágenes|Sí|Sí|Sí|Sí|Sí|||  
|Autenticación personalizada|Sí|Sí|Sí|Sí|Sí|||  
|Informe como fuentes de distribución de datos|Sí|Sí|Sí|Sí|Sí|||  
|Compatibilidad con los modelos|Sí|Sí|Sí|Sí||||  
|Crear roles personalizados para la seguridad basada en roles|Sí|Sí|Sí|||||  
|Seguridad de elementos del modelo|Sí|Sí|Sí|||||  
|Clic sobre aviso (click-through) infinito|Sí|Sí|Sí|||||  
|Biblioteca de componentes compartidos|Sí|Sí|Sí|||||  
|Suscripciones y programación de recursos compartidos de archivo y correo electrónico|Sí|Sí|Sí|||||  
|Historial de informes, instantáneas de ejecución y almacenamiento en memoria caché|Sí|Sí|Sí|||||  
|Integración de SharePoint|Sí|Sí|Sí|||||  
|Compatibilidad con orígenes de datos remotos y ajenos a SQL<sup>1</sup>|Sí|Sí|Sí|||||  
|Extensibilidad de orígenes de datos, entrega y representación, RDCE|Sí|Sí|Sí|||||  
|Suscripción a informes controlada por datos|Sí|Sí||||||  
|Implementación escalada (grupo de servidores web)|Sí|Sí||||||  
|Alertas<sup>2</sup>|Sí|Sí||||||  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] <sup>2</sup>|Sí|Sí||||||  
  
 <sup>1</sup>para obtener más información sobre los orígenes de datos admitidos en [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)], consulte [orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
 <sup>2</sup>requiere [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en modo de SharePoint. Para obtener más información, consulte [instalación de modo de SharePoint de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
### <a name="report-server-database-server-edition-requirements"></a>Requisitos de edición de servidor de la base de datos del servidor de informes  
 Al crear una base de datos del servidor de informes, no se pueden usar todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para hospedarla. En la tabla siguiente se muestra qué ediciones del [!INCLUDE[ssDE](../includes/ssde-md.md)] se pueden usar para ediciones concretas de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
|Para esta edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services|Utilice esta edición de la instancia del motor de base de datos para hospedar la base de datos|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Ediciones Standard, Business Intelligence Enterprise (local o remota)|  
|Business Intelligence|Ediciones Standard, Business Intelligence Enterprise (local o remota)|  
|Estándar|Standard Edition, Enterprise Edition (local o remota)|  
|Web|Web Edition (solo local)|  
|Express con Advanced Services|Express con Advanced Services (solo local).|  
|Evaluation|Evaluation|  
  
##  <a name="BIClients"></a> Clientes de Business Intelligence  
 Las siguientes aplicaciones cliente de software están disponibles en el centro de Microsoft Downloads y se proporcionan para ayudarle a crear documentos de business intelligence que se ejecutan en un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instancia. Si hospeda estos documentos en un entorno de servidor, utilice una edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que es compatible con ese tipo de documento. En la siguiente tabla se indica qué edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene las características de servidor necesarias para hospedar los documentos creados en estas aplicaciones cliente.  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)]|Sí|Sí|Sí|||||  
|Complementos de minería de datos para Excel y Visio 2010|Sí|Sí|Sí|||||  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010|Sí|Sí||||||  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]|Sí|Sí||||||  
  
> [!NOTE]  
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] es un complemento de Excel y no depende de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Sin embargo se requiere [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] para el uso compartido y la colaboración con los libros de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] de SharePoint y esta función está disponible como parte de las ediciones Enterprise y Business Intelligence de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
> 2.  La tabla anterior se identifican los [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ediciones que son necesarios para habilitar estas herramientas de cliente; sin embargo estas características pueden tener acceso a datos hospedados en cualquier edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="Spatial"></a> Spatial and Location Services  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Índices espaciales|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Tipos de datos planares y geodésicos|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Bibliotecas espaciales avanzadas|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Importación y exportación de formatos de datos espaciales estándar del sector|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
  
##  <a name="Add_DBServices"></a> Additional Database Services  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Correo electrónico de base de datos|Sí|Sí|Sí|Sí||||  
  
##  <a name="Other_Components"></a> Otros componentes  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Data Quality Services|Sí|Sí||||||  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|StreamInsight Standard Edition||||  
|StreamInsight HA|StreamInsight Premium Edition|||||||  
  
## <a name="see-also"></a>Vea también  
 [Especificaciones de producto para SQL Server 2014](../../2014/getting-started/sql-server-2014-product-specifications.md)   
 [Instalación de SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Inicio rápido de instalación de SQL Server 2014](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
