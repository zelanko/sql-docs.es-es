---
title: "Transferir inicios de sesión, tarea | Documentos de Microsoft"
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
- sql13.dts.designer.transferloginstask.f1
- sql13.dts.designer.transferloginstask.general.f1
- sql13.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins task [Integration Services]
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 2027b3ea760568ced8a41b72a7a2c3cf225de94f
ms.contentlocale: es-es
ms.lasthandoff: 08/11/2017

---
# <a name="transfer-logins-task"></a>Tarea Transferir inicios de sesión
  La tarea Transferir inicios de sesión transfiere uno o varios inicios de sesión entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="transfer-logins-between-instances-of-sql-server"></a>Transferir inicios de sesión entre instancias de SQL Server  
 La tarea Transferir inicios de sesión admite un origen y un destino que sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventos  
 La tarea Transferir inicios de sesión emite un evento de información que indica el número de inicios de sesión transferidos y un evento de advertencia cuando se sobrescribe un inicio de sesión.  
  
 La tarea Transferir inicios de sesión no indica el progreso incremental de la transferencia; solo indica 0% y 100%.  
  
## <a name="execution-value"></a>Valor de ejecución  
 El valor de ejecución, que se define en la propiedad **ExecutionValue** de la tarea, devuelve el número de inicios de sesión transferidos. Si se asigna una variable definida por el usuario a la propiedad **ExecValueVariable** de la tarea Transferir inicios de sesión, se puede conseguir que la información sobre la transferencia de inicios de sesión esté disponible para otros objetos del paquete. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Usar variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Entradas del registro  
 La tarea Transferir inicios de sesión incluye las siguientes entradas del registro personalizadas:  
  
-   TransferLoginsTaskStarTransferringObjects    Esta entrada del registro indica que se ha iniciado la transferencia. La entrada del registro incluye la hora de inicio.  
  
-   TransferLoginsTaskFinishedTransferringObjects    Esta entrada del registro indica que ha finalizado la transferencia. La entrada del registro incluye la hora de finalización.  
  
 Además, una entrada del registro para el evento **OnInformation** indica el número de inicios de sesión transferidos, y se escribe una entrada del registro para el evento **OnWarning** por cada inicio de sesión que se sobrescribe en el destino.  
  
## <a name="security-and-permissions"></a>Seguridad y permisos  
 Para examinar inicios de sesión en el servidor de origen y crear inicios de sesión en el servidor de destino, el usuario debe ser miembro del rol de servidor sysadmin en ambos servidores.  
  
## <a name="configuration-of-the-transfer-logins-task"></a>Configuración de la tarea Transferir inicios de sesión  
 La tarea Transferir inicios de sesión se puede configurar para que transfiera todos los inicios de sesión, solo los inicios de sesión especificados o solo todos los inicios de sesión que tengan acceso a las bases de datos especificadas. El inicio de sesión sa no se puede transferir. Se puede cambiar el nombre del inicio de sesión sa, aunque tampoco se podrá transferir el inicio de sesión sa con el nuevo nombre.  
  
 También puede indicar si la tarea copia los identificadores de seguridad (SID) asociados a los inicios de sesión. Si se utiliza la tarea Transferir inicios de sesión en combinación con la tarea Transferir bases de datos, se deben copiar los SID al destino; de lo contrario, la base de datos de destino no reconocería los inicios de sesión transferidos.  
  
 En el destino, los inicios de sesión transferidos se deshabilitan y se asignan contraseñas aleatorias. Un miembro del rol sysadmin en el servidor de destino debe cambiar las contraseñas y habilitar los inicios de sesión para que se puedan utilizar.  
  
 Es posible que los inicios de sesión transferidos ya existan en el destino. La tarea Transferir inicios de sesión se puede configurar para haga lo siguiente con los inicios de sesión existentes:  
  
-   Sobrescribir los inicios de sesión existentes.  
  
-   Hacer que la tarea genere un error cuando existan inicios de sesión duplicados.  
  
-   Omitir los inicios de sesión duplicados.  
  
 Durante la ejecución, la tarea Transferir inicios de sesión se conecta a los servidores de origen y de destino utilizando dos administradores de conexión SMO. Los administradores de conexión SMO se configuran independientemente de la tarea Transferir inicios de sesión y después se hace referencia a ellos en la tarea Transferir inicios de sesión. Los administradores de conexión SMO especifican el servidor y el modo de autenticación que se utilizará para tener acceso al servidor. Para más información, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-logins-task"></a>Configuración mediante programación de la tarea Transferir inicios de sesión  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
## <a name="transfer-logins-task-editor-general-page"></a>Editor de la tarea Transferir inicios de sesión (página General)
  Utilice la página **General** del cuadro de diálogo **Editor de la tarea Transferir inicios de sesión** para asignar un nombre y describir la tarea Transferir inicios de sesión.  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Escriba un nombre único para la tarea Transferir inicios de sesión. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Description**  
 Escriba una descripción de la tarea Transferir inicios de sesión.  
  
## <a name="transfer-logins-task-editor-logins-page"></a>Editor de la tarea Transferir inicios de sesión (página Inicios de sesión)
  Utilice la página **Inicios de sesión** del cuadro de diálogo **Editor de la tarea Transferir inicios de sesión** para especificar propiedades para copiar uno o varios inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otra.  
  
> [!IMPORTANT]  
>  Cuando se ejecuta la tarea Transferir inicios de sesión, se crean inicios de sesión en el servidor de destino con contraseñas aleatorias y se deshabilitan las contraseñas. Para utilizar estos inicios de sesión, un miembro del rol fijo de servidor **sysadmin** debe cambiar las contraseñas y, a continuación, habilitarlas. El inicio de sesión **sa** no se puede transferir.  
  
### <a name="options"></a>Opciones  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en  **\<nueva conexión... >** para crear una nueva conexión con el servidor de origen.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en  **\<nueva conexión... >** para crear una nueva conexión con el servidor de destino.  
  
 **LoginsToTransfer**  
 Seleccione los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que va a copiar del servidor de origen al de destino. Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Value|Description|  
|-----------|-----------------|  
|**AllLogins**|Todos los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el servidor de origen se copiarán al de destino.|  
|**SelectedLogins**|Solo los inicios de sesión especificados con **LoginsList** se copiarán al servidor de destino.|  
|**AllLoginsFromSelectedDatabases**|Todos los inicios de sesión de las bases de datos especificadas con **DatabasesList** se copiarán al servidor de destino.|  
  
 **LoginsList**  
 Seleccione los inicios de sesión en el servidor de origen que se copiarán al de destino. Esta opción solo está disponible cuando se selecciona **SelectedLogins** para **LoginsToTransfer**.  
  
 **DatabasesList**  
 Seleccione las bases de datos en el servidor de origen que contienen inicios de sesión que se copiarán al de destino. Esta opción solo está disponible cuando se selecciona **AllLoginsFromSelectedDatabases** para **LoginsToTransfer**.  
  
 **IfObjectExists**  
 Seleccione cómo debe administrar la tarea los inicios de sesión con el mismo nombre que existan ya en el servidor de destino.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Value|Description|  
|-----------|-----------------|  
|**FailTask**|La tarea genera un error si existen ya inicios de sesión con el mismo nombre en el servidor de destino.|  
|**Sobrescribir**|La tarea sobrescribe los inicios de sesión con el mismo nombre en el servidor de destino.|  
|**Omitir**|La tarea omite los inicios de sesión con el mismo nombre que existan en el servidor de destino.|  
  
 **CopySids**  
 Seleccione esta opción si los identificadores de seguridad asociados a los inicios de sesión deben copiarse al servidor de destino. **CopySids** debe establecerse en **True** si la tarea Transferir inicios de sesión se utiliza junto con la tarea Transferir bases de datos. De lo contrario, la base de datos transferida no reconocerá los inicios de sesión copiados.  
  

