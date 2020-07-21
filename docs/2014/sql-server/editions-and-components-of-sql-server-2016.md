---
title: Ediciones y componentes de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- 32-bit vs. 64-bit editions [SQL Server]
- default components
- Workgroup Edition [SQL Server]
- Internet servers [SQL Server]
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- client/server applications [SQL Server]
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- 64-bit edition [SQL Server]
- IIS [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
ms.assetid: e5186f02-dd91-47d0-8fa4-de3f41c76903
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8c72e46f95ec756faa9e103bbb23c4dadca5be36
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065473"
---
# <a name="editions-and-components-of-sql-server-2014"></a>Ediciones y componentes de SQL Server 2014
  Los requisitos de instalación varían según las necesidades de las aplicaciones. Las distintas ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] han sido diseñadas para satisfacer los requisitos de rendimiento, tiempo de ejecución y precio propios de cada organización y cada persona. Los componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que instale también dependen de sus necesidades concretas. Las secciones siguientes le servirán de ayuda para elegir la mejor opción entre las ediciones y los componentes disponibles en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="principal-editions-of-sscurrent"></a>Ediciones principales de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 En la tabla siguiente se describen las principales ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener más información, vea [Features Supported by the Editions of SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
|Edición de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Definición|  
|---------------------------------------|----------------|  
|Enterprise (64 bits y 32 bits)|La mejor oferta, [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise Edition proporciona funciones de centro de datos de tecnología avanzada completas con un rendimiento ultrarápido, virtualización ilimitada e inteligencia empresarial integral, lo que habilita los mayores niveles de servicio para las cargas de trabajo de gran importancia y el acceso del usuario final a información sobre los datos.|  
|Business Intelligence (64 bits y 32 bits)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Business Intelligence Edition ofrece una plataforma completa que capacita a las organizaciones para crear e implementar soluciones de BI seguras, escalables y fáciles de administrar. Ofrece una funcionalidad emocionante, como la exploración y visualización de los datos basados en el explorador. potentes capacidades de mashup de datos y administración de integraciones mejorada.|  
|Standard (64 bits y 32 bits)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Standard Edition proporciona administración básica de datos y base de datos de inteligencia empresarial para que los departamentos y pequeñas organizaciones ejecuten sus aplicaciones y admite las herramientas de desarrollo comunes, tanto locales como en la nube, que habilitan la administración eficaz de bases de datos con recursos de TI mínimos.|  
  
## <a name="specialized-editions-of-sscurrent"></a>Ediciones especializadas de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Las ediciones especializadas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] están destinadas a las cargas de trabajo empresariales. En la tabla siguiente se describen las ediciones especializadas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|Edición de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Description|  
|---------------------------------------|-----------------|  
|Web (64 bits y 32 bits)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Web Edition es una opción con un costo total de propiedad bajo para los hosts de Web y los VAP de Web que proporciona capacidades asequibles de administración y escalabilidad para propiedades web, tanto de pequeña como de gran escala.|  
  
## <a name="breadth-editions-of-sscurrent"></a>Ediciones de amplio uso de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Las ediciones de amplio uso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] están diseñadas para escenarios de clientes concretos y se proporcionan de forma GRATUITA o por un costo nominal. En la tabla siguiente se describen las ediciones de amplio uso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|Edición de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Description|  
|---------------------------------------|-----------------|  
|Developer (64 bits y 32 bits)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Developer Edition permite a los desarrolladores compilar cualquier tipo de aplicación en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Incluye toda la funcionalidad de la edición Enterprise, pero tiene licencias para usarse como sistema de prueba y desarrollo, no como un servidor de producción. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer es una opción ideal para las personas que compilan y prueban aplicaciones.|  
|Ediciones Express (64 bits y 32 bits)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Express Edition es una base de datos gratuita para principiantes y es ideal para aprender a compilar pequeñas aplicaciones de servidor y de escritorio orientadas a datos. Es la mejor opción para los fabricantes de software independientes, los desarrolladores y los aficionados que compilan aplicaciones cliente. Si necesita características de base de datos más avanzadas, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express se puede actualizar sin problemas a otras versiones superiores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Express LocalDB de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] es una versión ligera de Express que tiene todas sus características de capacidad de programación, pero se ejecuta en modo usuario y tiene una instalación rápida sin configuración y una lista reducida de requisitos previos.|  
  
## <a name="using-ssnoversion-with-an-internet-server"></a>Usar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con un servidor de Internet  
 En un servidor de Internet, como el servidor en el que se ejecuta Internet Information Services (IIS), se instalan normalmente las herramientas de cliente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Las herramientas de cliente incluyen los componentes de conectividad del cliente utilizados por una aplicación que se conecta a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Aunque puede instalar una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un equipo en el que se ejecute IIS, esto suele hacerse únicamente para sitios web pequeños que tienen un único equipo servidor. La mayoría de los sitios web tienen los sistemas IIS de capa intermedia en un servidor o un clúster de servidores, y las bases de datos en un servidor o federación de servidores independientes.  
  
## <a name="using-ssnoversion-with-clientserver-applications"></a>Usar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con aplicaciones cliente/servidor  
 Puede instalar solo los componentes de cliente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un equipo en el que se ejecuten aplicaciones cliente/servidor conectadas directamente a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Una instalación de componentes de cliente también es una buena opción si administra una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un servidor de bases de datos, o si tiene pensado desarrollar aplicaciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 La opción de herramientas cliente instala las características siguientes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] : componentes de compatibilidad con versiones anteriores, herramientas de datos de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], componentes de conectividad, herramientas de administración, kit de desarrollo de software y componentes de los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para obtener más información, consulte Instalación [de SQL Server 2014 desde el Asistente para la instalación &#40;&#41;de instalación ](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
## <a name="deciding-among-ssnoversion-components"></a>Decidir entre componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 Use la página Selección de características del Asistente para la instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para seleccionar los componentes que va a incluir en la instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. De forma predeterminada, ninguna de las características del árbol están seleccionadas.  
  
 Use la información de las tablas siguientes para determinar el conjunto de características que mejor satisface sus necesidades.  
  
|Componentes de servidor|Descripción|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]incluye el [!INCLUDE[ssDE](../includes/ssde-md.md)] , el servicio principal para almacenar, procesar y proteger datos, replicación, búsqueda de texto completo, herramientas para administrar datos XML y relacionales, y el [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] servidor de (DQS).|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] incluye las herramientas para crear y administrar aplicaciones de procesamiento analítico en línea (OLAP) y de minería de datos.|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] incluye componentes de servidor y de cliente para crear, administrar e implementar informes tabulares, matriciales, gráficos y de forma libre. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] es también una plataforma extensible que se puede usar para desarrollar aplicaciones de informes.|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] es un conjunto de herramientas gráficas y objetos programables para mover, copiar y transformar datos. También incluye el componente de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) para [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) es la solución de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para la administración de datos maestros. MDS se pueden configurar para administrar cualquier dominio (productos, clientes, cuentas) e incluye jerarquías, seguridad específica, transacciones, creación de versiones de datos y reglas de negocios, así como un [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] que se puede usar para administrar datos.|  
  
|Herramientas de administración|Description|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] es un entorno integrado para obtener acceso a los componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]y configurarlos, administrarlos y desarrollarlos. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] permite a los desarrolladores de software y a los administradores de diversos grados de conocimientos utilizar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Administrador de configuración|El Administrador de configuración de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporciona administración de configuración básica para los servicios, protocolos de servidor, protocolos de cliente y alias de cliente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] proporciona una interfaz gráfica de usuario para supervisar una instancia del [!INCLUDE[ssDE](../includes/ssde-md.md)] o de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|  
|Asistente para la optimización de[!INCLUDE[ssDE](../includes/ssde-md.md)]|El Asistente para la optimización de[!INCLUDE[ssDE](../includes/ssde-md.md)] crea conjuntos óptimos de índices, vistas indizadas y particiones.|  
|Cliente de calidad de datos|Proporciona una interfaz gráfica de usuario muy simple y intuitiva para conectarse al servidor de DQS y realizar operaciones de limpieza de datos. También permite supervisar de forma centralizada diversas actividades realizadas durante la operación de limpieza de datos.|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] proporciona un IDE para compilar soluciones para los componentes de Business Intelligence: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]y [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].<br /><br /> (Anteriormente denominado Business Intelligence Development Studio).<br /><br /> [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] SSDT también incluye "Proyectos de base de datos", que proporcionan un entorno integrado para que los desarrolladores de software de bases de datos realicen todo el trabajo de diseño de base de datos para cualquier plataforma de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (tanto interna como externa) en Visual Studio. Los desarrolladores de software de base de datos pueden usar el Explorador de servidores mejorado en Visual Studio para crear o modificar objetos de base de datos y datos fácilmente, o bien para ejecutar consultas.|  
|Componentes de conectividad|Instala componentes para la comunicación entre clientes y servidores, y bibliotecas de red para DB-Library, ODBC y OLE DB.|  
  
|Documentación|Description|  
|-------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Libros en pantalla|Documentación principal para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte también  
 [Planeación de una instalación de SQL Server](install/planning-a-sql-server-installation.md)   
 [Instale SQL Server 2014 desde el Asistente para la instalación &#40;el programa de instalación&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
  
