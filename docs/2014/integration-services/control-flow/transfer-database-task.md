---
title: Tarea Transferir base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f7ddf838269932c19b0614d5a5219a7f03daed17
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377042"
---
# <a name="transfer-database-task"></a>Tarea Transferir bases de datos
  La tarea Transferir bases de datos transfiere una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre dos instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A diferencia de otras tareas que solo transfieren objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] copiándolos, la tarea Transferir bases de datos puede copiar o mover una base de datos. Esta tarea también puede utilizarse para copiar una base de datos en el mismo servidor.  
  
## <a name="offline-and-online-modes"></a>Modo sin conexión y en línea  
 La base de datos se puede transferir en modo en línea o sin conexión. Cuando se utiliza el modo en línea, la base de datos permanece adjunta y se transfiere utilizando el Objeto de administración de SQL (SMO) para copiar los objetos de la base de datos. Cuando se utiliza el modo sin conexión, la base de datos se separa, los archivos de la base de datos se copian o se mueven, y la base de datos se adjunta en el destino cuando finaliza la transferencia correctamente. Si la base de datos se copia, se vuelve a adjuntar automáticamente al origen después de que la copia se lleve a cabo correctamente. En el modo sin conexión, la base de datos se copia más rápidamente, pero no está disponible para los usuarios durante la transferencia.  
  
 El modo sin conexión requiere que se especifiquen los recursos compartidos de archivos de red en los servidores de origen y de destino que contienen los archivos de la base de datos. Si la carpeta está compartida y el usuario tiene acceso a ella, puede hacer referencia al recurso compartido de red con la sintaxis \\\nombreDeEquipo\Archivos de programa\miCarpeta\\. De lo contrario, debe usar la sintaxis \\\nombreDeEquipo\c$\Archivos de programa\miCarpeta\\. Para utilizar esta última sintaxis, el usuario debe tener acceso de escritura a los recursos compartidos de red en el origen y en el destino.  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a>Transferencia de bases de datos entre versiones de SQL Server  
 La tarea Transferir bases de datos puede transferir una base de datos entre instancias de versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferentes.  
  
## <a name="events"></a>Eventos  
 La tarea Transferir bases de datos no indica el progreso incremental de la transferencia del mensaje de error; solo indica 0% y 100%.  
  
## <a name="execution-value"></a>Valor de ejecución  
 El valor de ejecución, definido en la propiedad `ExecutionValue` de la tarea, devuelve el valor 1, ya que a diferencia de otras tareas de transferencia, la tarea Transferir bases de datos solo puede transferir una base de datos.  
  
 Si se asigna una variable definida por el usuario a la propiedad `ExecValueVariable` de la tarea Transferir bases de datos, se puede hacer que la información de la transferencia del mensaje de error esté disponible para otros objetos del paquete. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) y [Usar variables en paquetes](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Entradas del registro  
 La tarea Transferir bases de datos incluye las siguientes entradas del registro personalizadas:  
  
-   SourceSQLServer    Esta entrada del registro muestra el nombre del servidor de origen.  
  
-   DestSQLServer    Esta entrada del registro muestra el nombre del servidor de destino.  
  
-   SourceDB    Esta entrada del registro muestra el nombre de la base de datos que se transfiere.  
  
 Además, se escribe una entrada del registro para el evento `OnInformation` cuando se sobrescribe la base de datos de destino.  
  
## <a name="security-and-permissions"></a>Seguridad y permisos  
 Para transferir una base de datos en el modo sin conexión, el usuario que ejecuta el paquete debe ser miembro del rol de servidor sysadmin.  
  
 Para transferir una base de datos en el modo en línea, el usuario que ejecuta el paquete debe ser miembro del rol de servidor sysadmin o el propietario (dbo) de la base de datos seleccionada.  
  
## <a name="configuration-of-the-transfer-database-task"></a>Configuración de la tarea Transferir bases de datos  
 Puede especificar si la tarea debe intentar volver a adjuntar la base de datos de origen si la transferencia de la base de datos no se realiza.  
  
 La tarea Transferir bases de datos también se puede configurar para que permita sobrescribir y reemplazar una base de datos de destino con el mismo nombre.  
  
 Asimismo, es posible cambiar el nombre de la base de datos de origen como parte del proceso de transferencia. Si desea transferir una base de datos a una instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ya contenga una base de datos con el mismo nombre, puede cambiar el nombre de la base de datos de origen para poder transferirla. Sin embargo, el nombre de los archivos de base de datos también deben ser distintos; si en el destino ya existen archivos de base de datos con el mismo nombre, la tarea generará un error.  
  
 Al copiar una base de datos, su tamaño no puede ser menor que el tamaño de la base de datos **model** del servidor de destino. Se puede aumentar el tamaño de la base de datos que se va a copiar o reducir el tamaño de **modelo**.  
  
 Durante la ejecución, la tarea Transferir bases de datos se conecta a los servidores de origen y de destino utilizando uno o dos administradores de conexión SMO. Cuando se crea una copia de la base de datos en el mismo servidor, solo se requiere un administrador de conexiones SMO. Los administradores de conexión SMO se configuran independientemente de la tarea Transferir bases de datos y después se hace referencia a ellos en dicha tarea. Los administradores de conexión SMO especifican el servidor y el modo de autenticación que se utilizan cuando la tarea tiene acceso al servidor. Para más información, consulte [SMO Connection Manager](../connection-manager/smo-connection-manager.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Transferir bases de datos &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de la tarea Transferir bases de datos &#40;página Bases de datos&#41;](../transfer-database-task-editor-databases-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>Configuración mediante programación de la tarea Transferir bases de datos  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
  
