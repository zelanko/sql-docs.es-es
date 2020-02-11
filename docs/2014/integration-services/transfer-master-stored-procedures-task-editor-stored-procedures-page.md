---
title: Editor de la tarea transferir procedimientos almacenados principales (página procedimientos almacenados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords:
- Transfer Stored Procedures Task Editor
ms.assetid: 5fcf171e-cc0b-4c24-8eb5-3a4b4775e64a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f233f0730286a1623ee54c38084d07a2aba903e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054860"
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
  
|Value|Descripción|  
|-----------|-----------------|  
|**FailTask**|La tarea genera un error si ya existen procedimientos almacenados con el mismo nombre en la base de datos **maestra** del servidor de destino.|  
|**Sobrescribir**|La tarea sobrescribe los procedimientos almacenados con el mismo nombre en la base de datos **maestra** del servidor de destino.|  
|**Skip**|La tarea omite los procedimientos almacenados con el mismo nombre que ya existen en la base de datos **maestra** del servidor de destino.|  
  
 **TransferAllStoredProcedures**  
 Seleccione esta opción si todos los procedimientos almacenados definidos por el usuario de la base de datos **maestra** del servidor de origen deben copiarse al servidor de destino.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**True**|Copie todos los procedimientos almacenados definidos por el usuario de la base de datos **maestra** .|  
|**False**|Copie solamente los procedimientos almacenados especificados.|  
  
 **StoredProceduresList**  
 Seleccione los procedimientos almacenados definidos por el usuario de la base de datos **maestra** del servidor de origen que deben copiarse a la base de datos **maestra** de destino. Esta opción solo está disponible cuando **TransferAllStoredProcedures** se establece en **False**.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Tareas de Integration Services](control-flow/integration-services-tasks.md)   
 [Editor de la tarea transferir procedimientos almacenados principales &#40;página general&#41;](general-page-of-integration-services-designers-options.md)   
 [Página Expresiones](expressions/expressions-page.md)   
 [SMO, administrador de conexiones](connection-manager/smo-connection-manager.md)  
  
  
