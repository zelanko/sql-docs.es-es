---
title: Ediciones y características admitidas de SQL Server 2017 ~ Linux | Microsoft Docs
ms.date: 09/14/2017
ms.prod: sql
ms.reviewer: ''
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
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 21e709b20df80fdecc7aff80ff983b0f33bbf101
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713173"
---
# <a name="editions-and-supported-features-of-sql-server-2017-on-linux"></a>Ediciones y características admitidas de SQL Server 2017 en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artículo proporciona detalles de las características admitidas por las distintas ediciones de SQL Server 2017 en Linux. Para las ediciones y características admitidas de SQL Server en Windows, consulte [SQL Server 2017 - Windows](../sql-server/editions-and-components-of-sql-server-2017.md).  
  
Los requisitos de instalación varían según las necesidades de las aplicaciones. Las distintas ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] han sido diseñadas para satisfacer los requisitos de rendimiento, tiempo de ejecución y precio propios de cada organización y cada persona. Los componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que instale también dependen de sus necesidades concretas. Las secciones siguientes le servirán de ayuda para elegir la mejor opción entre las ediciones y los componentes disponibles en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  

Para leer las notas de la versión más reciente e información sobre las novedades, vea lo siguiente:
- [Notas de la versión de SQL Server en Linux](sql-server-linux-release-notes.md)
- [Novedades de SQL Server en Linux](sql-server-linux-whats-new.md)

Para obtener una lista de características de SQL Server no está disponibles en Linux, consulte [servicios y características no admitidas](sql-server-linux-release-notes.md#Unsupported).

### <a name="try-sql-server"></a>Pruebe SQL Server.    
    
[Descargar SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-2017)

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>Ediciones de[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)]  
 En la siguiente tabla se describen las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 
  
|Edición de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Definición|  
|---------------------------------------|----------------|  
|Enterprise|La oferta premium, [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise edition proporciona funcionalidades de centro de datos de tecnología avanzada completas con un rendimiento ultrarrápida con habilitación altos niveles de servicio para cargas de trabajo críticas.|  
|Estándar|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard edition proporciona administración básica de datos para departamentos y pequeñas organizaciones ejecuten sus aplicaciones y es compatible con herramientas de desarrollo comunes para local y en la nube - habilitar la administración de bases de datos eficaz con recursos de TI mínimos.|  
|Web|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition es una opción con un costo total de propiedad bajo para los hosts de Web y los VAP de Web que proporciona capacidades asequibles de administración y escalabilidad para propiedades web, tanto de pequeña como de gran escala.|  
|Desarrollador|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer Edition permite a los desarrolladores compilar cualquier tipo de aplicación en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Incluye toda la funcionalidad de la edición Enterprise, pero tiene licencias para usarse como sistema de prueba y desarrollo, no como un servidor de producción. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer es una opción ideal para las personas que compilan y prueban aplicaciones.|  
|Express edition|Express Edition es una base de datos gratuita para principiantes y es ideal para aprender a compilar pequeñas aplicaciones de servidor y de escritorio orientadas a datos. Es la mejor opción para los fabricantes de software independientes, los desarrolladores y los aficionados que compilan aplicaciones cliente. Si necesita características de base de datos más avanzadas, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express se puede actualizar sin problemas a otras versiones superiores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>Uso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con aplicaciones cliente/servidor  

Puede instalar solo los componentes de cliente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un equipo en el que se ejecuten aplicaciones cliente/servidor conectadas directamente a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Una instalación de componentes de cliente también es una buena opción si administra una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un servidor de bases de datos, o si tiene pensado desarrollar aplicaciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="includessnoversionincludesssnoversion-mdmd-components"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Componentes  

SQL Server 2017 en Linux es compatible con el motor de base de datos de SQL Server. En la tabla siguiente se describe las características en el motor de base de datos.   
  
|Componentes de servidor|Descripción|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] incluye el [!INCLUDE[ssDE](../includes/ssde-md.md)], el servicio principal para almacenar, procesar y proteger datos, replicación, búsqueda de texto completo, herramientas para administrar relacionales y datos XML y, en la integración de análisis de base de datos.|  

**Ediciones Developer, Enterprise Core y evaluación**  
Para las características admitidas por Developer, Enterprise Core y las ediciones de evaluación, consulte las características enumeradas para la edición Enterprise de SQL Server en las tablas siguientes.

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
  
<sup>1</sup> Enterprise edition con el servidor y cliente acceso licencia (CAL) en función de licencias (no disponible para nuevos contratos) está limitada a un máximo de 20 núcleos por instancia de SQL Server. No hay ningún límite en el modelo de licencias de servidor basado en núcleos. Para obtener más información, consulte [límites de capacidad de proceso mediante la edición de SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
 
##  <a name="RDBMSHA"></a> Alta disponibilidad de RDBMS  
  
|Característica|Enterprise|Estándar|Web|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|Trasvase de registros|Sí|Sí|Sí|No|  
|Compresión de copia de seguridad|Sí|Sí|No|Sin| 
|Instantáneas de base de datos|Sí|No|No|No|
|Always On instancia en clúster de conmutación por error<sup>1</sup>|Sí|Sí|Sin|Sin| 
|Grupos de disponibilidad Always On<sup>2</sup>|Sí|No|Sin|Sin|
|Grupos de disponibilidad básica <sup>3</sup>|Sin|Sí|No|Sin|
|Grupo de disponibilidad de confirmación de réplica mínima|Sí|Sí|Sin|Sin|
|Grupo de disponibilidad sin clúster|Sí|Sí|No|Sin|
|Restauración de archivos y páginas en línea|Sí|No|Sin|Sin|
|Índices en línea|Sí|No|Sin|No|
|Recompilaciones de índices en línea reanudables|Sí|Sin|Sin|Sin|
|Cambio de esquema en línea|Sí|Sin|Sin|Sin|
|Recuperación rápida|Sí|Sin|No|Sin|
|Copias de seguridad reflejadas|Sí|Sin|Sin|No|
|Agregar memoria y CPU sin interrupción|Sí|No|Sin|Sin|
|Copia de seguridad cifrada|Sí|Sí|Sin|Sin|
|Copia de seguridad híbrida en Windows Azure (copia de seguridad en dirección URL)|Sí|Sí|No|Sin|
  
<sup>1</sup> en Enterprise edition, el número de nodos es el sistema operativo máximo. En Standard Edition hay compatibilidad con dos nodos. 

<sup>2</sup> en Enterprise edition, proporciona soporte técnico para hasta 8 réplicas secundarias, incluidas 2 réplicas secundarias sincrónicas. 

<sup>3</sup> standard edition admite grupos de disponibilidad básica. Un grupo de disponibilidad básica admite dos réplicas, con una base de datos. Para más información sobre los grupos de disponibilidad básica, vea [Grupos de disponibilidad básica](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).    

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
|Paralelismo de tabla con particiones|Sí|No|No|Sin|
|Asignación de memoria de página grande habilitada para NUMA y matriz de búferes|Sí|Sin|Sin|Sin|
|Regulación de recursos de E/S|Sí|Sin|No|No|  
|Perdurabilidad diferida|Sí|Sí|Sí|Sí|
|Ajuste automático|Sí|Sin|Sin|Sin|
|Combinaciones adaptables de modo de proceso por lotes|Sí|Sin|No|Sin|
|Comentarios de concesión de memoria de modo de proceso por lotes|Sí|Sin|No|Sin|
|Ejecución intercalada de funciones con valores de tabla de múltiples instrucciones|Sí|Sí|Sí|Sí|
|Mejoras de inserción masiva|Sí|Sí|Sí|Sí|


<sup>1</sup> El tamaño de los datos de OLTP en memoria y la memoria caché del segmento del almacén de columnas se limitan a la cantidad de memoria especificada por edición en la sección Límites de escala. Los grados de paralelismo máximos están limitados. Los grados de paralelismo (DOP) para generar un índice se limita a 2 DOP para Standard edition y 1 DOP para las ediciones Web y Express. Se refiere a los índices de almacén de columnas que se crean en tablas basadas en disco y en tablas optimizadas para memoria.

##  <a name="RDBMSS"></a> Seguridad de RDBMS  
  
|Característica|Enterprise|Estándar|Web|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|Seguridad de nivel de fila|Sí|Sí|Sí|Sí|  
|Always Encrypted|Sí|Sí|Sí|Sí| 
|Enmascaramiento de datos dinámicos|Sí|Sí|Sí|Sí|   
|Auditoría básica|Sí|Sí|Sí|Sí| 
|Auditoría específica|Sí|Sí|Sí|Sí| 
|Cifrado de base de datos transparente|Sí|Sin|No|Sin|   
|Roles definidos por el usuario|Sí|Sí|Sí|Sí| 
|Bases de datos independientes|Sí|Sí|Sí|Sí| 
|Cifrado para copias de seguridad|Sí|Sí|No|Sin|  

##  <a name="RDBMSM"></a> Capacidad de administración de RDBMS  
  
|Característica|Enterprise|Estándar|Web|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|Conexión de administración dedicada|Sí|Sí|Sí|Sí, con marca de seguimiento|Sí, con marca de seguimiento|   
|Compatibilidad con PowerShell scripting|Sí|Sí|Sí|Sí| 
|Compatibilidad con las operaciones de componentes de aplicación de capa de datos: extracción, implementación, actualización, eliminación|Sí|Sí|Sí|Sí| 
|Automatización de directivas (comprobar en la programación y cambio)|Sí|Sí|Sí|Sin|No|   
|Recopilador de datos de rendimiento|Sí|Sí|Sí|No|No| 
|Informes de rendimiento estándar|Sí|Sí|Sí|No|No| 
|Guías del plan y congelación del plan para las guías del plan|Sí|Sí|Sí|No|No|   
|Consulta directa de vistas indexadas (mediante la sugerencia NOEXPAND)|Sí|Sí|Sí|Sí| 
|Mantenimiento automático de vistas indexadas|Sí|Sí|Sí|No|Sin| 
|Vistas distribuidas con particiones|Sí|No|Sin|No| 
|Operaciones indizadas en paralelo|Sí|No|No|Sin|  
|Uso automático de vistas indexadas por el optimizador de consultas|Sí|Sin|Sin|Sin| 
|Comprobación de coherencia en paralelo|Sí|Sin|Sin|No| 
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
|Búsqueda de texto completo y semántica|Sí|Sí|Sí|Sí|No| 
|Especificación de idioma en la consulta|Sí|Sí|Sí|Sí|No|   
|Service Broker (mensajería)|Sí|Sí|No (solo cliente)|No (solo cliente)|No (solo cliente)|   
|Transact-SQL, extremos|Sí|Sí|Sí|Sin|Sin| 
|Gráfico|Sí|Sí|Sí|Sí|  


<sup>1</sup> El escalado horizontal con varios nodos de cálculo exige un nodo principal.

## <a name="IS"></a> Integration Services

Para obtener información sobre las características de Integration Services (SSIS) compatibles con las ediciones de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [características de Integration Services compatibles con las ediciones de SQL Server](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="SLS"></a> Servicios espaciales y de ubicación  
  
|Nombre de la característica|Enterprise|Estándar|Web|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Índices espaciales|Sí|Sí|Sí|Sí|   
|Tipos de datos planares y geodésicos|Sí|Sí|Sí|Sí| 
|Bibliotecas espaciales avanzadas|Sí|Sí|Sí|Sí|   
|Importación y exportación de formatos de datos espaciales estándar del sector|Sí|Sí|Sí|Sí|   

  
## <a name="next-steps"></a>Pasos siguientes 
 [Ediciones y características admitidas de SQL Server 2017 - Windows](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [Ediciones y características admitidas de SQL Server 2016 - Windows](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [Ediciones y características admitidas de SQL Server 2014 - Windows](https://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)  
 [Instalación de SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 [Especificaciones de producto para SQL Server](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb) 

  
  
