---
title: Ejecutar paquetes de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.component: packages
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.ispackageexecute.f1
- sql13.ssis.ssms.executepackage.f1
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
- executing packages [Integration Services]
- running packages [Integration Services]
- Integration Services, (See also Integration Services packages)
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
caps.latest.revision: 65
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6e91aeecb953f97d51591947c258fb7860864b48
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="run-integration-services-ssis-packages"></a>Ejecutar paquetes de Integration Services (SSIS)
  Para ejecutar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , puede utilizar una de las herramientas en función de dónde se almacenan los paquetes. Las herramientas se enumeran en la tabla a continuación.  
  
 Para almacenar un paquete en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , utilice el modelo de implementación del proyecto para implementar el proyecto en el servidor. Para obtener más información, consulte [Deploy Integration Services (SSIS) Projects and Package](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md) (Implementación de proyectos y paquetes de Integration Services [SSIS]).  
  
 Para almacenar un paquete en el almacén de paquetes SSIS, la base de datos msdb o en el sistema de archivos, utilice el modelo de implementación de paquetes. Para más información, vea [Implementación de paquetes heredada &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
|Herramienta|Paquetes que están almacenados en el servidor de Integration Services|Paquetes que están almacenados en el almacén de paquetes SSIS o en la base de datos msdb|Paquetes que están almacenados en el sistema de archivos, fuera de la ubicación que forma parte del almacén de paquetes SSIS|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|no|no<br /><br /> Pero puede agregar un paquete existente a un proyecto del almacén de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] , que incluye la base de datos msdb. La inclusión de un paquete existente en el proyecto de este modo crea una copia local del paquete en el sistema de archivos.|Sí|  
|**SQL Server Management Studio, cuando está conectado a una instancia del motor de base de datos que hospeda el servidor de Integration Services**<br /><br /> Para obtener más información, consulte [Execute Package Dialog Box](#execute_package_dialog).|Sí|no<br /><br /> Sin embargo, puede importar un paquete al servidor desde estas ubicaciones.|no<br /><br /> Sin embargo, puede importar un paquete al servidor desde el sistema de archivos.|
|**SQL Server Management Studio, cuando está conectado a una instancia del motor de base de datos que hospeda el servidor de Integration Services que está habilitado como patrón de escalado horizontal**<br /><br /> Para obtener más información, consulte [Ejecutar paquetes en el escalado horizontal](../../integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md).|Sí|no|no|
|**SQL Server Management Studio, cuando está conectado al servicio Integration Services que administra el almacén de paquetes SSIS**|no|Sí|no<br /><br /> Sin embargo, puede importar un paquete al almacén de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] desde el sistema de archivos.|  
|**dtexec**<br /><br /> Para más información, consulte [dtexec Utility](../../integration-services/packages/dtexec-utility.md).|Sí|Sí|Sí|  
|**dtexecui**<br /><br /> Para más información, vea [Referencia de la interfaz de usuario de la Utilidad de ejecución de paquetes &#40;DtExecUI&#41;](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)|no|Sí|Sí|  
|**Agente SQL Server**<br /><br /> Use un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para programar un paquete.<br /><br /> Para más información, consulte [SQL Server Agent Jobs for Packages](../../integration-services/packages/sql-server-agent-jobs-for-packages.md).|Sí|Sí|Sí|  
|**Procedimiento almacenado integrado**<br /><br /> Para más información, vea [catalog.start_execution &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)|Sí|no|no|  
|**API administrada, con tipos y miembros del espacio de nombres**  <xref:Microsoft.SqlServer.Management.IntegrationServices>|Sí|no|no|  
|**API administrada, con tipos y miembros del espacio de nombres**  <xref:Microsoft.SqlServer.Dts.Runtime>|No actualmente|Sí|Sí|  

## <a name="execution-and-logging"></a>Ejecución y registro  
 Los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se pueden habilitar para el registro y el usuario puede capturar la información en tiempo de ejecución de los archivos de registro. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
 Puede supervisar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que se implementan y se ejecutan en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante informes de operación. Los informes están disponibles en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información, consulte [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
## <a name="run-a-package-in-sql-server-data-tools"></a>Ejecutar un paquete en SQL Server Data Tools
  Los paquetes se ejecutan normalmente en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante el desarrollo, la depuración y la comprobación de los paquetes. Cuando se ejecuta un paquete desde el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , siempre se ejecuta inmediatamente.  
  
 Mientras se ejecuta un paquete, el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] muestra el progreso de la ejecución en la pestaña **Progreso** . Puede ver la hora de inicio y de fin del paquete y sus tareas y contendores, además de información acerca de las tareas o contenedores del paquete que generó un error. Una vez que el paquete ha terminado de ejecutarse, la información de tiempo de ejecución permanece disponible en la pestaña **Resultados de la ejecución** . Para obtener más información, vea la sección "Informes de progreso" en el tema [Debugging Control Flow](../../integration-services/troubleshooting/debugging-control-flow.md).  
  
 **Implementación en tiempo de diseño**. Cuando se ejecuta un paquete en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], el paquete se genera y luego se implementa en una carpeta. Antes de ejecutar el paquete, puede especificar la carpeta en que se implementa el paquete. Si no especifica una carpeta, se usa de forma predeterminada la carpeta **bin** de forma predeterminada. Este tipo de implementación se denomina implementación en tiempo de diseño.  
  
### <a name="to-run-a-package-in-sql-server-data-tools"></a>Para ejecutar un paquete en herramientas de datos de SQL Server  
  
1.  En el Explorador de soluciones, si la solución contiene varios proyectos, haga clic con el botón derecho en el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete y, después, haga clic en **Establecer como objeto StartUp** para establecer el proyecto inicial.  
  
2.  En el Explorador de soluciones, si el proyecto contiene varios paquetes, haga clic con el botón derecho en un paquete y, después, haga clic en **Establecer como objeto StartUp** para establecer el paquete inicial.  
  
3.  Para ejecutar un paquete, use uno de los procedimientos siguientes:  
  
    -   Abra el paquete que desea ejecutar y haga clic en **Iniciar depuración** en la barra de menús, o presione F5. Cuando se termine de ejecutar el paquete, presione Mayús+F5 para volver al modo de diseño.  
  
    -   En el Explorador de soluciones, haga clic con el botón derecho en el paquete y, después, haga clic en **Ejecutar paquete**.  
  
### <a name="to-specify-a-different-folder-for-design-time-deployment"></a>Para especificar una carpeta diferente para la implementación en tiempo de diseño  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en la carpeta del proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que quiera ejecutar y, después, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **\<nombre del proyecto> Página de propiedades**, haga clic en **Compilar**.  
  
3.  Actualice el valor de la propiedad OutputPath para especificar la carpeta que quiere usar para la implementación en tiempo de diseño y haga clic en **Aceptar**.  


## <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>Ejecutar un paquete en el servidor SSIS con SQL Server Management Studio
  Después de implementar el proyecto en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , puede ejecutar el paquete en el servidor.  
  
 Puede utilizar los informes de operaciones para ver información sobre los paquetes que se han ejecutado, o que se están ejecutando actualmente, en el servidor. Para obtener más información, consulte [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>Para ejecutar un paquete en el servidor con SQL Server Management Studio  
  
1.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  En el Explorador de objetos, expanda el nodo **Catálogos de Integration Services** , expanda el nodo **SSISDB** y vaya al paquete contenido en el proyecto que ha implementado.  
  
3.  Haga clic con el botón derecho en el nombre del paquete y seleccione **Ejecutar**.  
  
4.  Configure la ejecución del paquete mediante las opciones de las pestañas **Parámetros**, **Administradores de conexión**y **Avanzadas** del cuadro de diálogo **Ejecutar paquete** .  
  
5.  Haga clic en **Aceptar** para ejecutar el paquete.  
  
     -O bien-  
  
     Utilice procedimientos almacenados para ejecutar el paquete. Haga clic en **Script** para generar la instrucción Transact-SQL que crea una instancia de la ejecución y la inicia. La instrucción incluye una llamada a los procedimientos almacenados catalog.create_execution, catalog.set_execution_parameter_value y catalog.start_execution. Para obtener más información sobre estos procedimientos almacenados, vea [catalog.create_execution &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) y [catalog.start_execution &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).  

## <a name="execute_package_dialog"></a> Execute Package Dialog Box
  Use el cuadro de diálogo **Ejecutar paquete** para ejecutar un paquete que está almacenado en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] puede contener parámetros que hagan referencia a valores almacenados en variables de entorno. Antes de ejecutar este tipo de paquete, debe especificar qué referencia del entorno se utilizará para proporcionar los valores de la variable de entorno. Un proyecto puede contener varios entornos, pero se puede utilizar solo un entorno para enlazar los valores de variable de entorno en el momento de la ejecución. Si no se usan variables de entorno en el paquete, no se requiere un entorno.  
  
 ¿Qué desea hacer?  
  
-   [Abrir el cuadro de diálogo Ejecutar paquete](#open_dialog)  
  
-   [Establecer las opciones de la página General](#general)  
  
-   [Establecer las opciones de la pestaña Parámetros](#parameters)  
  
-   [Establecer las opciones de la pestaña Administradores de conexiones](#connection)  
  
-   [Establecer las opciones de la pestaña Avanzadas](#advanced)  
  
-   [Scripting de las opciones del cuadro de diálogo Ejecutar paquete](#script)  
  
###  <a name="open_dialog"></a> Abrir el cuadro de diálogo Ejecutar paquete  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese al servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Se conectará a la instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda la base de datos SSISDB.  
  
2.  En el Explorador de objetos, expanda el árbol para que se muestre el nodo **Catálogos de Integration Services** .  
  
3.  Expanda el nodo **SSISDB** .  
  
4.  Expanda la carpeta que contiene el paquete que desea ejecutar.  
  
5.  Haga clic con el botón derecho en el paquete y, después, haga clic en **Ejecutar**.  
  
###  <a name="general"></a> Establecer las opciones de la página General  
 Seleccione **Entorno** para especificar el entorno que se aplica cuando se ejecuta el paquete.  
  
###  <a name="parameters"></a> Establecer las opciones de la pestaña Parámetros  
 Utilice la pestaña **Parámetros** para modificar los valores de parámetro que se utilizan cuando se ejecuta el paquete.  
  
###  <a name="connection"></a> Establecer las opciones de la pestaña Administradores de conexiones  
 Utilice la pestaña Administradores de conexiones para establecer las propiedades de los administradores de conexiones del paquete.  
  
###  <a name="advanced"></a> Establecer las opciones de la pestaña Avanzadas  
 Utilice la pestaña Avanzadas para administrar propiedades y otra configuración del paquete.  
  
 **Agregar**, **Editar**, **Quitar**  
 Haga clic para agregar, editar o quitar una propiedad.  
  
 **Nivel de registro**  
 Seleccione el nivel de registro de la ejecución del paquete. Para más información, vea [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md).  
  
 **Volcado de errores**  
 Especifique si se crea un archivo de volcado cuando se producen errores durante la ejecución del paquete. Para obtener más información, consulte [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
 **Tiempo de ejecución de 32 bits**  
 Especifique que el paquete se ejecutará en un sistema de 32 bits.  
  
###  <a name="script"></a> Scripting de las opciones del cuadro de diálogo Ejecutar paquete  
 Mientras está en el cuadro de diálogo **Ejecutar paquete** , también puede utilizar el botón **Script** de la barra de herramientas para escribir código de [!INCLUDE[tsql](../../includes/tsql-md.md)] . El script generado realiza una llamada a los procedimientos almacenados [catalog.start_execution &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) con las mismas opciones que ha seleccionado en el cuadro de diálogo **Ejecutar paquete**. El script aparece en una nueva ventana de script en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  

## <a name="see-also"></a>Ver también  
 [dtexec (utilidad)](../../integration-services/packages/dtexec-utility.md)   
[Start the SQL Server Import and Export Wizard](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)
  
  
