---
title: Administrador de conexiones MSMQ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], message queues
- connection managers [Integration Services], MSMQ
- MSMQ connection manager
- message queue connections [Integration Services]
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 015488fc30b364b9f82086acb995df3967eb5b10
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52766857"
---
# <a name="msmq-connection-manager"></a>MSMQ, administrador de conexiones
  Un administrador de conexiones MSMQ permite a un paquete conectarse a una cola de mensajes que usa Message Queue Server (que también recibe el nombre de MSMQ). La tarea Cola de mensajes que incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa un administrador de conexiones MSMQ.  
  
 Cuando agrega un administrador de conexiones MSMQ a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión MSMQ en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección `Connections` del paquete. La propiedad `ConnectionManagerType` del administrador de conexiones se establece en `MSMQ`.  
  
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
  
 Para más información sobre las propiedades que puede configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor del administrador de conexiones MSMQ](../msmq-connection-manager-editor.md).  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vea también  
 [Tarea Cola de mensajes](../control-flow/message-queue-task.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](integration-services-ssis-connections.md)  
  
  
