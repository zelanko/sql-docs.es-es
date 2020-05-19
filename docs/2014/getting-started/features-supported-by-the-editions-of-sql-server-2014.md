---
title: Características admitidas por las ediciones de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 118fe59e76f23089ce56371ea4ba981bb4ab1f7f
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706963"
---
# <a name="features-supported-by-the-editions-of-sql-server-2014"></a>Características compatibles con las ediciones de SQL Server 2014


  Este tema proporciona información detallada de las características admitidas por las diversas ediciones de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. 

 > **Nota:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está disponible en una edición de evaluación durante un período de prueba de 180 días. Para obtener más información, vea el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [de](https://go.microsoft.com/fwlink/?LinkId=190955).  
> 
> **Nota:** Para ver las características admitidas por las ediciones Evaluation y Developer, vea el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] conjunto de características de Enterprise.  
  
 Para navegar hasta la tabla de una tecnología de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , haga clic en su vínculo:  
  
 [Límites de escala entre cuadros](#CrossBoxScale)  
  
 [Alta disponibilidad](#High_availability)  
  
 [Escalabilidad y rendimiento](#Scalability)  
  
 [Seguridad](#Enterprise_security)  
  
 [Replicación](#Replication)  
  
 [Herramientas de administración](#Mgmt_Tools)  
  
 [Capacidad de administración de RDBMS](#RDBMS_mgmt)  
  
 [Herramientas de desarrollo](#Dev_tools)  
  
 [Programación](#Programmability)  
  
 [Servicio de integración](#SSIS)  
  
 [Integration Services: adaptadores avanzados](#SSIS_AA)  
  
 [Integration Services: transformaciones avanzadas](#SSIS_AT)  
  
 [Master Data Services](#MDS)  
  
 [Almacenamiento de datos](#Data_warehouse)  
  
 [Analysis Services](#SSAS)  
  
 [Modelo semántico BI (multidimensional)](#BISemModel_multi)  
  
 [Modelo semántico BI (tabular)](#BISemModel_tabular)  
  
 [PowerPivot para SharePoint](#PowerPivot)  
  
 [Minería de datos](#DataMining)  
  
 [Reporting Services](#Reporting)  
  
 [Clientes de Business Intelligence](#BIClients)  
  
 [Servicios espaciales y de ubicación](#Spatial)  
  
 [Servicios de bases de datos adicionales](#Add_DBServices)  
  
 [Otros componentes](#Other_Components)  
  
##  <a name="cross-box-scale-limits"></a><a name="CrossBoxScale"></a>Límites de escala entre cuadros  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Capacidad máxima de proceso utilizada por una instancia única (motor de base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)])<sup>1</sup>|Sistema operativo máximo|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|  
|Capacidad máxima de cálculo utilizada por una instancia única (Analysis Services, Reporting Services) <sup>1</sup>|Sistema operativo máximo|Sistema operativo máximo|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|  
|Memoria máxima usada (por instancia del motor de base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] )|Sistema operativo máximo|128 GB|128 GB|64 GB|1 GB|1 GB|1 GB|  
|Memoria máxima usada (por instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)])|Sistema operativo máximo|Sistema operativo máximo|64 GB|N/D|N/D|N/D|N/D|  
|Memoria máxima usada (por instancia de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)])|Sistema operativo máximo|Sistema operativo máximo|64 GB|64 GB|4 GB|N/D|N/D|  
|Tamaño máximo de la base de datos relacional|524 PB|524 PB|524 PB|524 PB|10 GB|10 GB|10 GB|  
  
 <sup>1</sup> la licencia basada en Enterprise Edition con licencia de servidor y acceso de cliente (cal) (no disponible para nuevos contratos) está limitada a un máximo de 20 núcleos por [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instancia. No hay ningún límite en el modelo de licencias de servidor basado en núcleos. Para obtener más información, consulte [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
##  <a name="high-availability"></a><a name="High_availability"></a>Alta disponibilidad  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Compatibilidad con Server Core<sup>1</sup>|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Trasvase de registros|Yes|Yes|Yes|Yes||||  
|Creación de reflejo de la base de datos|Yes|Sí (solo seguridad completa)|Sí (solo seguridad completa)|Solo testigo|Solo testigo|Solo testigo|Solo testigo|  
|Compresión de copia de seguridad|Yes|Yes|Yes|||||  
|Instantáneas de base de datos|Yes|||||||  
|Instancias de clúster de conmutación por error de AlwaysOn|Sí (soporte del nodo: sistema operativo máximo)|Sí (soporte del nodo: 2)|Sí (soporte del nodo: 2)|||||  
|Grupos de disponibilidad AlwaysOn|Sí (hasta 8 réplicas secundarias, incluidas 2 réplicas secundarias síncronas)|||||||  
|Connection Director|Yes|||||||  
|Restauración de archivos y páginas en línea|Yes|||||||  
|Índices en línea|Yes|||||||  
|Cambio de esquema en línea|Yes|||||||  
|Recuperación rápida|Yes|||||||  
|Copias de seguridad reflejadas|Yes|||||||  
|Agregar memoria y CPU<sup>2</sup> en caliente|Yes|||||||  
|Asistente para recuperación de base de datos|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Copia de seguridad cifrada|Yes|Yes|Yes|||||  
|Copia de seguridad inteligente|Yes|Yes|Yes|No||||  
  
 <sup>1</sup> Para obtener más información sobre cómo instalar [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] en Server Core, consulte [instalación de SQL Server 2014 en Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md).  
  
 <sup>2</sup> Esta característica solo está disponible para 64 bits [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
##  <a name="scalability-and-performance"></a><a name="Scalability"></a>Escalabilidad y rendimiento  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Compatibilidad con varias instancias|50|50|50|50|50|50|50|  
|Particiones de tabla e índice|Yes|||||||  
|Compresión de datos|Sí|||||||  
|regulador de recursos|Sí|||||||  
|Paralelismo de la tabla de particiones|Yes|||||||  
|Varios contenedores de secuencias de archivo|Yes|||||||  
|Asignación de memoria de página grande habilitada para NUMA y matriz de búferes|Yes|||||||  
|Extensión del grupo de búferes <sup>1</sup>|Yes|Yes|Yes|||||  
|Regulación de recursos de E/S|Yes|||||||  
|OLTP en memoria <sup>1</sup>|Yes|||||||  
|Durabilidad diferida|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
  
 <sup>1</sup> esta característica solo está disponible para 64 bits [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
##  <a name="security"></a><a name="Enterprise_security"></a> Seguridad  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Auditoría básica|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Auditoría específica|Yes|||||||  
|Cifrado de base de datos transparente|Sí|||||||  
|Administración extensible de claves|Yes|||||||  
|Roles definidos por el usuario|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Bases de datos independientes|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Cifrado para copias de seguridad|Yes|Yes|Sí|||||  
  
##  <a name="replication"></a><a name="Replication"></a> Replicación  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Seguimiento de los cambios de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Replicación de mezcla|Yes|Yes|Yes|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|  
|Replicación transaccional|Yes|Yes|Yes|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|  
|Replicación de instantáneas|Yes|Yes|Yes|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|  
|Suscriptores heterogéneos|Yes|Yes|Yes|||||  
|Publicación de Oracle|Yes|||||||  
|Replicación transaccional punto a punto|Yes|||||||  
  
##  <a name="management-tools"></a><a name="Mgmt_Tools"></a>Herramientas de administración  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Objetos de administración de SQL (SMO)|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Administrador de configuración de SQL|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|SQL CMD (herramienta del símbolo del sistema)|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio|Yes|Yes|Yes|Yes|Yes|Yes||  
|Distributed Replay: herramienta de administración|Yes|Yes|Yes|Yes|Yes|Yes||  
|Distributed Replay: cliente|Sí|No|Sí|Yes||||  
|Distributed Replay: controlador|Sí (Enterprise admite hasta 16 clientes, Developer admite solo 1 cliente)|No|Sí (solo admite 1 cliente)|Sí (solo admite 1 cliente)||||  
|SQL Profiler|Yes|Yes|Yes|No<sup>2</sup>|No<sup>2</sup>|No<sup>2</sup>|No<sup>2</sup>|  
|e[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Yes|Yes|Yes|Yes||||  
|Paquete de administración de Microsoft System Center Operations Manager|Yes|Yes|Yes|Yes||||  
|Asistente para la optimización de motor de base de datos (DTA)|Yes|Yes|Sí<sup>3</sup>|Sí<sup>3</sup>||||  
|Implementar una [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] base de datos en un asistente para VM de Azure|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Archivos de datos en Azure|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
  
 <sup>2</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] se pueden crear perfiles de Web,, con herramientas y [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] con Advanced Services mediante las [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ediciones Standard y [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise.  
  
 <sup>3</sup> la optimización se habilita solo en las características de la edición Standard.  
  
##  <a name="rdbms-manageability"></a><a name="RDBMS_mgmt"></a>Capacidad de administración de RDBMS  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Instancias de usuario|||||Yes|Yes|Yes|  
|LocalDB|||||Yes|Yes||  
|Conexión de administración dedicada|Yes|Yes|Yes|Yes|Sí (bajo marca de seguimiento)|Sí (bajo marca de seguimiento)|Sí (bajo marca de seguimiento)|  
|Compatibilidad con PowerShell scripting|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Compatibilidad con SysPrep<sup>1</sup>|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Compatibilidad con operaciones de componentes de aplicación de capa de datos: extracción, implementación, actualización, eliminación|Yes|Yes|Yes|Yes|Yes|Yes|Sí|  
|Automatización de directivas (comprobar en la programación y cambio)|Yes|Yes|Yes|Yes||||  
|Recopilador de datos de rendimiento|Yes|Yes|Yes|Yes||||  
|Capacidad de inscribirse como instancia administrada en una administración de varias instancias|Yes|Yes|Yes|Yes||||  
|Informes de rendimiento estándar|Yes|Yes|Yes|Yes||||  
|Guías del plan y congelación del plan para las guías del plan|Yes|Yes|Yes|Yes||||  
|Consulta directa de vistas indexadas (mediante la sugerencia NOEXPAND)|Yes|Yes|Yes|Yes||||  
|Mantenimiento automático de vistas indexadas|Yes|Yes|Yes|Yes||||  
|Vistas distribuidas con particiones|Sí|Parcial. Las vistas distribuidas con particiones no son actualizables|Parcial. Las vistas distribuidas con particiones no son actualizables|Parcial. Las vistas distribuidas con particiones no son actualizables|Parcial. Las vistas distribuidas con particiones no son actualizables|Parcial. Las vistas distribuidas con particiones no son actualizables|Parcial. Las vistas distribuidas con particiones no son actualizables|  
|Operaciones indizadas en paralelo|Yes|||||||  
|Uso automático de vistas indexadas por el optimizador de consultas|Yes|||||||  
|Comprobación de coherencia en paralelo|Yes|||||||  
|Punto de control de la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Yes|||||||  
|Bases de datos independientes|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Extensión del grupo de búferes<sup>2</sup>|Yes|Yes|Yes|||||  
  
 <sup>1</sup> para obtener más información, consulte [consideraciones para instalar SQL Server con Sysprep](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
  
 <sup>2</sup> esta característica solo está disponible para 64 bits [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
##  <a name="development-tools"></a><a name="Dev_tools"></a>Herramientas de desarrollo  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Integración de [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Intellisense ([!INCLUDE[tsql](../includes/tsql-md.md)] y MDX)|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Yes|Yes|Yes|Yes|Yes|||  
|Herramientas de edición y diseño de consultas SQL<sup>1</sup>|Yes|Yes|Yes|||||  
|Compatibilidad con el control de versiones<sup>1</sup>|Yes|Yes|Yes|||||  
|Herramientas de edición, depuración y diseño de MDX<sup>1</sup>|Yes|Yes|Yes|||||  
  
 <sup>1</sup> esta característica no está disponible para la versión de 64 bits de la edición Standard.  
  
##  <a name="programmability"></a><a name="Programmability"></a> Programmability  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Integración de Common Language Runtime (CLR)|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Compatibilidad con XML nativo|Yes|Yes|Yes|Yes|Yes|Yes|Sí|  
|Índices XML|Sí|Yes|Yes|Yes|Yes|Yes|Yes|  
|COMBINACIONES & funcionalidades de UPSERT|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|compatibilidad con FILESTREAM|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|FileTable|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Tipos de datos de fecha y hora|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Compatibilidad para internacionalización|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Búsqueda de texto completo y semántica|Yes|Yes|Yes|Yes|Yes|||  
|Especificación de idioma en la consulta|Yes|Yes|Yes|Yes|Yes|||  
|Service Broker (mensajería)|Sí|Yes|Sí|No (solo cliente)|No (solo cliente)|No (solo cliente)|No (solo cliente)|  
|Extremos de [!INCLUDE[tsql](../includes/tsql-md.md)]|Yes|Yes|Yes|Yes||||  
  
##  <a name="integration-services"></a><a name="SSIS"></a> Integration Services  
  
|Característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Conectores de origen de datos integrados|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Diseñador y tiempo de ejecución de SSIS|Yes|Yes|Yes|||||  
|Transformaciones básicas|Yes|Yes|Yes|||||  
|Herramientas de generación de perfiles de datos básicos|Yes|Yes|Yes|||||  
|Servicio de captura de datos modificados para Oracle de Attunity|Yes|||||||  
|Diseñador de captura de datos modificados para Oracle de Attunity|Yes|||||||  
  
###  <a name="integration-services---advanced-adapters"></a><a name="SSIS_AA"></a>Integration Services-adaptadores avanzados  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Destino de Oracle de alto rendimiento|Yes|||||||  
|Destino de teradatos de alto rendimiento|Yes|||||||  
|Origen y destino de SAP BW|Yes|||||||  
|Adaptador de destino de entrenamiento del modelo de minería de datos|Yes|||||||  
|Adaptador de destino de procesamiento de dimensiones|Yes|||||||  
|Adaptador de destino de procesamiento de particiones|Yes|||||||  
|Componentes de Captura de datos modificados de Attunity|Yes|||||||  
|Conector de Conectividad abierta de base de datos (ODBC) de Attunity|Yes|||||||  
  
###  <a name="integration-services---advanced-transforms"></a><a name="SSIS_AT"></a>Integration Services-transformaciones avanzadas  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Búsquedas persistentes (alto rendimiento)|Yes|||||||  
|Transformación de consulta de minería de datos|Yes|||||||  
|Transformaciones de búsqueda y agrupación aproximada|Yes|||||||  
|Transformaciones de búsqueda y extracción de términos|Yes|||||||  
  
##  <a name="master-data-services"></a><a name="MDS"></a>Master Data Services  
  
> [!NOTE]  
>  -   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] solo está disponible en las ediciones de 64 bits de Business Intelligence y Enterprise.  
  
|Característica|Empresa|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|Sí|Sí||||||  
|Aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]|Sí|Sí||||||  
  
##  <a name="data-warehouse"></a><a name="Data_warehouse"></a>Almacenamiento de datos  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Crear cubos sin base de datos|Sí|Sí|Sí|||||  
|Ensayo de generación automática y esquema de almacenamiento de datos|Sí|Sí|Sí|||||  
|captura de datos modificados|Yes|||||||  
|Optimizaciones de consultas de combinación en estrella|Yes|||||||  
|Configuración de solo lectura escalable de Analysis Services|Yes|||||||  
|Procesamiento de consultas en paralelo en las tablas e índices con particiones|Yes|||||||  
|índices de almacén de columnas optimizados de memoria xVelocity|Yes|||||||  
|Agregación global de lotes|Yes|||||||  
  
##  <a name="analysis-services"></a><a name="SSAS"></a>Analysis Services  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Bases de datos compartidas escalables (adjuntar y separar, leer solo las bases de datos)|Sí|Sí||||||  
|Copia de seguridad o restauración, adjuntar y separar bases de datos|Sí|Sí|Sí|||||  
|Sincronizar bases de datos|Sí|Sí||||||  
|Alta disponibilidad|Sí|Sí|Sí|||||  
|Programación (AMO, ADOMD.Net, OLEDB, XML/A, ASSL)|Sí|Sí|Sí|||||  
  
###  <a name="bi-semantic-model-multidimensional"></a><a name="BISemModel_multi"></a>Modelo semántico de BI (multidimensional)  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
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
  
 <sup>1</sup> La medida de suma parcial LastChild se admite en la edición estándar, pero otras medidas de suma parcial, como None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren y ByAccount, no lo son. En todas las ediciones se admiten medidas de suma, como Sum, Count, Min y Max, y medidas de no suma (DistinctCount).  
  
###  <a name="bi-semantic-model-tabular"></a><a name="BISemModel_tabular"></a>Modelo semántico de BI (tabular)  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Jerarquías|Sí|Sí||||||  
|KPI|Sí|Sí||||||  
|perspectivas|Sí|Sí||||||  
|Translations|Sí|Sí||||||  
|Cálculos de DAX, consultas de DAX, consultas MDX|Sí|Sí||||||  
|Seguridad de filas|Sí|Sí||||||  
|Particiones|Sí|Sí||||||  
|Modos de almacenamiento In-Memory y DirectQuery (solo tabulares)|Sí|Sí||||||  
  
###  <a name="powerpivot-for-sharepoint"></a><a name="PowerPivot"></a> PowerPivot para SharePoint  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Integración de la granja de servidores de SharePoint según la arquitectura del servicio|Sí|Sí||||||  
|Informes de uso|Sí|Sí||||||  
|Reglas de seguimiento de estado|Sí|Sí||||||  
|Galería de PowerPivot|Sí|Sí||||||  
|Actualización de datos PowerPivot|Sí|Sí||||||  
|Fuentes de distribución de datos de PowerPivot|Sí|Sí||||||  
  
###  <a name="data-mining"></a><a name="DataMining"></a>Minería de datos  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Algoritmos estándar|Sí|Sí|Sí|||||  
|Herramientas de minería de datos (asistentes, editores, generadores de consultas)|Sí|Sí|Sí|||||  
|Validación cruzada|Sí|Sí||||||  
|Modelos de subconjuntos filtrados de datos de estructura de minería de datos|Sí|Sí||||||  
|Series temporales: mezcla personalizada entre métodos ARTXP y ARIMA|Sí|Sí||||||  
|Series horarias: predicción con nuevos datos|Sí|Sí||||||  
|Consultas de minería de datos simultáneas ilimitadas|Sí|Sí||||||  
|Configuración avanzada & opciones de optimización para algoritmos de minería de datos|Sí|Sí||||||  
|Compatibilidad con algoritmos de complemento|Sí|Sí||||||  
|Procesamiento de modelos en paralelo|Sí|Sí||||||  
|Series temporales: predicción de series cruzadas|Sí|Sí||||||  
|Atributos ilimitados para reglas de asociación|Sí|Sí||||||  
|Predicción de secuencias|Sí|Sí||||||  
|Varios destinos de predicción para Bayes naive, red neuronal y regresión logística|Sí|Sí||||||  
  
##  <a name="reporting-services"></a><a name="Reporting"></a>Reporting Services  
  
###  <a name="reporting-services-features"></a><a name="Reporting_features"></a>Reporting Services características  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
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
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]<sup>2</sup>|Sí|Sí||||||  
  
 <sup>1</sup> Para obtener más información sobre los orígenes de datos admitidos en [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] , vea [orígenes de datos compatibles con Reporting Services &#40;SSRS&#41;](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
 <sup>2</sup> Requiere [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en modo de SharePoint. Para obtener más información, vea [Reporting Services la instalación en modo de sharepoint &#40;sharepoint 2010 y sharepoint 2013&#41;](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
### <a name="report-server-database-server-edition-requirements"></a>Requisitos de edición de servidor de la base de datos del servidor de informes  
 Al crear una base de datos del servidor de informes, no se pueden usar todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para hospedarla. En la tabla siguiente se muestra qué ediciones del [!INCLUDE[ssDE](../includes/ssde-md.md)] se pueden usar para ediciones concretas de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
|Para esta edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services|Utilice esta edición de la instancia del motor de base de datos para hospedar la base de datos|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Empresa|Ediciones Standard, Business Intelligence Enterprise (local o remota)|  
|Inteligencia empresarial|Ediciones Standard, Business Intelligence Enterprise (local o remota)|  
|Estándar|Standard Edition, Enterprise Edition (local o remota)|  
|Web|Web Edition (solo local)|  
|Express con Advanced Services|Express con Advanced Services (solo local).|  
|Evaluación|Evaluación|  
  
##  <a name="business-intelligence-clients"></a><a name="BIClients"></a>Clientes de Business Intelligence  
 Las siguientes aplicaciones cliente de software están disponibles en el centro de descargas de Microsoft y se proporcionan para ayudarle a crear documentos de Business Intelligence que se ejecutan en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Si hospeda estos documentos en un entorno de servidor, utilice una edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] compatible con ese tipo de documento. En la siguiente tabla se indica qué edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene las características de servidor necesarias para hospedar los documentos creados en estas aplicaciones cliente.  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]|Yes|Yes|Yes|||||  
|Complementos de minería de datos para Excel y Visio 2010|Yes|Yes|Yes|||||  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010|Yes|Yes||||||  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]|Yes|Yes||||||  
  
> [!NOTE]
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)]es un complemento de Excel y no depende de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Sin embargo se requiere [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] para el uso compartido y la colaboración con los libros de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] de SharePoint y esta función está disponible como parte de las ediciones Enterprise y Business Intelligence de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
> 2.  En la tabla anterior se identifican las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] necesarias para habilitar estas herramientas de cliente. No obstante, estas características pueden acceder a los datos hospedados en cualquier edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="spatial-and-location-services"></a><a name="Spatial"></a>Servicios espaciales y de ubicación  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Índices espaciales|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Tipos de datos planares y geodésicos|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Bibliotecas espaciales avanzadas|Yes|Yes|Yes|Yes|Yes|Yes|Sí|  
|Importación y exportación de formatos de datos espaciales estándar del sector|Sí|Yes|Yes|Yes|Yes|Yes|Yes|  
  
##  <a name="additional-database-services"></a><a name="Add_DBServices"></a>Servicios de base de datos adicionales  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Correo electrónico de base de datos|Yes|Yes|Yes|Yes||||  
  
##  <a name="other-components"></a><a name="Other_Components"></a>Otros componentes  
  
|Nombre de la característica|Enterprise|Inteligencia empresarial|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Data Quality Services|Sí|Sí||||||  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|StreamInsight Standard Edition||||  
|StreamInsight HA|StreamInsight Premium Edition|||||||  
  
## <a name="see-also"></a>Consulte también  
 [Especificaciones del producto para SQL Server 2014](../../2014/getting-started/sql-server-2014-product-specifications.md)   
 [Instalación de SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Instalación del tutorial de SQL Server 2014](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
