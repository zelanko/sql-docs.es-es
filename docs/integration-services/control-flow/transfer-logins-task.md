---
title: "Tarea Transferir inicios de sesi&#243;n | Microsoft Docs"
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
  - "sql13.dts.designer.transferloginstask.f1"
helpviewer_keywords: 
  - "Transferir inicios de sesión, tarea [Integration Services]"
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# Tarea Transferir inicios de sesi&#243;n
  La tarea Transferir inicios de sesión transfiere uno o varios inicios de sesión entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Transferir inicios de sesión entre instancias de SQL Server  
 La tarea Transferir inicios de sesión admite un origen y un destino que sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## Eventos  
 La tarea Transferir inicios de sesión emite un evento de información que indica el número de inicios de sesión transferidos y un evento de advertencia cuando se sobrescribe un inicio de sesión.  
  
 La tarea Transferir inicios de sesión no indica el progreso incremental de la transferencia; solo indica 0% y 100%.  
  
## Valor de ejecución  
 El valor de ejecución, que se define en la propiedad **ExecutionValue** de la tarea, devuelve el número de inicios de sesión transferidos. Si se asigna una variable definida por el usuario a la propiedad **ExecValueVariable** de la tarea Transferir inicios de sesión, se puede conseguir que la información sobre la transferencia de inicios de sesión esté disponible para otros objetos del paquete. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Usar variables en paquetes](../Topic/Use%20Variables%20in%20Packages.md).  
  
## Entradas del registro  
 La tarea Transferir inicios de sesión incluye las siguientes entradas del registro personalizadas:  
  
-   TransferLoginsTaskStarTransferringObjects    Esta entrada del registro indica que se ha iniciado la transferencia. La entrada del registro incluye la hora de inicio.  
  
-   TransferLoginsTaskFinishedTransferringObjects    Esta entrada del registro indica que ha finalizado la transferencia. La entrada del registro incluye la hora de finalización.  
  
 Además, una entrada del registro para el evento **OnInformation** indica el número de inicios de sesión transferidos, y se escribe una entrada del registro para el evento **OnWarning** por cada inicio de sesión que se sobrescribe en el destino.  
  
## Seguridad y permisos  
 Para examinar inicios de sesión en el servidor de origen y crear inicios de sesión en el servidor de destino, el usuario debe ser miembro del rol de servidor sysadmin en ambos servidores.  
  
## Configuración de la tarea Transferir inicios de sesión  
 La tarea Transferir inicios de sesión se puede configurar para que transfiera todos los inicios de sesión, solo los inicios de sesión especificados o solo todos los inicios de sesión que tengan acceso a las bases de datos especificadas. El inicio de sesión sa no se puede transferir. Se puede cambiar el nombre del inicio de sesión sa, aunque tampoco se podrá transferir el inicio de sesión sa con el nuevo nombre.  
  
 También puede indicar si la tarea copia los identificadores de seguridad (SID) asociados a los inicios de sesión. Si se utiliza la tarea Transferir inicios de sesión en combinación con la tarea Transferir bases de datos, se deben copiar los SID al destino; de lo contrario, la base de datos de destino no reconocería los inicios de sesión transferidos.  
  
 En el destino, los inicios de sesión transferidos se deshabilitan y se asignan contraseñas aleatorias. Un miembro del rol sysadmin en el servidor de destino debe cambiar las contraseñas y habilitar los inicios de sesión para que se puedan utilizar.  
  
 Es posible que los inicios de sesión transferidos ya existan en el destino. La tarea Transferir inicios de sesión se puede configurar para haga lo siguiente con los inicios de sesión existentes:  
  
-   Sobrescribir los inicios de sesión existentes.  
  
-   Hacer que la tarea genere un error cuando existan inicios de sesión duplicados.  
  
-   Omitir los inicios de sesión duplicados.  
  
 Durante la ejecución, la tarea Transferir inicios de sesión se conecta a los servidores de origen y de destino utilizando dos administradores de conexión SMO. Los administradores de conexión SMO se configuran independientemente de la tarea Transferir inicios de sesión y después se hace referencia a ellos en la tarea Transferir inicios de sesión. Los administradores de conexión SMO especifican el servidor y el modo de autenticación que se utilizará para tener acceso al servidor. Para más información, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Transferir inicios de sesión &#40;página General&#41;](../../integration-services/control-flow/transfer-logins-task-editor-general-page.md)  
  
-   [Editor de la tarea Transferir inicios de sesión &#40;página Inicios de sesión&#41;](../../integration-services/control-flow/transfer-logins-task-editor-logins-page.md)  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Configuración mediante programación de la tarea Transferir inicios de sesión  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
  