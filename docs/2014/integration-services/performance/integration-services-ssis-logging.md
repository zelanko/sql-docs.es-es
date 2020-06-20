---
title: Registro de Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], logs
- Windows Event log provider [Integration Services]
- XML File log provider [Integration Services]
- SQL Server Profiler, log provider
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- tasks [Integration Services], logs
- logs [Integration Services], log providers
- Integration Services packages, logs
- log providers [Integration Services]
- packages [Integration Services], logs
- Text File log provider
- SQL Server log provider
ms.assetid: 65e17889-371f-4951-9a7e-9932b2d0dcde
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b563160c9cd41a449b4669bb6b17ca43d427ff6e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964725"
---
# <a name="integration-services-ssis-logging"></a>Registro de Integration Services (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye proveedores de registro que se pueden usar para implementar registros en paquetes, contenedores y tareas. Con los registros, se puede capturar información de tiempo de ejecución sobre un paquete, lo que le ayuda a auditar y solucionar los problemas de un paquete cada vez que se ejecuta. Por ejemplo, un registro puede capturar el nombre del operador que ejecutó el paquete y la hora en que el paquete empezó y terminó.  
  
 Puede configurar el ámbito del registro que se realiza durante la ejecución de un paquete en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para más información, vea [Habilitar el registro para la ejecución de paquetes en el servidor SSIS](../enable-logging-for-package-execution-on-the-ssis-server.md).  
  
 También puede incluir el registro al ejecutar un paquete con la utilidad del símbolo del sistema **dtexec**. Para obtener información acerca de los argumentos del símbolo del sistema que admiten registro, vea [dtexec Utility](../packages/dtexec-utility.md).  
  
## <a name="configure-logging-in-sql-server-data-tools"></a>Configurar el registro en SQL Server Data Tools  
 Los registros se asocian a paquetes y se configuran en el nivel de paquete. Cada tarea o contenedor de un paquete puede registrar información en cualquier registro del paquete. Es posible habilitar las tareas y contenedores de un paquete para registro aunque el paquete no lo esté. Por ejemplo, puede habilitar el registro en una tarea Ejecutar SQL sin habilitar el registro en el paquete primario. Un paquete, un contenedor o una tarea pueden escribir en varios registros. Puede habilitar el registro solamente en el paquete, o en cualquier tarea o contenedor individual que incluya el paquete.  
  
 Cuando se agrega el registro a un paquete, se elige el proveedor de registro y la ubicación del registro. El proveedor de registro especifica el formato para los datos del registro: por ejemplo, una base de datos o un archivo de texto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye los siguientes proveedores de registros:  
  
-   El proveedor de registro de archivo de texto, que escribe entradas de registro en archivos de texto ASCII con un formato de valores separados por comas (CSV). La extensión predeterminada de los nombres de archivo de este proveedor es .log.  
  
-   El proveedor de registro del [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , que escribe seguimientos que se pueden ver con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler. La extensión predeterminada de los nombres de archivo de este proveedor es .trc.  
  
    > [!NOTE]  
    >  No se puede usar el proveedor de registro de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] en un paquete que se ejecute en modo de 64 bits.  
  
-   El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de registro, que escribe entradas de registro en la `sysssislog` tabla de una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos.  
  
-   El proveedor de registro de eventos de Windows, que escribe entradas en el registro de aplicación del registro de eventos de Windows en el equipo local.  
  
-   El proveedor de registro de archivos XML, que escribe archivos de registro en un archivo XML. La extensión predeterminada de los nombres de archivo de este proveedor es .xml.  
  
 Si agrega un proveedor de registro a un paquete o configura los registros mediante programación, puede usar un ProgID o ClassID para identificar el proveedor de registro, en lugar de usar los nombres que el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] muestra en el cuadro de diálogo **Configurar registros de SSIS** .  
  
 La siguiente tabla enumera los ProgID y ClassID para los proveedores de registro que incluye [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y la ubicación de los registros en los que los proveedores de registro escriben.  
  
|Proveedor de registro|ProgID|ClassID|Location|  
|------------------|------------|-------------|--------------|  
|Archivo de texto|DTS.LogProviderTextFile|{0A039101-ACC1-4E06-943F-279948323883}|El administrador de conexiones de archivos que utiliza el proveedor de registro especifica la ruta de acceso al archivo de texto.|  
|SQL Server Profiler|DTS.LogProviderSQLProfiler|{E93F6300-AE0C-4916-A7BF-A8D0CE12C77A}|El administrador de conexiones de archivos que utiliza el proveedor de registro especifica la ruta de acceso al archivo usado por [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|SQL Server|DTS.LogProviderSQLServer|{94150B25-6AEB-4C0D-996D-D37D1C4FDEDA}|El administrador de conexiones OLE DB que usa el proveedor de registro especifica la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene la tabla sysssislog con las entradas de registro.|  
|Registro de eventos de Windows|DTS.LogProviderEventLog|{071CC8EB-C343-4CFF-8D58-564B92FCA3CF}|El registro de aplicación del Visor de eventos de Windows contiene la información de registro de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|Archivo XML|DTS.LogProviderXMLFile|{440945A4-2A22-4F19-B577-EAF5FDDC5F7A}|El administrador de conexiones de archivos que utiliza el proveedor de registro especifica la ruta de acceso al archivo XML.|  
  
 También puede crear proveedores de registro personalizados. Para más información, vea [Creating a Custom Log Provider](../extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md).  
  
 Los proveedores de registro de un paquete son miembros de la colección de proveedores de registro del paquete. Cuando crea un paquete e implementa el registro mediante el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , puede ver una lista de los miembros de la colección en las carpetas **Proveedor de registro** en la pestaña **Explorador de paquetes** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Puede configurar un proveedor de registro proporcionando un nombre y descripción para el proveedor de registro y especificando el administrador de conexiones que usa el proveedor de registro. El proveedor de registro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza un administrador de conexiones OLE DB. Todos los proveedores de registro de archivos de texto, de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]y de archivos XML utilizan administradores de conexión de archivos. El proveedor de registro de eventos de Windows no usa un administrador de conexiones, dado que escribe directamente en el registro de eventos de Windows. Para obtener más información, consulte [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md) y [File Connection Manager](../connection-manager/file-connection-manager.md).  
  
### <a name="logging-customization"></a>Personalización del registro  
 Para personalizar el registro de un evento o mensaje personalizado, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona un esquema de la información registrada habitualmente que se puede incluir en entradas del registro. El esquema de registro [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] define la información que puede registrar. Puede seleccionar elementos del esquema de registro para cada entrada del registro.  
  
 Un paquete y sus contenedores y tareas no tienen que registrar la misma información; además, las tareas y contenedores de un mismo paquete pueden registrar diferente información. Por ejemplo, un paquete puede registrar información del operador al iniciarse, una tarea puede registrar el origen del error de la tarea y otra tarea puede registrar la información de cuándo se producen errores. Si un paquete y sus contenedores y tareas utilizan varios registros, se escribirá la misma información en todos los registros.  
  
 Puede seleccionar un nivel de registro adaptado a sus necesidades, especificando los eventos que desea registrar y la información que desea registrar para cada evento. Algunos eventos pueden proporcionarle más información útil que otros. Por ejemplo, puede registrar únicamente el nombre del equipo y del operador para el evento **PreExecute** , y toda la información disponible para el evento **Error** .  
  
 Para evitar que los archivos de registro utilicen una gran cantidad de espacio en disco o evitar el registro excesivo, que podría reducir el rendimiento, puede limitar el registro, seleccionando los eventos y elementos de información específicos que desee registrar. Por ejemplo, puede configurar un registro para capturar únicamente la fecha y el nombre del equipo para cada error.  
  
 En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , puede definir las opciones de registro en el cuadro de diálogo **Configurar registros de SSIS** .  
  
#### <a name="log-schema"></a>Esquema de registro  
 En la tabla siguiente se describen los elementos del esquema de registro.  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|Computer|Nombre del equipo en el que ocurrió el evento del registro.|  
|Operator|La identidad del usuario que inició el paquete.|  
|SourceName|Nombre del contenedor o la tarea en los que ocurrió el evento del registro.|  
|SourceID|Identificador único del paquete; el contenedor de bucles For, bucles Foreach o secuencias, o bien la tarea en la que ocurrió el evento del registro.|  
|ExecutionID|GUID de la instancia de ejecución del paquete.<br /><br /> Nota: Al ejecutar un paquete único, se podrían crear entradas de registro con valores diferentes para el elemento ExecutionID. Por ejemplo, al ejecutar un paquete en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], la fase de validación podría crear entradas de registro con un elemento ExecutionID que corresponda a [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Sin embargo, la fase de ejecución podría crear entradas de registro con un elemento ExecutionID que corresponda a dtshost.exe. Otro ejemplo de esta situación es cuando se ejecuta un paquete que contiene tareas Ejecutar paquete, cada una de las cuales ejecuta un paquete secundario. Estos paquetes secundarios podrían crear entradas de registro que tengan un elemento ExecutionID diferente al de las entradas de registro que crea el paquete principal.|  
|MessageText|Mensaje asociado a la entrada del registro.|  
|DataBytes|Matriz de bytes específica de la entrada del registro. El significado de este campo varía para cada entrada del registro.|  
  
 En la tabla siguiente se describen tres elementos adicionales del esquema del registro que no están disponibles en la pestaña **Detalles** del cuadro de diálogo **Configurar registros de SSIS** .  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|StartTime|Hora en que el contenedor o la tarea empieza a ejecutarse.|  
|EndTime|Hora en que el contenedor o la tarea deja de ejecutarse.|  
|DataCode|Valor entero opcional que suele contener un valor de la enumeración <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> , que indica el resultado de la ejecución del contenedor o tarea:<br /><br /> 0 (correcto)<br /><br /> 1 (error)<br /><br /> 2 (completado)<br /><br /> 3 (cancelado)|  
  
##### <a name="log-entries"></a>Entradas del registro  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] admite entradas del registro en eventos predefinidos y proporciona entradas del registro personalizadas para muchos objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . El cuadro de diálogo **Configurar registros de SSIS** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] enumera estos eventos y entradas del registro personalizadas.  
  
 En la tabla siguiente se describen los eventos predefinidos que se pueden habilitar para escribir entradas del registro cuando se producen eventos en tiempo de ejecución. Estas entradas del registro se aplican a los ejecutables, al paquete y a las tareas y contenedores que incluye el paquete. El nombre de la entrada del registro es el nombre del evento que se produjo en tiempo de ejecución y que originó la entrada del registro.  
  
|Eventos|Descripción|  
|------------|-----------------|  
|**OnError**|Escribe una entrada del registro cuando se produce un error.|  
|**OnExecStatusChanged**|Escribe una entrada del registro cuando una tarea (no un contenedor) se suspende o se reanuda durante la depuración.|  
|**OnInformation**|Escribe una entrada del registro durante la validación y ejecución de un ejecutable, para proporcionar información.|  
|**OnPostExecute**|Escribe una entrada del registro inmediatamente después de que termine de ejecutarse el ejecutable.|  
|**OnPostValidate**|Escribe una entrada del registro cuando finaliza la validación del ejecutable.|  
|**OnPreExecute**|Escribe una entrada del registro inmediatamente antes de que se ejecute el ejecutable.|  
|**OnPreValidate**|Escribe una entrada del registro cuando se inicia la validación del ejecutable.|  
|**OnProgress**|Escribe una entrada del registro cuando el ejecutable realiza un progreso que se puede medir.|  
|**OnQueryCancel**|Escribe una entrada del registro en cualquier momento del procesamiento de la tarea en el que es posible cancelar la ejecución.|  
|**OnTaskFailed**|Escribe una entrada del registro cuando una tarea genera un error.|  
|**OnVariableValueChanged**|Escribe una entrada del registro cuando cambia el valor de una variable.|  
|**OnWarning**|Escribe una entrada del registro cuando se produce una advertencia.|  
|**PipelineComponentTime**|Por cada componente de flujo de datos, escribe una entrada de registro de cada fase de validación y ejecución. La entrada del registro especifica el tiempo de procesamiento para cada fase.|  
|**Diagnostic**|Escribe una entrada de registro que proporciona información de diagnóstico.<br /><br /> Por ejemplo, puede registrar un mensaje antes y después de cada llamada a un proveedor de datos externo. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../troubleshooting/troubleshooting-tools-for-package-execution.md).|  
  
 El paquete y muchas tareas poseen entradas del registro personalizadas que se pueden habilitar para el registro. Por ejemplo, la tarea Enviar correo proporciona la entrada de registro personalizada **SendMailTaskBegin** , que registra información cuando se inicia la ejecución de la tarea Enviar correo, pero antes de que la tarea envíe un mensaje de correo. Para obtener más información, consulte [Custom messages for Logging](../custom-messages-for-logging.md).  
  
### <a name="differentiating-package-copies"></a>Diferenciar copias de paquetes  
 Los datos del registro incluyen el nombre y GUID del paquete al que pertenecen las entradas del registro. Si crea un nuevo paquete mediante la copia de un paquete existente, también se copian el nombre y GUID del paquete existente. Como resultado, puede tener dos paquetes con el mismo nombre y GUID, lo que dificulta la diferenciación entre los paquetes en los datos del registro.  
  
 Para eliminar esta ambigüedad, deberá actualizar el nombre y GUID de los nuevos paquetes. En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], puede volver a generar el GUID en la propiedad `ID` y actualizar el valor de la propiedad `Name` en la ventana Propiedades. También puede cambiar el nombre y GUID mediante programación o con el símbolo del sistema de **dtutil** . Para más información, vea [Establecer las propiedades de paquetes](../set-package-properties.md) y [dtutil (utilidad)](../dtutil-utility.md).  
  
### <a name="parent-logging-options"></a>Opciones del registro primario  
 Con frecuencia, las opciones de registro de tareas y de los contenedores de bucles For y Foreach y de secuencias coinciden con las del paquete o el contenedor primario. En ese caso, puede configurarlas para que hereden las opciones de registro del contenedor primario. Por ejemplo, en un contenedor de bucles For que incluya una tarea Ejecutar SQL, esta tarea puede utilizar las opciones de registro configuradas para el contenedor de bucles For. Para usar las opciones de registro primario, establezca la propiedad LoggingMode del contenedor en **UseParentSetting**. Puede establecer esta propiedad en la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o mediante el cuadro de diálogo **Configurar registros de SSIS** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
### <a name="logging-templates"></a>Plantillas de registro  
 En el cuadro de diálogo **Configurar registros de SSIS** , también puede crear y guardar como plantillas las configuraciones del registro que utiliza con frecuencia y después, utilizar las plantillas en distintos paquetes. Esto permite aplicar más fácilmente una estrategia de registro coherente entre varios paquetes y modificar las configuraciones del registro en los paquetes actualizando las plantillas y aplicándolas después. Las plantillas se almacenan en archivos XML.  
  
 **Para configurar el registro con el cuadro de diálogo Configurar registros de SSIS**  
  
1.  Habilite el paquete y sus tareas para el registro. El registro se puede producir en el nivel de paquete, de contenedor y de tarea. Puede especificar diferentes registros para paquetes, contenedores y tareas.  
  
2.  Seleccione un proveedor de registro y agregue un registro para el paquete. Solo se pueden crear registros en el nivel de paquete y una tarea o un contenedor deben utilizar uno de los registros creados para el paquete. Cada registro está asociado a uno de los proveedores de registro siguientes: archivo de texto, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Registro de eventos de Windows o archivo XML. Para más información, vea [Habilitar el registro de paquetes en SQL Server Data Tools](../enable-package-logging-in-sql-server-data-tools.md).  
  
3.  Seleccione los eventos y la información del esquema de registro de cada evento que desee capturar en el registro. Para más información, vea [Configurar el registro usando un archivo de configuración guardado](../configure-logging-by-using-a-saved-configuration-file.md).  
  
### <a name="configuration-of-log-provider"></a>Configuración de un proveedor de registro  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Un proveedor de registro se crea y configura como un paso en la implementación de registros en un paquete. Para obtener más información, vea [registro de Integration Services](integration-services-ssis-logging.md).  
  
 Después de crear un proveedor de registro, puede ver y modificar sus propiedades en la ventana Propiedades de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Para obtener información sobre cómo establecer estas propiedades mediante programación, vea la documentación de la clase <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> .  
  
### <a name="logging-for-data-flow-tasks"></a>Registrar tareas Flujo de datos  
 La tarea Flujo de datos proporciona varias entradas del registro personalizadas que pueden utilizarse para supervisar y ajustar el rendimiento. Por ejemplo, puede supervisar componentes que puedan causar pérdidas de memoria o realizar un seguimiento del tiempo que lleva ejecutar un componente determinado. Para obtener una lista de las entradas del registro personalizadas y ejemplos de la salida del registro, vea [Data Flow Task](../control-flow/data-flow-task.md).  
  
#### <a name="use-the-pipelinecomponenttime-event"></a>Usar el evento PipelineComponentTime  
 Quizás la entrada de registro personalizada más útil es el evento PipelineComponentTime. Esta entrada de registro notifica el número de milisegundos que cada componente del flujo de datos emplea en cada uno de los cinco pasos de procesamiento principales. En la tabla siguiente se describen estos pasos de procesamiento. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Los desarrolladores reconocerán estos pasos como los métodos principales de <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>.  
  
|Paso|Descripción|  
|----------|-----------------|  
|Validación|El componente comprueba los valores de configuración y los valores de propiedad válidos.|  
|PreExecute|El componente realiza el procesamiento único antes de empezar a procesar filas de datos.|  
|PostExecute|El componente realiza el procesamiento único después de haber procesado todas las filas de datos.|  
|ProcessInput|El componente de transformación o de destino procesa las filas de datos entrantes que un origen o una transformación de nivel superior le han pasado.|  
|PrimeOutput|El componente de origen o de transformación llena los búferes con los datos que se van a pasar a un componente transformación o de destino de nivel inferior.|  
  
 Cuando habilita el evento PipelineComponentTime, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra un mensaje para cada paso de procesamiento realizado por cada componente. Las entradas de registro siguientes muestran un subconjunto de los mensajes que el ejemplo de paquete CalculatedColumns de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra:  
  
 `The component "Calculate LineItemTotalCost" (3522) spent 356 milliseconds in ProcessInput.`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 79 milliseconds in ProcessInput.`  
  
 `The component "Calculate Average Cost" (3662) spent 16 milliseconds in ProcessInput.`  
  
 `The component "Sort by ProductID" (3717) spent 125 milliseconds in ProcessInput.`  
  
 `The component "Load Data" (3773) spent 0 milliseconds in ProcessInput.`  
  
 `The component "Extract Data" (3869) spent 688 milliseconds in PrimeOutput filling buffers on output "OLE DB Source Output" (3879).`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 141 milliseconds in PrimeOutput filling buffers on output "Aggregate Output 1" (3621).`  
  
 `The component "Sort by ProductID" (3717) spent 16 milliseconds in PrimeOutput filling buffers on output "Sort Output" (3719).`  
  
 Estas entradas de registro muestran que la tarea de flujo de datos empleó la mayor parte del tiempo en los pasos siguientes, presentados en orden descendente:  
  
-   El origen de OLE DB, que se denomina "Extract Data", empleó 688 ms en cargar los datos.  
  
-   La transformación de la columna derivada, denominada "Calculate LineItemTotalCost" empleó 356 ms en realizar los cálculos de las filas entrantes.  
  
-   La transformación Agregado denominada “Sum Quantity and LineItemTotalCost” ha usado un tiempo combinado de 220 ms (141 ms en PrimeOutput y 79 ms en ProcessInput) en las operaciones de realizar cálculos y pasar los datos a la transformación siguiente.  
  
## <a name="related-tasks"></a>Related Tasks  
 La lista siguiente contiene vínculos a temas que muestran cómo realizar tareas relacionadas con la característica de registro.  
  
-   [Configurar registros de SSIS, cuadro de diálogo](../configure-ssis-logs-dialog-box.md)  
  
-   [Habilitar el registro de paquetes en SQL Server Data Tools](../enable-package-logging-in-sql-server-data-tools.md)  
  
-   [Habilitar el registro para la ejecución de paquetes en el servidor SSIS](../enable-logging-for-package-execution-on-the-ssis-server.md)  
  
-   [Ver entradas del registro en la ventana Registrar eventos](../view-log-entries-in-the-log-events-window.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [Herramienta DTLoggedExec para el registro completo y detallado (proyecto CodePlex)](https://go.microsoft.com/fwlink/?LinkId=150579)  
  
## <a name="see-also"></a>Consulte también  
 [Ver entradas del registro en la ventana Registrar eventos](../view-log-entries-in-the-log-events-window.md)  
  
  
