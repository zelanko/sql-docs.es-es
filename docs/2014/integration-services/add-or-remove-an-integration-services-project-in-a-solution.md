---
title: Agregar o quitar un proyecto de Integration Services en una solución | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- Integration Services projects, adding
- SQL Server Integration Services projects, adding
- SSIS projects, adding
- projects [Integration Services], adding
ms.assetid: f01f6475-b63c-41dc-82ac-b62162b3adf7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7d338cac89b7b6c8f2588817cfd6718d4f415589
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84925971"
---
# <a name="add-or-remove-an-integration-services-project-in-a-solution"></a>Agregar o quitar un proyecto de Integration Services en una solución
  Los procedimientos siguientes describen cómo agregar o quitar un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en una solución.  
  
 Solo se puede agregar un proyecto a una solución existente, o quitar un proyecto de una solución, mientras esta está visible en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Si ha seleccionado la opción **Mostrar solución siempre** en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , mostrará [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] una solución aunque esa solución contenga solo un proyecto. En caso contrario, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] solo mostrará una solución cuando esta contenga varios proyectos. Los proyectos adicionales pueden ser proyectos de [!INCLUDE[ssIS](../includes/ssis-md.md)] o de otros tipos.  
  
## <a name="adding-an-integration-services-project"></a>Agregar un proyecto de Integration Services  
 Cuando agregue un proyecto, puede crear uno en blanco con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o agregar uno creado anteriormente para otra solución. Solo puede agregar un proyecto a una solución existente mientras la solución está visible en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
#### <a name="to-add-a-new-integration-services-project-to-a-solution"></a>Para agregar un proyecto nuevo de Integration Services a una solución  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra la solución para la cual desea agregar un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nuevo y realice una de las siguientes acciones:  
  
    -   Haga clic con el botón derecho en la solución, seleccione **Agregar** y, después, haga clic en **Nuevo proyecto**.  
  
    -   En el menú **Archivo** , seleccione **Agregar**y haga clic en **Nuevo proyecto**.  
  
2.  En el cuadro de diálogo **Nuevo proyecto** , seleccione **Proyecto de Integration Services** del panel **Plantillas** .  
  
3.  Opcionalmente, modifique el nombre y ubicación del proyecto.  
  
4.  Haga clic en **OK**.  
  
#### <a name="to-add-an-existing-integration-services-project-to-a-solution"></a>Para agregar un proyecto de Integration Services existente a una solución  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra la solución para la cual desee agregar un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] existente y realice una de las siguientes acciones:  
  
    -   Haga clic con el botón derecho en la solución, seleccione **Agregar** y, después, haga clic en **Proyecto existente**.  
  
    -   En el menú **Archivo** , seleccione **Agregar**y haga clic en **Proyecto existente**.  
  
2.  En el cuadro de diálogo **Agregar proyecto existente** , busque el proyecto que desee agregar y haga clic en **Abrir**.  
  
3.  El proyecto se agrega a la carpeta de soluciones en el **Explorador de soluciones**.  
  
## <a name="removing-an-integration-services-project"></a>Quitar un proyecto de Integration Services  
 Solo puede quitar un proyecto de una solución mientras la solución está visible en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Una vez que la solución está visible, puede quitar todos los proyectos excepto uno. Tan pronto como queda un solo proyecto, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ya no muestra la carpeta de la solución y no se puede quitar el último proyecto.  
  
#### <a name="to-remove-an-integration-services-project-from-a-solution"></a>Para quitar un proyecto de Integration Services de una solución  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra la solución de la que desea quitar un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en el proyecto y, después, haga clic en **Descargar el proyecto**.  
  
3.  Haga clic en **Aceptar** para confirmar la eliminación.  
  
## <a name="see-also"></a>Consulte también  
 [Integration Services &#40;proyectos&#41; de SSIS](integration-services-ssis-projects-and-solutions.md)   
 [Crear un proyecto de Integration Services](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
  
