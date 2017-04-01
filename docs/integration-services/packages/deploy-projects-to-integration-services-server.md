---
title: "Implementar proyectos en el servidor de Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6e9402f4-4d50-49ff-820d-65a77829c4a5
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Implementar proyectos en el servidor de Integration Services
  En la versión actual de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], puede implementar los proyectos en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . El servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite administrar paquetes, ejecutar paquetes y configurar valores de tiempo de ejecución para paquetes usando entornos.  
  
 Para obtener más información sobre los entornos, vea [Crear y asignar un entorno de servidor](../../integration-services/packages/create-and-map-a-server-environment.md).  
  
> [!NOTE]  
>  Al igual que en versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], en la versión actual también puede implementar los paquetes en una instancia de SQL Server y usar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para ejecutar y administrar los paquetes. Se usa el modelo de implementación de paquetes. Para obtener más información, vea [Implementación de paquetes heredada &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
 Para implementar un proyecto en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , debe completar las tareas siguientes:  
  
1.  Crear un catálogo de SSISDB, si no lo tiene todavía. Para obtener más información, vea [Crear el catálogo de SSIS](../../integration-services/service/create-the-ssis-catalog.md).  
  
2.  Convierta el proyecto al modelo de implementación de proyectos ejecutando el **Asistente para conversión de proyectos de Integration Services** . Para obtener más información, vea las instrucciones siguientes: [Para convertir un proyecto al modelo de implementación de proyectos](#convert)  
  
    -   Si creó el proyecto en [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], de forma predeterminada el proyecto utiliza el modelo de implementación de proyectos.  
  
    -   Si creó el proyecto en la versión anterior de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], después de abrir el archivo de proyecto en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], deberá convertir el proyecto al modelo de implementación de proyectos.  
  
        > [!NOTE]  
        >  Si el proyecto contiene uno o más orígenes de datos, se quitan los orígenes de datos cuando se completa la conversión del proyecto. Para crear una conexión a un origen de datos que los paquetes del proyecto puedan compartir, agregue un administrador de conexiones en el nivel de proyecto. Para más información, consulte [Add, Delete, or Share a Connection Manager in a Package](../Topic/Add,%20Delete,%20or%20Share%20a%20Connection%20Manager%20in%20a%20Package.md).  
  
         Dependiendo de si ejecuta el **Asistente para la conversión de proyectos de Integration Services** desde [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], el asistente realiza tareas de conversión diferentes.  
  
        -   Si ejecuta el asistente desde [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], los paquetes incluidos en el proyecto se convierten de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 2005, 2008 o 2008 R2 al formato utilizado por la versión actual de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se actualizan los archivos originales del proyecto (.dtproj) y del paquete (.dtsx).  
  
        -   Si ejecuta el asistente desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], el asistente genera un archivo de implementación del proyecto (.ispac) a partir de los paquetes y las configuraciones incluidos en el proyecto. Los archivos originales del paquete (.dtsx) no se actualizan.  
  
             Puede seleccionar un archivo existente o crear un archivo nuevo en la página **Destino de selección** del asistente.  
  
             Para actualizar archivos del paquete cuando se convierte un proyecto, ejecute el **Asistente para conversión de proyectos de Integration Services** desde [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Para actualizar los archivos de paquete independientemente de la conversión del proyecto, ejecute el **Asistente para la conversión de proyectos de Integration Services** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y el **Asistente para actualizar paquetes SSIS**. Si actualiza los archivos de paquete por separado, asegúrese de guardar los cambios. De lo contrario, cuando convierte el proyecto al modelo de implementación de proyectos, los cambios no guardados efectuados en el paquete no se convierten.  
  
     Para obtener más información sobre la actualización de paquetes, vea [Actualizar paquetes de Integration Services](../../integration-services/install-windows/upgrade-integration-services-packages.md) y [Actualizar paquetes de Integration Services mediante el Asistente para actualizar paquetes SSIS](../../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
3.  Implemente el proyecto en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obtener más información, vea las instrucciones siguientes: [Para implementar un proyecto en el servidor de Integration Services](#deploy).  
  
4.  (Opcional) Crear un entorno para el proyecto implementado. Para obtener más información, vea [Crear y asignar un entorno de servidor](../../integration-services/packages/create-and-map-a-server-environment.md).  
  
##  <a name="convert"></a> Para convertir un proyecto al modelo de implementación de proyectos  
  
1.  Abra el proyecto en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] y, en el Explorador de soluciones, haga clic con el botón derecho en el proyecto y haga clic en **Convertir en el modelo de implementación de proyectos**.  
  
     -O bien-  
  
     En el Explorador de objetos de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], haga clic con el botón derecho en el nodo **Proyectos** y seleccione **Importar paquetes**.  
  
2.  Finalice el asistente. Para más información, consulte [Integration Services Project Conversion Wizard](../../integration-services/packages/integration-services-project-conversion-wizard.md).  
  
##  <a name="deploy"></a> Para implementar un proyecto en el servidor de Integration Services  
  
1.  Abra el proyecto en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]y, en el menú **Proyecto** , seleccione **Implementar** para iniciar el **Asistente para implementación de Integration Services**.  
  
     -O bien-  
  
     En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] > **SSISDB** en el Explorador de objetos y busque la carpeta Proyectos correspondiente al proyecto que quiere implementar. Haga clic con el botón derecho en la carpeta **Proyectos** y, después, haga clic en **Implementar proyecto**.  
  
     -O bien-  
  
     En el símbolo del sistema, ejecute **isdeploymentwizard.exe** desde **%Archivos de programa%\Microsoft SQL Server\110\DTS\Binn**. En equipos de 64 bits, también hay una versión de 32 bits de la herramienta en **%Archivos de programa (x86)%\Microsoft SQL Server\100\DTS\Binn**.  
  
2.  En la página **Seleccionar origen** , haga clic en **Archivo de implementación de proyecto** para seleccionar el archivo de implementación del proyecto.  
  
     -OR-  
  
     Haga clic en **Catálogo de Integration Services** para seleccionar un proyecto que ya se haya implementado en el catálogo de SSISDB.  
  
3.  Finalice el asistente. Para más información, consulte [Integration Services Deployment Wizard](../../integration-services/packages/integration-services-deployment-wizard.md).  
  
  