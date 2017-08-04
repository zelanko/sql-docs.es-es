---
title: "Editor de la tarea de lector de datos WMI (página de opciones de WMI) | Documentos de Microsoft"
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
- sql13.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WMI Data Reader Task Editor
ms.assetid: 4b8d4716-882d-41b0-b77e-e0e2741a2cd5
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2d87bb0cfa2ca6a0ad103ac803e6fac662a9d385
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="wmi-data-reader-task-editor-wmi-options-page"></a>Editor de la tarea Lector de datos WMI (página Opciones WMI)
  Use la página **Opciones WMI** del cuadro de diálogo **Editor de la tarea Lector de datos WMI** para especificar el origen de la consulta WQL (Lenguaje de consulta de Instrumental de administración de Windows) y el destino del resultado de la consulta.  
  
 Para obtener información acerca de esta tarea, vea [WMI Data Reader Task](../../integration-services/control-flow/wmi-data-reader-task.md). Para obtener más información sobre WQL (Lenguaje de consulta de WMI), vea el tema de Instrumental de administración de Windows sobre cómo [realizar consultas con WQL](http://go.microsoft.com/fwlink/?LinkId=79045)en MSDN Library.  
  
## <a name="static-options"></a>Opciones estáticas  
 **WMIConnectionName**  
 Seleccione un administrador de conexión de WMI en la lista o haga clic en \< **nueva conexión de WMI...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados**: [Administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager.md), [Editor del administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md).  
  
 **WQLQuerySourceType**  
 Seleccione el tipo de origen de la consulta WQL que ejecuta la tarea. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada directa**|Establezca el origen en una consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySourceType**.|  
|**Conexión de archivos**|Seleccione el archivo que contiene la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySourceType**.|  
|**Variable**|Establezca el origen en una variable que defina la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySourceType**.|  
  
 **OutputType**  
 Especifique si la salida debe ser una tabla de datos, un valor de propiedad o un valor y nombre de propiedad.  
  
 **OverwriteDestination**  
 Especifica si mantener, sobrescribir o anexar a los datos originales en el archivo de destino o variable.  
  
 **DestinationType**  
 Seleccione el tipo de destino de la consulta WQL que ejecuta la tarea. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Conexión de archivos**|Seleccione un archivo donde guardar los resultados de la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **DestinationType**.|  
|**Variable**|Establezca la variable donde almacenar los resultados de la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **DestinationType**.|  
  
## <a name="wqlquerysourcetype-dynamic-options"></a>Opciones dinámicas WQLQuerySourceType  
  
### <a name="wqlquerysourcetype--direct-input"></a>WQLQuerySourceType = Entrada directa  
 **WQLQuerySource**  
 Proporcione una consulta o haga clic en los puntos suspensivos (…) y escriba una consulta mediante el cuadro de diálogo **Consulta WQL** .  
  
### <a name="wqlquerysourcetype--file-connection"></a>WQLQuerySourceType = Conexión de archivos  
 **WQLQuerySource**  
 Seleccione un administrador de conexión de archivos en la lista o haga clic en \< **nueva conexión...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="wqlquerysourcetype--variable"></a>WQLQuerySourceType = Variable  
 **WQLQuerySource**  
 Seleccione una variable en la lista o haga clic en \< **nueva variable...** > para crear una nueva variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Agregar variable](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
## <a name="destinationtype-dynamic-options"></a>Opciones dinámicas DestinationType  
  
### <a name="destinationtype--file-connection"></a>DestinationType = Conexión de archivos  
 **Destino**  
 Seleccione un administrador de conexión de archivos en la lista o haga clic en \< **nueva conexión...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="destinationtype--variable"></a>DestinationType = Variable  
 **Destino**  
 Seleccione una variable en la lista o haga clic en \< **nueva variable...** > para crear una nueva variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Agregar variable](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de tareas de lector de datos WMI &#40; Página general &#41;](../../integration-services/control-flow/wmi-data-reader-task-editor-general-page.md)   
 [Página expresiones](../../integration-services/expressions/expressions-page.md)   
 [Tarea Monitor de eventos WMI](../../integration-services/control-flow/wmi-event-watcher-task.md)  
  
  
