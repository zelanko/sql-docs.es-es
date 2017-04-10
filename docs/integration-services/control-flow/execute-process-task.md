---
title: "Tarea Ejecutar proceso | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.executeprocesstask.f1"
helpviewer_keywords: 
  - "Ejecutar proceso, tarea [Integration Services]"
ms.assetid: aca5a0b5-34a9-45bc-a234-8e63ea51a1ee
caps.latest.revision: 65
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 65
---
# Tarea Ejecutar proceso
  La tarea Ejecutar proceso ejecuta una aplicación o un archivo por lotes como parte de un flujo de trabajo de paquete de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Aunque puede utilizar la tarea Ejecutar proceso para abrir cualquier aplicación estándar, como [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] o [!INCLUDE[ofprword](../../includes/ofprword-md.md)], normalmente la utilizará para ejecutar aplicaciones empresariales o archivos por lotes que trabajen con un origen de datos. Por ejemplo, puede utilizar la tarea Ejecutar proceso para expandir un archivo de texto comprimido. Una vez hecho esto, el paquete puede usar el archivo de texto como origen de datos para el flujo de datos. Otro ejemplo sería utilizar la tarea Ejecutar proceso para ejecutar una aplicación de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] personalizada que genera un informe de ventas diario. Se puede adjuntar este informe a una tarea Enviar correo para reenviarlo a una lista de distribución.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye otras tareas que realizan operaciones de flujo de trabajo, como ejecutar paquetes. Para obtener más información, consulte [Execute Package Task](../../integration-services/control-flow/execute-package-task.md).  
  
## Entradas del registro personalizadas disponibles en la tarea Ejecutar proceso  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Ejecutar proceso. Para más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md) y [Mensajes personalizados para registro](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Entrada del registro|Description|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|Proporciona información sobre el proceso que se configuró para que ejecute la tarea.<br /><br /> Se escriben dos entradas del registro. Una entrada contiene información sobre el nombre y la ubicación del ejecutable que ejecuta la tarea, y la otra entrada registra la salida del ejecutable.|  
|**ExecuteProcessVariableRouting**|Proporciona información acerca de las variables que se enrutan a la entrada y las salidas del ejecutable. Se escriben entradas del registro para stdin (la entrada), stdout (la salida) y stderr (la salida de errores).|  
  
## Configuración de la tarea Ejecutar proceso  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Ejecutar proceso &#40;página General&#41;](../../integration-services/control-flow/execute-process-task-editor-general-page.md)  
  
-   [Editor de la tarea Ejecutar proceso &#40;página Procesar&#41;](../../integration-services/control-flow/execute-process-task-editor-process-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
### Valores de propiedades  
 Cuando la tarea Ejecutar proceso ejecuta una aplicación personalizada, la tarea proporciona la entrada para la aplicación por medio de los métodos siguientes:  
  
-   Una variable que se especifica en la configuración de la propiedad **StandardInputVariable** . Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Usar variables en paquetes](../Topic/Use%20Variables%20in%20Packages.md).  
  
-   Un argumento que se especifica en la configuración de la propiedad **Arguments** . Por ejemplo, si la tarea abre un documento en Word, el argumento puede asignar un nombre al archivo .doc.  
  
 Cuando se pasan varios argumentos a una aplicación personalizada en una tarea Ejecutar proceso, se usan espacios para separarlos. Los argumentos no pueden incluir espacios; de lo contrario, la tarea no se ejecutará. Puede usar una expresión para pasar un valor de variable como argumento. En el ejemplo siguiente, la expresión pasa dos valores de variable como argumentos y usa un espacio para delimitar los argumentos:  
  
 `@variable1 + " " + @variable2`  
  
 Puede usar una expresión para establecer diversas propiedades de la tarea Ejecutar proceso.  
  
 Cuando use la propiedad **StandardInputVariable** para configurar la tarea Ejecutar proceso para proporcionar la entrada, llame al método **Console.ReadLine** desde la aplicación para leer la entrada. Para obtener más información, vea el tema [Console.ReadLine (Método)](http://go.microsoft.com/fwlink/?LinkId=129201), en la Biblioteca de clases de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
 Cuando use la propiedad **Argumentos** para configurar la tarea Ejecutar proceso con el fin de proporcionar la entrada, realice uno de los pasos siguientes para obtener los argumentos:  
  
-   Si usa Microsoft Visual Basic para escribir la aplicación, establezca la propiedad **My.Application.CommandLineArgs** . En el ejemplo siguiente se establece la propiedad **My.Application.CommandLineArgs** para recuperar dos argumentos:  
  
    ```  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     Para obtener más información, vea el tema [My.Application.CommandLineArgs (Propiedad)](http://go.microsoft.com/fwlink/?LinkId=129200)en la Referencia del lenguaje [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .  
  
-   Si escribe la aplicación en Microsoft Visual C#, use el método **Main**.  
  
     Para más información, vea el tema [Argumentos de la línea de comandos (Guía de programación de C#)](http://go.microsoft.com/fwlink/?LinkId=129406) en la Guía de programación de C#.  
  
 La tarea Ejecutar proceso también incluye las propiedades **StandardOutputVariable** y **StandardErrorVariable** para especificar las variables que usan la salida estándar y la salida de errores de la aplicación, respectivamente.  
  
 Además, puede configurar la tarea Ejecutar proceso para especificar un directorio de trabajo, un período de tiempo de espera o un valor que indique que el ejecutable se ejecutó correctamente. La tarea también se puede configurar para que no se complete su ejecución si el código de retorno del ejecutable no coincide con el valor que indica que se ejecutó correctamente o si el ejecutable no se encuentra en la ubicación especificada.  
  
## Configuración mediante programación de la tarea Ejecutar proceso  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## Vea también  
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  