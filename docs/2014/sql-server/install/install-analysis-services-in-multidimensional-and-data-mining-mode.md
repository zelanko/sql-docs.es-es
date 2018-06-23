---
title: Instalar Analysis Services en multidimensionales y modelo de minería de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing Analysis Services, about installing Analysis Services
- installing Analysis Services
- SSAS, installing
- Analysis Services, installing
- SQL Server Analysis Services, installing
ms.assetid: 8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60
caps.latest.revision: 47
author: HeidiSteen
ms.author: heidist
manager: jhubbard
ms.openlocfilehash: 1a35dae4817d38ea3485b8b34a493314302bdfa0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201538"
---
# <a name="install-analysis-services-in-multidimensional-and-data-mining-mode"></a>Instalar Analysis Services en el modo de minería de datos y multidimensional
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona funciones de procesamiento analítico en línea (OLAP) y minería de datos para aplicaciones de Business Intelligence. En esta versión, compatibilidad con bases de datos OLAP y modelos de minería de datos está disponible cuando se instala [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en *modo Multidimensional*. El modo multidimensional es uno de los tres modos de servidor en los que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se ejecuta. Este es el modo predeterminado. Si instala [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con los valores predeterminados, obtendrá una instancia que ejecuta bases de datos multidimensionales y modelos de minería de datos.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es una característica de varias instancias, lo que significa que puede instalar más de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en un único equipo o ejecutar una nueva instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en paralelo a una versión anterior. El modo de servidor es específico de una instancia. El uso de otros modos requiere que instale instancias adicionales del servidor.  
  
 Puede instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo o con otros componentes. Si instala solo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], las siguientes características se instalan al seleccionar **Analysis Services** en la página Selección de características de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Asistente para la instalación:  
  
-   Servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para ejecutar modelos de minería de datos y bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   Proveedores de datos utilizados para el acceso a datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a las bases de datos de origen  
  
-   Administrador de configuración de SQL Server  
  
## <a name="choosing-additional-features"></a>Elegir características adicionales  
 OLAP de Analysis Services y las soluciones de almacenamiento de datos requerirán la instalación de componentes adicionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para permitir el desarrollo, la implementación y la administración de bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Las siguientes características adicionales son opciones para muchos escenarios de usuario habituales:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] se usa para crear y ver estructuras de datos y modelos de minería de datos de Analysis Services.  
  
-   Componentes de conectividad de herramientas de cliente, se utiliza para la comunicación entre clientes y servidores, incluidas las bibliotecas de red para DB-Library, ODBC y OLE DB.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], un conjunto de objetos gráficos y programables para mover, copiar y transformar datos.  
  
-   Herramientas de administración, incluido el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] y el Monitor de replicación.  
  
## <a name="installation-tasks"></a>Tareas de instalación  
 Entre las tareas de instalación se incluyen las siguientes:  
  
|Vínculos|Tareas|  
|-----------|-----------|  
|[Requisitos de hardware y Software para instalar SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md) y [configurar los permisos y cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).|Antes de ejecutar el programa de instalación, comprobar los requisitos previos para instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y determinar qué cuenta utilizará para aprovisionar el servidor.|  
|[Instalar SQL Server 2014 desde el Asistente para la instalación &#40;el programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).|Ejecutar el programa de instalación de SQL Server para instalar el software.|  
|[Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Una vez finalizada la instalación, debe configurar el firewall para permitir conexiones remotas al servidor.|  
|[Cómo autorizar el acceso a objetos y operaciones &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)|Los usuarios que acceden a las bases de datos de Analysis Services deben tener permiso de lectura en al menos una base de datos del servidor.|  
  
## <a name="related-content"></a>Contenido relacionado  
 En los siguientes temas se puede encontrar contenido adicional sobre la instalación:  
  
 [Instalar Analysis Services en modo Tabular](../../analysis-services/instances/install-windows/install-analysis-services.md)  
  
 [PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
 [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
 [Complementos de minería de datos de SQL Server](http://go.microsoft.com/fwlink/?LinkId=197091)  
  
 De forma predeterminada, las bases de datos de ejemplo y el código muestra, así como los complementos de aplicaciones cliente no se instalan como parte del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar las bases de datos y el código de ejemplo, vea el [sitio web de CodePlex](http://go.microsoft.com/fwlink/?LinkId=87843).  
  
## <a name="see-also"></a>Vea también  
 [Características compatibles con las ediciones de SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473)   
 [Idiomas e intercalaciones &#40;Analysis Services&#41;](../../../2014/analysis-services/languages-and-collations-analysis-services.md)   
 [Actualizar Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
  
  