---
title: Editor de tareas de cola de mensajes (página General) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.general.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 09368b18-37a5-4321-a173-7cfe5d42d2a2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7668cf38f01f049b95423547430e1027a4ab6090
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375863"
---
# <a name="message-queue-task-editor-general-page"></a>Editor de la tarea Cola de mensajes (página General)
  Utilice la página **General** del cuadro de diálogo **Editor de la tarea Cola de mensajes** para asignar un nombre y describir la tarea Cola de mensajes, especificar el formato del mensaje e indicar si la tarea envía o recibe o mensajes.  
  
 Para obtener información acerca de esta tarea, vea [Message Queue Task](control-flow/message-queue-task.md).  
  
## <a name="options"></a>Opciones  
 **Name**  
 Proporcione un nombre único para la tarea Cola de mensajes. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Cola de mensajes.  
  
 **Use2000Format**  
 Indica si se va a utilizar el formato 2000 de Message Queue Server (que también recibe el nombre de MSMQ). De manera predeterminada, es `False`.  
  
 **MSMQConnection**  
 Seleccione un administrador de conexiones MSMQ existente o haga clic en \<**Nueva conexión…**> para crear un administrador de conexiones.  
  
 **Temas relacionados**: [Administrador de conexiones MSMQ](connection-manager/msmq-connection-manager.md), [Editor del Administrador de conexiones MSMQ](../../2014/integration-services/msmq-connection-manager-editor.md)  
  
 **de mensaje**  
 Especifique si la tarea Cola de mensajes envía o recibe mensajes. Si selecciona **Enviar mensaje**, la página Enviar se agrega a la lista del panel izquierdo del cuadro de diálogo. Si selecciona **Recibir mensaje**, se agrega la página Recibir. De forma predeterminada, este valor está establecido en **Enviar mensaje**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea Cola de mensajes &#40;página Recibir&#41;](../../2014/integration-services/message-queue-task-editor-receive-page.md)   
 [Editor de la tarea Cola de mensajes &#40;página Enviar&#41;](../../2014/integration-services/message-queue-task-editor-send-page.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  
