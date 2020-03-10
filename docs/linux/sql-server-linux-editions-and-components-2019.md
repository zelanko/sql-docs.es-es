---
title: Ediciones y características admitidas de SQL Server 2019 en Linux
ms.date: 01/08/2020
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- default components
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
author: VanMSFT
ms.author: vanto
ms.reviewer: mikeray
ms.openlocfilehash: 7327d63e9c22ab1020c885e9b372c444c485de8d
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2020
ms.locfileid: "78340497"
---
# <a name="editions-and-supported-features-of-sql-server-2019-on-linux"></a>Ediciones y características admitidas de SQL Server 2019 en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se proporcionan detalles de las características admitidas en las diversas ediciones de SQL Server 2019 en Linux. Para conocer las ediciones y las características admitidas de SQL Server en Windows, vea [SQL Server 2019 en Windows](../sql-server/editions-and-components-of-sql-server-version-15.md).  
  
Los requisitos de instalación varían según las necesidades de las aplicaciones. Las distintas ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] han sido diseñadas para satisfacer los requisitos de rendimiento, tiempo de ejecución y precio propios de cada organización y cada persona. Los componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que instale también dependen de sus necesidades concretas. Las secciones siguientes le servirán de ayuda para elegir la mejor opción entre las ediciones y los componentes disponibles en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  

Para leer las notas de la versión más reciente e información sobre las novedades, vea lo siguiente:
- [Notas de la versión de SQL Server 2019 en Linux](sql-server-linux-release-notes-2019.md)
- [Novedades de SQL Server 2019 en Linux](sql-server-linux-whats-new-2019.md)

Para obtener una lista de las características de SQL Server no disponibles en Linux, vea [Características y servicios no admitidos](#Unsupported).

### <a name="try-sql-server"></a>Pruebe SQL Server.    
    
[Descarga de SQL Server 2019](https://www.microsoft.com/sql-server/sql-server-2019)

## <a name="ssnoversion-editions"></a>Ediciones de[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)]  
 En la siguiente tabla se describen las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 
  
|Edición de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Definición|  
|---------------------------------------|----------------|  
|Enterprise|La oferta premium, [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise Edition ofrece completas capacidades de centro de datos de tecnología avanzada con un rendimiento ultrarrápido que permiten altos niveles de servicio para cargas de trabajo críticas.|  
|Estándar|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard Edition proporciona administración básica de datos para que los departamentos y las pequeñas organizaciones ejecuten sus aplicaciones y admite herramientas de desarrollo comunes, tanto locales como en la nube, que habilitan la administración eficaz de bases de datos con recursos de TI mínimos.|  
|Web|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition es una opción con un costo total de propiedad bajo para los hosts de Web y los VAP de Web que proporciona capacidades asequibles de administración y escalabilidad para propiedades web, tanto de pequeña como de gran escala.|  
|Desarrollador|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer Edition permite a los desarrolladores compilar cualquier tipo de aplicación en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Incluye toda la funcionalidad de la edición Enterprise, pero tiene licencias para usarse como sistema de prueba y desarrollo, no como un servidor de producción. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer es una opción ideal para las personas que compilan y prueban aplicaciones.|  
|Express edition|Express Edition es una base de datos gratuita para principiantes y es ideal para aprender a compilar pequeñas aplicaciones de servidor y de escritorio orientadas a datos. Es la mejor opción para los fabricantes de software independientes, los desarrolladores y los aficionados que compilan aplicaciones cliente. Si necesita características de base de datos más avanzadas, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express se puede actualizar sin problemas a otras versiones superiores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
## <a name="using-ssnoversion-with-clientserver-applications"></a>Uso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con aplicaciones cliente/servidor  

Puede instalar solo los componentes de cliente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un equipo en el que se ejecuten aplicaciones cliente/servidor conectadas directamente a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Una instalación de componentes de cliente también es una buena opción si administra una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un servidor de bases de datos, o si tiene pensado desarrollar aplicaciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="ssnoversion-components"></a>Componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  

SQL Server 2019 en Linux es compatible con el motor de base de datos de SQL Server. En la tabla siguiente se indican las características del motor de base de datos.   
  
|Componentes de servidor|Descripción|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] incluye el [!INCLUDE[ssDE](../includes/ssde-md.md)], el servicio principal para almacenar, procesar y proteger datos; también incluye replicación, búsqueda de texto completo, herramientas para administrar datos XML y relacionales e integración analítica en base de datos.|  

**Ediciones Developer, Enterprise Core y Evaluation**  
Para conocer las características admitidas en las ediciones Developer, Enterprise Core y Evaluation, vea las características indicadas para SQL Server Enterprise Edition en las tablas siguientes.

La edición Developer sigue siendo compatible con solo un cliente de [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md). 
  
##  <a name="Cross-BoxScaleLimits"></a> Límites de escala  
  
|Característica|Enterprise|Estándar|Web|Express| 
|-------------|----------------|--------------|---------|------------------------|
|Capacidad máxima de cálculo que usa una sola instancia: [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Sistema operativo máximo|Limitada a menos de 4 sockets o 24 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos| 
|Capacidad máxima de cálculo que usa una sola instancia: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Sistema operativo máximo|Limitada a menos de 4 sockets o 24 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos|
|Memoria máxima para el grupo de búferes por cada instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Sistema operativo máximo|128 GB|64 GB|1410 MB|
|Cantidad máxima de memoria para la caché de segmento del almacén de columnas por cada instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memoria ilimitada| 32 GB| 16 GB| 352 MB|  
|Tamaño máximo de datos optimizados para memoria por base de datos en [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memoria ilimitada| 32 GB| 16 GB| 352 MB|
|Tamaño máximo de la base de datos relacional|524 PB|524 PB|524 PB|10 GB|  
  
<sup>1</sup> La licencia basada en Enterprise Edition con licencia de servidor y acceso de cliente (CAL) (no disponible para nuevos contratos) está limitada a un máximo de 20 núcleos por instancia de SQL Server. No hay ningún límite en el modelo de licencias de servidor basado en núcleos. Para obtener más información, vea [Límites de la capacidad de cálculo de cada edición de SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
 
##  <a name="RDBMSHA"></a> Alta disponibilidad de RDBMS  
  
|Característica|Enterprise|Estándar|Web|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|Trasvase de registros|Sí|Sí|Sí|Sin|  
|Compresión de copia de seguridad|Sí|Sí|Sin|Sin| 
|Instantáneas de base de datos|Sí|Sin|Sin|Sin|
|Instancia de clúster de conmutación por error AlwaysOn<sup>1</sup>|Sí|Sí|Sin|Sin| 
|Grupos de disponibilidad AlwaysOn<sup>2</sup>|Sí|Sin|Sin|Sin|
|Grupos de disponibilidad básica<sup>3</sup>|Sin|Sí|Sin|Sin|
|Grupo de disponibilidad de confirmación de réplica mínima|Sí|Sí|Sin|Sin|
|Grupo de disponibilidad sin clúster|Sí|Sí|Sin|Sin|
|Restauración de archivos y páginas en línea|Sí|Sin|Sin|Sin|
|Índices en línea|Sí|Sin|Sin|Sin|
|Recompilaciones de índices en línea reanudables|Sí|Sin|Sin|Sin|
|Cambio de esquema en línea|Sí|Sin|Sin|Sin|
|Recuperación rápida|Sí|Sin|Sin|Sin|
|Copias de seguridad reflejadas|Sí|Sin|Sin|Sin|
|Agregar memoria y CPU sin interrupción|Sí|Sin|Sin|Sin|
|Copia de seguridad cifrada|Sí|Sí|Sin|Sin|
|Copia de seguridad híbrida en Azure (copia de seguridad en dirección URL)|Sí|Sí|Sin|Sin|
  
<sup>1</sup> En Enterprise Edition, el número de nodos es el máximo del sistema operativo. En Standard Edition hay compatibilidad con dos nodos. 

<sup>2</sup> En Enterprise Edition, proporciona compatibilidad con hasta 8 réplicas secundarias, incluidas 2 réplicas secundarias sincrónicas. 

<sup>3</sup> Standard Edition admite grupos de disponibilidad básica. Un grupo de disponibilidad básica admite dos réplicas, con una base de datos. Para más información sobre los grupos de disponibilidad básica, vea [Grupos de disponibilidad básica](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).    

##  <a name="RDBMSSP"></a> Escalabilidad y rendimiento de RDBMS  
  
|Característica|Enterprise|Estándar|Web|Express|  
|-------------|----------------|--------------|---------|------------------------| 
|Almacén de columnas <sup>1</sup>|Sí|Sí|Sí|Sí|  
|Archivos binarios de objetos de gran tamaño en índices de almacén de columnas en clúster|Sí|Sí|Sí|Sí|  
|Recompilación de índices de almacén de columnas no en clúster en línea|Sí|Sin|Sin|Sin|
|OLTP en memoria <sup>1</sup>|Sí|Sí|Sí|Sí|
|Memoria principal persistente|Sí|Sí|Sí|Sí|
|Particiones de tabla e índice|Sí|Sí|Sí|Sí|  
|Compresión de datos|Sí|Sí|Sí|Sí|
|regulador de recursos|Sí|Sin|Sin|Sin|  
|Paralelismo de tabla con particiones|Sí|Sin|Sin|Sin|
|Asignación de memoria de página grande habilitada para NUMA y matriz de búferes|Sí|Sin|Sin|Sin|
|Regulación de recursos de E/S|Sí|Sin|Sin|Sin|  
|Perdurabilidad diferida|Sí|Sí|Sí|Sí|
|Ajuste automático|Sí|Sin|Sin|Sin|
|Combinaciones adaptables de modo de proceso por lotes|Sí|Sin|Sin|Sin|
|Comentarios de concesión de memoria de modo de proceso por lotes|Sí|Sin|Sin|Sin|
|Ejecución intercalada de funciones con valores de tabla de múltiples instrucciones|Sí|Sí|Sí|Sí|
|Mejoras de inserción masiva|Sí|Sí|Sí|Sí|


<sup>1</sup> El tamaño de los datos de OLTP en memoria y la memoria caché del segmento del almacén de columnas se limitan a la cantidad de memoria especificada por edición en la sección Límites de escala. Los grados de paralelismo máximos están limitados. El grado paralelismo (DOP) de la compilación de un índice se limita a 2 DOP para Standard Edition y 1 DOP para las ediciones Web y Express. Se refiere a los índices de almacén de columnas que se crean en tablas basadas en disco y en tablas optimizadas para memoria.

##  <a name="RDBMSS"></a> Seguridad de RDBMS  
  
|Característica|Enterprise|Estándar|Web|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|Seguridad de nivel de fila|Sí|Sí|Sí|Sí|  
|Always Encrypted|Sí|Sí|Sí|Sí| 
|Enmascaramiento de datos dinámicos|Sí|Sí|Sí|Sí|   
|Auditoría básica|Sí|Sí|Sí|Sí| 
|Auditoría específica|Sí|Sí|Sí|Sí| 
|Cifrado de base de datos transparente|Sí|Sin|Sin|Sin|   
|Roles definidos por el usuario|Sí|Sí|Sí|Sí| 
|Bases de datos independientes|Sí|Sí|Sí|Sí| 
|Cifrado para copias de seguridad|Sí|Sí|Sin|Sin|  

##  <a name="RDBMSM"></a> Capacidad de administración de RDBMS  
  
|Característica|Enterprise|Estándar|Web|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|Conexión de administración dedicada|Sí|Sí|Sí|Sí, con marca de seguimiento|   
|Compatibilidad con PowerShell scripting|Sí|Sí|Sí|Sí| 
|Compatibilidad con las operaciones de componentes de aplicación de capa de datos: extracción, implementación, actualización, eliminación|Sí|Sí|Sí|Sí| 
|Automatización de directivas (comprobar en la programación y cambio)|Sí|Sí|Sí|Sin|  
|Recopilador de datos de rendimiento|Sí|Sí|Sí|Sin|
|Informes de rendimiento estándar|Sí|Sí|Sí|Sin|
|Guías del plan y congelación del plan para las guías del plan|Sí|Sí|Sí|Sin| 
|Consulta directa de vistas indexadas (mediante la sugerencia NOEXPAND)|Sí|Sí|Sí|Sí| 
|Mantenimiento automático de vistas indexadas|Sí|Sí|Sí|Sin|
|Vistas distribuidas con particiones|Sí|Sin|Sin|Sin| 
|Operaciones indizadas en paralelo|Sí|Sin|Sin|Sin|  
|Uso automático de vistas indexadas por el optimizador de consultas|Sí|Sin|Sin|Sin| 
|Comprobación de coherencia en paralelo|Sí|Sin|Sin|Sin| 
|Punto de control de la utilidad de SQL Server|Sí|Sin|Sin|Sin|    

##  <a name="Programmability"></a> Programmability  
  
|Característica|Enterprise|Estándar|Web|Express 
|-------------|----------------|--------------|---------|------------------------|  
|JSON|Sí|Sí|Sí|Sí|   
|Almacén de consultas|Sí|Sí|Sí|Sí|   
|Temporal|Sí|Sí|Sí|Sí|   
|Compatibilidad con XML nativo|Sí|Sí|Sí|Sí| 
|Índices XML|Sí|Sí|Sí|Sí| 
|Funciones MERGE y UPSERT|Sí|Sí|Sí|Sí|   
|Tipos de datos de fecha y hora|Sí|Sí|Sí|Sí|  
|Compatibilidad para internacionalización|Sí|Sí|Sí|Sí| 
|Búsqueda de texto completo y semántica|Sí|Sí|Sí|Sí|
|Especificación de idioma en la consulta|Sí|Sí|Sí|Sí|
|Service Broker (mensajería)|Sí|Sí|No (solo cliente)|No (solo cliente)|
|Transact-SQL, extremos|Sí|Sí|Sí|Sin|
|Grafo|Sí|Sí|Sí|Sí|  


<sup>1</sup> El escalado horizontal con varios nodos de cálculo exige un nodo principal.

## <a name="IS"></a> Integration Services

Para obtener información sobre las características de Integration Services (SSIS) compatibles con las ediciones de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], vea [Características de Integration Services compatibles con las ediciones de SQL Server](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="SLS"></a> Servicios espaciales y de ubicación  
  
|Nombre de la característica|Enterprise|Estándar|Web|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Índices espaciales|Sí|Sí|Sí|Sí|   
|Tipos de datos planares y geodésicos|Sí|Sí|Sí|Sí| 
|Bibliotecas espaciales avanzadas|Sí|Sí|Sí|Sí|   
|Importación y exportación de formatos de datos espaciales estándar del sector|Sí|Sí|Sí|Sí|   

## <a name="Unsupported"></a> Características y servicios no admitidos

Las siguientes características y servicios no están disponibles para SQL Server 2019 en Linux. La compatibilidad de estas características se incrementará con el tiempo.

| Área | Característica o servicio no admitido |
|-----|-----|
| **Motor de base de datos** | Replicación de mezcla |
| &nbsp; | Stretch DB |
| &nbsp; | Consulta distribuida con conexiones de terceros |
| &nbsp; | Servidores vinculados a orígenes de datos distintos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  |
| &nbsp; | Procedimientos extendidos almacenados del sistema (XP_CMDSHELL, etc.) |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | Ensamblados de CLR con el conjunto de permisos EXTERNAL_ACCESS o UNSAFE |
| &nbsp; | Buffer Pool Extension |
| **Agente SQL Server** |  Subsistemas: CmdExec, PowerShell, Agente de lectura de cola, SSIS, SSAS, SSRS |
| &nbsp; | Alertas |
| &nbsp; | Copia de seguridad administrada |
| **Alta disponibilidad** | Creación de reflejo de la base de datos  |
| **Seguridad** | Administración extensible de claves |
| &nbsp; | Autenticación de AD para servidores vinculados | 
| &nbsp; | Autenticación de AD para grupos de disponibilidad | 
| **Servicios** | SQL Server Browser |
| &nbsp; | SQL Server R Services<sup>1</sup> |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

<sup>1</sup> SQL Server R es compatible con SQL Server, pero SQL Server R Services como paquete independiente no lo es.
  
## <a name="next-steps"></a>Pasos siguientes
 [Características compatibles con las ediciones de SQL Server 2017 en Linux](sql-server-linux-editions-and-components-2017.md)  
 [Ediciones y características admitidas de SQL Server 2019 en Windows](../sql-server/editions-and-components-of-sql-server-version-15.md)  
 [Ediciones y características admitidas de SQL Server 2017 en Windows](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [Ediciones y características admitidas de SQL Server 2016 en Windows](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [Ediciones y características admitidas de SQL Server 2014 en Windows](https://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)  
 [Instalación de SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 [Especificaciones de producto para SQL Server](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)


