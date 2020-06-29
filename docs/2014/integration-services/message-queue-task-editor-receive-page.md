---
title: Editor de la tarea cola de mensajes (página recibir) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.receive.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 7028756d-1dcc-480c-bbcd-e9654f0772a0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 53a392a09e2120c08c43b1e373c942ff9c60e148
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424592"
---
# <a name="message-queue-task-editor-receive-page"></a>Editor de la tarea Cola de mensajes (página Recibir)
  Use la página **Recibir** del cuadro de diálogo **Editor de la tarea Cola de mensajes** para configurar una tarea de la cola de mensajes para recibir mensajes de [!INCLUDE[msCoName](../includes/msconame-md.md)] Message Queuing (MSMQ).  
  
 Para obtener información acerca de esta tarea, vea [Message Queue Task](control-flow/message-queue-task.md).  
  
## <a name="options"></a>Opciones  
 **RemoveFromMessageQueue**  
 Indique si desea eliminar el mensaje de la cola una vez recibido. De forma predeterminada, este valor está establecido en `False`.  
  
 **ErrorIfMessageTimeOut**  
 Indique si desea mostrar un mensaje de error si se produce un error en la tarea al exceder el tiempo de espera. De manera predeterminada, es `False`.  
  
 **TimeoutAfter**  
 Si elige mostrar un mensaje de error al producirse errores en la tarea, indique el número de segundos que deben transcurrir antes de mostrar el mensaje de tiempo de espera.  
  
 **MessageType**  
 Seleccione el tipo de mensaje. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Mensaje de archivo de datos**|El mensaje se almacena en un archivo. Al seleccionar este valor se muestra la opción dinámica **DataFileMessage**.|  
|**Mensaje de variable**|El mensaje se almacena en una variable. Al seleccionar este valor se muestra la opción dinámica **VariableMessage**.|  
|**Mensaje de cadena**|El mensaje se almacena en la tarea Cola de mensajes. Al seleccionar este valor se muestra la opción dinámica **StringMessage**.|  
|**Mensaje de cadena para variable**|El mensaje.<br /><br /> Al seleccionar este valor se muestra la opción dinámica **StringMessage**.|  
  
## <a name="messagetype-dynamic-options"></a>Opciones dinámicas de MessageType  
  
### <a name="messagetype--data-file-message"></a>MessageType = Mensaje de archivo de datos  
 **SaveFileAs**  
 Escriba la ruta del archivo que quiere usar, o bien haga clic en el botón de puntos suspensivos **(…)** para buscar el archivo.  
  
 **Sobrescribir**  
 Indique si desea sobrescribir los datos de un archivo existente al guardar el contenido del mensaje de archivo de datos. De manera predeterminada, es `False`.  
  
 **Filter**  
 Indique si desea aplicar un filtro al mensaje. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Sin filtro**|La tarea no filtra mensajes. Al seleccionar este valor se muestra la opción dinámica **IdentifierReadOnly**.|  
|**De paquete**|El mensaje solo recibe mensajes del paquete seleccionado. Al seleccionar este valor se muestra la opción dinámica **Identifier**.|  
  
### <a name="filter-dynamic-options"></a>Opciones dinámicas de Filtro  
  
#### <a name="filter--no-filter"></a>Filtro = Sin filtro  
 **IdentifierReadOnly**  
 Esta opción es de solo lectura. Podría estar en blanco o contener el GUID de un paquete si se ha establecido anteriormente la propiedad Filtro.  
  
#### <a name="filter--from-package"></a>Filtro = De paquete  
 **Identificador**  
 Si decide aplicar un filtro, escriba el identificador único del paquete del que se recibirán los mensajes, o bien haga clic en el botón de puntos suspensivos **(…)** y, después, especifique el paquete.  
  
 **Temas relacionados:** [Seleccionar un paquete](control-flow/select-a-package.md)  
  
### <a name="messagetype--variable-message"></a>MessageType = Mensaje de variable  
 **Filter**  
 Especifica si se desea aplicar un filtro a los mensajes. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Sin filtro**|La tarea no filtra mensajes. Al seleccionar este valor se muestra la opción dinámica **IdentifierReadOnly**.|  
|**De paquete**|El mensaje solo recibe mensajes del paquete seleccionado. Al seleccionar este valor se muestra la opción dinámica **Identifier**.|  
  
 **Variable**  
 Escriba el nombre de la variable o haga clic en \<**New variable...**> y, a continuación, configure una nueva variable.  
  
 **Temas relacionados:** [Agregar variable](../../2014/integration-services/add-variable.md)  
  
### <a name="filter-dynamic-options"></a>Opciones dinámicas de Filtro  
  
#### <a name="filter--no-filter"></a>Filtro = Sin filtro  
 **IdentifierReadOnly**  
 Esta opción está en blanco.  
  
#### <a name="filter--from-package"></a>Filtro = De paquete  
 **Identificador**  
 Si decide aplicar un filtro, escriba el identificador único del paquete del que se recibirán los mensajes, o bien haga clic en el botón de puntos suspensivos **(…)** y, después, especifique el paquete.  
  
 **Temas relacionados:** [Seleccionar un paquete](control-flow/select-a-package.md)  
  
### <a name="messagetype--string-message"></a>MessageType = Mensaje de cadena  
 **Comparar**  
 Especifica si se desea aplicar un filtro a los mensajes. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
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
  
|Value|Descripción|  
|-----------|-----------------|  
|**None**|Los mensajes no se comparan.|  
|**Coincidencia exacta**|Los mensajes deben coincidir exactamente con la cadena de la opción **CompareString** .|  
|**Omitir mayúsculas y minúsculas**|El mensaje debe coincidir con la cadena de la opción **CompareString** , pero la comparación no distingue mayúsculas de minúsculas.|  
|**Que contenga**|El mensaje debe contener la cadena de la opción **CompareString** .|  
  
 **CompareString**  
 A menos que la opción **Comparar** se haya establecido en **Ninguno**, deberá indicar la cadena con la que se comparará el mensaje.  
  
 **Variable**  
 Escriba el nombre de la variable que contendrá el mensaje recibido o haga clic \<**New variable...**> y, a continuación, configure una nueva variable.  
  
 **Temas relacionados:** [Agregar variable](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea cola de mensajes &#40;página general&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de la tarea cola de mensajes &#40;página envío&#41;](../../2014/integration-services/message-queue-task-editor-send-page.md)   
 [Página expresiones](expressions/expressions-page.md)   
 [Tarea Cola de mensajes](control-flow/message-queue-task.md)  
  
  
