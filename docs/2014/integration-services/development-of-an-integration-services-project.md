---
title: Desarrollo de la integración de una proyecto de servicios | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- projects [Integration Services], creating
- Integration Services projects, creating
- SQL Server Integration Services projects, creating
- SSIS projects, creating
ms.assetid: 6e90b016-36a5-415e-9440-a20199fffff0
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2eab6834047938a908cc9ca034ad64ad8c7082cc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106385"
---
# <a name="development-of-an-integration-services-project"></a>Desarrollo de un proyecto de Integration Services
  Puede agregar paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] a proyectos. Para crear y trabajar con proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , debe instalar el entorno de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] . Para obtener más información, vea [Instalar Integration Services](install-windows/install-integration-services.md).  
  
 Al crear un proyecto nuevo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], el cuadro de diálogo **Nuevo proyecto** incluye una plantilla **Proyecto de Integration Services** . Esta plantilla de proyecto crea un proyecto nuevo que contiene un único paquete.  
  
## <a name="projects-and-solutions"></a>Proyectos y soluciones  
 Los proyectos se almacenan en soluciones. Primero se crea una solución y luego se agrega un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] a la solución. Si no existe solución, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] crea automáticamente una cuando se crea el proyecto. Una solución puede contener varios proyectos de tipos diferentes.  
  
> [!NOTE]  
>  De forma predeterminada, al crear un proyecto nuevo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], la solución no se muestra en el panel **Explorador de soluciones** . Para cambiar este comportamiento predeterminado, en el menú **Herramientas** , haga clic en **Opciones**. En el cuadro de diálogo **Opciones** , expanda **Proyectos y soluciones**y, a continuación, haga clic en **General**. En la página **General** , seleccione **Mostrar solución siempre**.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Crear un nuevo proyecto de Integration Services](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
-   [Agregar que un elemento a la integración de un proyecto de servicios](../../2014/integration-services/add-an-item-to-an-integration-services-project.md)  
  
-   [Agregar o quitar un proyecto de Integration Services en una solución](../../2014/integration-services/add-or-remove-an-integration-services-project-in-a-solution.md)  
  
  