---
title: Crear multidimensionales modelos utilizando SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, environments
- Analysis Services, development
- SQL Server Analysis Services, environments
- projects [Analysis Services]
- solutions [Analysis Services]
ms.assetid: 132ed779-3ec8-4734-9698-802116d1b017
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 41ddab5d08673ea71cefb7cf44169e8da6777292
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368797"
---
# <a name="creating-multidimensional-models-using-sql-server-data-tools-ssdt"></a>Crear modelos multidimensionales utilizando las herramientas de datos de SQL Server (SSDT)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece dos entornos diferentes para generar, implementar y administrar soluciones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] : [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Ambos entornos implementan un sistema de proyectos. Para obtener más información acerca de los proyectos de Visual Studio, vea [Proyectos como contenedores](https://go.microsoft.com/fwlink/?LinkId=63960) en MSDN Library.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] es un entorno de desarrollo basado en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2010 que se emplea para crear y modificar soluciones de Business Intelligence. Con [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]se pueden crear proyectos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contienen definiciones de objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (cubos, dimensiones, etc.) que se almacenan en archivos XML que contienen elementos ASSL ( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language). Estos proyectos se incluyen en soluciones que a su vez pueden contener proyectos de otros componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluidos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], puede desarrollar proyectos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como parte de una solución independiente de cualquier instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] concreta. Puede implementar los objetos en una instancia de un servidor de pruebas para realizar comprobaciones durante el desarrollo y, a continuación, utilizar el mismo proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para implementar los objetos en instancias de uno o más servidores de ensayo o de producción. Los proyectos y elementos de una solución que incluya [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se pueden integrar con control de código fuente, como [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual SourceSafe. Para más información sobre cómo crear un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Create an Analysis Services Project &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md). También puede usar [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para conectar directamente con una instancia existente de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a fin de crear y modificar objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , sin necesidad de trabajar con un proyecto ni de almacenar definiciones de objeto en archivos XML. Para más información, vea [Bases de datos de modelos multidimensionales &#40;SSAS&#41;](multidimensional-model-databases-ssas.md)y [Conectarse en el modo con conexión a una base de datos de Analysis Services](connect-in-online-mode-to-an-analysis-services-database.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] es un entorno de administración que se usa principalmente para administrar instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede administrar objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (realizar copias de seguridad, procesar, etc.), así como crear objetos directamente en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente con scripts XMLA. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] proporciona un proyecto de scripts de Analysis Server en el que se pueden desarrollar y guardar los scripts escritos en Expresiones multidimensionales (MDX), Extensiones de minería de Datos (DMX) y XML for Analysis (XMLA). Normalmente, los proyectos de scripts de Analysis Server se usan para realizar tareas de administración o para volver a crear objetos (como bases de datos o cubos) en instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Estos proyectos se pueden guardar como parte de una solución e integrarlos con un control de código fuente. Para más información sobre cómo crear un proyecto de scripts de Analysis Server en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Proyecto de scripts de Analysis Services en SQL Server Management Studio](../instances/analysis-services-scripts-project-in-sql-server-management-studio.md).  
  
## <a name="introducing-solutions-projects-and-items"></a>Introducción a soluciones, proyectos y elementos  
 Tanto [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] proporcionan proyectos que están organizados en soluciones. Una solución puede contener varios proyectos y un proyecto normalmente contiene varios elementos. Al crear un proyecto se genera automáticamente una nueva solución; puede agregar proyectos adicionales a una solución a medida que los vaya necesitando. Los objetos que contiene un proyecto dependen del tipo de proyecto. Los elementos de cada contenedor de proyectos se guardan como archivos en las carpetas de proyecto del sistema de archivos.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] contiene los siguientes proyectos en el tipo de proyecto Proyectos de Business Intelligence.  
  
|Proyecto|Descripción|  
|-------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Proyecto|Contiene las definiciones de objeto de una única base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para más información sobre cómo crear un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , vea [Create an Analysis Services Project &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md).|  
|Importar base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 2008|Proporciona un asistente que se puede utilizar para crear un nuevo proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] importando definiciones de objeto de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Proyecto|Contiene las definiciones de objeto de un conjunto de paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para más información, vea [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).|  
|Asistente para proyectos de informe|Proporciona un asistente que le guía en el proceso de creación de un proyecto de informe con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para más información, vea [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).|  
|Proyecto de modelos de informe|Contiene las definiciones de objeto de un modelo de informe de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para más información, vea [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).|  
|Proyecto de servidor de informes|Contiene las definiciones de objeto de uno o más informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para más información, vea [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).|  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] también contiene varios tipos de proyectos que se centran en distintas consultas o scripts, como se muestra en la tabla siguiente.  
  
|Proyecto|Descripción|  
|-------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripts|Contiene scripts DMX, MDX y XMLA para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], así como conexiones con instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en las que se pueden ejecutar dichos scripts. Para más información, vea [Proyecto de scripts de Analysis Services en SQL Server Management Studio](../instances/analysis-services-scripts-project-in-sql-server-management-studio.md).|  
|Scripts de SQL Server Compact|Contiene scripts de SQL para SQL Server Compact, así como conexiones con instancias de SQL Server Compact en las que se pueden ejecutar dichos scripts.|  
|Scripts de SQL Server|Contiene scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] y XQuery para una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , así como conexiones con instancias de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] en las que se pueden ejecutar dichos scripts. Para más información, consulte [SQL Server Database Engine](../../database-engine/sql-server-database-engine-overview.md).|  
  
 Para obtener más información sobre soluciones y proyectos, vea "Administrar soluciones, proyectos y archivos" en la documentación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] .NET o en MSDN Library.  
  
## <a name="choosing-between-sql-server-management-studio-and-sql-server-data-tools"></a>Elegir entre SQL Server Management Studio y Herramientas de datos de SQL Server  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] está diseñado para administrar y configurar los objetos existentes en [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] está diseñado para desarrollar soluciones de Business Intelligence que incluyen funciones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 A continuación se mencionan algunas de las diferencias entre [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] proporciona un entorno integrado para conectarse con instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con el fin de configurar y administrar objetos en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Con la utilización de scripts, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] se puede usar también para crear o modificar los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , pero [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no ofrece una interfaz gráfica para el diseño y definición de objetos.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] proporciona un entorno de desarrollo integrado para programar soluciones de Business Intelligence. Puede usar [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] en modo de proyecto, que usa las definiciones basadas en XML de objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que se encuentran en proyectos y soluciones. Si se usa [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] en modo de proyecto, los cambios realizados en objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] se realizan en dichas definiciones de objeto basadas en XML y no se aplican directamente a un objeto de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] hasta que se implementa la solución. También puede usar [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] en el modo en línea, es decir, conectándose directamente a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y trabajando con los objetos de una base de datos existente.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mejora el desarrollo de aplicaciones de Business Intelligence, ya que permite trabajar en proyectos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en un entorno multiusuario con control de código fuente, sin necesidad de tener una conexión activa con una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] proporciona acceso directo a los objetos existentes para realizar consultas y pruebas, y se puede usar para implementar más rápidamente bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que dispongan de scripts previos. Sin embargo, una vez que un proyecto se ha implementado en el entorno de producción, se debe tener cuidado al trabajar con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y sus objetos con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y con [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. El objeto es evitar sobrescribir los cambios realizados directamente en los objetos de una base de datos existente y los cambios realizados en el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que generó originalmente la solución implementada. Para más información, vea [Trabajar con bases de datos y proyectos de Analysis Services durante la fase de desarrollo](work-with-analysis-services-projects-and-databases-in-development.md)y [Trabajar con bases de datos de proyectos de Analysis Services en un entorno de producción](work-with-analysis-services-projects-and-databases-in-production.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Crear un proyecto de Analysis Services &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)  
  
-   [Configurar las propiedades de un proyecto de Analysis Services &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)  
  
-   [Generar proyectos de Analysis Services &#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)  
  
-   [Implementar proyectos de Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
-   [Trabajar con bases de datos y proyectos de Analysis Services durante la fase de desarrollo](work-with-analysis-services-projects-and-databases-in-development.md)  
  
-   [Trabajar con bases de datos de proyectos de Analysis Services en un entorno de producción](work-with-analysis-services-projects-and-databases-in-production.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear un proyecto de Analysis Services &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)   
 [Proyecto de scripts de Analysis Services en SQL Server Management Studio](../instances/analysis-services-scripts-project-in-sql-server-management-studio.md)   
 [Bases de datos de modelos multidimensionales &#40;SSAS&#41;](multidimensional-model-databases-ssas.md)  
  
  
