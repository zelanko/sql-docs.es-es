---
title: Transferir el Editor de la tarea los inicios de sesión (página inicios de sesión) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins Task Editor
ms.assetid: bf244c24-bd45-4ece-b66b-78b488f35c5b
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 877d7d8e4831a785586680ce57d21975443da645
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070055"
---
# <a name="transfer-logins-task-editor-logins-page"></a>Editor de la tarea Transferir inicios de sesión (página Inicios de sesión)
  Utilice la página **Inicios de sesión** del cuadro de diálogo **Editor de la tarea Transferir inicios de sesión** para especificar propiedades para copiar uno o varios inicios de sesión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a otra. Para obtener más información acerca de esta tarea, vea [Transfer Logins Task](control-flow/transfer-logins-task.md).  
  
> [!IMPORTANT]  
>  Cuando se ejecuta la tarea Transferir inicios de sesión, se crean inicios de sesión en el servidor de destino con contraseñas aleatorias y se deshabilitan las contraseñas. Para utilizar estos inicios de sesión, un miembro del rol fijo de servidor **sysadmin** debe cambiar las contraseñas y, a continuación, habilitarlas. El inicio de sesión **sa** no se puede transferir.  
  
## <a name="options"></a>Opciones  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista, o bien haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de origen.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de destino.  
  
 **LoginsToTransfer**  
 Seleccione los inicios de sesión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que va a copiar del servidor de origen al de destino. Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**AllLogins**|Todos los inicios de sesión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el servidor de origen se copiarán al de destino.|  
|**SelectedLogins**|Solo los inicios de sesión especificados con **LoginsList** se copiarán al servidor de destino.|  
|**AllLoginsFromSelectedDatabases**|Todos los inicios de sesión de las bases de datos especificadas con **DatabasesList** se copiarán al servidor de destino.|  
  
 **LoginsList**  
 Seleccione los inicios de sesión en el servidor de origen que se copiarán al de destino. Esta opción solo está disponible cuando se selecciona **SelectedLogins** para **LoginsToTransfer**.  
  
 **DatabasesList**  
 Seleccione las bases de datos en el servidor de origen que contienen inicios de sesión que se copiarán al de destino. Esta opción solo está disponible cuando se selecciona **AllLoginsFromSelectedDatabases** para **LoginsToTransfer**.  
  
 **IfObjectExists**  
 Seleccione cómo debe administrar la tarea los inicios de sesión con el mismo nombre que existan ya en el servidor de destino.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**FailTask**|La tarea genera un error si existen ya inicios de sesión con el mismo nombre en el servidor de destino.|  
|**Sobrescribir**|La tarea sobrescribe los inicios de sesión con el mismo nombre en el servidor de destino.|  
|**Omitir**|La tarea omite los inicios de sesión con el mismo nombre que existan en el servidor de destino.|  
  
 **CopySids**  
 Seleccione esta opción si los identificadores de seguridad asociados a los inicios de sesión deben copiarse al servidor de destino. **CopySids** debe establecerse en **True** si la tarea Transferir inicios de sesión se utiliza junto con la tarea Transferir bases de datos. De lo contrario, la base de datos transferida no reconocerá los inicios de sesión copiados.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Tareas de Integration Services](control-flow/integration-services-tasks.md)   
 [Editor de la tarea los inicios de sesión de transferencia &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Página expresiones](expressions/expressions-page.md)   
 [Administrador de conexiones SMO](connection-manager/smo-connection-manager.md)   
 [Contraseñas seguras](../relational-databases/security/strong-passwords.md)   
 [Consideraciones de seguridad para una instalación de SQL Server](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
