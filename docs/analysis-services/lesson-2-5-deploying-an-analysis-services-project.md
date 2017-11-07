---
title: "Proyecto de servicios de implementación de un análisis | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5d98bab3-3577-4143-b737-5196444a36ac
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c933a78cedb5bf0169bd18efba310676a4cde7a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-5---deploying-an-analysis-services-project"></a>Lección 2-5: implementar un proyecto de Analysis Services
Para ver los datos de dimensión y de cubo de los objetos del cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] del proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , debe implementar el proyecto en una instancia determinada de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y luego procesar el cubo y sus dimensiones. Al*implementar* un proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] project creates the defined objects in un proyecto de instun proyecto dece of [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Cuando se*procesan* los objetos en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , se copian los datos de los orígenes de datos subyacentes en los objetos del cubo. Para obtener más información, consulte [Implementar proyectos de Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md) y [Configurar las propiedades de un proyecto de Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
En este punto del proceso de implementación, generalmente se implementa el cubo en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en un servidor de implementación. Una vez finalizado el proceso de implementación del proyecto de Business Intelligence, generalmente utilizará el Asistente para la implementación de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para implementarlo desde el servidor de desarrollo en un servidor de producción. Para obtener más información, consulte [Implementación de soluciones de modelos multidimensionales](../analysis-services/multidimensional-models/multidimensional-model-solution-deployment.md) e [Implementar soluciones de modelos con el Asistente para la implementación](../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md).  
  
En la tarea siguiente, revisará las propiedades de implementación del proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y luego implementará el proyecto en la instancia local de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
### <a name="to-deploy-the-analysis-services-project"></a>Para implementar el proyecto de Analysis Services  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **Tutorial de Analysis Services** y, después, haga clic en **Propiedades**.  
  
    Aparece el cuadro de diálogo **Páginas de propiedades de Tutorial de Analysis Services** , en el que se muestran las propiedades de configuración de Active(Development). Puede definir varias configuraciones, cada una con distintas propiedades. Por ejemplo, es posible que un programador desee configurar el mismo proyecto para implementarlo en distintos equipos de implementación y con distintas propiedades de implementación, como nombres de base de datos o propiedades de procesamiento. Fíjese en el valor de la propiedad **Ruta de acceso de los resultados** . Esta propiedad especifica la ubicación en la que se guardan los scripts de implementación XMLA cuando se crea un proyecto. Estos son los scripts que se utilizan para implementar los objetos del proyecto en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
2.  En el nodo **Propiedades de configuración** del panel de la izquierda, haga clic en **Implementación**.  
  
    Revise las propiedades de implementación del proyecto. De forma predeterminada, la plantilla del proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] configura un proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para implementar de forma incremental todos los proyectos en la instancia predeterminada de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en el equipo local, crear una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] con el mismo nombre que el proyecto y procesar los objetos después de la implementación utilizando la opción de procesamiento predeterminada. Para obtener más información, consulte [Configurar las propiedades de un proyecto de Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
    > [!NOTE]  
    > Si desea implementar el proyecto en una instancia con nombre de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en el equipo local o en una instancia de un servidor remoto, cambiar el **Server** nombre de propiedad a la instancia adecuada, como \<  *ServerName**>\\<**nombreDeInstancia**>*.  
  
3.  Haga clic en **Aceptar**.  
  
4.  En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **Tutorial de Analysis Services** y, después, haga clic en **Implementar**. Es posible que tenga que esperar.  
  
    > [!NOTE]  
    > Si obtiene errores durante la implementación, utilice SQL Server Management Studio para comprobar los permisos de base de datos. La cuenta que especificó para la conexión a un origen de datos debe tener un inicio de sesión en la instancia de SQL Server. Haga doble clic en el inicio de sesión para ver las propiedades de la asignación de usuarios. La cuenta debe tener permisos db_datareader para la base de datos **AdventureWorksDW2012** .  
  
    [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] genera e implementa el proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , Tutorial en la instancia especificada de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , mediante un script de implementación. El progreso de la implementación se muestra en dos ventanas: la ventana **Salida** y la ventana **Progreso de la implementación: Tutorial de Analysis Services** .  
  
    Para abrir la ventana Resultados, si es necesario, haga clic en **Resultados** en el menú **Ver** . La ventana **Resultados** muestra el progreso global de la implementación. La ventana **Progreso de la implementación – Tutorial de Analysis Services** muestra los detalles de cada paso realizado durante la implementación. Para obtener más información, consulte [Generar proyectos de Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md) e [Implementar proyectos de Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md).  
  
5.  Revise el contenido de las ventanas **Resultados** y **Progreso de la implementación – Tutorial de Analysis Services** para comprobar que la compilación, implementación y procesamiento del cubo se realizaron sin errores.  
  
6.  Para ocultar la ventana **Progreso de la implementación - Tutorial de Analysis Services** , haga clic en el icono **Ocultar automáticamente** (similar a una chincheta) en la barra de herramientas de la ventana.  
  
7.  Para ocultar la ventana **Resultados** haga clic en el icono **Ocultar automáticamente** en la barra de herramientas de la ventana.  
  
Ha implementado correctamente el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en la instancia local de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]y luego lo ha procesado.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Examinar el cubo](../analysis-services/lesson-2-6-browsing-the-cube.md)  
  
## <a name="see-also"></a>Vea también  
[Implementar proyectos de Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
[Configurar las propiedades de un proyecto de Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)  
  
  
  

