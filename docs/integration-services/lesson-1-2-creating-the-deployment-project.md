---
title: "Paso 2: Crear el proyecto de implementación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e92d8018d600c88e444cebd4623d290e24c0a779
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-2---creating-the-deployment-project"></a>Lección 1-2-crear el proyecto de implementación
En [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], la unidad que se puede implementar es un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Antes de que pueda implementar paquetes, debe crear un nuevo proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y agregar todos los paquetes y archivos auxiliares que desee implementar con los paquetes en ese proyecto.  
  
### <a name="to-create-the-integration-services-project"></a>Para crear el proyecto de Integration Services  
  
1.  Haga clic en **Inicio**, seleccione **Todos los programas**, **Microsoft SQL Server**y, después, haga clic en **SQL Server Data Tools**.  
  
2.  En el menú **Archivo** , seleccione **Nuevo**y haga clic en **Proyecto** para crear un proyecto nuevo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
3.  En el cuadro de diálogo **Nuevo proyecto** , seleccione **Proyecto de Integration Services** en el panel **Plantillas** .  
  
4.  En el cuadro **Nombre** , cambie el nombre predeterminado por **Deployment Tutorial**. Opcionalmente, desactive la casilla **Crear directorio para la solución** .  
  
5.  Acepte la ubicación predeterminada o haga clic en **Examinar** para buscar la carpeta que quiere usar.  
  
6.  En el cuadro de diálogo **Ubicación del proyecto** , haga clic en la carpeta y, después, en **Abrir**.  
  
7.  Haga clic en **Aceptar**.  
  
8.  De forma predeterminada, se crea un paquete vacío, denominado Package.dtsx, que se agrega al nuevo proyecto. Sin embargo, no utilizará este paquete; en su lugar, agregará paquetes existentes al proyecto. Puesto que todos los paquetes de un proyecto se incluirán en la implementación, deber eliminar Package.dtsx. Para eliminarlo, haga clic con el botón derecho en el paquete y, después, haga clic en **Eliminar**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Paso 3: agregar paquetes y otros archivos](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
## <a name="see-also"></a>Vea también  
[Proyectos de Integration Services &#40;SSIS&#41;](~/integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
  


