---
title: "Editor de la tarea Cola de mensajes (p&#225;gina Recibir) | Microsoft Docs"
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
  - "sql13.dts.designer.msgqueuetask.receive.f1"
helpviewer_keywords: 
  - "Editor de la tarea Cola de mensajes"
ms.assetid: 7028756d-1dcc-480c-bbcd-e9654f0772a0
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# Editor de la tarea Cola de mensajes (p&#225;gina Recibir)
  Use la página **Recibir** del cuadro de diálogo **Editor de la tarea Cola de mensajes** para configurar una tarea de la cola de mensajes para recibir mensajes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ).  
  
 Para obtener información acerca de esta tarea, vea [Message Queue Task](../../integration-services/control-flow/message-queue-task.md).  
  
## Opciones  
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
  
## Opciones dinámicas de MessageType  
  
### MessageType = Mensaje de archivo de datos  
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
  
### Opciones dinámicas de Filtro  
  
#### Filtro = Sin filtro  
 **IdentifierReadOnly**  
 Esta opción es de solo lectura. Podría estar en blanco o contener el GUID de un paquete si se ha establecido anteriormente la propiedad Filtro.  
  
#### Filtro = De paquete  
 **Identificador**  
 Si elige aplicar un filtro, escriba el identificador único del paquete del que se recibirán los mensajes o haga clic en el botón de puntos suspensivos **(…)** y seleccione el paquete.  
  
 **Temas relacionados:** [Seleccionar un paquete](../../integration-services/control-flow/select-a-package.md).  
  
### MessageType = Mensaje de variable  
 **Filtro**  
 Especifica si se desea aplicar un filtro a los mensajes. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Sin filtro**|La tarea no filtra mensajes. Al seleccionar este valor se muestra la opción dinámica **IdentifierReadOnly**.|  
|**De paquete**|El mensaje solo recibe mensajes del paquete seleccionado. Al seleccionar este valor se muestra la opción dinámica **Identifier**.|  
  
 **Variable**  
 Escriba el nombre de la variable o haga clic en \<**Nueva variable…**> y configure una nueva variable.  
  
 **Temas relacionados:** [Agregar variable](../Topic/Add%20Variable.md).  
  
### Opciones dinámicas de Filtro  
  
#### Filtro = Sin filtro  
 **IdentifierReadOnly**  
 Esta opción está en blanco.  
  
#### Filtro = De paquete  
 **Identificador**  
 Si elige aplicar un filtro, escriba el identificador único del paquete del que se recibirán los mensajes o haga clic en el botón de puntos suspensivos **(…)** y seleccione el paquete.  
  
 **Temas relacionados:** [Seleccionar un paquete](../../integration-services/control-flow/select-a-package.md).  
  
### MessageType = Mensaje de cadena  
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
  
### MessageType = Mensaje de cadena para variable  
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
 Escriba el nombre de la variable para retener el mensaje recibido o haga clic en \<**Nueva variable…**> y configure una nueva variable.  
  
 **Temas relacionados:** [Agregar variable](../Topic/Add%20Variable.md).  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea Cola de mensajes &#40;página General&#41;](../../integration-services/control-flow/message-queue-task-editor-general-page.md)   
 [Editor de la tarea Cola de mensajes &#40;página Enviar&#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [Página Expresiones](../../integration-services/expressions/expressions-page.md)   
 [Tarea Cola de mensajes](../../integration-services/control-flow/message-queue-task.md)  
  
  