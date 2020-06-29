---
title: Tarea Transferir trabajos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferjobstask.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b987f15fd7108027b5038858be2cd875b1e5b473
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438112"
---
# <a name="transfer-jobs-task"></a>Tarea Transferir trabajos
  La tarea Transferir trabajos transfiere uno o varios trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La tarea Transferir trabajos se puede configurar para que transfiera todos los trabajos o solo los trabajos especificados. También puede indicar si los trabajos transferidos se habilitarán en el destino.  
  
 Es posible que los trabajos transferidos ya existan en el destino. La tarea Transferir trabajos se puede configurar para haga lo siguiente con los trabajos existentes:  
  
-   Sobrescribir los trabajos existentes.  
  
-   Hacer que la tarea genere un error cuando existan trabajos duplicados.  
  
-   Omitir los trabajos duplicados.  
  
 Durante la ejecución, la tarea Transferir trabajos se conecta a los servidores de origen y de destino utilizando uno o dos administradores de conexión SMO. El administrador de conexiones SMO se configura independientemente de la tarea Transferir trabajos y después se hace referencia a él en la tarea Transferir trabajos. El administrador de conexiones SMO especifica el servidor y el modo de autenticación que se utiliza para tener acceso al servidor. Para más información, consulte [SMO Connection Manager](../connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>Transferir trabajos entre instancias de SQL Server  
 La tarea Transferir trabajos admite un origen y un destino que sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No hay restricciones respecto a qué versión hay que usar como origen o como destino.  
  
## <a name="events"></a>Eventos  
 La tarea Transferir trabajos emite un evento de información que indica el número de trabajos transferidos y un evento de advertencia cuando se sobrescribe un trabajo. La tarea no indica el progreso incremental de la transferencia de los trabajos; solo indica 0% y 100%.  
  
## <a name="execution-value"></a>Valor de ejecución  
 El valor de ejecución, que se define en la propiedad `ExecutionValue` de la tarea, devuelve el número de trabajos transferidos. Si se asigna una variable definida por el usuario a la propiedad `ExecValueVariable` de la tarea Transferir trabajos, se puede hacer que la información de la transferencia de trabajos esté disponible para otros objetos del paquete. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) y [Usar variables en paquetes](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Entradas del registro  
 La tarea Transferir trabajos incluye las siguientes entradas del registro personalizadas:  
  
-   TransferJobsTaskStarTransferringObjects   Esta entrada del registro indica que se ha iniciado la transferencia. La entrada del registro incluye la hora de inicio.  
  
-   TransferJobsTaskFinishedTransferringObjects   Esta entrada del registro indica que ha finalizado la transferencia. La entrada del registro incluye la hora de finalización.  
  
 Además, una entrada del registro para el evento `OnInformation` indica el número de trabajos transferidos y se escribe una entrada del registro para el evento `OnWarning` por cada trabajo que se sobrescribe en el destino.  
  
## <a name="security-and-permissions"></a>Seguridad y permisos  
 Para transferir trabajos, el usuario debe ser miembro del rol fijo de servidor sysadmin o de uno de los roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos msdb tanto en la instancia de origen como en la de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>Configuración de la tarea Transferir trabajos  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Transferir trabajos &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de la tarea Transferir trabajos &#40;página Trabajos&#41;](../transfer-jobs-task-editor-jobs-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener información acerca de cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Consulte también  
 [Tareas de Integration Services](integration-services-tasks.md)   
 [Flujo de control](control-flow.md)  
  
  
