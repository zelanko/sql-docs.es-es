---
title: Administrador de conexiones MSMQ | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.msmqconnectionmanager.f1
helpviewer_keywords:
- connections [Integration Services], message queues
- connection managers [Integration Services], MSMQ
- MSMQ connection manager
- message queue connections [Integration Services]
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: add29828603c19a3d909ebb621e99ba58bdc6052
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="msmq-connection-manager"></a>MSMQ, administrador de conexiones
  Un administrador de conexiones MSMQ permite a un paquete conectarse a una cola de mensajes que usa Message Queue Server (que también recibe el nombre de MSMQ). La tarea Cola de mensajes que incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa un administrador de conexiones MSMQ.  
  
 Cuando agrega un administrador de conexiones MSMQ a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión MSMQ en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Conexiones** del paquete. La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **MSMQ**.  
  
 Puede configurar el administrador de conexiones MSMQ de las maneras siguientes:  
  
-   Proporcionar una cadena de conexión.  
  
-   Proporcionar la ruta de la cola de mensajes con la que se debe hacer la conexión.  
  
 El formato de la ruta de acceso depende del tipo de cola, como se muestra en la tabla siguiente.  
  
|Tipo de cola|Ruta de acceso de ejemplo|  
|----------------|-----------------|  
|Público|\<nombre del equipo>\\<nombre de la cola\>|  
|Privada|\<nombre del equipo>\Private$\\<nombre de la cola\>|  
  
 Puede usar un punto (.) para representar el equipo local.  
  
## <a name="configuration-of-the-msmq-connection-manager"></a>Configuración del administrador de conexiones MSMQ  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para más información sobre las propiedades que puede configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor del administrador de conexiones MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md).  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="msmq-connection-manager-editor"></a>administrador de conexiones MSMQ, editor del
  Use el cuadro de diálogo **Administrador de conexiones MSMQ** para especificar la ruta de acceso a una cola de mensajes de Message Queuing (que también recibe el nombre de MSMQ).  
  
 Para obtener más información acerca del administrador de conexiones MSMQ, vea [MSMQ Connection Manager](../../integration-services/connection-manager/msmq-connection-manager.md).  
  
> [!NOTE]  
>  El administrador de conexiones MSMQ admite colas públicas y privadas locales, además de colas públicas remotas. No admite colas privadas remotas. Para obtener una solución que utilice la tarea Script, vea [Sending to a Remote Private Message Queue with the Script Task](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md).  
  
### <a name="options"></a>.  
 **Nombre**  
 Proporcione un nombre único para el administrador de conexiones MSMQ en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descripción**  
 Describa el administrador de conexiones. Como método recomendado, describa el administrador de conexiones desde el punto de vista de su propósito, para que los paquetes estén autodocumentados y sean más fáciles de mantener.  
  
 **Ruta de acceso**  
 Escriba la ruta de acceso completa de la cola de mensajes. El formato de la ruta de acceso depende del tipo de cola.  
  
|Tipo de cola|Ruta de acceso de ejemplo|  
|----------------|-----------------|  
|Público|\<nombre del equipo>\\<nombre de la cola\>|  
|Privada|\<nombre del equipo>\Private$\\<nombre de la cola\>|  
  
 Puede utilizar "." para representar el equipo local.  
  
 **Prueba**  
 Después de configurar el Administrador de conexiones MSMQ, confirme que la conexión es viable haciendo clic en **Probar**.  
  
## <a name="see-also"></a>Ver también  
 [Tarea Cola de mensajes](../../integration-services/control-flow/message-queue-task.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
