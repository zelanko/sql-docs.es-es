---
title: Tarea Monitor de eventos WMI | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.wmieventwatchertask.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Event Watcher task [Integration Services]
ms.assetid: b5bb52e9-a77e-41e1-93f9-d4c3bc6b2c9a
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: f91107cf76f48f60b23b7ee1f0f93352468a1422
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="wmi-event-watcher-task"></a>Tarea Monitor de eventos WMI
  La tarea Monitor de eventos WMI supervisa un evento de Instrumental de administración de Windows (WMI) mediante una consulta de evento de Lenguaje de consulta de Instrumental de administración (WQL) para especificar los eventos de interés. Puede usar la tarea Monitor de eventos WMI para los siguientes fines:  
  
-   Esperar la notificación de que se han agregado archivos a una carpeta y luego iniciar el procesamiento del archivo.  
  
-   Ejecutar un paquete que elimine archivos cuando la memoria disponible en un servidor alcance un porcentaje inferior al especificado.  
  
-   Controlar la instalación de una aplicación y luego ejecutar un paquete que usa la aplicación.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye una tarea que lee información de WMI.  
  
 Para obtener más información sobre esta tarea, haga clic en el tema siguiente:  
  
-   [Tarea Lector de datos WMI](../../integration-services/control-flow/wmi-data-reader-task.md)  
  
## <a name="wql-queries"></a>Consultas WQL  
 WQL es un dialecto de SQL con extensiones para admitir la notificación de eventos de WMI y otras características específicas de WMI. Para obtener más información sobre WQL, vea la documentación sobre Instrumental de administración de Windows en [MSDN Library](http://go.microsoft.com/fwlink/?linkid=62553).  
  
> [!NOTE]  
>  Las clases de WMI varían en las diferentes versiones de Windows.  
  
 La siguiente consulta supervisa la notificación de que el uso de la CPU supera el 40 por ciento.  
  
```  
SELECT * from __InstanceModificationEvent WITHIN 2 WHERE TargetInstance ISA 'Win32_Processor' and TargetInstance.LoadPercentage > 40  
```  
  
 La siguiente consulta detecta la notificación de que se ha agregado un archivo a una carpeta.  
  
```  
SELECT * FROM __InstanceCreationEvent WITHIN 10 WHERE TargetInstance ISA "CIM_DirectoryContainsFile" and TargetInstance.GroupComponent= "Win32_Directory.Name=\"c:\\\\WMIFileWatcher\""   
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-event-watcher-task"></a>Mensajes de registro personalizados disponibles en la tarea Monitor de eventos WMI  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Monitor de eventos WMI. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada del registro|Description|  
|---------------|-----------------|  
|**WMIEventWatcherEventOccurred**|Indica que ocurrió un evento que supervisaba la tarea.|  
|**WMIEventWatcherTimedout**|Indica que se superó el tiempo de espera de la tarea.|  
|**WMIEventWatcherWatchingForWMIEvents**|Indica que la tarea inició la ejecución de la consulta WQL. La entrada incluye la consulta.|  
  
## <a name="configuration-of-the-wmi-event-watcher-task"></a>Configuración de la tarea Monitor de eventos WMI  
 Puede configurar la tarea Lector de datos WMI de las maneras siguientes:  
  
-   Especificar el administrador de conexiones WMI que se debe usar.  
  
-   Especificar el origen de la consulta WQL. El origen puede ser externo con respecto a la tarea, una variable o un archivo, o la consulta se puede almacenar en una propiedad de tarea.  
  
-   Especificar la acción realizada por la tarea cuando se produce el evento WMI. Puede registrar la notificación de eventos y el estado después del evento, o activar eventos personalizados de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que proporcionen información asociada con el evento WMI, la notificación y el estado después del evento.  
  
-   Definir de qué manera la tarea responde ante el evento. La tarea se puede configurar para realizarse correctamente o generar un error, según el evento, o la tarea puede supervisar el evento nuevamente.  
  
-   Especificar la acción realizada por la tarea cuando se agota el tiempo de espera de la consulta WMI. Puede registrar el tiempo de espera y el estado después del tiempo de espera, o activar un evento personalizado de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , que indique que se agotó el tiempo de espera del evento WMI y que registre el tiempo de espera y el estado del tiempo de espera.  
  
-   Definir de qué manera la tarea responde ante el tiempo de espera. La tarea se puede configurar para realizarse correctamente o presentar un error, o la tarea puede detectar el evento nuevamente.  
  
-   Especificar la cantidad de veces que la tarea supervisa el evento.  
  
-   Especificar el tiempo de espera.  
  
 Si el origen es un archivo, la tarea Monitor de eventos WMI usa un administrador de conexiones de archivos para conectarse al archivo. Para más información, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 La tarea Monitor de eventos WMI usa un administrador de conexiones WMI para conectarse al servidor desde el cual lee la información de WMI. Para más información, consulte [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Monitor de eventos WMI &#40;página General&#41;](../../integration-services/control-flow/wmi-event-watcher-task-editor-general-page.md)  
  
-   [Editor de la tarea Monitor de eventos WMI &#40;página Opciones WMI&#41;](../../integration-services/control-flow/wmi-event-watcher-task-editor-wmi-options-page.md)  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-wmi-event-watcher-task"></a>Configuración mediante programación de la tarea Monitor de eventos WMI  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiEventWatcherTask.WmiEventWatcherTask>  
  
  
