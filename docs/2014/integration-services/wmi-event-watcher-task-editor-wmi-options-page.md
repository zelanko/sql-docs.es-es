---
title: Editor de la tarea monitor de eventos WMI (Página opciones WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmieventwatcher.wmiquery.f1
helpviewer_keywords:
- WMI Event Watcher Task Editor
ms.assetid: 525f3de7-a021-4e52-9939-3a83c88f131a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a64ac51999d15ad226894540d3eb2819164e90e2
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85419852"
---
# <a name="wmi-event-watcher-task-editor-wmi-options-page"></a>Editor de la tarea Monitor de eventos WMI (página Opciones WMI)
  Use la página **Opciones WMI** del cuadro de diálogo **Editor de la tarea Monitor de eventos WMI** para especificar el origen de la consulta WQL (Lenguaje de consulta de Instrumental de administración de Windows) y la manera en que la tarea Monitor de eventos WMI responde a los eventos WMI (Instrumentación de Microsoft Windows).  
  
 Para obtener información acerca de esta tarea, vea [WMI Event Watcher Task](control-flow/wmi-event-watcher-task.md). Para más información sobre el lenguaje de consulta de WMI (WQL), vea el tema sobre Instrumental de administración de Windows, [Querying with WQL](https://go.microsoft.com/fwlink/?LinkId=79045)(Realizar consultas con WQL), en MSDN Library.  
  
## <a name="static-options"></a>Opciones estáticas  
 **WMIConnectionName**  
 Seleccione un administrador de conexiones WMI de la lista o haga clic en \<**New WMI Connection...**> para crear un nuevo administrador de conexiones.  
  
 **Temas relacionados** [Administrador de conexiones WMI](connection-manager/wmi-connection-manager.md), [Editor del administrador de conexiones WMI](../../2014/integration-services/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 Seleccione el tipo de origen de la consulta WQL que ejecuta la tarea. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Entrada directa**|Establezca el origen en una consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySource**.|  
|**Conexión de archivos**|Seleccione el archivo que contiene la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySource**.|  
|**Variable**|Establezca el origen en una variable que defina la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySource**.|  
  
 **ActionAtEvent**  
 Especifique si el evento WMI registra el evento e inicia una acción de [!INCLUDE[ssIS](../includes/ssis-md.md)] o si solamente registra el evento.  
  
 **AfterEvent**  
 Especifique si la tarea se realiza correctamente o se produce un error después de recibir el evento WMI, o si la tarea continúa inspeccionando si el evento se vuelve a producir.  
  
 **ActionAtTimeout**  
 Especifique si la tarea registra un tiempo de espera de consulta WMI e inicia un evento de [!INCLUDE[ssIS](../includes/ssis-md.md)] como respuesta o si solamente registra el tiempo de espera.  
  
 **AfterTimeout**  
 Especifique si la tarea se realiza correctamente o se produce un error en respuesta a un tiempo de espera, o si la tarea continúa inspeccionando si se vuelve a producir otro tiempo de espera.  
  
 **NumberOfEvents**  
 Especifique el número de eventos a inspeccionar.  
  
 **Tiempo de espera**  
 Especifique el número de segundos que se debe esperar a que el evento ocurra. Un valor de 0 significa que no rige ningún tiempo de espera.  
  
## <a name="wqlquerysource-dynamic-options"></a>Opciones dinámicas de WQLQuerySource  
  
### <a name="wqlquerysource--direct-input"></a>WQLQuerySource = Entrada directa  
 **WQLQuerySource**  
 Proporcione una consulta o haga clic en el botón de puntos suspensivos (...) y escriba una consulta mediante el cuadro de diálogo **consulta WQL** .  
  
### <a name="wqlquerysource--file-connection"></a>WQLQuerySource = Conexión de archivos  
 **WQLQuerySource**  
 Seleccione un administrador de conexiones de archivos de la lista o haga clic en \<**New connection...**> para crear un nuevo administrador de conexiones.  
  
 **Temas relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="wqlquerysource--variable"></a>WQLQuerySource = Variable  
 **WQLQuerySource**  
 Seleccione una variable de la lista o haga clic \<**New variable...**> para crear una nueva variable.  
  
 **Temas relacionados:** [Integration Services &#40;SSIS&#41; variables](integration-services-ssis-variables.md), [Agregar variable](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea monitor de eventos WMI &#40;página general&#41;](general-page-of-integration-services-designers-options.md)   
 [Página expresiones](expressions/expressions-page.md)   
 [Tarea Lector de datos WMI](control-flow/wmi-data-reader-task.md)  
  
  
