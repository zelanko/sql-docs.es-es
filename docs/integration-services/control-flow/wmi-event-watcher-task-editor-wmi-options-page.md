---
title: "Editor de la tarea de Monitor de eventos WMI (página de opciones de WMI) | Documentos de Microsoft"
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
- sql13.dts.designer.wmieventwatcher.wmiquery.f1
helpviewer_keywords:
- WMI Event Watcher Task Editor
ms.assetid: 525f3de7-a021-4e52-9939-3a83c88f131a
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 410a65bf316b27fac565388d09bf4c9f5cd82b29
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="wmi-event-watcher-task-editor-wmi-options-page"></a>Editor de la tarea Monitor de eventos WMI (página Opciones WMI)
  Use la página **Opciones WMI** del cuadro de diálogo **Editor de la tarea Monitor de eventos WMI** para especificar el origen de la consulta WQL (Lenguaje de consulta de Instrumental de administración de Windows) y la manera en que la tarea Monitor de eventos WMI responde a los eventos WMI (Instrumentación de Microsoft Windows).  
  
 Para obtener información acerca de esta tarea, vea [WMI Event Watcher Task](../../integration-services/control-flow/wmi-event-watcher-task.md). Para obtener más información sobre WQL (Lenguaje de consulta de WMI), vea el tema de Instrumental de administración de Windows sobre cómo [realizar consultas con WQL](http://go.microsoft.com/fwlink/?LinkId=79045)en MSDN Library.  
  
## <a name="static-options"></a>Opciones estáticas  
 **WMIConnectionName**  
 Seleccione un administrador de conexión de WMI en la lista o haga clic en \< **nueva conexión de WMI...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados**: [Administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager.md), [Editor del administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md).  
  
 **WQLQuerySourceType**  
 Seleccione el tipo de origen de la consulta WQL que ejecuta la tarea. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada directa**|Establezca el origen en una consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySource**.|  
|**Conexión de archivos**|Seleccione el archivo que contiene la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySource**.|  
|**Variable**|Establezca el origen en una variable que defina la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySource**.|  
  
 **ActionAtEvent**  
 Especifique si el evento WMI registra el evento e inicia una acción de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o si solamente registra el evento.  
  
 **AfterEvent**  
 Especifique si la tarea se realiza correctamente o se produce un error después de recibir el evento WMI, o si la tarea continúa inspeccionando si el evento se vuelve a producir.  
  
 **ActionAtTimeout**  
 Especifique si la tarea registra un tiempo de espera de consulta WMI e inicia un evento de [!INCLUDE[ssIS](../../includes/ssis-md.md)] como respuesta o si solamente registra el tiempo de espera.  
  
 **AfterTimeout**  
 Especifique si la tarea se realiza correctamente o se produce un error en respuesta a un tiempo de espera, o si la tarea continúa inspeccionando si se vuelve a producir otro tiempo de espera.  
  
 **NumberOfEvents**  
 Especifique el número de eventos a inspeccionar.  
  
 **Timeout**  
 Especifique el número de segundos que se debe esperar a que el evento ocurra. Un valor de 0 significa que no rige ningún tiempo de espera.  
  
## <a name="wqlquerysource-dynamic-options"></a>Opciones dinámicas de WQLQuerySource  
  
### <a name="wqlquerysource--direct-input"></a>WQLQuerySource = Entrada directa  
 **WQLQuerySource**  
 Proporcione una consulta o haga clic en el botón de puntos suspensivos (…) y escriba una consulta mediante el cuadro de diálogo **Consulta WQL** .  
  
### <a name="wqlquerysource--file-connection"></a>WQLQuerySource = Conexión de archivos  
 **WQLQuerySource**  
 Seleccione un administrador de conexión de archivos en la lista o haga clic en \< **nueva conexión...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="wqlquerysource--variable"></a>WQLQuerySource = Variable  
 **WQLQuerySource**  
 Seleccione una variable en la lista o haga clic en \< **nueva variable...** > para crear una nueva variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Agregar variable](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de tareas de Monitor de eventos WMI &#40; Página general &#41;](../../integration-services/control-flow/wmi-event-watcher-task-editor-general-page.md)   
 [Página expresiones](../../integration-services/expressions/expressions-page.md)   
 [Tarea lector de datos WMI](../../integration-services/control-flow/wmi-data-reader-task.md)  
  
  
