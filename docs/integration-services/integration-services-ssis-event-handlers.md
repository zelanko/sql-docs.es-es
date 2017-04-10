---
title: "Controladores de eventos de Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "paquetes de Integration Services, eventos"
  - "tiempo de ejecución [Integration Services]"
  - "paquetes de SQL Server Integration Services, eventos"
  - "controladores de eventos [Integration Services], acerca de los controladores de eventos"
  - "eventos [Integration Services]"
  - "paquetes [Integration Services], eventos"
  - "controladores de eventos [Integration Services]"
  - "paquetes SSIS, eventos"
  - "contenedores [Integration Services], eventos"
  - "eventos [Integration Services], acerca de los eventos"
ms.assetid: 6f60cf93-35dc-431c-908d-2049c4ab66ba
caps.latest.revision: 52
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 51
---
# Controladores de eventos de Integration Services (SSIS)
  En el tiempo de ejecución, los ejecutables (paquetes y contenedores de bucles Foreach, bucles For, de secuencia y de host de tarea) producen eventos. Por ejemplo un evento OnError se produce cuando se genera un error. Puede crear controladores de eventos personalizados para estos eventos con el fin de ampliar la funcionalidad de paquetes y facilitar la administración de paquetes en el tiempo de ejecución. Los controladores de eventos pueden realizar tareas tales como las siguientes:  
  
-   Limpiar un almacén temporal de datos cuando un paquete o tarea termina de ejecutarse.  
  
-   Recuperar la información de sistema para evaluar la disponibilidad de los recursos antes de que el paquete se ejecute.  
  
-   Actualizar datos en una tabla cuando se produce un error en una búsqueda en una tabla de referencia.  
  
-   Enviar un mensaje de correo electrónico cuando se produce un error o una advertencia, o cuando se genera un error en una tarea.  
  
 Si un evento no tiene controlador de eventos, el evento se desencadena en el siguiente contenedor en sentido ascendente en la jerarquía de contenedores en un paquete. Si este contenedor tiene un controlador de eventos, éste se ejecuta en respuesta al evento. En caso contrario, el evento se desencadena en el siguiente contenedor en sentido ascendente en la jerarquía de contenedores.  
  
 El diagrama siguiente muestra un paquete simple que tiene un contenedor de bucles For que contiene una tarea Ejecutar SQL.  
  
 ![Paquete, bucle For, host de tarea y tarea Ejecutar SQL](../integration-services/media/mw-dts-eventhandlerpkg.gif "Paquete, bucle For, host de tarea y tarea Ejecutar SQL")  
  
 Solo el paquete tiene un controlador de eventos, para su evento **OnError** . Si se produce un error cuando se ejecuta una tarea Ejecutar SQL, se ejecuta el controlador de eventos **OnError** para el paquete. El siguiente diagrama muestra la secuencia de llamadas que produce el controlador de eventos **OnError** para que se ejecute el paquete.  
  
 ![Flujo del controlador de eventos](../integration-services/media/mw-dts-eventhandlers.gif "Flujo del controlador de eventos")  
  
 Los controladores de eventos son miembros de una colección de controladores de eventos y todos los contenedores incluyen esta colección. Si crea el paquete mediante el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , puede ver los miembros de las colecciones de controladores de eventos en las carpetas **Controladores de eventos** en la pestaña **Explorador de paquetes** del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 Puede configurar el contenedor del controlador de eventos de las maneras siguientes:  
  
-   Especifique un nombre y una descripción para el controlador de eventos.  
  
-   Indique si se ejecuta el controlador de eventos, si se produce un error en el paquete cuando se produce un error en el controlador de eventos, y la cantidad de errores que se pueden producir antes de que se produzca un error en el controlador de eventos.  
  
-   Especifique un resultado de ejecución que se debe devolver en lugar del resultado de ejecución real que el controlador de eventos devuelve en el tiempo de ejecución.  
  
-   Especifique la opción de transacción para el controlador de eventos.  
  
-   Especifique el modo de registro que usa el controlador de eventos.  
  
## Contenido del controlador de eventos  
 Crear un controlador de eventos es similar a generar un paquete. Un controlador de eventos tiene tareas y contenedores, que se ordenan en un flujo de control, y un controlador de eventos también puede incluir flujos de datos. El Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] incluye la pestaña **Controladores de eventos** para crear controladores de eventos personalizados.  
  
 También se pueden crear controladores de eventos mediante programación. Para obtener más información, consulte [Controlar eventos mediante programación](../integration-services/building-packages-programmatically/handling-events-programmatically.md).  
  
## Eventos de tiempo de ejecución  
 En la siguiente tabla se enumeran los controladores de eventos que proporciona [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y se describen los eventos de tiempo de ejecución que hacen que el controlador de eventos se ejecute.  
  
|Controlador de eventos|Evento|  
|-------------------|-----------|  
|**OnError**|El controlador de eventos para el evento **OnError** . Este evento es desencadenado por un ejecutable cuando se produce un error.|  
|**OnExecStatusChanged**|El controlador de eventos para el evento **OnExecStatusChanged** . Este evento es desencadenado por un ejecutable cuando se modifica su estado de ejecución.|  
|**OnInformation**|El controlador de eventos para el evento **OnInformation** . Este evento se desencadena durante la validación y ejecución de un ejecutable para proporcionar información. Este evento transmite únicamente información, no errores o advertencias.|  
|**OnPostExecute**|El controlador de eventos para el evento **OnPostExecute** . Este evento es desencadenado por un ejecutable inmediatamente después de haber terminado de ejecutarse.|  
|**OnPostValidate**|El controlador de eventos para el evento **OnPostValidate** . Este evento es desencadenado por un ejecutable cuando termina su validación.|  
|**OnPreExecute**|El controlador de eventos para el evento **OnPreExecute** . Este evento es desencadenado por un ejecutable inmediatamente antes de que se ejecuta.|  
|**OnPreValidate**|El controlador de eventos para el evento **OnPreValidate** . Este evento es desencadenado por un ejecutable cuando se inicia su validación.|  
|**OnProgress**|El controlador de eventos para el evento **OnProgress** . Este evento es desencadenado por un ejecutable cuando el ejecutable realiza un progreso que se puede medir.|  
|**OnQueryCancel**|El controlador de eventos para el evento **OnQueryCancel** . Este evento es desencadenado por un ejecutable para determinar si debe dejar de ejecutarse.|  
|**OnTaskFailed**|El controlador de eventos para el evento **OnTaskFailed** . Este evento es desencadenado por una tarea cuando se produce un error.|  
|**OnVariableValueChanged**|El controlador de eventos para el evento **OnVariableValueChanged** . Este evento es desencadenado por un ejecutable cuando se modifica el valor de una variable. El evento es desencadenado por el ejecutable en el que se define la variable. Este evento no se desencadena si establece la propiedad **RaiseChangeEvent** de la variable en **False**. Para obtener más información, vea [Variables de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md).|  
|**OnWarning**|El controlador de eventos para el evento **OnWarning** . Este evento es desencadenado por un ejecutable cuando se produce una advertencia.|  
  
## Configuración de un controlador de eventos  
 Puede establecer propiedades en la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] o mediante programación.  
  
 Para obtener información sobre cómo establecer estas propiedades en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], vea [Establecer las propiedades de tareas o contenedores](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md).  
  
 Para obtener información sobre cómo establecer mediante programación estas propiedades, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>.  
  
## Tareas relacionadas  
 Para obtener información sobre cómo agregar un controlador de eventos a un paquete, vea [agregar un controlador de eventos a un paquete](../Topic/Add%20an%20Event%20Handler%20to%20a%20Package.md).  
  
  