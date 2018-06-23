---
title: Tarea Transferir procedimientos almacenados principales | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.transfermasterspstask.f1
helpviewer_keywords:
- Transfer Master Stored Procedures task [Integration Services]
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: fe704e638cb32ff397bf906c61593af6d07ba866
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202994"
---
# <a name="transfer-master-stored-procedures-task"></a>Tarea Transferir procedimientos almacenados principales
  La tarea Transferir procedimientos almacenados principales transfiere uno o más procedimientos almacenados definidos por el usuario entre las bases de datos **master** en instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para transferir un procedimiento almacenado de la base de datos **master** , el propietario del procedimiento debe ser dbo.  
  
 La tarea Transferir procedimientos almacenados principales se puede configurar para que transfiera todos los procedimientos almacenados o solo los procedimientos especificados. Esta tarea no copia procedimientos almacenados del sistema.  
  
 Es posible que los procedimientos almacenados principales que desea transferir ya existan en el destino. La tarea Transferir procedimientos almacenados principales se puede configurar para que haga lo siguiente con los procedimientos almacenados existentes:  
  
-   Sobrescribir procedimientos almacenados existentes.  
  
-   Hacer que la tarea genere un error cuando existan procedimientos almacenados duplicados.  
  
-   Omitir los procedimientos almacenados duplicados.  
  
 Durante la ejecución, la tarea Transferir procedimientos almacenados principales se conecta a los servidores de origen y de destino a través de dos administradores de conexión SMO. Los administradores de conexión SMO se configuran independientemente de la tarea Transferir procedimientos almacenados principales y después se hace referencia a ellos en la tarea Transferir procedimientos almacenados principales. Los administradores de conexión SMO especifican el servidor y el modo de autenticación que se utilizará para tener acceso al servidor. Para más información, consulte [SMO Connection Manager](../connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-stored-procedures-between-instances-of-sql-server"></a>Transferir procedimientos almacenados entre instancias de SQL Server  
 La tarea Transferir procedimientos almacenados principales admite un origen y un destino que sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventos  
 La tarea emite un evento de información que indica el número de procedimientos almacenados transferidos y un evento de advertencia cuando se sobrescribe un procedimiento almacenado.  
  
 La tarea Transferir procedimientos almacenados principales no indica el progreso incremental de la transferencia; solo indica 0% y 100%.  
  
## <a name="execution-value"></a>Valor de ejecución  
 El valor de ejecución, definido en el `ExecutionValue` propiedad de la tarea, devuelve el número de procedimientos almacenados transferidos. Mediante la asignación de una variable definida por el usuario para el `ExecValueVariable` propiedad de la tarea Transferir procedimientos almacenados principales, información sobre la transferencia del procedimiento almacenado puede ponerse a disposición de otros objetos en el paquete. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) y [Usar variables en paquetes](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Entradas del registro  
 La tarea Transferir procedimientos almacenados principales incluye las siguientes entradas del registro personalizadas:  
  
-   TransferStoredProceduresTaskStartTransferringObjects  Esta entrada del registro indica que se ha iniciado la transferencia. La entrada del registro incluye la hora de inicio.  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  Esta entrada del registro indica que ha finalizado la transferencia. La entrada del registro incluye la hora de finalización.  
  
 Además, una entrada del registro para el `OnInformation` eventos informa del número de procedimientos almacenados que se han transferido y una entrada del registro para el `OnWarning` se escribe el evento por cada procedimiento almacenado que se sobrescribe en el destino.  
  
## <a name="security-and-permissions"></a>Seguridad y permisos  
 El usuario debe tener permisos para ver la lista de procedimientos almacenados de la base de datos **master** en el origen y debe ser miembro del rol de servidor sysadmin o tener permisos para crear procedimientos almacenados en la base de datos **master** del servidor de destino.  
  
## <a name="configuration-of-the-transfer-master-stored-procedures-task"></a>Configuración de la tarea Transferir procedimientos almacenados principales  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Transferir el Editor de tareas de procedimientos almacenados Master &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Transferir el Editor de tareas de procedimientos almacenados Master &#40;almacena la página de procedimientos&#41;](../transfer-master-stored-procedures-task-editor-stored-procedures-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### <a name="configuring-the-transfer-master-stored-procedures-task-programmatically"></a>Configurar la tarea Transferir procedimientos almacenados principales mediante programación  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Vea también  
 [Transferir objetos de tarea SQL Server](transfer-sql-server-objects-task.md)   
 [Tareas de Integration Services](integration-services-tasks.md)   
 [Flujo de control](control-flow.md)  
  
  