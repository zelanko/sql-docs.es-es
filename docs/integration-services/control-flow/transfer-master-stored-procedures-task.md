---
title: Tarea Transferir procedimientos almacenados principales | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transfermasterspstask.f1
- sql13.dts.designer.transferstoredprocedurestask.general.f1
- sql13.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords:
- Transfer Master Stored Procedures task [Integration Services]
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 83001193fc8cedf13bf7425d6b8bae88ac09c987
ms.contentlocale: es-es
ms.lasthandoff: 08/11/2017

---
# <a name="transfer-master-stored-procedures-task"></a>Tarea Transferir procedimientos almacenados principales
  La tarea Transferir procedimientos almacenados principales transfiere uno o más procedimientos almacenados definidos por el usuario entre las bases de datos **master** en instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para transferir un procedimiento almacenado de la base de datos **master** , el propietario del procedimiento debe ser dbo.  
  
 La tarea Transferir procedimientos almacenados principales se puede configurar para que transfiera todos los procedimientos almacenados o solo los procedimientos especificados. Esta tarea no copia procedimientos almacenados del sistema.  
  
 Es posible que los procedimientos almacenados principales que desea transferir ya existan en el destino. La tarea Transferir procedimientos almacenados principales se puede configurar para que haga lo siguiente con los procedimientos almacenados existentes:  
  
-   Sobrescribir procedimientos almacenados existentes.  
  
-   Hacer que la tarea genere un error cuando existan procedimientos almacenados duplicados.  
  
-   Omitir los procedimientos almacenados duplicados.  
  
 Durante la ejecución, la tarea Transferir procedimientos almacenados principales se conecta a los servidores de origen y de destino a través de dos administradores de conexión SMO. Los administradores de conexión SMO se configuran independientemente de la tarea Transferir procedimientos almacenados principales y después se hace referencia a ellos en la tarea Transferir procedimientos almacenados principales. Los administradores de conexión SMO especifican el servidor y el modo de autenticación que se utilizará para tener acceso al servidor. Para más información, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-stored-procedures-between-instances-of-sql-server"></a>Transferir procedimientos almacenados entre instancias de SQL Server  
 La tarea Transferir procedimientos almacenados principales admite un origen y un destino que sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventos  
 La tarea emite un evento de información que indica el número de procedimientos almacenados transferidos y un evento de advertencia cuando se sobrescribe un procedimiento almacenado.  
  
 La tarea Transferir procedimientos almacenados principales no indica el progreso incremental de la transferencia; solo indica 0% y 100%.  
  
## <a name="execution-value"></a>Valor de ejecución  
 El valor de ejecución, que se define en la propiedad **ExecutionValue** de la tarea, devuelve el número de procedimientos almacenados transferidos. Si se asigna una variable definida por el usuario a la propiedad **ExecValueVariable** de la tarea Transferir procedimientos almacenados principales, se puede hacer que la información sobre la transferencia de procedimientos almacenados esté disponible para otros objetos del paquete. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Usar variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Entradas del registro  
 La tarea Transferir procedimientos almacenados principales incluye las siguientes entradas del registro personalizadas:  
  
-   TransferStoredProceduresTaskStartTransferringObjects  Esta entrada del registro indica que se ha iniciado la transferencia. La entrada del registro incluye la hora de inicio.  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  Esta entrada del registro indica que ha finalizado la transferencia. La entrada del registro incluye la hora de finalización.  
  
 Además, una entrada del registro para el evento **OnInformation** indica el número de procedimientos almacenados transferidos, y se escribe una entrada del registro para el evento **OnWarning** por cada procedimiento almacenado que se sobrescribe en el destino.  
  
## <a name="security-and-permissions"></a>Seguridad y permisos  
 El usuario debe tener permisos para ver la lista de procedimientos almacenados de la base de datos **master** en el origen y debe ser miembro del rol de servidor sysadmin o tener permisos para crear procedimientos almacenados en la base de datos **master** del servidor de destino.  
  
## <a name="configuration-of-the-transfer-master-stored-procedures-task"></a>Configuración de la tarea Transferir procedimientos almacenados principales  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### <a name="configuring-the-transfer-master-stored-procedures-task-programmatically"></a>Configurar la tarea Transferir procedimientos almacenados principales mediante programación  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-master-stored-procedures-task-editor-general-page"></a>Editor de la tarea Transferir procedimientos almacenados principales (Página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea Transferir procedimientos almacenados principales** para asignar un nombre a la tarea de transferencia de procedimientos almacenados master y describirla.  
  
> [!NOTE]  
>  Esta tarea transfiere solo los procedimientos almacenados definidos por el usuario que pertenecen a **dbo** desde una base de datos **master** del servidor de origen a una base de datos **master** del servidor de destino. A los usuarios se les debe conceder el permiso CREATE PROCEDURE en la base de datos **maestra** del servidor de destino o deben ser miembros del rol fijo del servidor **sysadmin** del servidor de destino para crear procedimientos almacenados en dicho servidor.  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Escriba un nombre único para la tarea de transferencia de procedimientos almacenados principales. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Description**  
 Escriba una descripción de la tarea de transferencia de procedimientos almacenados principales.  
  
## <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>Editor de la tarea Transferir procedimientos almacenados principales (página Procedimientos almacenados)
  Use la página **Procedimientos almacenados** del cuadro de diálogo **Editor de la tarea Transferir procedimientos almacenados principales** a fin de especificar las propiedades para copiar uno o más procedimientos definidos por el usuario desde la base de datos **maestra** en una instancia de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a una base de datos **maestra** de otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Esta tarea transfiere solo los procedimientos almacenados definidos por el usuario que pertenecen a **dbo** desde una base de datos **master** del servidor de origen a una base de datos **master** del servidor de destino. A los usuarios se les debe conceder el permiso CREATE PROCEDURE en la base de datos **maestra** del servidor de destino o deben ser miembros del rol fijo del servidor **sysadmin** del servidor de destino para crear procedimientos almacenados en dicho servidor.  
  
### <a name="options"></a>Opciones  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en  **\<nueva conexión... >** para crear una nueva conexión con el servidor de origen.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en  **\<nueva conexión... >** para crear una nueva conexión con el servidor de destino.  
  
 **IfObjectExists**  
 Seleccione el modo en que la tarea debe controlar los procedimientos almacenados definidos por el usuario que tengan el mismo nombre que los que ya existen en la base de datos **maestra** del servidor de destino.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Value|Description|  
|-----------|-----------------|  
|**FailTask**|La tarea genera un error si ya existen procedimientos almacenados con el mismo nombre en la base de datos **maestra** del servidor de destino.|  
|**Sobrescribir**|La tarea sobrescribe los procedimientos almacenados con el mismo nombre en la base de datos **maestra** del servidor de destino.|  
|**Omitir**|La tarea omite los procedimientos almacenados con el mismo nombre que ya existen en la base de datos **maestra** del servidor de destino.|  
  
 **TransferAllStoredProcedures**  
 Seleccione esta opción si todos los procedimientos almacenados definidos por el usuario de la base de datos **maestra** del servidor de origen deben copiarse al servidor de destino.  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|Copie todos los procedimientos almacenados definidos por el usuario de la base de datos **maestra** .|  
|**False**|Copie solamente los procedimientos almacenados especificados.|  
  
 **StoredProceduresList**  
 Seleccione los procedimientos almacenados definidos por el usuario de la base de datos **maestra** del servidor de origen que deben copiarse a la base de datos **maestra** de destino. Esta opción solo está disponible cuando **TransferAllStoredProcedures** se establece en **False**.  
  
## <a name="see-also"></a>Vea también  
 [Tarea Transferir objetos de SQL Server](../../integration-services/control-flow/transfer-sql-server-objects-task.md)   
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  

