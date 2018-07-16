---
title: Editor de tareas de cola de mensajes (página General) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.general.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 09368b18-37a5-4321-a173-7cfe5d42d2a2
caps.latest.revision: 25
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 22a76ae1c006eae5b2670e0405fb0c61c3b8f6e3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37320655"
---
# <a name="message-queue-task-editor-general-page"></a>Editor de la tarea Cola de mensajes (página General)
  Utilice la página **General** del cuadro de diálogo **Editor de la tarea Cola de mensajes** para asignar un nombre y describir la tarea Cola de mensajes, especificar el formato del mensaje e indicar si la tarea envía o recibe o mensajes.  
  
 Para obtener información acerca de esta tarea, vea [Message Queue Task](control-flow/message-queue-task.md).  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Proporcione un nombre único para la tarea Cola de mensajes. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Cola de mensajes.  
  
 **Use2000Format**  
 Indica si se va a utilizar el formato 2000 de Message Queue Server (que también recibe el nombre de MSMQ). El valor predeterminado es `False`.  
  
 **MSMQConnection**  
 Seleccione un administrador de conexiones MSMQ existente o haga clic en \<**Nueva conexión…**> para crear un administrador de conexiones.  
  
 **Temas relacionados**: [Administrador de conexiones MSMQ](connection-manager/msmq-connection-manager.md), [Editor del administrador de conexiones MSMQ](../../2014/integration-services/msmq-connection-manager-editor.md)  
  
 **de mensaje**  
 Especifique si la tarea Cola de mensajes envía o recibe mensajes. Si selecciona **Enviar mensaje**, la página Enviar se agrega a la lista del panel izquierdo del cuadro de diálogo. Si selecciona **Recibir mensaje**, se agrega la página Recibir. De forma predeterminada, este valor está establecido en **Enviar mensaje**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea cola de mensajes &#40;página de recepción&#41;](../../2014/integration-services/message-queue-task-editor-receive-page.md)   
 [Editor de la tarea cola de mensajes &#40;Enviar página&#41;](../../2014/integration-services/message-queue-task-editor-send-page.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  
