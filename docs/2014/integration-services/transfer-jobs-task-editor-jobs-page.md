---
title: Editor de la tarea transferir trabajos (página trabajos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs Task Editor
ms.assetid: e72b1dc7-8cda-4ee6-abb5-d438370f04df
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 43066d036a23a063c218234b3a346bf89560994f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054988"
---
# <a name="transfer-jobs-task-editor-jobs-page"></a>Editor de la tarea Transferir trabajos (página Trabajos)
  Utilice la página **Trabajos** del cuadro de diálogo **Editor de la tarea Transferir trabajos** para especificar las propiedades de copia de una o más tareas del Agente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a otra. Para obtener más información acerca de la tarea Transferir trabajos, vea [Transfer Jobs Task](control-flow/transfer-jobs-task.md).  
  
> [!NOTE]  
>  Para tener acceso a trabajos del servidor de origen, los usuarios deben ser miembros de al menos el rol fijo de base de datos **SQLAgentUserRole** en el servidor. Para crear trabajos correctamente en el servidor de destino, el usuario debe ser miembro del rol fijo de servidor **sysadmin** o una de los roles fijos de base de datos del Agente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para obtener más información sobre los roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y sus permisos, vea [Roles fijos de base de datos del Agente SQL Server](../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="options"></a>Opciones  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista, o bien haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de origen.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de destino.  
  
 **TransferAllJobs**  
 Seleccione si la tarea debe copiar todos los trabajos del Agente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o solo los trabajos especificados del origen al servidor de destino.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**True**|Copia todos los trabajos.|  
|**False**|Copia solo los trabajos especificados.|  
  
 **JobsList**  
 Haga clic en el botón Examinar **(…)** para seleccionar los trabajos que quiere copiar. Se debe seleccionar al menos un trabajo.  
  
> [!NOTE]  
>  Especifique **SourceConnection** antes de seleccionar los trabajos que quiere copiar.  
  
 La opción **JobsList** no está disponible cuando **TransferAllJobs** se establece como **True**.  
  
 **IfObjectExists**  
 Seleccione cómo debería controlar la tarea los trabajos con el mismo nombre que ya existen en el servidor de destino.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**FailTask**|La tarea falla si ya existen trabajos con el mismo nombre en el servidor de destino.|  
|**Sobrescribir**|La tarea sobrescribe los trabajos con el mismo nombre en el servidor de destino.|  
|**Skip**|La tarea omite los trabajos con el mismo nombre que existen en el servidor de destino.|  
  
 **EnableJobsAtDestination**  
 Seleccione si se deben habilitar los trabajos copiados en el servidor de destino.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**True**|Habilita los trabajos en el servidor de destino.|  
|**False**|Deshabilita los trabajos en el servidor de destino.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Tareas de Integration Services](control-flow/integration-services-tasks.md)   
 [Editor de la tarea Transferir trabajos &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Página Expresiones](expressions/expressions-page.md)   
 [SMO, administrador de conexiones](connection-manager/smo-connection-manager.md)  
  
  
