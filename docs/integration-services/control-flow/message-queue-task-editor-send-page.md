---
title: "Editor de la tarea Cola de mensajes (p&#225;gina Enviar) | Microsoft Docs"
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
  - "sql13.dts.designer.msgqueuetask.send.f1"
helpviewer_keywords: 
  - "Editor de la tarea Cola de mensajes"
ms.assetid: 565aa079-ac44-4407-8efc-cddab839de30
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# Editor de la tarea Cola de mensajes (p&#225;gina Enviar)
  Utilice la página **Enviar** del cuadro de diálogo **Editor de la tarea Cola de mensajes** para configurar una tarea Cola de mensajes para enviar mensajes desde un paquete de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Para obtener información acerca de esta tarea, vea [Message Queue Task](../../integration-services/control-flow/message-queue-task.md).  
  
## Opciones  
 **UseEncryption**  
 Indica si se debe cifrar el mensaje. El valor predeterminado es **False**.  
  
 **EncryptionAlgorithm**  
 Si opta por usar cifrado, especifique el nombre del algoritmo de cifrado que debe utilizarse. La tarea Cola de mensajes puede utilizar los algoritmos RC2 y RC4. El valor predeterminado es **RC2**.  
  
> [!NOTE]  
>  El algoritmo RC4 se admite únicamente por razones de compatibilidad con versiones anteriores. El material nuevo solo se puede cifrar con RC4 o RC4_128 cuando la base de datos tenga el nivel de compatibilidad 90 o 100. (No se recomienda). Use un algoritmo más reciente como uno de los algoritmos AES en su lugar. En la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el material cifrado con RC4 o RC4_128 se puede descifrar en cualquier nivel de compatibilidad.  
  
> [!IMPORTANT]  
>  Éstos son los algoritmos de cifrado que admite la tecnología de Message Queue Server (que también recibe el nombre de MSMQ). Ambos algoritmos de cifrado se consideran en estos momentos criptográficamente menos seguros que otros algoritmos más recientes con los que Message Queue Server aún no es compatible. Por tanto, debe considerar con detenimiento sus necesidades criptográficas a la hora de enviar mensajes con la tarea Cola de mensajes.  
  
 **MessageType**  
 Seleccione el tipo de mensaje. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Mensaje de archivo de datos**|El mensaje se almacena en un archivo. Al seleccionar este valor se muestra la opción dinámica **DataFileMessage**.|  
|**Mensaje de variable**|El mensaje se almacena en una variable. Al seleccionar este valor se muestra la opción dinámica **VariableMessage**.|  
|**Mensaje de cadena**|El mensaje se almacena en la tarea Cola de mensajes. Al seleccionar este valor se muestra la opción dinámica **StringMessage**.|  
  
## Opciones dinámicas de MessageType  
  
### MessageType = Mensaje de archivo de datos  
 **DataFileMessage**  
 Escriba la ruta de acceso del archivo de datos o haga clic en el botón de puntos suspensivos **(…)** para ubicar el archivo.  
  
### MessageType = Mensaje de variable  
 **VariableMessage**  
 Escriba los nombres de las variables o haga clic en el botón de puntos suspensivos **(…)** para seleccionar las variables. Las variables se separan con comas.  
  
 **Temas relacionados:** Seleccionar variables  
  
### MessageType = Mensaje de cadena  
 **StringMessage**  
 Escriba el mensaje de cadena o haga clic en el botón de puntos suspensivos **(…)** y escriba el mensaje en el cuadro de diálogo **Escribir mensaje de cadena**.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea Cola de mensajes &#40;página General&#41;](../../integration-services/control-flow/message-queue-task-editor-general-page.md)   
 [Editor de la tarea Cola de mensajes &#40;página Recibir&#41;](../../integration-services/control-flow/message-queue-task-editor-receive-page.md)   
 [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
  