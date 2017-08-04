---
title: "Transferir Editor (página procedimientos almacenados) de la tarea de procedimientos almacenados Master | Documentos de Microsoft"
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
- sql13.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords:
- Transfer Stored Procedures Task Editor
ms.assetid: 5fcf171e-cc0b-4c24-8eb5-3a4b4775e64a
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 454835b1fe51015f9fd7668dcb4c639f3287edd6
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>Editor de la tarea Transferir procedimientos almacenados principales (página Procedimientos almacenados)
  Use la página **Procedimientos almacenados** del cuadro de diálogo **Editor de la tarea Transferir procedimientos almacenados principales** a fin de especificar las propiedades para copiar uno o más procedimientos definidos por el usuario desde la base de datos **maestra** en una instancia de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a una base de datos **maestra** de otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información acerca de esta tarea, vea [Transfer Master Stored Procedures Task](../../integration-services/control-flow/transfer-master-stored-procedures-task.md).  
  
> [!NOTE]  
>  Esta tarea transfiere solo los procedimientos almacenados definidos por el usuario que pertenecen a **dbo** desde una base de datos **master** del servidor de origen a una base de datos **master** del servidor de destino. A los usuarios se les debe conceder el permiso CREATE PROCEDURE en la base de datos **maestra** del servidor de destino o deben ser miembros del rol fijo del servidor **sysadmin** del servidor de destino para crear procedimientos almacenados en dicho servidor.  
  
## <a name="options"></a>Opciones  
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
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor de la tarea de transferencia de maestro de procedimientos almacenados &#40; Página general &#41;](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-general-page.md)   
 [Página expresiones](../../integration-services/expressions/expressions-page.md)   
 [Administrador de conexiones SMO.](../../integration-services/connection-manager/smo-connection-manager.md)  
  
  
