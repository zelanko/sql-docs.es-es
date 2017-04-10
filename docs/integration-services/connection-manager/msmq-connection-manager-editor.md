---
title: "administrador de conexiones MSMQ, editor del  | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.msmqconnectionmanager.f1"
helpviewer_keywords: 
  - "administrador de conexiones MSMQ, editor del "
ms.assetid: ef842cb4-82da-4550-85fe-9bedbc1e77c7
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# administrador de conexiones MSMQ, editor del 
  Use el cuadro de diálogo **Administrador de conexiones MSMQ** para especificar la ruta de acceso a una cola de mensajes de Message Queuing (que también recibe el nombre de MSMQ).  
  
 Para obtener más información acerca del administrador de conexiones MSMQ, vea [MSMQ Connection Manager](../../integration-services/connection-manager/msmq-connection-manager.md).  
  
> [!NOTE]  
>  El administrador de conexiones MSMQ admite colas públicas y privadas locales, además de colas públicas remotas. No admite colas privadas remotas. Para obtener una solución que utilice la tarea Script, vea [Sending to a Remote Private Message Queue with the Script Task](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md).  
  
## Opciones  
 **Nombre**  
 Proporcione un nombre único para el administrador de conexiones MSMQ en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Describa el administrador de conexiones. Como método recomendado, describa el administrador de conexiones desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Ruta de acceso**  
 Escriba la ruta de acceso completa de la cola de mensajes. El formato de la ruta de acceso depende del tipo de cola.  
  
|Tipo de cola|Ruta de acceso de ejemplo|  
|----------------|-----------------|  
|Público|\<nombre de equipo>\\<nombre de cola\>|  
|Privada|\<nombre de equipo>\Private$\\<nombre de cola\>|  
  
 Puede utilizar "." para representar el equipo local.  
  
 **Prueba**  
 Después de configurar el Administrador de conexiones MSMQ, confirme que la conexión es viable haciendo clic en **Probar**.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
  
  