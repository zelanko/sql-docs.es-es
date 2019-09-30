---
title: Herramientas para solucionar problemas de la ejecución de paquetes
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: f18d6ff6-e881-444c-a399-730b52130e7c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a2c2dc7aac7ae6eb86b66a6bbb371f11dc6372cf
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295083"
---
# <a name="troubleshooting-tools-for-package-execution"></a>Herramientas para solucionar problemas con la ejecución de paquetes

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye características y herramientas que puede utilizar para solucionar problemas de los paquetes durante su ejecución, después de que los paquetes se hayan completado e implementado.  
  
 En tiempo de diseño, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] proporciona puntos de interrupción para pausar la ejecución de los paquetes, la ventana de progreso y los visores de datos para ver los datos a medida que pasan por el flujo de datos. Sin embargo, estas características no están disponibles cuando se ejecutan paquetes que se han implementado. Las principales técnicas para solucionar problemas de paquetes implementados son las siguientes:  
  
-   Detectar y controlar errores de paquetes mediante controladores de eventos.  
  
-   Capturar datos incorrectos mediante las salidas de error.  
  
-   Realizar un seguimiento de los pasos en la ejecución de paquetes mediante el registro.  
  
 También se pueden aplicar las siguientes sugerencias y técnicas para evitar la generación de problemas al ejecutar paquetes:  
  
-   **Ayudar a garantizar la integridad de los datos mediante el uso de transacciones**. Para más información, vea [Transacciones de Integration Services](../../integration-services/integration-services-transactions.md).  
  
-   **Reiniciar los paquetes desde el momento del error mediante el uso de puntos de comprobación**. Para obtener más información, vea [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
## <a name="catch-and-handle-package-errors-by-using-event-handlers"></a>Detectar y controlar errores de paquetes mediante controladores de eventos  
 Se puede responder a los diversos eventos que generan el paquete y los objetos del paquete utilizando controladores de eventos.  
  
-   **Crear un controlador de eventos para el evento OnError**. En el controlador de eventos, puede utilizar una tarea Enviar correo para notificar sobre el error a un administrador, emplear una tarea Script y la lógica personalizada a fin de obtener información del sistema para solucionar problemas, o bien limpiar recursos temporales o salidas incompletas. Para más información, vea [Controladores de eventos de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md).  
  
## <a name="troubleshoot-bad-data-by-using-error-outputs"></a>Solución de problemas de datos incorrectos mediante las salidas de error  
 Se puede utilizar la salida de error disponible en varios componentes de flujo de datos para dirigir las filas que contienen errores a un destino independiente para su análisis posterior. Para más información, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).  
  
-   **Capturar datos incorrectos mediante las salidas de error**. Envíe las filas que contengan errores a un destino independiente, como una tabla de errores o un archivo de texto. Automáticamente, la salida de error agrega dos columnas numéricas que contienen el número de error que causó el rechazo de la fila y el Id. de la columna en la que se produjo el error.  
  
-   **Agregar información descriptiva a las salidas de error**. Se puede facilitar el análisis de la salida de error si se agrega el mensaje de error y el nombre de la columna, además de los dos identificadores numéricos que proporciona la salida de error. Para obtener un ejemplo de cómo agregar estas dos columnas adicionales mediante el uso de scripting, consulte [Mejorar una salida de errores con el componente de script](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md).  
  
-   **O bien, obtenga los nombres de columna mediante el registro del evento DiagnosticEx**. Este evento escribe un mapa de linaje de flujo de datos en el registro. Luego, puede buscar el nombre de columna en este mapa de linaje mediante el identificador de columna que captura una salida de error.  Para obtener más información, vea [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md) (Control de errores en los datos).  
  
     El valor de la columna de mensaje para **DiagnosticEx** es texto XML. Para ver el texto del mensaje de una ejecución de paquete, ejecute una consulta en la vista [catalog.operation_messages &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md). Tenga en cuenta que el evento **DiagnosticEx** no conserva el espacio en blanco en la salida XML para reducir el tamaño del registro. Para mejorar la legibilidad, copie el registro en un editor XML (en Visual Studio, por ejemplo) que admita el formato XML y el resaltado de sintaxis.  
  
## <a name="troubleshoot-package-execution-by-using-operations-reports"></a>Solucionar problemas de ejecución de paquetes mediante informes de operaciones  
 Los informes de operaciones estándar se encuentran disponibles en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] al objeto de ayudarle a supervisar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que se han implementado en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Estos informes sobre paquetes le ayudan a ver el estado e historial y, si fuera necesario, identificar la causa de los errores de ejecución.  
  
 Para obtener más información, consulte [Troubleshooting Reports for Package Execution](../../integration-services/troubleshooting/troubleshooting-reports-for-package-execution.md).  
  
## <a name="troubleshoot-package-execution-by-using-ssisdb-views"></a>Solución de problemas de la ejecución de paquetes mediante vistas de SSISDB  
 Se encuentran disponibles diversas vistas de la base de datos de SSISDB, las cuales puede consultar para supervisar la ejecución de paquetes y otra información sobre operaciones. Para más información, vea [Monitor de ejecución de paquetes y otras operaciones](../../integration-services/performance/monitor-running-packages-and-other-operations.md).  
  
## <a name="troubleshoot-package-execution-by-using-logging"></a>Solución de problemas de la ejecución de paquetes mediante el registro  
 Al habilitar el registro, se puede hacer un seguimiento de gran parte de lo que sucede en los paquetes en ejecución. Los proveedores de registro capturan información sobre los eventos especificados para su análisis posterior y guardan la información en una tabla de base de datos, un archivo plano, un archivo XML u otro formato de salida compatible.  
  
-   **Habilitar el registro**. Se puede precisar la salida del registro seleccionando solamente los eventos y solamente los datos que desea capturar. Para más información, consulte [Registro de Integration Services (SSIS)](../performance/integration-services-ssis-logging.md).  
  
-   **Seleccione el evento Diagnostic del paquete para solucionar problemas relativos al proveedor.** Existen una serie de mensajes de registro que pueden ayudarle a solucionar problemas relacionados con la interacción de un paquete con orígenes de datos externos. Para obtener más información, consulte [Troubleshooting Tools Package Connectivity](troubleshooting-tools-for-package-connectivity.md).  
  
-   **Mejorar la salida predeterminada del registro**. Normalmente, el registro anexa filas al destino de registro cada vez que se ejecuta un paquete. Si bien cada fila de la salida del registro identifica el paquete por su nombre e identificador único, y también identifica la ejecución del paquete mediante un ExecutionID único, la gran cantidad de datos de salida del registro incluidos en una sola lista puede ser difícil de analizar.  
  
     A continuación se sugiere un enfoque posible para mejorar la salida predeterminada del registro y facilitar la generación de informes:  
  
    1.  **Crear una tabla primaria que almacene cada ejecución de un paquete**. La tabla primaria solo tendrá una fila para cada ejecución de un paquete y utilizará ExecutionID para establecer vínculos con los registros secundarios de la tabla de registro de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se puede utilizar una tarea Ejecutar SQL al principio de cada paquete para crear esta fila y registrar la hora de inicio. Se puede utilizar otra tarea Ejecutar SQL al final del paquete para actualizar la fila con la hora de finalización, duración y estado.  
  
    2.  **Agregar información de auditoría al flujo de datos**. Se puede utilizar la transformación Auditar para agregar información a las filas del flujo de datos sobre la ejecución de paquetes que creó o modificó cada fila. La transformación Auditar pone a disposición del usuario nueve datos, que incluyen PackageName y ExecutionInstanceGUID. Para obtener más información, consulte [Audit Transformation](../../integration-services/data-flow/transformations/audit-transformation.md). Si existe información personalizada que desearía incluir también en cada fila para fines de auditoría, puede agregar esa información a las filas del flujo de datos utilizando una transformación Columna derivada. Para más información, consulte [Derived Column Transformation](../../integration-services/data-flow/transformations/derived-column-transformation.md).  
  
    3.  **Posibilidad de capturar datos de recuento de filas**. Tenga en cuenta la posibilidad de crear una tabla independiente para almacenar información de recuento de filas, donde cada instancia de ejecución del paquete se identifique mediante su ExecutionID. Utilice la transformación Recuento de filas para guardar el recuento de filas en una serie de variables en puntos clave del flujo de datos. Tras finalizar el flujo de datos, utilice una tarea Ejecutar SQL para insertar la serie de valores en una fila de la tabla para permitir realizar análisis y generar informes posteriormente.  
  
     Para más información sobre este enfoque, consulte la sección sobre auditoría y registro del ETL, en las notas del producto de [!INCLUDE[msCoName](../../includes/msconame-md.md)], [Project REAL: Business Intelligence ETL Design Practices](https://go.microsoft.com/fwlink/?LinkId=96602).  
  
## <a name="troubleshoot-package-execution-by-using-debug-dump-files"></a>Solución de problemas de ejecución de paquetes utilizando archivos de volcado de depuración  
 En [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], puede crear archivos de volcado de depuración que proporcionen información sobre la ejecución de un paquete. Para obtener más información, consulte [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
## <a name="troubleshoot-run-time-validation-issues"></a>Solución de problemas de validación en tiempo de ejecución  
 Puede haber momentos en los que no sea posible conectarse a los orígenes de datos, o en los que no puedan validarse partes del paquete, sin ejecutar primero tareas anteriores del paquete. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye las siguientes características para ayudarle a evitar los errores de validación que, sin su utilización, se producirían como resultado de las siguientes situaciones:  
  
-   **Configurar la propiedad DelayValidation para los elementos del paquete que no son válidos al cargar el paquete**. Se puede establecer **DelayValidation** en **True** para los elementos del paquete cuya configuración no sea válida, a fin de evitar errores de validación al cargar el paquete. Por ejemplo, puede haber una tarea Flujo de datos que utilice una tabla de destino inexistente antes de que la tarea de ejecución de SQL cree la tabla en tiempo de ejecución. La propiedad **DelayValidation** se puede habilitar en el nivel de paquete o en el de tareas y contenedores individuales incluidos en el paquete.  
  
     Es posible establecer la propiedad **DelayValidation** para una tarea Flujo de datos, pero no para componentes individuales de flujo de datos. Se puede obtener un resultado similar al establecer la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> para componentes individuales de flujo de datos en **false**. No obstante, cuando el valor de esta propiedad es **false**, el componente no detecta los cambios realizados en los metadatos de los orígenes de datos externos. Cuando se establece en **true**, la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> puede ayudar a evitar problemas de bloqueo causados por bloqueos en la base de datos, en especial cuando el paquete usa transacciones.  
  
## <a name="troubleshoot-run-time-permissions-issues"></a>Solución de problemas de permisos en tiempo de ejecución  
 Si surgen errores al intentar ejecutar paquetes implementados mediante el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede suceder que las cuentas que utiliza el Agente no cuenten con los permisos necesarios. Para obtener información sobre cómo solucionar problemas de los paquetes que se ejecutan desde trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea el artículo [Un paquete SSIS no se ejecuta al llamar al paquete SSIS desde un paso de trabajo de Agente SQL Server](https://support.microsoft.com/kb/918760). Para más información sobre cómo ejecutar paquetes desde trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Trabajos del Agente SQL Server para paquetes](../../integration-services/packages/sql-server-agent-jobs-for-packages.md).  
  
 Para establecer conexión con orígenes de datos de Excel o Access, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesita una cuenta que tenga permiso para leer, escribir, crear y eliminar archivos temporales en la carpeta especificada por las variables de entorno TMP y TEMP.  
  
## <a name="troubleshoot-64-bit-issues"></a>Solución de problemas de la modalidad de 64 bits  
  
-   **Algunos proveedores de datos no están disponibles en la plataforma de 64 bits**. En concreto, el proveedor OLE DB para [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet, que se necesita para la conexión a orígenes de datos de Excel o Access, no está disponible en una versión de 64 bits.  
  
## <a name="troubleshoot-errors-without-a-description"></a>Solución de problemas de errores sin descripción  
 Si se encuentra un error de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que no tiene ninguna descripción asociada, puede ver la descripción en [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md) buscando el error por su número. En este momento, la lista no incluye información sobre cómo solucionar problemas.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Depurar el flujo de datos](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada de blog [Agregar el nombre de columna de error a una salida de error](https://go.microsoft.com/fwlink/?LinkId=261546), en dougbert.com.  
