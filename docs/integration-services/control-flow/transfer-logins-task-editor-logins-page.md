---
title: "Editor de la tarea Transferir inicios de sesi&#243;n (p&#225;gina Inicios de sesi&#243;n) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.transferloginstask.logins.f1"
helpviewer_keywords: 
  - "Transferir inicios de sesión, editor de la tarea"
ms.assetid: bf244c24-bd45-4ece-b66b-78b488f35c5b
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# Editor de la tarea Transferir inicios de sesi&#243;n (p&#225;gina Inicios de sesi&#243;n)
  Utilice la página **Inicios de sesión** del cuadro de diálogo **Editor de la tarea Transferir inicios de sesión** para especificar propiedades para copiar uno o varios inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otra. Para obtener más información acerca de esta tarea, vea [Transfer Logins Task](../../integration-services/control-flow/transfer-logins-task.md).  
  
> [!IMPORTANT]  
>  Cuando se ejecuta la tarea Transferir inicios de sesión, se crean inicios de sesión en el servidor de destino con contraseñas aleatorias y se deshabilitan las contraseñas. Para utilizar estos inicios de sesión, un miembro del rol fijo de servidor **sysadmin** debe cambiar las contraseñas y, a continuación, habilitarlas. El inicio de sesión **sa** no se puede transferir.  
  
## Opciones  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista, o bien haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de origen.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista, o bien haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de destino.  
  
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
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor de la tarea Transferir inicios de sesión &#40;página General&#41;](../../integration-services/control-flow/transfer-logins-task-editor-general-page.md)   
 [Página Expresiones](../../integration-services/expressions/expressions-page.md)   
 [Administrador de conexiones SMO](../../integration-services/connection-manager/smo-connection-manager.md)   
 [Contraseñas seguras](../../relational-databases/security/strong-passwords.md)   
 [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  