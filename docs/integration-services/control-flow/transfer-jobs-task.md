---
title: Tarea Transferir trabajos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferjobstask.f1
- sql13.dts.designer.transferjobstask.general.f1
- sql13.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e5747cc9fbac122e9bca7fa6a127fd74a4ec47ff
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916125"
---
# <a name="transfer-jobs-task"></a>Tarea Transferir trabajos

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  La tarea Transferir trabajos transfiere uno o varios trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La tarea Transferir trabajos se puede configurar para que transfiera todos los trabajos o solo los trabajos especificados. También puede indicar si los trabajos transferidos se habilitarán en el destino.  
  
 Es posible que los trabajos transferidos ya existan en el destino. La tarea Transferir trabajos se puede configurar para haga lo siguiente con los trabajos existentes:  
  
-   Sobrescribir los trabajos existentes.  
  
-   Hacer que la tarea genere un error cuando existan trabajos duplicados.  
  
-   Omitir los trabajos duplicados.  
  
 Durante la ejecución, la tarea Transferir trabajos se conecta a los servidores de origen y de destino utilizando uno o dos administradores de conexión SMO. El administrador de conexiones SMO se configura independientemente de la tarea Transferir trabajos y después se hace referencia a él en la tarea Transferir trabajos. El administrador de conexiones SMO especifica el servidor y el modo de autenticación que se utiliza para tener acceso al servidor. Para más información, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>Transferir trabajos entre instancias de SQL Server  
 La tarea Transferir trabajos admite un origen y un destino que sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No hay restricciones respecto a qué versión hay que usar como origen o como destino.  
  
## <a name="events"></a>Eventos  
 La tarea Transferir trabajos emite un evento de información que indica el número de trabajos transferidos y un evento de advertencia cuando se sobrescribe un trabajo. La tarea no indica el progreso incremental de la transferencia de los trabajos; solo indica 0% y 100%.  
  
## <a name="execution-value"></a>Valor de ejecución  
 El valor de ejecución, que se define en la propiedad **ExecutionValue** de la tarea, devuelve el número de trabajos transferidos. Si se asigna una variable definida por el usuario a la propiedad **ExecValueVariable** de la tarea Transferir trabajos, se puede hacer que la información de la transferencia de trabajos esté disponible para otros objetos del paquete. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Usar variables en paquetes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Entradas del registro  
 La tarea Transferir trabajos incluye las siguientes entradas del registro personalizadas:  
  
-   TransferJobsTaskStarTransferringObjects   Esta entrada del registro indica que se ha iniciado la transferencia. La entrada del registro incluye la hora de inicio.  
  
-   TransferJobsTaskFinishedTransferringObjects   Esta entrada del registro indica que ha finalizado la transferencia. La entrada del registro incluye la hora de finalización.  
  
 Además, una entrada del registro para el evento **OnInformation** indica el número de trabajos transferidos y se escribe una entrada del registro para el evento **OnWarning** por cada trabajo que se sobrescribe en el destino.  
  
## <a name="security-and-permissions"></a>Seguridad y permisos  
 Para transferir trabajos, el usuario debe ser miembro del rol fijo de servidor sysadmin o de uno de los roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos msdb tanto en la instancia de origen como en la de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>Configuración de la tarea Transferir trabajos  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener información acerca de cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-jobs-task-editor-general-page"></a>Editor de la tarea Transferir trabajos (página General)
  Utilice la página **General** del cuadro de diálogo **Editor de la tarea Transferir trabajos** para asignar un nombre y describir la tarea Transferir trabajos.  
  
> [!NOTE]  
>  Solo los miembros del rol fijo de servidor **sysadmin** o uno de los roles fijos de base de datos del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el servidor de destino pueden crear trabajos correctamente en este servidor. Para tener acceso a los trabajos del servidor de origen, los usuarios deben ser miembros de al menos el rol fijo de base de datos **SQLAgentUserRole** en este servidor. Para obtener más información sobre los roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus permisos, vea [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Escriba un nombre único para la tarea Transferir trabajos. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Transferir trabajos.  
  
## <a name="transfer-jobs-task-editor-jobs-page"></a>Editor de la tarea Transferir trabajos (página Trabajos)
  Utilice la página **Trabajos** del cuadro de diálogo **Editor de la tarea Transferir trabajos** para especificar las propiedades de copia de una o más tareas del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otra.  
  
> [!NOTE]  
>  Para tener acceso a trabajos del servidor de origen, los usuarios deben ser miembros de al menos el rol fijo de base de datos **SQLAgentUserRole** en el servidor. Para crear trabajos correctamente en el servidor de destino, el usuario debe ser miembro del rol fijo de servidor **sysadmin** o una de los roles fijos de base de datos del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información sobre los roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus permisos, vea [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
### <a name="options"></a>Opciones  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en **\<New connection...>** para crear una nueva conexión al servidor de origen.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en **\<New connection...>** para crear una nueva conexión al servidor de destino.  
  
 **TransferAllJobs**  
 Seleccione si la tarea debe copiar todos los trabajos del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o solo los trabajos especificados del origen al servidor de destino.  
  
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
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  
