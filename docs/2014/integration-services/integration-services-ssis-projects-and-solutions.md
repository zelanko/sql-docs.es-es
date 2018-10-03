---
title: Integration Services (SSIS), proyectos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Integration Services], creating
- folders [Integration Services], projects
- files [Integration Services], projects
- folders [Integration Services]
- projects [Integration Services], about projects
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c3ea3adf8d22cb65127fca6e187bf4887051fff2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48110215"
---
# <a name="integration-services-ssis-projects"></a>Proyectos de Integration Services (SSIS)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporciona [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para el desarrollo de paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Cuando implemente paquetes en una base de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o en el Almacén de paquetes de [!INCLUDE[ssIS](../includes/ssis-md.md)] , utilice el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para administrar los paquetes. El servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] solo está disponible en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para más información sobre el servicio, vea [Servicio Integration Services &#40;servicio SSIS&#41;](service/integration-services-service-ssis-service.md). Para obtener más información acerca de la implementación de paquetes, consulte [la implementación del paquete &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md).  
  
 Al implementar proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], utilice los procedimientos almacenados y las vistas de Transact-SQL de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para administrarlos. Para obtener más información acerca de la implementación de proyectos, vea [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md). Para más información sobre el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], vea [Integration Services &#40;SSIS&#41; Server (Servidor de Integration Services &#40;SSIS&#41;)](catalog/integration-services-ssis-server-and-catalog.md).  
  
 Para una introducción a [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] y [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], vea [Entornos de Studio e Integration Services &#40;SSIS&#41;](integration-services-ssis-development-and-management-tools.md).  
  
## <a name="understanding-integration-services-projects"></a>Descripción de los proyectos de Integration Services  
 Un proyecto es un contenedor en el que se desarrollan los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] almacena y agrupa los archivos que están relacionados con el paquete. Por ejemplo, un proyecto incluye los archivos necesarios para crear una solución de extracción, transferencia y carga específica.  
  
 Antes de crear un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , debería familiarizarse con el contenido básico de este tipo de proyecto. Cuando sepa lo que un proyecto contiene, puede empezar a crear y trabajar con un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
### <a name="folders-in-integration-services-projects"></a>Carpetas en proyectos de Integration Services  
 El diagrama siguiente muestra las carpetas en un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 ![Carpetas en un proyecto de Integration Services](media/solutionexplorer.gif "Folders in an Integration Services project")  
  
 La tabla siguiente describe las carpetas que aparecen en un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
|Carpeta|Descripción|  
|------------|-----------------|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] .|Contiene paquetes. Para obtener más información, vea [Paquetes de Integration Services &#40;SSIS&#41;](../../2014/integration-services/integration-services-ssis-packages.md).|  
|Varios|Contiene archivos que no son archivos de paquete.|  
  
### <a name="files-in-integration-services-projects"></a>Archivos en proyectos de Integration Services  
 Cuando se agrega un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nuevo o existente a una solución, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] crea archivos de proyecto que tienen las extensiones .dtproj, .dtproj.user y .database.  
  
-   El archivo *.dtproj contiene información sobre las configuraciones del proyecto y elementos tales como paquetes.  
  
-   El archivo *.dtproj.user contiene información sobre sus preferencias para trabajar con el proyecto.  
  
-   El archivo *.database contiene información que [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] requiere para abrir el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="understanding-solutions"></a>Descripción de las soluciones  
 Una solución es un contenedor que agrupa y administra los proyectos que se utilizan cuando se desarrollan soluciones empresariales de extremo a extremo. Una solución le permite manejar varios proyectos como una sola unidad y unir uno o más proyectos relacionados que contribuyen a una solución empresarial.  
  
 Las soluciones pueden incluir diferentes tipos de proyectos. Si desea usar el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] para crear un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , debe trabajar en un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en una solución proporcionada por [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Cuando se crea una nueva solución, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] agrega una carpeta Solución al Explorador de soluciones y crea archivos con las extensiones .sln y .suo:  
  
-   El archivo *.sln contiene información sobre la configuración de soluciones y enumera los proyectos de la solución.  
  
-   El archivo *.suo contiene información sobre sus preferencias para trabajar con la solución.  
  
 Aunque [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] crea automáticamente una solución al crear un nuevo proyecto, también puede crear una solución en blanco y agregar proyectos posteriormente.  
  
> [!NOTE]  
>  De forma predeterminada, al crear un nuevo proyecto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], la solución no se muestra en el panel **Explorador de proyectos** . Para cambiar este comportamiento predeterminado, en el menú **Herramientas** , haga clic en **Opciones**. En el cuadro de diálogo **Opciones** , expanda **Proyectos y soluciones**y, a continuación, haga clic en **General**. En la página **General** , seleccione **Mostrar solución siempre**.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Agregar o quitar un proyecto de Integration Services en una solución](../../2014/integration-services/add-or-remove-an-integration-services-project-in-a-solution.md)  
  
 [Crear un proyecto de Integration Services](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
 [Agregar un elemento a un proyecto de Integration Services](../../2014/integration-services/add-an-item-to-an-integration-services-project.md)  
  
 [Copiar los elementos de proyectos](../../2014/integration-services/copy-project-items.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [Desarrollo de un proyecto de Integration Services](../../2014/integration-services/development-of-an-integration-services-project.md)  
  
  
