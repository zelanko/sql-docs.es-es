---
title: "Habilitar el registro para la ejecuci&#243;n de paquetes en el servidor SSIS | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL13.SSIS.SSMS.ISMANAGECUSTOMIZEDLOGGINGLEVEL.F1"
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# Habilitar el registro para la ejecuci&#243;n de paquetes en el servidor SSIS
  En este tema se describe cómo establecer o cambiar el nivel de registro para un paquete cuando se ejecuta un paquete implementado en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . El nivel de registro que se establece al ejecutar el paquete invalida el registro de paquete configurado en tiempo de diseño en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Vea [Habilitar el registro de paquetes en SQL Server Data Tools](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md) para obtener más información.  
  
 En **Propiedades del servidor** de SQL Server, en la propiedad **Server logging level** (Nivel de registro de servidor), puede seleccionar un nivel de registro predeterminado de todo el servidor. Puede elegir entre uno de los niveles de registro integrados que se describen en este tema o puede elegir un nivel de registro personalizado existente. El nivel de registro seleccionado se aplica de manera predeterminada a todos los paquetes que se implementen en el catálogo de SSIS. También se aplica de forma predeterminada a un paso de trabajo del Agente SQL que ejecuta un paquete SSIS.  
  
 También puede especificar el nivel de registro de un paquete individual mediante uno de los métodos siguientes. En este tema se trata el primer método.  
  
-   Configurar una instancia de una ejecución de paquetes mediante el cuadro de diálogo Ejecutar paquete  
  
-   Configurar parámetros para una instancia de una ejecución mediante [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
-   Configurar un trabajo del Agente SQL Server para una ejecución de paquetes mediante el cuadro de diálogo Nuevo paso de trabajo.  
  
## Establecer el nivel de registro de un paquete mediante el cuadro de diálogo Ejecutar paquete  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], navegue hasta el paquete en el Explorador de objetos.  
  
2.  Haga clic con el botón derecho en el paquete y seleccione **Ejecutar**.  
  
3.  Seleccione la pestaña **Avanzadas** en el cuadro de diálogo **Ejecutar paquete** .  
  
4.  En **Nivel de registro**, seleccione el nivel de registro. Este tema contiene una descripción de los valores disponibles.  
  
5.  Complete otras configuraciones de paquetes que desee y haga clic en **Aceptar** para ejecutar el paquete.  
  
## Seleccionar un nivel de registro  
 Están disponibles los siguientes niveles de registro integrados. También puede seleccionar un nivel de registro personalizado existente. Este tema contiene una descripción de los niveles de registro personalizados.  
  
|Nivel de registro|Description|  
|-------------------|-----------------|  
|None|El registro está desactivado. Solo se registra el estado de ejecución del paquete.|  
|Básico|Se registran todos los eventos, excepto los eventos personalizados y de diagnóstico. Es el valor predeterminado.|  
|RuntimeLineage|Recopila los datos necesarios para realizar un seguimiento de la información de linaje en el flujo de datos. Puede analizar esta información de linaje para asignar la relación de linaje entre las tareas. Los ISV y los desarrolladores pueden generar herramientas de asignación de linaje personalizadas con esta información.|  
|Rendimiento|Solo se registran las estadísticas de rendimiento, y los eventos OnError y OnWarning.<br /><br /> El informe **Rendimiento de la ejecución** muestra el Tiempo activo y el TIempo total para los componentes de flujo de datos del paquete. Esta información está disponible cuando el nivel de registro de la última ejecución del paquete se estableció en **Performance** (Rendimiento) o **Verbose**(Detallado). Para obtener más información, consulte [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md).<br /><br /> La vista [catalog.execution_component_phases](../../integration-services/system-views/catalog-execution-component-phases.md) muestra las horas de inicio y de finalización de los componentes de flujo de datos, para cada fase de una ejecución. Esta vista muestra esta información para estos componentes solo cuando el nivel de registro de la ejecución del paquete se estableció en **Rendimiento** o en **Detallado**.|  
|Detallado|Se registran todos los eventos, incluidos los eventos personalizados y de diagnóstico.<br /><br /> Los eventos personalizados incluyen los eventos registrados por las tareas de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obtener más información sobre los eventos personalizados, vea [Custom Messages for Logging](../../integration-services/performance/custom-messages-for-logging.md).<br /><br /> Un ejemplo de un evento de diagnóstico es el evento **DiagnosticEx** . Cada vez que una tarea Ejecutar paquete ejecuta un paquete secundario, este evento captura los valores de parámetro que se pasan a los paquetes secundarios.<br /><br /> El evento **DiagnosticEx** también le ayuda a obtener los nombres de las columnas en las que se producen errores de nivel de fila. Este evento escribe un mapa de linaje de flujo de datos en el registro. Luego, puede buscar el nombre de columna en este mapa de linaje mediante el identificador de columna que captura una salida de error.  Para obtener más información, vea [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md).<br /><br /> El valor de la columna de mensaje para **DiagnosticEx** es texto XML. Para ver el texto de mensaje para la ejecución del paquete, consulte la vista [catalog.operation_messages &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md). Tenga en cuenta que el evento **DiagnosticEx** no conserva el espacio en blanco en la salida XML para reducir el tamaño del registro. Para mejorar la legibilidad, copie el registro en un editor XML (en Visual Studio, por ejemplo) que admita el formato XML y el resaltado de sintaxis.<br /><br /> La vista [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) muestra una fila cada vez que un componente de flujo de datos envía datos a un componente de nivel inferior para una ejecución del paquete. El nivel de registro se debe establecer en **Detallado** para capturar esta información en la vista.|  
  
## Crear y administrar niveles de registro personalizados mediante el cuadro de diálogo de administración de niveles de registro personalizados  
 Puede crear niveles de registro personalizados que solo recopilen las estadísticas y los eventos que quiera. También puede capturar el contexto de los eventos, que incluye valores de variables, cadenas de conexión y propiedades de componentes. Cuando ejecuta un paquete, puede seleccionar un nivel de registro personalizado en el que puede seleccionar un nivel de registro integrado.  
  
> [!TIP]  
>  Para capturar los valores de las variables de paquete, la propiedad **IncludeInDebugDump** de las variables debe estar establecida en **True**.  
  
1.  Para crear y administrar niveles de registro personalizados, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en la base de datos SSISDB y seleccione **Customized Logging Level** (Nivel de registro personalizado) para abrir el cuadro de diálogo **Administración del nivel de registro personalizado**. La lista **Customized Logging Levels** (Niveles de registro personalizados) contiene todos los niveles de registro personalizados existentes.  
  
2.  Para **crear** un nuevo registro personalizado, haga clic en **Create**(Crear) y proporcione un nombre y una descripción. En las pestañas **Statistics** (Estadísticas) y **Events** (Eventos), seleccione las estadísticas y los eventos que quiera recopilar. En la pestaña **Events** (Eventos), seleccione opcionalmente **Include Context** (Incluir contexto) para los eventos individuales. A continuación, haga clic en **Save**(Guardar).  
  
3.  Para **actualizar** un nivel de registro personalizado existente, selecciónelo en la lista, vuelva a configurarlo y haga clic en **Save**(Guardar).  
  
4.  Para **eliminar** un nivel de registro personalizado existente, selecciónelo en la lista y haga clic en **Delete**(Eliminar).  
  
 **Permisos para los niveles de registro personalizados.**  
  
-   Todos los usuarios de la base de datos SSISDB pueden ver los niveles de registro personalizados y seleccionar uno al ejecutar paquetes.  
  
-   Solo los usuarios del rol ssis_admin o sysadmin pueden crear, actualizar o eliminar niveles de registro personalizados.  
  
## Vea también  
 [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)   
 [Habilitar el registro de paquetes en SQL Server Data Tools](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)  
  
  