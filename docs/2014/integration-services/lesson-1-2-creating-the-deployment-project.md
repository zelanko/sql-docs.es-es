---
title: 'Paso 2: Crear el proyecto de implementación | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6f5b0cc2c86ef483a7e2b2c0f5dccba21383641f
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376643"
---
# <a name="step-2-creating-the-deployment-project"></a>Paso 2: Crear el proyecto de implementación
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
 [Paso 3: Agregar paquetes y otros archivos](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
![Icono de Integration Services (pequeño)](media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Proyectos de Integration Services &#40;SSIS&#41;](integration-services-ssis-projects-and-solutions.md)  
  
  
