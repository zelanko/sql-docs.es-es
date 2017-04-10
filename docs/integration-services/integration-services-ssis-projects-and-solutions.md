---
title: "Integration Services (SSIS), proyectos y soluciones | Microsoft Docs"
ms.custom: ""
ms.date: "08/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.importprojectwizard.f1"
helpviewer_keywords: 
  - "proyectos [Integration Services], crear"
  - "carpetas [Integration Services], proyectos"
  - "archivos [Integration Services], proyectos"
  - "carpetas [Integration Services]"
  - "proyectos [Integration Services], acerca de los proyectos"
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
caps.latest.revision: 63
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 62
---
# Integration Services (SSIS), proyectos y soluciones
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporciona [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para el desarrollo de paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Cuando implemente paquetes en una base de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o en el Almacén de paquetes de [!INCLUDE[ssIS](../includes/ssis-md.md)] , utilice el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para administrar los paquetes. El servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] solo está disponible en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para más información sobre el servicio, vea [Servicio Integration Services &#40;servicio SSIS&#41;](../integration-services/service/integration-services-service-ssis-service.md). Para más información sobre la implementación de paquetes, vea [Implementación de paquetes heredada &#40;SSIS&#41;](../integration-services/packages/legacy-package-deployment-ssis.md).  
  
 Al implementar proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], utilice los procedimientos almacenados y las vistas de Transact-SQL de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para administrarlos. Para obtener más información acerca de la implementación de proyectos, vea [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx). Para más información sobre el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], vea [Integration Services &#40;SSIS&#41; Server (Servidor de Integration Services &#40;SSIS&#41;)](https://msdn.microsoft.com/library/ms137731.aspx).  
  
 Para información general sobre [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] y [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], consulte [Integration Services &#40;SSIS&#41; y herramientas de administración](https://msdn.microsoft.com/library/ms140028.aspx)%20and%20Studio%20Environments.md).  
  
## Los proyectos de Integration Services contienen paquetes  
 Un proyecto es un contenedor en el que se desarrollan los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] almacena y agrupa los archivos que están relacionados con el paquete. Por ejemplo, un proyecto incluye los archivos necesarios para crear una solución de extracción, transferencia y carga específica.  
  
 Antes de crear un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , debería familiarizarse con el contenido básico de este tipo de proyecto. Cuando sepa lo que un proyecto contiene, puede empezar a crear y trabajar con un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## Carpetas en proyectos de Integration Services  
 El diagrama siguiente muestra las carpetas en un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 ![Carpetas de un proyecto de Integration Services](../integration-services/media/solutionexplorer.gif "Carpetas de un proyecto de Integration Services")  
  
 La tabla siguiente describe las carpetas que aparecen en un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
|Carpeta|Description|  
|------------|-----------------|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] .|Contiene paquetes. Para obtener más información, vea [Paquetes de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-packages.md).|  
|Varios|Contiene archivos que no son archivos de paquete.|  
  
## Archivos en proyectos de Integration Services  
 Cuando se agrega un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nuevo o existente a una solución, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] crea archivos de proyecto que tienen las extensiones .dtproj, .dtproj.user y .database.  
  
-   El archivo *.dtproj contiene información sobre las configuraciones del proyecto y elementos tales como paquetes.  
  
-   El archivo *.dtproj.user contiene información sobre sus preferencias para trabajar con el proyecto.  
  
-   El archivo *.database contiene información que [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] requiere para abrir el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
## Versión de destino en proyectos de Integration Services  
 En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], puede crear, mantener y ejecutar paquetes que tienen como destino SQL Server 2016, SQL Server 2014 o SQL Server 2012.  
  
 En el Explorador de soluciones, haga clic con el botón derecho en un proyecto de Integration Services y seleccione **Propiedades** para abrir las páginas de propiedades del proyecto. En la pestaña **General** de **Propiedades de configuración**, seleccione la propiedad **TargetServerVersion** y luego elija SQL Server 2016, SQL Server 2014 o SQL Server 2012.  
  
 ![TargetServerVersion property in project properties dialog box](../integration-services/media/targetserverversion2.png "TargetServerVersion property in project properties dialog box")  
  
## Las soluciones contienen proyectos  
 Una solución es un contenedor que agrupa y administra los proyectos que se utilizan cuando se desarrollan soluciones empresariales de extremo a extremo. Una solución le permite manejar varios proyectos como una sola unidad y unir uno o más proyectos relacionados que contribuyen a una solución empresarial.  
  
 Las soluciones pueden incluir diferentes tipos de proyectos. Si desea usar el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] para crear un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , debe trabajar en un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en una solución proporcionada por [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Cuando se crea una nueva solución, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] agrega una carpeta Solución al Explorador de soluciones y crea archivos con las extensiones .sln y .suo:  
  
-   El archivo *.sln contiene información sobre la configuración de soluciones y enumera los proyectos de la solución.  
  
-   El archivo *.suo contiene información sobre sus preferencias para trabajar con la solución.  
  
 Aunque [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] crea automáticamente una solución al crear un nuevo proyecto, también puede crear una solución en blanco y agregar proyectos posteriormente.  
  
> **NOTA:** De manera predeterminada, al crear un nuevo proyecto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], la solución no aparece en el panel **Explorador de proyectos**. Para cambiar este comportamiento predeterminado, en el menú **Herramientas** , haga clic en **Opciones**. En el cuadro de diálogo **Opciones** , expanda **Proyectos y soluciones**y, a continuación, haga clic en **General**. En la página **General** , seleccione **Mostrar solución siempre**.  
  
## Tareas relacionadas  
 [Agregar o quitar un proyecto de Integration Services en una solución](../Topic/Add%20or%20Remove%20an%20Integration%20Services%20Project%20in%20a%20Solution.md)  
  
 [Crear un proyecto de Integration Services](../Topic/Create%20a%20New%20Integration%20Services%20Project.md)  
  
 [Agregar un elemento a un proyecto de Integration Services](../Topic/Add%20an%20Item%20to%20an%20Integration%20Services%20Project.md)  
  
 [Copiar los elementos de proyectos](../Topic/Copy%20Project%20Items.md)  
  
## Contenido relacionado  
 [Desarrollo de un proyecto de Integration Services](../Topic/Development%20of%20an%20Integration%20Services%20Project.md)  
  
  