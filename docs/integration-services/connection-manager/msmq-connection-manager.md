---
title: "Administrador de conexiones MSMQ | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "conexiones [Integration Services], colas de mensajes"
  - "administradores de conexión [Integration Services], MSMQ"
  - "MSMQ, administrador de conexiones"
  - "conexiones de colas de mensajes [Integration Services]"
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# Administrador de conexiones MSMQ
  Un administrador de conexiones MSMQ permite a un paquete conectarse a una cola de mensajes que usa Message Queue Server (que también recibe el nombre de MSMQ). La tarea Cola de mensajes que incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa un administrador de conexiones MSMQ.  
  
 Cuando agrega un administrador de conexiones MSMQ a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión MSMQ en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Conexiones** del paquete. La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **MSMQ**.  
  
 Puede configurar el administrador de conexiones MSMQ de las maneras siguientes:  
  
-   Proporcionar una cadena de conexión.  
  
-   Proporcionar la ruta de la cola de mensajes con la que se debe hacer la conexión.  
  
 El formato de la ruta de acceso depende del tipo de cola, como se muestra en la tabla siguiente.  
  
|Tipo de cola|Ruta de acceso de ejemplo|  
|----------------|-----------------|  
|Público|\<nombre de equipo>\\<nombre de cola\>|  
|Privada|\<nombre de equipo>\Private$\\<nombre de cola\>|  
  
 Puede usar un punto (.) para representar el equipo local.  
  
## Configuración del administrador de conexiones MSMQ  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para más información sobre las propiedades que puede configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)], vea [Editor del administrador de conexiones MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md).  
  
 Para más información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## Vea también  
 [Tarea Cola de mensajes](../../integration-services/control-flow/message-queue-task.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  