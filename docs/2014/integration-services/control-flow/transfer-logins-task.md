---
title: Tarea Transferir inicios de sesión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferloginstask.f1
helpviewer_keywords:
- Transfer Logins task [Integration Services]
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 805c89c24b0a16051de1d555b484a0870de0cfde
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62830016"
---
# <a name="transfer-logins-task"></a>Tarea Transferir inicios de sesión
  La tarea Transferir inicios de sesión transfiere uno o varios inicios de sesión entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="transfer-logins-between-instances-of-sql-server"></a>Transferir inicios de sesión entre instancias de SQL Server  
 La tarea Transferir inicios de sesión admite un origen y un destino que sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventos  
 La tarea Transferir inicios de sesión emite un evento de información que indica el número de inicios de sesión transferidos y un evento de advertencia cuando se sobrescribe un inicio de sesión.  
  
 La tarea Transferir inicios de sesión no indica el progreso incremental de la transferencia; solo indica 0% y 100%.  
  
## <a name="execution-value"></a>Valor de ejecución  
 El valor de ejecución, que se define en la propiedad `ExecutionValue` de la tarea, devuelve el número de inicios de sesión transferidos. Si se asigna una variable definida por el usuario a la propiedad `ExecValueVariable` de la tarea Transferir inicios de sesión, se puede hacer que la información de la transferencia de inicios de sesión esté disponible para otros objetos del paquete. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) y [Usar variables en paquetes](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Entradas del registro  
 La tarea Transferir inicios de sesión incluye las siguientes entradas del registro personalizadas:  
  
-   TransferLoginsTaskStarTransferringObjects    Esta entrada del registro indica que se ha iniciado la transferencia. La entrada del registro incluye la hora de inicio.  
  
-   TransferLoginsTaskFinishedTransferringObjects    Esta entrada del registro indica que ha finalizado la transferencia. La entrada del registro incluye la hora de finalización.  
  
 Además, una entrada del registro para el evento `OnInformation` indica el número de inicios de sesión transferidos, y se escribe una entrada del registro para el evento `OnWarning` por cada inicio de sesión que se sobrescribe en el destino.  
  
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
  
 Durante la ejecución, la tarea Transferir inicios de sesión se conecta a los servidores de origen y de destino utilizando dos administradores de conexión SMO. Los administradores de conexión SMO se configuran independientemente de la tarea Transferir inicios de sesión y después se hace referencia a ellos en la tarea Transferir inicios de sesión. Los administradores de conexión SMO especifican el servidor y el modo de autenticación que se utilizará para tener acceso al servidor. Para más información, consulte [SMO Connection Manager](../connection-manager/smo-connection-manager.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Transferir inicios de sesión &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de la tarea Transferir inicios de sesión &#40;página Inicios de sesión&#41;](../transfer-logins-task-editor-logins-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-logins-task"></a>Configuración mediante programación de la tarea Transferir inicios de sesión  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
  
