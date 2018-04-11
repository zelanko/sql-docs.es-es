---
title: Ediciones y las características admitidas de SQL Server 2017 ~ Linux | Documentos de Microsoft
ms.custom: sql-linux
ms.date: 09/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: sql-linux
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 121
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: da867b1125d4ee444a0e04e34d729484bee43514
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/10/2018
---
# <a name="editions-and-supported-features-of-sql-server-2017-on-linux"></a>Ediciones y las características admitidas de SQL Server 2017 en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artículo proporciona detalles de las características admitidas por las diferentes ediciones de SQL Server 2017 en Linux. Para las ediciones y las características admitidas de SQL Server en Windows, vea [2017 de SQL Server - Windows](../sql-server/editions-and-components-of-sql-server-2017.md).  
  
Los requisitos de instalación varían según las necesidades de las aplicaciones. Las distintas ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] han sido diseñadas para satisfacer los requisitos de rendimiento, tiempo de ejecución y precio propios de cada organización y cada persona. Los componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que instale también dependen de sus necesidades concretas. Las secciones siguientes le servirán de ayuda para elegir la mejor opción entre las ediciones y los componentes disponibles en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  

Para leer las notas de la versión más reciente e información sobre las novedades, vea lo siguiente:
- [Notas de la versión de SQL Server en Linux](sql-server-linux-release-notes.md)
- [Novedades de SQL Server en Linux](sql-server-linux-whats-new.md)

Para obtener una lista de características de SQL Server no está disponibles en Linux, consulte [no admite servicios y características](sql-server-linux-release-notes.md#Unsupported).

### <a name="try-sql-server"></a>Pruebe SQL Server.    
    
[Descargar SQL Server de 2017](http://www.microsoft.com/sql-server/sql-server-2017)

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>Ediciones de [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)]  
 En la siguiente tabla se describen las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 
  
|Edición de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] |Definición|  
|---------------------------------------|----------------|  
|Enterprise|La mejor oferta, [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise edition proporciona capacidades de centro de datos de tecnología avanzada completas con un rendimiento ultrarápido habilitar altos niveles de servicio para las cargas de trabajo críticas.|  
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard edition ofrece administración de datos básicos para departamentos y pequeñas organizaciones ejecuten sus aplicaciones y es compatible con herramientas de desarrollo comunes para local y la nube: permitir una administración eficaz de la base de datos con recursos de TI mínimos.|  
|Web|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition es una opción con un costo total de propiedad bajo para los hosts de Web y los VAP de Web que proporciona capacidades asequibles de administración y escalabilidad para propiedades web, tanto de pequeña como de gran escala.|  
|Desarrollador|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer Edition permite a los desarrolladores compilar cualquier tipo de aplicación en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Incluye toda la funcionalidad de la edición Enterprise, pero tiene licencias para usarse como sistema de prueba y desarrollo, no como un servidor de producción. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer es una opción ideal para las personas que compilan y prueban aplicaciones.|  
|Express edition|Express Edition es una base de datos gratuita para principiantes y es ideal para aprender a compilar pequeñas aplicaciones de servidor y de escritorio orientadas a datos. Es la mejor opción para los fabricantes de software independientes, los desarrolladores y los aficionados que compilan aplicaciones cliente. Si necesita características de base de datos más avanzadas, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express se puede actualizar sin problemas a otras versiones superiores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>Uso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con aplicaciones cliente/servidor  

Puede instalar solo los componentes de cliente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un equipo en el que se ejecuten aplicaciones cliente/servidor conectadas directamente a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Una instalación de componentes de cliente también es una buena opción si administra una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un servidor de bases de datos, o si tiene pensado desarrollar aplicaciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="includessnoversionincludesssnoversion-mdmd-components"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Componentes de  

SQL Server 2017 en Linux es compatible con el motor de base de datos de SQL Server. En la tabla siguiente describe las características en el motor de base de datos.   
  
|Componentes de servidor|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] incluye el [!INCLUDE[ssDE](../includes/ssde-md.md)], el servicio principal para almacenar, procesar y proteger los datos, replicación, búsqueda de texto completo, herramientas para administrar relacionales y datos XML y, en la integración del análisis de base de datos.|  

**Ediciones Developer, Enterprise Core y evaluación**  
Para características compatibles con Developer, Enterprise Core y las ediciones de evaluación, vea las características enumeradas para la edición Enterprise de SQL Server en las tablas siguientes.

La edición Developer sigue siendo compatible con solo un cliente de [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md). 
  
##  <a name="Cross-BoxScaleLimits"></a> Límites de escala  
  
|Característica|Enterprise|Standard|Web|Express| 
|-------------|----------------|--------------|---------|------------------------|
|Capacidad máxima de cálculo que usa una sola instancia: [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Sistema operativo máximo|Limitada a menos de 4 sockets o 24 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos| 
|Capacidad máxima de cálculo que usa una sola instancia: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Sistema operativo máximo|Limitada a menos de 4 sockets o 24 núcleos|Limitada a menos de 4 sockets o 16 núcleos|Limitada a menos de 1 socket o 4 núcleos|
|Memoria máxima para el grupo de búferes por cada instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Sistema operativo máximo|128 GB|64 GB|1410 MB|
|Cantidad máxima de memoria para la caché de segmento del almacén de columnas por cada instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memoria ilimitada| 32 GB| 16 GB| 352 MB|  
|Tamaño máximo de datos optimizados para memoria por base de datos en [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memoria ilimitada| 32 GB| 16 GB| 352 MB|
|Tamaño máximo de la base de datos relacional|524 PB|524 PB|524 PB|10 GB|  
  
<sup>1</sup> Enterprise edition con el servidor y cliente acceso licencia (CAL) en función de licencias (no disponible para nuevos contratos) está limitada a un máximo de 20 núcleos por instancia de SQL Server. No hay ningún límite en el modelo de licencias de servidor basado en núcleos. Para obtener más información, consulte [límites de capacidad de cálculo de cada edición de SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
 
##  <a name="RDBMSHA"></a> Alta disponibilidad de RDBMS  
  
|Característica|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|Trasvase de registros|Sí|Sí|Sí|no|  
|Compresión de copia de seguridad|Sí|Sí|No|no| 
|Instantáneas de base de datos|Sí|No|No|no|
|Siempre en instancia de clúster de conmutación por error<sup>1</sup>|Sí|Sí|No|no| 
|Grupos de disponibilidad AlwaysOn<sup>2</sup>|Sí|No|No|no|
|Grupos de disponibilidad básica <sup>3</sup>|no|Sí|No|no|
|Grupo de disponibilidad de confirmación de réplica mínima|Sí|Sí|No|no|
|Grupo de disponibilidad sin clúster|Sí|Sí|No|no|
|Restauración de archivos y páginas en línea|Sí|No|No|no|
|Índices en línea|Sí|No|No|no|
|Recompilaciones de índices en línea reanudables|Sí|No|No|no|
|Cambio de esquema en línea|Sí|No|No|no|
|Recuperación rápida|Sí|No|No|no|
|Copias de seguridad reflejadas|Sí|No|No|no|
|Agregar memoria y CPU sin interrupción|Sí|No|No|no|
|Copia de seguridad cifrada|Sí|Sí|No|no|
|Copia de seguridad híbrida en Windows Azure (copia de seguridad en dirección URL)|Sí|Sí|No|no|
  
<sup>1</sup> en Enterprise edition, el número de nodos es el máximo del sistema operativo. En Standard Edition hay compatibilidad con dos nodos. 

<sup>2</sup> en Enterprise edition, proporciona compatibilidad para hasta 8 réplicas secundarias - incluidas 2 réplicas secundarias sincrónicas. 

<sup>3</sup> standard edition admite grupos de disponibilidad básica. Un grupo de disponibilidad básica admite dos réplicas, con una base de datos. Para más información sobre los grupos de disponibilidad básica, vea [Grupos de disponibilidad básica](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).    

##  <a name="RDBMSSP"></a> Escalabilidad y rendimiento de RDBMS  
  
|Característica|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------| 
|Almacén de columnas <sup>1</sup>|Sí|Sí|Sí|Sí|  
|Archivos binarios de objetos de gran tamaño en índices de almacén de columnas en clúster|Sí|Sí|Sí|Sí|  
|Recompilación de índices de almacén de columnas no en clúster en línea|Sí|No|No|no|
|OLTP en memoria <sup>1</sup>|Sí|Sí|Sí|Sí|
|Memoria principal persistente|Sí|Sí|Sí|Sí|
|Particiones de tabla e índice|Sí|Sí|Sí|Sí|  
|Compresión de datos|Sí|Sí|Sí|Sí|
|Regulador de recursos|Sí|No|No|no|  
|Paralelismo de tabla con particiones|Sí|No|No|no|
|Asignación de memoria de página grande habilitada para NUMA y matriz de búferes|Sí|No|No|no|
|Regulación de recursos de E/S|Sí|No|No|no|  
|Perdurabilidad diferida|Sí|Sí|Sí|Sí|
|Ajuste automático|Sí|No|No|no|
|Combinaciones adaptables de modo de proceso por lotes|Sí|No|No|no|
|Comentarios de concesión de memoria de modo de proceso por lotes|Sí|No|No|no|
|Ejecución intercalada de funciones con valores de tabla de múltiples instrucciones|Sí|Sí|Sí|Sí|
|Mejoras de inserción masiva|Sí|Sí|Sí|Sí|


<sup>1</sup> El tamaño de los datos de OLTP en memoria y la memoria caché del segmento del almacén de columnas se limitan a la cantidad de memoria especificada por edición en la sección Límites de escala. Los grados de paralelismo máximos están limitados. Los grados de paralelismo (DOP) del proceso para una generación de índice se limita a 2 DOP para la edición Standard y 1 DOP para las ediciones Express y Web. Se refiere a los índices de almacén de columnas que se crean en tablas basadas en disco y en tablas optimizadas para memoria.

##  <a name="RDBMSS"></a> Seguridad de RDBMS  
  
|Característica|Enterprise|Standard|Web|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|Seguridad de nivel de fila|Sí|Sí|Sí|Sí|  
|Always Encrypted|Sí|Sí|Sí|Sí| 
|Enmascaramiento de datos dinámicos|Sí|Sí|Sí|Sí|   
|Auditoría básica|Sí|Sí|Sí|Sí| 
|Auditoría específica|Sí|Sí|Sí|Sí| 
|Cifrado de base de datos transparente|Sí|No|No|no|   
|Roles definidos por el usuario|Sí|Sí|Sí|Sí| 
|Bases de datos independientes|Sí|Sí|Sí|Sí| 
|Cifrado para copias de seguridad|Sí|Sí|No|no|  

##  <a name="RDBMSM"></a> Capacidad de administración de RDBMS  
  
|Característica|Enterprise|Standard|Web|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|Conexión de administración dedicada|Sí|Sí|Sí|Sí, con marca de seguimiento|Sí, con marca de seguimiento|   
|Compatibilidad con PowerShell scripting|Sí|Sí|Sí|Sí| 
|Compatibilidad con las operaciones de componentes de aplicación de capa de datos: extracción, implementación, actualización, eliminación|Sí|Sí|Sí|Sí| 
|Automatización de directivas (comprobar en la programación y cambio)|Sí|Sí|Sí|No|no|   
|Recopilador de datos de rendimiento|Sí|Sí|Sí|No|no| 
|Informes de rendimiento estándar|Sí|Sí|Sí|No|no| 
|Guías del plan y congelación del plan para las guías del plan|Sí|Sí|Sí|No|no|   
|Consulta directa de vistas indexadas (mediante la sugerencia NOEXPAND)|Sí|Sí|Sí|Sí| 
|Mantenimiento automático de vistas indexadas|Sí|Sí|Sí|No|no| 
|Vistas distribuidas con particiones|Sí|No|No|no| 
|Operaciones indizadas en paralelo|Sí|No|No|no|  
|Uso automático de vistas indexadas por el optimizador de consultas|Sí|No|No|no| 
|Comprobación de coherencia en paralelo|Sí|No|No|no| 
|Punto de control de la utilidad de SQL Server|Sí|No|No|no|    

##  <a name="Programmability"></a> Programmability  
  
|Característica|Enterprise|Standard|Web|Express 
|-------------|----------------|--------------|---------|------------------------|  
|JSON|Sí|Sí|Sí|Sí|   
|Almacén de consultas|Sí|Sí|Sí|Sí|   
|Temporal|Sí|Sí|Sí|Sí|   
|Compatibilidad con XML nativo|Sí|Sí|Sí|Sí| 
|Índices XML|Sí|Sí|Sí|Sí| 
|Funciones MERGE y UPSERT|Sí|Sí|Sí|Sí|   
|Tipos de datos de fecha y hora|Sí|Sí|Sí|Sí|  
|Compatibilidad para internacionalización|Sí|Sí|Sí|Sí| 
|Búsqueda de texto completo y semántica|Sí|Sí|Sí|Sí|no| 
|Especificación de idioma en la consulta|Sí|Sí|Sí|Sí|no|   
|Service Broker (mensajería)|Sí|Sí|No (solo cliente)|No (solo cliente)|No (solo cliente)|   
|Transact-SQL, extremos|Sí|Sí|Sí|No|no| 
|Gráfico|Sí|Sí|Sí|Sí|  


<sup>1</sup> El escalado horizontal con varios nodos de cálculo exige un nodo principal.

## <a name="IS"></a> Integration Services

Para obtener información acerca de las características de Integration Services (SSIS) compatibles con las ediciones de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [características de Integration Services compatibles con las ediciones de SQL Server](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="SLS"></a> Servicios espaciales y de ubicación  
  
|Nombre de la característica|Enterprise|Standard|Web|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Índices espaciales|Sí|Sí|Sí|Sí|   
|Tipos de datos planares y geodésicos|Sí|Sí|Sí|Sí| 
|Bibliotecas espaciales avanzadas|Sí|Sí|Sí|Sí|   
|Importación y exportación de formatos de datos espaciales estándar del sector|Sí|Sí|Sí|Sí|   

  
## <a name="next-steps"></a>Pasos siguientes 
 [Ediciones y características admitidas de SQL Server 2017 - Windows](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [Ediciones y las características admitidas de SQL Server 2016 - Windows](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [Ediciones y características admitidas de SQL Server 2014 - Windows](http://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)  
 [Instalación de SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 [Especificaciones de producto para SQL Server](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb) 

  
  
