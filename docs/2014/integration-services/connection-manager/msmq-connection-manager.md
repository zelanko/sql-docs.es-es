---
title: Administrador de conexiones MSMQ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
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
ms.openlocfilehash: a1501af4a26c0e039df3113a719a61e1e2c3f40a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135045"
---
# <a name="msmq-connection-manager"></a>MSMQ, administrador de conexiones
  Un administrador de conexiones MSMQ permite a un paquete conectarse a una cola de mensajes que usa Message Queue Server (que también recibe el nombre de MSMQ). La tarea Cola de mensajes que incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa un administrador de conexiones MSMQ.  
  
 Cuando se agrega un administrador de conexiones MSMQ a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una conexión de administrador que se resuelve como una conexión MSMQ en tiempo de ejecución, Establece las propiedades del Administrador de la conexión y agrega el Administrador de conexiones para el `Connections` colección en el paquete. El `ConnectionManagerType` propiedad del Administrador de conexiones se establece en `MSMQ`.  
  
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
  
 Para obtener información acerca de cómo configurar un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vea también  
 [Tarea cola de mensajes](../control-flow/message-queue-task.md)   
 [Servicios de integración &#40;SSIS&#41; conexiones](integration-services-ssis-connections.md)  
  
  
