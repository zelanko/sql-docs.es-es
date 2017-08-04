---
title: "Editor de tareas de cola de mensajes (página recibir) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.msgqueuetask.receive.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 7028756d-1dcc-480c-bbcd-e9654f0772a0
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1f51937fa402accf4e18fefdcec5763987241de4
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="message-queue-task-editor-receive-page"></a>Editor de la tarea Cola de mensajes (página Recibir)
  Use la página **Recibir** del cuadro de diálogo **Editor de la tarea Cola de mensajes** para configurar una tarea de la cola de mensajes para recibir mensajes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ).  
  
 Para obtener información acerca de esta tarea, vea [Message Queue Task](../../integration-services/control-flow/message-queue-task.md).  
  
## <a name="options"></a>Opciones  
 **RemoveFromMessageQueue**  
 Indique si desea eliminar el mensaje de la cola una vez recibido. De manera predeterminada, este valor se establece en **False**.  
  
 **ErrorIfMessageTimeOut**  
 Indique si desea mostrar un mensaje de error si se produce un error en la tarea al exceder el tiempo de espera. El valor predeterminado es **False**.  
  
 **TimeoutAfter**  
 Si elige mostrar un mensaje de error al producirse errores en la tarea, indique el número de segundos que deben transcurrir antes de mostrar el mensaje de tiempo de espera.  
  
 **MessageType**  
 Seleccione el tipo de mensaje. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Mensaje de archivo de datos**|El mensaje se almacena en un archivo. Al seleccionar este valor se muestra la opción dinámica **DataFileMessage**.|  
|**Mensaje de variable**|El mensaje se almacena en una variable. Al seleccionar este valor se muestra la opción dinámica **VariableMessage**.|  
|**Mensaje de cadena**|El mensaje se almacena en la tarea Cola de mensajes. Al seleccionar este valor se muestra la opción dinámica **StringMessage**.|  
|**Mensaje de cadena para variable**|El mensaje.<br /><br /> Al seleccionar este valor se muestra la opción dinámica **StringMessage**.|  
  
## <a name="messagetype-dynamic-options"></a>Opciones dinámicas de MessageType  
  
### <a name="messagetype--data-file-message"></a>MessageType = Mensaje de archivo de datos  
 **SaveFileAs**  
 Escriba la ruta del archivo que quiere usar o haga clic en el botón de puntos suspensivos **(…)** para buscar el archivo.  
  
 **Sobrescribir**  
 Indique si desea sobrescribir los datos de un archivo existente al guardar el contenido del mensaje de archivo de datos. El valor predeterminado es **False**.  
  
 **Filtro**  
 Indique si desea aplicar un filtro al mensaje. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Sin filtro**|La tarea no filtra mensajes. Al seleccionar este valor se muestra la opción dinámica **IdentifierReadOnly**.|  
|**De paquete**|El mensaje solo recibe mensajes del paquete seleccionado. Al seleccionar este valor se muestra la opción dinámica **Identifier**.|  
  
### <a name="filter-dynamic-options"></a>Opciones dinámicas de Filtro  
  
#### <a name="filter--no-filter"></a>Filtro = Sin filtro  
 **IdentifierReadOnly**  
 Esta opción es de solo lectura. Podría estar en blanco o contener el GUID de un paquete si se ha establecido anteriormente la propiedad Filtro.  
  
#### <a name="filter--from-package"></a>Filtro = De paquete  
 **Identifier**  
 Si elige aplicar un filtro, escriba el identificador único del paquete del que se recibirán los mensajes o haga clic en el botón de puntos suspensivos **(…)** y seleccione el paquete.  
  
 **Temas relacionados:** [Seleccionar un paquete](../../integration-services/control-flow/select-a-package.md)  
  
### <a name="messagetype--variable-message"></a>MessageType = Mensaje de variable  
 **Filtro**  
 Especifica si se desea aplicar un filtro a los mensajes. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Sin filtro**|La tarea no filtra mensajes. Al seleccionar este valor se muestra la opción dinámica **IdentifierReadOnly**.|  
|**De paquete**|El mensaje solo recibe mensajes del paquete seleccionado. Al seleccionar este valor se muestra la opción dinámica **Identifier**.|  
  
 **Variable**  
 Escriba el nombre de variable o haga clic en \< **nueva variable...** > y, a continuación, configure una nueva variable.  
  
 **Temas relacionados:** [Agregar variable](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
### <a name="filter-dynamic-options"></a>Opciones dinámicas de Filtro  
  
#### <a name="filter--no-filter"></a>Filtro = Sin filtro  
 **IdentifierReadOnly**  
 Esta opción está en blanco.  
  
#### <a name="filter--from-package"></a>Filtro = De paquete  
 **Identifier**  
 Si elige aplicar un filtro, escriba el identificador único del paquete del que se recibirán los mensajes o haga clic en el botón de puntos suspensivos **(…)** y seleccione el paquete.  
  
 **Temas relacionados:** [Seleccionar un paquete](../../integration-services/control-flow/select-a-package.md)  
  
### <a name="messagetype--string-message"></a>MessageType = Mensaje de cadena  
 **Comparar**  
 Especifica si se desea aplicar un filtro a los mensajes. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**None**|Los mensajes no se comparan.|  
|**Coincidencia exacta**|Los mensajes deben coincidir exactamente con la cadena de la opción **CompareString** .|  
|**Omitir mayúsculas y minúsculas**|El mensaje debe coincidir con la cadena de la opción **CompareString** , pero la comparación no distingue mayúsculas de minúsculas.|  
|**Que contenga**|El mensaje debe contener la cadena de la opción **CompareString** .|  
  
 **CompareString**  
 A menos que la opción **Comparar** se haya establecido en **Ninguno**, deberá indicar la cadena con la que se comparará el mensaje.  
  
### <a name="messagetype--string-message-to-variable"></a>MessageType = Mensaje de cadena para variable  
 **Comparar**  
 Especifica si se desea aplicar un filtro a los mensajes. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**None**|Los mensajes no se comparan.|  
|**Coincidencia exacta**|Los mensajes deben coincidir exactamente con la cadena de la opción **CompareString** .|  
|**Omitir mayúsculas y minúsculas**|El mensaje debe coincidir con la cadena de la opción **CompareString** , pero la comparación no distingue mayúsculas de minúsculas.|  
|**Que contenga**|El mensaje debe contener la cadena de la opción **CompareString** .|  
  
 **CompareString**  
 A menos que la opción **Comparar** se haya establecido en **Ninguno**, deberá indicar la cadena con la que se comparará el mensaje.  
  
 **Variable**  
 Escriba el nombre de la variable para conservar el mensaje recibido o haga clic en \< **nueva variable...** > y, a continuación, configure una nueva variable.  
  
 **Temas relacionados:** [Agregar variable](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de tareas de cola de mensajes &#40; Página general &#41;](../../integration-services/control-flow/message-queue-task-editor-general-page.md)   
 [Editor de tareas de cola de mensajes &#40; Enviar página &#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [Página expresiones](../../integration-services/expressions/expressions-page.md)   
 [Tarea cola de mensajes](../../integration-services/control-flow/message-queue-task.md)  
  
  
