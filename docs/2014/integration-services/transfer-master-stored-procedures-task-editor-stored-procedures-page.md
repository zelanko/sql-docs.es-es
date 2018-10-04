---
title: Transferir el Editor de tareas de procedimientos almacenados principales (página procedimientos almacenados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords:
- Transfer Stored Procedures Task Editor
ms.assetid: 5fcf171e-cc0b-4c24-8eb5-3a4b4775e64a
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5dbc012d6f6e14847f38d7fe4a8de2f47eb907d2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218893"
---
# <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>Editor de la tarea Transferir procedimientos almacenados principales (página Procedimientos almacenados)
  Use la página **Procedimientos almacenados** del cuadro de diálogo **Editor de la tarea Transferir procedimientos almacenados principales** a fin de especificar las propiedades para copiar uno o más procedimientos definidos por el usuario desde la base de datos **maestra** en una instancia de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a una base de datos **maestra** de otra instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener más información acerca de esta tarea, vea [Transfer Master Stored Procedures Task](control-flow/transfer-master-stored-procedures-task.md).  
  
> [!NOTE]  
>  Esta tarea transfiere solo los procedimientos almacenados definidos por el usuario que pertenecen a **dbo** desde una base de datos **master** del servidor de origen a una base de datos **master** del servidor de destino. A los usuarios se les debe conceder el permiso CREATE PROCEDURE en la base de datos **maestra** del servidor de destino o deben ser miembros del rol fijo del servidor **sysadmin** del servidor de destino para crear procedimientos almacenados en dicho servidor.  
  
## <a name="options"></a>Opciones  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista, o bien haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de origen.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de destino.  
  
 **IfObjectExists**  
 Seleccione el modo en que la tarea debe controlar los procedimientos almacenados definidos por el usuario que tengan el mismo nombre que los que ya existen en la base de datos **maestra** del servidor de destino.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**FailTask**|La tarea genera un error si ya existen procedimientos almacenados con el mismo nombre en la base de datos **maestra** del servidor de destino.|  
|**Sobrescribir**|La tarea sobrescribe los procedimientos almacenados con el mismo nombre en la base de datos **maestra** del servidor de destino.|  
|**Omitir**|La tarea omite los procedimientos almacenados con el mismo nombre que ya existen en la base de datos **maestra** del servidor de destino.|  
  
 **TransferAllStoredProcedures**  
 Seleccione esta opción si todos los procedimientos almacenados definidos por el usuario de la base de datos **maestra** del servidor de origen deben copiarse al servidor de destino.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**True**|Copie todos los procedimientos almacenados definidos por el usuario de la base de datos **maestra** .|  
|**False**|Copie solamente los procedimientos almacenados especificados.|  
  
 **StoredProceduresList**  
 Seleccione los procedimientos almacenados definidos por el usuario de la base de datos **maestra** del servidor de origen que deben copiarse a la base de datos **maestra** de destino. Esta opción solo está disponible cuando **TransferAllStoredProcedures** se establece en **False**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Tareas de Integration Services](control-flow/integration-services-tasks.md)   
 [Transferir el Editor de tareas de procedimientos almacenados principales &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Página expresiones](expressions/expressions-page.md)   
 [Administrador de conexiones SMO](connection-manager/smo-connection-manager.md)  
  
  
