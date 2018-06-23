---
title: Herramientas para solucionar problemas de la ejecución de paquetes
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: f18d6ff6-e881-444c-a399-730b52130e7c
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 37c82e4f4977e9749413a29fd539379476b29c47
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107682"
---
# <a name="troubleshooting-tools-for-package-execution"></a>Herramientas para solucionar problemas con la ejecución de paquetes
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye características y herramientas que puede utilizar para solucionar problemas de los paquetes durante su ejecución, después de que los paquetes se hayan completado e implementado.  
  
 En tiempo de diseño, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] proporciona puntos de interrupción para pausar la ejecución de los paquetes, la ventana de progreso y los visores de datos para ver los datos a medida que pasan por el flujo de datos. Sin embargo, estas características no están disponibles cuando se ejecutan paquetes que se han implementado. Las principales técnicas para solucionar problemas de paquetes implementados son las siguientes:  
  
-   Detectar y controlar errores de paquetes mediante controladores de eventos.  
  
-   Capturar datos incorrectos mediante las salidas de error.  
  
-   Realizar un seguimiento de los pasos en la ejecución de paquetes mediante el registro.  
  
 También se pueden aplicar las siguientes sugerencias y técnicas para evitar la generación de problemas al ejecutar paquetes:  
  
-   **Ayudar a garantizar la integridad de los datos mediante el uso de transacciones**. Para obtener más información, consulte [Transacciones de Integration Services](../integration-services-transactions.md).  
  
-   **Reiniciar los paquetes desde el momento del error mediante el uso de puntos de comprobación**. Para obtener más información, vea [Reiniciar paquetes de usando puntos de comprobación](../packages/restart-packages-by-using-checkpoints.md).  
  
## <a name="catch-and-handle-package-errors-by-using-event-handlers"></a>Detectar y controlar errores de paquetes mediante controladores de eventos  
 Se puede responder a los diversos eventos que generan el paquete y los objetos del paquete utilizando controladores de eventos.  
  
-   **Crear un controlador de eventos para el evento OnError**. En el controlador de eventos, puede utilizar una tarea Enviar correo para notificar sobre el error a un administrador, emplear una tarea Script y la lógica personalizada a fin de obtener información del sistema para solucionar problemas, o bien limpiar recursos temporales o salidas incompletas. Para más información, vea [Controladores de eventos de Integration Services &#40;SSIS&#41;](../integration-services-ssis-event-handlers.md).  
  
## <a name="troubleshoot-bad-data-by-using-error-outputs"></a>Solución de problemas de datos incorrectos mediante las salidas de error  
 Se puede utilizar la salida de error disponible en varios componentes de flujo de datos para dirigir las filas que contienen errores a un destino independiente para su análisis posterior.  
  
-   **Capturar datos incorrectos mediante las salidas de error**. Envíe las filas que contengan errores a un destino independiente, como una tabla de errores o un archivo de texto. Automáticamente, la salida de error agrega dos columnas numéricas que contienen el número de error que causó el rechazo de la fila y el Id. de la columna en la que se produjo el error. Para obtener más información, vea [Control de errores en los datos](../data-flow/error-handling-in-data.md).  
  
-   **Agregar información descriptiva a las salidas de error**. Se puede facilitar el análisis de la salida de error agregando información descriptiva a los dos identificadores numéricos que proporciona la salida de error.  
  
     **Agregue la descripción del error**. Es sencillo buscar la descripción de un error mediante un componente de script. Para obtener más información, consulte [mejorar una salida de Error para el componente de Script](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md).  
  
     **Agregue el nombre de la columna de error**. No es sencillo buscar en el componente de script el nombre de la columna que corresponde al Id. de columna guardado por la salida de error, y se requieren pasos adicionales. Cada Id. de columna de un flujo de datos es único dentro de esa tarea Flujo de datos y se mantiene en el paquete en tiempo de diseño. A continuación se sugiere un enfoque posible para agregar el nombre de columna a la salida de error. Para obtener un ejemplo de cómo utilizar este enfoque, consulte [agregar el nombre de columna de error a una salida de error](http://go.microsoft.com/fwlink/?LinkId=261546) en dougbert.com.  
  
    1.  **Crear una tabla de búsqueda de nombres de columna**. Cree una aplicación independiente que use la API de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para establecer una iteración en cada paquete guardado, cada flujo de datos del paquete, cada objeto del flujo de datos, y cada entrada y salida del objeto de flujo de datos. La aplicación deberá almacenar el Id. y el nombre de columna de cada columna en una tabla de búsqueda, junto con el Id. de la tarea Flujo de datos primaria y el Id. del paquete.  
  
    2.  **Agregue el nombre de columna a la salida de**. Agregue una transformación Búsqueda a la salida de error que busque el nombre de columna en la tabla de búsqueda creada en el paso anterior. La búsqueda puede utilizar el Id. de columna en la salida de error, el Id. de paquete (disponible en la variable del sistema System::PackageID) y el Id. de la tarea Flujo de datos (disponible en la variable del sistema System::TaskID).  
  
## <a name="troubleshoot-package-execution-by-using-operations-reports"></a>Solucionar problemas de ejecución de paquetes mediante informes de operaciones  
 Los informes de operaciones estándar se encuentran disponibles en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] al objeto de ayudarle a supervisar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que se han implementado en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Estos informes sobre paquetes le ayudan a ver el estado e historial y, si fuera necesario, identificar la causa de los errores de ejecución.  
  
 Para obtener más información, consulte [Troubleshooting Reports for Package Execution](troubleshooting-reports-for-package-execution.md).  
  
## <a name="troubleshoot-package-execution-by-using-ssisdb-views"></a>Solución de problemas de la ejecución de paquetes mediante vistas de SSISDB  
 Se encuentran disponibles diversas vistas de la base de datos de SSISDB, las cuales puede consultar para supervisar la ejecución de paquetes y otra información sobre operaciones. Para obtener más información, consulte [para ejecuciones de paquetes y otras operaciones de supervisión](../performance/monitor-running-packages-and-other-operations.md).  
  
## <a name="troubleshoot-package-execution-by-using-logging"></a>Solución de problemas de la ejecución de paquetes mediante el registro  
 Al habilitar el registro, se puede hacer un seguimiento de gran parte de lo que sucede en los paquetes en ejecución. Los proveedores de registro capturan información sobre los eventos especificados para su análisis posterior y guardan la información en una tabla de base de datos, un archivo plano, un archivo XML u otro formato de salida compatible.  
  
-   **Habilitar el registro**. Se puede precisar la salida del registro seleccionando solamente los eventos y solamente los datos que desea capturar. Para más información, vea [Registro de Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) y [Registro de Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md).  
  
-   **Seleccione el evento Diagnostic del paquete para solucionar problemas relativos al proveedor.** Existen una serie de mensajes de registro que pueden ayudarle a solucionar problemas relacionados con la interacción de un paquete con orígenes de datos externos. Para obtener más información, consulte [Troubleshooting Tools Package Connectivity](troubleshooting-tools-for-package-connectivity.md).  
  
-   **Mejorar la salida predeterminada del registro**. Normalmente, el registro anexa filas al destino de registro cada vez que se ejecuta un paquete. Si bien cada fila de la salida del registro identifica el paquete por su nombre e identificador único, y también identifica la ejecución del paquete mediante un ExecutionID único, la gran cantidad de datos de salida del registro incluidos en una sola lista puede ser difícil de analizar.  
  
     A continuación se sugiere un enfoque posible para mejorar la salida predeterminada del registro y facilitar la generación de informes:  
  
    1.  **Crear una tabla primaria que almacene cada ejecución de un paquete**. La tabla primaria solo tendrá una fila para cada ejecución de un paquete y utilizará ExecutionID para establecer vínculos con los registros secundarios de la tabla de registro de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se puede utilizar una tarea Ejecutar SQL al principio de cada paquete para crear esta fila y registrar la hora de inicio. Se puede utilizar otra tarea Ejecutar SQL al final del paquete para actualizar la fila con la hora de finalización, duración y estado.  
  
    2.  **Agregar información de auditoría al flujo de datos**. Se puede utilizar la transformación Auditar para agregar información a las filas del flujo de datos sobre la ejecución de paquetes que creó o modificó cada fila. La transformación Auditar pone a disposición del usuario nueve datos, que incluyen PackageName y ExecutionInstanceGUID. Para obtener más información, consulte [Audit Transformation](../data-flow/transformations/audit-transformation.md). Si existe información personalizada que desearía incluir también en cada fila para fines de auditoría, puede agregar esa información a las filas del flujo de datos utilizando una transformación Columna derivada. Para más información, consulte [Derived Column Transformation](../data-flow/transformations/derived-column-transformation.md).  
  
    3.  **Posibilidad de capturar datos de recuento de filas**. Tenga en cuenta la posibilidad de crear una tabla independiente para almacenar información de recuento de filas, donde cada instancia de ejecución del paquete se identifique mediante su ExecutionID. Utilice la transformación Recuento de filas para guardar el recuento de filas en una serie de variables en puntos clave del flujo de datos. Tras finalizar el flujo de datos, utilice una tarea Ejecutar SQL para insertar la serie de valores en una fila de la tabla para permitir realizar análisis y generar informes posteriormente.  
  
     Para obtener más información sobre este enfoque, vea la sección sobre auditoría y registro del ETL, en las notas del producto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , [Project REAL: Business Intelligence ETL Design Practices](http://go.microsoft.com/fwlink/?LinkId=96602).  
  
## <a name="troubleshoot-package-execution-by-using-debug-dump-files"></a>Solución de problemas de ejecución de paquetes utilizando archivos de volcado de depuración  
 En [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], puede crear archivos de volcado de depuración que proporcionen información sobre la ejecución de un paquete. Para obtener más información, consulte [Generating Dump Files for Package Execution](generating-dump-files-for-package-execution.md).  
  
## <a name="troubleshoot-run-time-validation-issues"></a>Solución de problemas de validación en tiempo de ejecución  
 Puede haber momentos en los que no sea posible conectarse a los orígenes de datos, o en los que no puedan validarse partes del paquete, sin ejecutar primero tareas anteriores del paquete. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye las siguientes características para ayudarle a evitar los errores de validación que, sin su utilización, se producirían como resultado de las siguientes situaciones:  
  
-   **Configurar la propiedad DelayValidation para los elementos del paquete que no son válidos al cargar el paquete**. Puede establecer `DelayValidation` a `True` elementos del paquete cuya configuración no es válido, para evitar errores de validación al cargar el paquete. Por ejemplo, puede haber una tarea Flujo de datos que utilice una tabla de destino inexistente antes de que la tarea de ejecución de SQL cree la tabla en tiempo de ejecución. El `DelayValidation` propiedad puede estar habilitada en el nivel de paquete o en el nivel de las tareas y contenedores individuales incluidos en el paquete.  
  
     El `DelayValidation` propiedad puede establecerse en una tarea de flujo de datos, pero no en datos individuales componentes de flujo. Se puede obtener un resultado similar estableciendo la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> para componentes individuales de flujo de datos en `false`. Sin embargo, cuando el valor de esta propiedad es `false`, el componente no es consciente de los cambios en los metadatos de orígenes de datos externos. Cuando se establece en `true`, el <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> propiedad puede ayudar a evitar problemas de bloqueo causados por bloqueos en la base de datos, especialmente cuando el paquete está utilizando transacciones.  
  
## <a name="troubleshoot-run-time-permissions-issues"></a>Solución de problemas de permisos en tiempo de ejecución  
 Si surgen errores al intentar ejecutar paquetes implementados mediante el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede suceder que las cuentas que utiliza el Agente no cuenten con los permisos necesarios. Para obtener información sobre cómo solucionar problemas de los paquetes que se ejecutan desde trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea el artículo [Un paquete SSIS no se ejecuta al llamar al paquete SSIS desde un paso de trabajo de Agente SQL Server](http://support.microsoft.com/kb/918760). Para más información sobre cómo ejecutar paquetes desde trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Trabajos del Agente SQL Server para paquetes](../packages/sql-server-agent-jobs-for-packages.md).  
  
 Para establecer conexión con orígenes de datos de Excel o Access, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesita una cuenta que tenga permiso para leer, escribir, crear y eliminar archivos temporales en la carpeta especificada por las variables de entorno TMP y TEMP.  
  
## <a name="troubleshoot-64-bit-issues"></a>Solución de problemas de la modalidad de 64 bits  
  
-   **Algunos proveedores de datos no están disponibles en la plataforma de 64 bits**. En concreto, el proveedor OLE DB para [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet, que se necesita para la conexión a orígenes de datos de Excel o Access, no está disponible en una versión de 64 bits.  
  
## <a name="troubleshoot-errors-without-a-description"></a>Solución de problemas de errores sin descripción  
 Si se encuentra un error de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que no tiene ninguna descripción asociada, puede ver la descripción en [Referencia de errores y mensajes de Integration Services](../integration-services-error-and-message-reference.md) buscando el error por su número. En este momento, la lista no incluye información sobre cómo solucionar problemas.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Configurar una salida de Error en un componente de flujo de datos](../configure-an-error-output-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada de blog [Agregar el nombre de columna de error a una salida de error](http://go.microsoft.com/fwlink/?LinkId=261546), en dougbert.com.  
  
  