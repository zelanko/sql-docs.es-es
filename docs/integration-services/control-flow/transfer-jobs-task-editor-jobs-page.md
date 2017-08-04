---
title: "Transferir el Editor de la tarea de trabajos (página trabajos) | Documentos de Microsoft"
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
- sql13.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs Task Editor
ms.assetid: e72b1dc7-8cda-4ee6-abb5-d438370f04df
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5efb3b22c8cb6849b5a70423cfd4b51b45c21686
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-jobs-task-editor-jobs-page"></a>Editor de la tarea Transferir trabajos (página Trabajos)
  Utilice la página **Trabajos** del cuadro de diálogo **Editor de la tarea Transferir trabajos** para especificar las propiedades de copia de una o más tareas del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otra. Para obtener más información acerca de la tarea Transferir trabajos, vea [Transfer Jobs Task](../../integration-services/control-flow/transfer-jobs-task.md).  
  
> [!NOTE]  
>  Para tener acceso a trabajos del servidor de origen, los usuarios deben ser miembros de al menos el rol fijo de base de datos **SQLAgentUserRole** en el servidor. Para crear trabajos correctamente en el servidor de destino, el usuario debe ser miembro del rol fijo de servidor **sysadmin** o una de los roles fijos de base de datos del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información sobre los roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus permisos, vea [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="options"></a>Opciones  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en  **\<nueva conexión... >** para crear una nueva conexión con el servidor de origen.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en  **\<nueva conexión... >** para crear una nueva conexión con el servidor de destino.  
  
 **TransferAllJobs**  
 Seleccione si la tarea debe copiar todos los trabajos del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o solo los trabajos especificados del origen al servidor de destino.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|Copia todos los trabajos.|  
|**False**|Copia solo los trabajos especificados.|  
  
 **JobsList**  
 Haga clic en el botón para examinar **(…)** para seleccionar los trabajos que quiere copiar. Se debe seleccionar al menos un trabajo.  
  
> [!NOTE]  
>  Especifique **SourceConnection** antes de seleccionar los trabajos que quiere copiar.  
  
 La opción **JobsList** no está disponible cuando **TransferAllJobs** se establece como **True**.  
  
 **IfObjectExists**  
 Seleccione cómo debería controlar la tarea los trabajos con el mismo nombre que ya existen en el servidor de destino.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Value|Description|  
|-----------|-----------------|  
|**FailTask**|La tarea falla si ya existen trabajos con el mismo nombre en el servidor de destino.|  
|**Sobrescribir**|La tarea sobrescribe los trabajos con el mismo nombre en el servidor de destino.|  
|**Omitir**|La tarea omite los trabajos con el mismo nombre que existen en el servidor de destino.|  
  
 **EnableJobsAtDestination**  
 Seleccione si se deben habilitar los trabajos copiados en el servidor de destino.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|Habilita los trabajos en el servidor de destino.|  
|**False**|Deshabilita los trabajos en el servidor de destino.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor de la tarea Transferir trabajos &#40; Página general &#41;](../../integration-services/control-flow/transfer-jobs-task-editor-general-page.md)   
 [Página expresiones](../../integration-services/expressions/expressions-page.md)   
 [Administrador de conexiones SMO.](../../integration-services/connection-manager/smo-connection-manager.md)  
  
  
