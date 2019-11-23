---
title: Características admitidas por las ediciones de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caae4212e2182ae6afde29b0fed1aaee4f05645a
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176127"
---
# <a name="features-supported-by-the-editions-of-sql-server-2014"></a>Características compatibles con las ediciones de SQL Server 2014


  Este tema proporciona información detallada de las características admitidas por las diversas ediciones de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. 

 > **Nota:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está disponible en una edición de evaluación durante un período de prueba de 180 días. Para obtener más información, consulte el [sitio web de software de prueba](https://go.microsoft.com/fwlink/?LinkId=190955)de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
> 
> **Nota:** Para ver las características admitidas por las ediciones Evaluation y Developer, vea el conjunto de características de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise.  
  
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
  
 [Integration Services](#SSIS)  
  
 [Integration Services-adaptadores avanzados](#SSIS_AA)  
  
 [Integration Services-transformaciones avanzadas](#SSIS_AT)  
  
 [Master Data Services](#MDS)  
  
 [Data Warehouse](#Data_warehouse)  
  
 [Analysis Services](#SSAS)  
  
 [Modelo semántico de BI (multidimensional)](#BISemModel_multi)  
  
 [Modelo semántico BI (tabular)](#BISemModel_tabular)  
  
 [PowerPivot para SharePoint](#PowerPivot)  
  
 [Minería de datos](#DataMining)  
  
 [Reporting Services](#Reporting)  
  
 [Clientes de Business Intelligence](#BIClients)  
  
 [Servicios espaciales y de ubicación](#Spatial)  
  
 [Servicios de base de datos adicionales](#Add_DBServices)  
  
 [Otros componentes](#Other_Components)  
  
##  <a name="CrossBoxScale"></a> Límites de escala entre cuadros  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Capacidad máxima de proceso utilizada por una instancia única (motor de base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)])<sup>1</sup>|Sistema operativo máximo|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|  
|Capacidad máxima de cálculo utilizada por una instancia única (Analysis Services, Reporting Services) <sup>1</sup>|Sistema operativo máximo|Sistema operativo máximo|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|  
|Memoria máxima usada (por instancia del motor de base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] )|Sistema operativo máximo|128 GB|128 GB|64 GB|1 GB|1 GB|1 GB|  
|Memoria máxima usada (por instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)])|Sistema operativo máximo|Sistema operativo máximo|64 GB|N/A|N/A|N/A|N/A|  
|Memoria máxima usada (por instancia de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)])|Sistema operativo máximo|Sistema operativo máximo|64 GB|64 GB|4 GB|N/A|N/A|  
|Tamaño máximo de la base de datos relacional|524 PB|524 PB|524 PB|524 PB|10 GB|10 GB|10 GB|  
  
 <sup>1</sup> la licencia basada en Enterprise Edition con licencia de servidor y acceso de cliente (cal) (no disponible para nuevos contratos) está limitada a un máximo de 20 núcleos por instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No hay ningún límite en el modelo de licencias de servidor basado en núcleos. Para obtener más información, vea [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
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
|Agregar memoria y CPU<sup>2</sup> en caliente|Sí|||||||  
|Asistente para recuperación de base de datos|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Copia de seguridad cifrada|Sí|Sí|Sí|||||  
|Copia de seguridad inteligente|Sí|Sí|Sí|No||||  
  
 <sup>1</sup> Para obtener más información sobre cómo instalar [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] en Server Core, consulte [instalación de SQL Server 2014 en Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md).  
  
 <sup>2</sup> Esta característica solo está disponible para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]de 64 bits.  
  
##  <a name="Scalability"></a>Escalabilidad y rendimiento  
  
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
  
 <sup>1</sup> esta característica solo está disponible para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]de 64 bits.  
  
##  <a name="Enterprise_security"></a> Seguridad  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Auditoría básica|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Auditoría específica|Sí|||||||  
|Cifrado de base de datos transparente|Sí|||||||  
|Administración extensible de claves|Sí|||||||  
|Roles definidos por el usuario|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Contained Databases|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Cifrado para copias de seguridad|Sí|Sí|Sí|||||  
  
##  <a name="Replication"></a> Replication  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Seguimiento de los cambios de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Replicación de mezcla|Sí|Sí|Sí|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|  
|Replicación transaccional|Sí|Sí|Sí|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|  
|Replicación de instantáneas|Sí|Sí|Sí|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|Sí (solo suscriptor)|  
|Suscriptores heterogéneos|Sí|Sí|Sí|||||  
|Publicación de Oracle|Sí|||||||  
|Replicación transaccional punto a punto|Sí|||||||  
  
##  <a name="Mgmt_Tools"></a> Herramientas de administración  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Objetos de administración de SQL (SMO)|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Administrador de configuración de SQL|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|SQL CMD (herramienta del símbolo del sistema)|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio|Sí|Sí|Sí|Sí|Sí|Sí||  
|Distributed Replay: herramienta de administración|Sí|Sí|Sí|Sí|Sí|Sí||  
|Distributed Replay: cliente|Sí|No|Sí|Sí||||  
|Distributed Replay: controlador|Sí (Enterprise admite hasta 16 clientes, Developer admite solo 1 cliente)|No|Sí (solo admite 1 cliente)|Sí (solo admite 1 cliente)||||  
|SQL Profiler|Sí|Sí|Sí|No<sup>2</sup>|No<sup>2</sup>|No<sup>2</sup>|No<sup>2</sup>|  
|e[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Sí|Sí|Sí|Sí||||  
|Paquete de administración de Microsoft System Center Operations Manager|Sí|Sí|Sí|Sí||||  
|Asistente para la optimización de motor de base de datos (DTA)|Sí|Sí|Sí<sup>3</sup>|Sí<sup>3</sup>||||  
|Implementar una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un asistente para VM de Azure|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de los archivos de datos en Azure|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
  
 <sup>2</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Web, [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] con herramientas y [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] con Advanced Services se pueden crear perfiles con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ediciones Standard y [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise.  
  
 <sup>3</sup> la optimización se habilita solo en las características de la edición Standard.  
  
##  <a name="RDBMS_mgmt"></a> RDBMS Manageability  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Instancias de usuario|||||Sí|Sí|Sí|  
|LocalDB|||||Sí|Sí||  
|Conexión de administración dedicada|Sí|Sí|Sí|Sí|Sí (bajo marca de seguimiento)|Sí (bajo marca de seguimiento)|Sí (bajo marca de seguimiento)|  
|Compatibilidad con PowerShell scripting|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Compatibilidad con SysPrep<sup>1</sup>|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Compatibilidad con operaciones de componentes de aplicación de capa de datos: extracción, implementación, actualización, eliminación|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
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
|Punto de control de la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Sí|||||||  
|Contained Databases|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Extensión del grupo de búferes<sup>2</sup>|Sí|Sí|Sí|||||  
  
 <sup>1</sup> Para más información, vea [Consideraciones acerca de la instalación de SQL Server con SysPrep](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
  
 <sup>2</sup> esta característica solo está disponible para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]de 64 bits.  
  
##  <a name="Dev_tools"></a> Development Tools  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Integración de [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Intellisense ([!INCLUDE[tsql](../includes/tsql-md.md)] y MDX)|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Sí|Sí|Sí|Sí|Sí|||  
|Herramientas de edición y diseño de consultas SQL<sup>1</sup>|Sí|Sí|Sí|||||  
|Compatibilidad con el control de versiones<sup>1</sup>|Sí|Sí|Sí|||||  
|Herramientas de edición, depuración y diseño de MDX<sup>1</sup>|Sí|Sí|Sí|||||  
  
 <sup>1</sup> esta característica no está disponible para la versión de 64 bits de la edición Standard.  
  
##  <a name="Programmability"></a> Programación  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Integración de Common Language Runtime (CLR)|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Compatibilidad con XML nativo|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|Índices XML|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
|COMBINACIONES & funcionalidades de UPSERT|Sí|Sí|Sí|Sí|Sí|Sí|Sí|  
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
>  -   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] solo está disponible en las ediciones de 64 bits de Business Intelligence y Enterprise.  
  
|Característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database|Sí|Sí||||||  
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
  
###  <a name="BISemModel_multi"></a>Modelo semántico de BI (multidimensional)  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Medidas de suma parcial|Sí|Sí|No<sup>1</sup>|||||  
|Jerarquías|Sí|Sí|Sí|||||  
|KPI|Sí|Sí|Sí|||||  
|Perspectivas|Sí|Sí||||||  
|Acciones|Sí|Sí|Sí|||||  
|Inteligencia de cuentas|Sí|Sí|Sí|||||  
|Inteligencia de tiempo|Sí|Sí|Sí|||||  
|Resúmenes personalizados|Sí|Sí|Sí|||||  
|Reescritura de cubos|Sí|Sí|Sí|||||  
|Reescritura de dimensiones|Sí|Sí||||||  
|Reescritura de celdas|Sí|Sí|Sí|||||  
|detallados|Sí|Sí|Sí|||||  
|Tipos de jerarquías avanzadas (jerarquías primarios-secundario, jerarquías desiguales)|Sí|Sí|Sí|||||  
|Dimensiones avanzadas (dimensiones de referencia, dimensiones de varios a varios)|Sí|Sí|Sí|||||  
|Medidas y dimensiones vinculadas|Sí|Sí||||||  
|Traducciones|Sí|Sí|Sí|||||  
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
  
###  <a name="BISemModel_tabular"></a> BI Semantic Model (Tabular)  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Jerarquías|Sí|Sí||||||  
|KPI|Sí|Sí||||||  
|Perspectivas|Sí|Sí||||||  
|Traducciones|Sí|Sí||||||  
|Cálculos de DAX, consultas de DAX, consultas MDX|Sí|Sí||||||  
|Seguridad de filas|Sí|Sí||||||  
|Particiones|Sí|Sí||||||  
|Modos de almacenamiento In-Memory y DirectQuery (solo tabulares)|Sí|Sí||||||  
  
###  <a name="PowerPivot"></a>PowerPivot para SharePoint  
  
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
|Configuración avanzada & opciones de optimización para algoritmos de minería de datos|Sí|Sí||||||  
|Compatibilidad con algoritmos de complemento|Sí|Sí||||||  
|Procesamiento de modelos en paralelo|Sí|Sí||||||  
|Series temporales: predicción de series cruzadas|Sí|Sí||||||  
|Atributos ilimitados para reglas de asociación|Sí|Sí||||||  
|Predicción de secuencias|Sí|Sí||||||  
|Varios destinos de predicción para Bayes naive, red neuronal y regresión logística|Sí|Sí||||||  
  
##  <a name="Reporting"></a> Reporting Services  
  
###  <a name="Reporting_features"></a>Reporting Services características  
  
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
  
 <sup>1</sup> Para obtener más información sobre los orígenes de datos admitidos en [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)], vea [orígenes de datos &#40;compatibles&#41;con Reporting Services SSRS](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
 <sup>2</sup> Requiere [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en modo de SharePoint. Para obtener más información, vea [Reporting Services la instalación &#40;del modo de sharepoint de&#41;SharePoint 2010 y SharePoint 2013](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
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
  
##  <a name="BIClients"></a> Business Intelligence Clients  
 Las siguientes aplicaciones cliente de software están disponibles en el centro de descargas de Microsoft y se proporcionan para ayudarle a crear documentos de Business Intelligence que se ejecutan en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Si hospeda estos documentos en un entorno de servidor, utilice una edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] compatible con ese tipo de documento. En la siguiente tabla se indica qué edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene las características de servidor necesarias para hospedar los documentos creados en estas aplicaciones cliente.  
  
|Nombre de la característica|Enterprise|Business Intelligence|Estándar|Web|Express con Advanced Services|Express con herramientas|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]|Sí|Sí|Sí|||||  
|Complementos de minería de datos para Excel y Visio 2010|Sí|Sí|Sí|||||  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010|Sí|Sí||||||  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]|Sí|Sí||||||  
  
> [!NOTE]
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] es un complemento de Excel y no depende de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Sin embargo se requiere [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] para el uso compartido y la colaboración con los libros de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] de SharePoint y esta función está disponible como parte de las ediciones Enterprise y Business Intelligence de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
> 2.  En la tabla anterior se identifican las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] necesarias para habilitar estas herramientas de cliente. No obstante, estas características pueden acceder a los datos hospedados en cualquier edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
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
 [Especificaciones del producto para SQL Server 2014](../../2014/getting-started/sql-server-2014-product-specifications.md)   
 [Instalación de SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Inicio rápido de instalación de SQL Server 2014](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
