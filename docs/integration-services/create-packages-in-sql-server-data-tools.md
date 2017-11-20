---
title: Crear paquetes en SQL Server Data Tools | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: bb3c085b-1458-49fa-8348-6a76b6e97ea6
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 0d949644408de74f118d352a89047137cdcd0350
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="create-packages-in-sql-server-data-tools"></a>Crear paquetes en herramientas de datos de SQL Server
  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], puede crear un paquete nuevo utilizando uno de los métodos siguientes:  
  
-   Usar la plantilla de paquete que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye.  
  
-   Usar una plantilla personalizada  
  
     Para utilizar paquetes personalizados como plantillas en la creación de nuevos paquetes, solo tiene que copiarlos en la carpeta DataTransformationItems. De forma predeterminada, esta carpeta se encuentra en C:\Archivos de programa\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
-   Copiar un paquete existente.  
  
     Si los paquetes existentes incluyen funcionalidades que desea volver a usar, puede general el flujo de control y los flujos de datos en el nuevo paquete más rápidamente copiando y pegando objetos desde otros paquetes. Para más información sobre el uso de copiar y pegar en proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , vea [Volver a utilizar objetos de paquete](../integration-services/reuse-of-package-objects.md).  
  
     Si crea un nuevo paquete mediante la copia de un paquete existente o mediante el uso de un paquete personalizado como plantilla, también se copian el nombre y GUID del paquete existente. Deberá actualizar el nombre y el GUID del nuevo paquete para diferenciarlo del paquete del que se copió. Por ejemplo, si los paquetes tienen el mismo GUID, es más difícil identificar el paquete al que pertenecen los datos del registro. Puede volver a generar el GUID en la propiedad **ID** y actualizar el valor de la propiedad **Name** con la ventana Propiedades de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para más información, vea [Establecer las propiedades de paquetes](../integration-services/set-package-properties.md) y [dtutil (utilidad)](../integration-services/dtutil-utility.md).  
  
-   Usar un paquete personalizado que ha designado como una plantilla.  
  
-   Ejecutar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
     El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] crea un paquete completo para una importación o exportación simples. Este asistente configura las conexiones, el origen y el destino, y agrega las transformaciones de datos que se necesiten para poder ejecutar la importación o exportación inmediatamente. Si lo desea, puede guardar el paquete para ejecutarlo de nuevo posteriormente o refinarlo y mejorarlo en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Sin embargo, si lo guarda, debe agregar el paquete a un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] existente para poder cambiar o ejecutar el paquete en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
 Los paquetes que creó en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] mediante el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] se guardan en el sistema de archivos. Para guardar un paquete en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o en el almacén de paquetes, necesita guardar una copia del paquete. Para más información, vea [Guardar una copia de un paquete](http://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31).  

 Para ver un vídeo donde se muestra cómo crear un paquete básico con la plantilla de paquete predeterminada, visite [Crear un paquete básico (vídeo de SQL Server)](http://go.microsoft.com/fwlink/?LinkId=131023).  

## <a name="get-sql-server-data-tools"></a>Obtener SQL Server Data Tools
Para instalar SQL Server Data Tools (SSDT), vea [Descargar SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md).

## <a name="create-a-package-in-sql-server-data-tools-using-the-package-template"></a>Crear un paquete en SQL Server Data Tools con la plantilla de paquete  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el que desea crear un paquete.  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en la carpeta **Paquetes SSIS** y, después, haga clic en **Nuevo paquete de SSIS**.  
  
3.  Opcionalmente, agregue flujo de control, tareas de flujo de datos y controladores de eventos al paquete. Para más información, vea [Flujo de control](../integration-services/control-flow/control-flow.md), [Flujo de datos](../integration-services/data-flow/data-flow.md)y [Controladores de eventos de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-event-handlers.md).  
  
4.  En el menú **Archivo** , haga clic en **Guardar los elementos seleccionados** para guardar el nuevo paquete.  
  
    > [!NOTE]  
    >  Puede guardar un paquete vacío.  
  
## <a name="choose-the-target-version-of-a-project-and-its-packages"></a>Para elegir la versión de destino de un proyecto y sus paquetes  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en un proyecto de Integration Services y seleccione **Propiedades** para abrir las páginas de propiedades del proyecto.  
  
2.  En la pestaña **General** de **Propiedades de configuración**, seleccione la propiedad **TargetServerVersion** y luego elija SQL Server 2016, SQL Server 2014 o SQL Server 2012.  
  
     ![Propiedad TargetServerVersion en el cuadro de diálogo de propiedades de proyecto](../integration-services/media/targetserverversion2.png "TargetServerVersion propiedad en el cuadro de diálogo de propiedades de proyecto")  
  
 Puede crear, mantener y ejecutar paquetes cuyo destino es SQL Server 2016, SQL Server 2014 o SQL Server 2012.  
  
  

