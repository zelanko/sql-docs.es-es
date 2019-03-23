---
title: Asistente para la implementación de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.deploymentwizard.f1
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b091518f61944b3eb62f8abdc02f0270e086538a
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389143"
---
# <a name="integration-services-deployment-wizard"></a>Asistente para implementación de Integration Services
  El Asistente para la implementación de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] implementa proyectos en el catálogo de SSISDB en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante el modelo de implementación de proyectos.  
  
 Para iniciar el [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Asistente para la implementación de un proyecto abierto en [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], seleccione **implementar** desde el **proyecto** menú. Para iniciar el asistente [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], expanda el **catálogos de Integration Services** > **SSISDB** nodo en el Explorador de objetos, haga clic en el **proyectos** carpeta y, a continuación, haga clic en **implementar proyecto**.  
  
 El asistente continua con los siguientes cuatro pasos. Haga clic en **siguiente** para ir al paso siguiente, o **anterior** para volver al paso anterior.  
  
1.  **Seleccionar origen** : seleccione el [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proyecto que desea implementar.  
  
2.  **Seleccionar destino** -seleccionar el destino del proyecto.  
  
3.  **Revisión** -mostrará sus selecciones.  
  
4.  **Implementar/resultados** : implementa el proyecto y muestra los resultados.  
  
## <a name="select-source"></a>Seleccionar origen  
 Para implementar un archivo de implementación del proyecto que creó, seleccione **archivo de proyecto de implementación** y escriba la ruta de acceso al archivo .ispac o haga clic en **examinar** para encontrarlo en el [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] carpeta del proyecto. Para implementar un proyecto que resida en el catálogo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , seleccione **Catálogo de Integration Services**y especifique el nombre del servidor y la ruta de acceso al proyecto en el catálogo.  
  
 Si inicia el asistente en [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], posteriormente, de forma predeterminada el asistente selecciona el proyecto abierto como origen y omite este paso. Para volver a este paso y seleccionar un origen diferente, haga clic en **anterior** o haga clic en **Seleccionar origen** en el panel izquierdo.  
  
## <a name="select-destination"></a>Seleccionar destino  
 Para seleccionar la carpeta de destino para el proyecto en el catálogo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , escriba la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o haga clic en **Examinar** para seleccionarla en una lista de servidores. Escriba la ruta de acceso del proyecto en SSISDB o haga clic en **Examinar** para seleccionarla.  
  
 Si inicia el asistente en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], de forma predeterminada, el asistente selecciona la instancia de servidor conectado y especifica la ruta de acceso para el proyecto seleccionado. Puede cambiar estos valores para implementar el proyecto en una ubicación diferente.  
  
## <a name="review"></a>Revisar  
 El asistente le permite revisar los valores de configuración que ha seleccionado antes de implementar el proyecto. Puede cambiar las selecciones si hace clic en **Anterior**o si hace clic en cualquiera de los pasos del panel izquierdo.  
  
## <a name="deployresults"></a>Implementar/Resultados  
 Al hacer clic en **implementar** desde el **revisión** página, el proyecto se implementa y **resultados** página muestra el éxito o fracaso de cada acción. Si la acción no se realiza correctamente, haga clic en **Error** en la columna **Resultado** para que aparezca una explicación del error. Haga clic en **Guardar informe...**  para guardar los resultados en un archivo XML.  
  
 Haga clic en **Cerrar** para salir del asistente.  
  
## <a name="see-also"></a>Vea también  
 [Implementar proyectos en el servidor de Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [Implementación de proyectos y paquetes](packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
