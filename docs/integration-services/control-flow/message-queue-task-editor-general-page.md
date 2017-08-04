---
title: "Editor de tareas de cola de mensajes (página General) | Documentos de Microsoft"
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
- sql13.dts.designer.msgqueuetask.general.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 09368b18-37a5-4321-a173-7cfe5d42d2a2
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 25313cc6decaea073409143e468621a1ed40993c
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="message-queue-task-editor-general-page"></a>Editor de la tarea Cola de mensajes (página General)
  Utilice la página **General** del cuadro de diálogo **Editor de la tarea Cola de mensajes** para asignar un nombre y describir la tarea Cola de mensajes, especificar el formato del mensaje e indicar si la tarea envía o recibe o mensajes.  
  
 Para obtener información acerca de esta tarea, vea [Message Queue Task](../../integration-services/control-flow/message-queue-task.md).  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Proporcione un nombre único para la tarea Cola de mensajes. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Description**  
 Escriba una descripción de la tarea Cola de mensajes.  
  
 **Use2000Format**  
 Indica si se va a utilizar el formato 2000 de Message Queue Server (que también recibe el nombre de MSMQ). El valor predeterminado es **False**.  
  
 **MSMQConnection**  
 Seleccione un administrador de conexiones MSMQ existente o haga clic en \< **nueva conexión...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados**: [Administrador de conexiones MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md), [Editor del administrador de conexiones MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)  
  
 **de mensaje**  
 Especifique si la tarea Cola de mensajes envía o recibe mensajes. Si selecciona **Enviar mensaje**, la página Enviar se agrega a la lista del panel izquierdo del cuadro de diálogo. Si selecciona **Recibir mensaje**, se agrega la página Recibir. De forma predeterminada, este valor está establecido en **Enviar mensaje**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de tareas de cola de mensajes &#40; Aparece la página &#41;](../../integration-services/control-flow/message-queue-task-editor-receive-page.md)   
 [Editor de tareas de cola de mensajes &#40; Enviar página &#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
  
