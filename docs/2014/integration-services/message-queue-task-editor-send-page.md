---
title: Editor de tareas de cola de mensajes (página Enviar) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.send.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 565aa079-ac44-4407-8efc-cddab839de30
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: efaadce1425de4468056f0df5e3d7106432ca804
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516098"
---
# <a name="message-queue-task-editor-send-page"></a>Editor de la tarea Cola de mensajes (página Enviar)
  Utilice la página **Enviar** del cuadro de diálogo **Editor de la tarea Cola de mensajes** para configurar una tarea Cola de mensajes para enviar mensajes desde un paquete de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Para obtener información acerca de esta tarea, vea [Message Queue Task](control-flow/message-queue-task.md).  
  
## <a name="options"></a>Opciones  
 **UseEncryption**  
 Indica si se debe cifrar el mensaje. De manera predeterminada, es `False`.  
  
 **EncryptionAlgorithm**  
 Si opta por usar cifrado, especifique el nombre del algoritmo de cifrado que debe utilizarse. La tarea Cola de mensajes puede utilizar los algoritmos RC2 y RC4. El valor predeterminado es **RC2**.  
  
> [!NOTE]  
>  El algoritmo RC4 se admite únicamente por razones de compatibilidad con versiones anteriores. El material nuevo solo se puede cifrar con RC4 o RC4_128 cuando la base de datos tenga el nivel de compatibilidad 90 o 100. (No se recomienda). Use un algoritmo más reciente como uno de los algoritmos AES en su lugar. En la versión actual de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el material cifrado con RC4 o RC4_128 se puede descifrar en cualquier nivel de compatibilidad.  
  
> [!IMPORTANT]  
>  Éstos son los algoritmos de cifrado que admite la tecnología de Message Queue Server (que también recibe el nombre de MSMQ). Ambos algoritmos de cifrado se consideran en estos momentos criptográficamente menos seguros que otros algoritmos más recientes con los que Message Queue Server aún no es compatible. Por tanto, debe considerar con detenimiento sus necesidades criptográficas a la hora de enviar mensajes con la tarea Cola de mensajes.  
  
 **MessageType**  
 Seleccione el tipo de mensaje. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Mensaje de archivo de datos**|El mensaje se almacena en un archivo. Al seleccionar este valor se muestra la opción dinámica **DataFileMessage**.|  
|**Mensaje de variable**|El mensaje se almacena en una variable. Al seleccionar este valor se muestra la opción dinámica **VariableMessage**.|  
|**Mensaje de cadena**|El mensaje se almacena en la tarea Cola de mensajes. Al seleccionar este valor se muestra la opción dinámica **StringMessage**.|  
  
## <a name="messagetype-dynamic-options"></a>Opciones dinámicas de MessageType  
  
### <a name="messagetype--data-file-message"></a>MessageType = Mensaje de archivo de datos  
 **DataFileMessage**  
 Escriba la ruta de acceso del archivo de datos, o bien haga clic en el botón de puntos suspensivos **(…)** y busque el archivo.  
  
### <a name="messagetype--variable-message"></a>MessageType = Mensaje de variable  
 **VariableMessage**  
 Escriba los nombres de variable, o bien haga clic en el botón de puntos suspensivos **(…)** y seleccione las variables. Las variables se separan con comas.  
  
 **Temas relacionados:** Seleccionar variables  
  
### <a name="messagetype--string-message"></a>MessageType = Mensaje de cadena  
 **StringMessage**  
 Escriba el mensaje de cadena, o bien haga clic en el botón de puntos suspensivos **(…)** y escriba el mensaje en el cuadro de diálogo **Escribir mensaje de cadena**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea Cola de mensajes &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de la tarea Cola de mensajes &#40;página Recibir&#41;](../../2014/integration-services/message-queue-task-editor-receive-page.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  
