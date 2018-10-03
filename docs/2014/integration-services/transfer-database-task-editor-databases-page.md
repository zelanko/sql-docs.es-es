---
title: Transferir el Editor de tareas de base de datos (página bases de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.database.f1
helpviewer_keywords:
- Transfer Database Task Editor
ms.assetid: ccdb74d0-4bea-420c-a726-2e0eb8957e0a
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 69a3c17a5b247c3c1ccefa5887404ad0865c673e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070645"
---
# <a name="transfer-database-task-editor-databases-page"></a>Editor de la tarea Transferir bases de datos (página Bases de datos)
  Utilice la página **Bases de datos** del cuadro de diálogo **Editor de la tarea Transferir bases de datos** para especificar propiedades para las bases de datos de origen y destino implicadas en la tarea Transferir bases de datos. La tarea Transferir bases de datos copia o mueve una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] entre dos instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Esta tarea también puede utilizarse para copiar una base de datos en el mismo servidor. Para obtener más información sobre esta tarea, vea [Tarea Transferir bases de datos](control-flow/transfer-database-task.md).  
  
## <a name="options"></a>Opciones  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista, o bien haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de origen.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de destino.  
  
 **DestinationDatabaseName**  
 Especifique el nombre de la base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el servidor de destino.  
  
 Para rellenar automáticamente este campo con el nombre de la base de datos de origen, especifique los parámetros **SourceConnection** y **SourceDatabaseName** primero.  
  
 Para cambiar el nombre de la base de datos en el servidor de destino, escriba el nuevo nombre en este campo.  
  
 **DestinationDatabaseFiles**  
 Especifica los nombres y ubicaciones de los archivos de la base de datos en el servidor de destino.  
  
 Para rellenar automáticamente este campo con los nombres y ubicaciones de los archivos de la base de datos de origen, especifique los parámetros **SourceConnection**, **SourceDatabaseName**y **SourceDatabaseFiles** primero.  
  
 Para cambiar el nombre de los archivos de la base de datos o especificar las nuevas ubicaciones en el servidor de destino, rellene este campo con la información de la base de datos de origen y, a continuación, haga clic en el botón Examinar. En el cuadro de diálogo **Archivos de base de datos de destino** , edite el **archivo de destino**, la **carpeta de destino**o el **recurso compartido de archivos de red**.  
  
> [!NOTE]  
>  Si busca los archivos de la base de datos mediante el botón Examinar, la ubicación de los archivos se especifica con la notación de la unidad local; por ejemplo, c:\\. Debe reemplazar ésta por la notación del recurso compartido de red, incluidos los nombres del equipo y del recurso compartido. Si se utiliza el recurso compartido administrativo predeterminado, debe usar la notación $ y tener acceso administrativo al recurso compartido.  
  
 **DestinationOverwrite**  
 Especifique si la base de datos del servidor de destino se puede sobrescribir.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**True**|Sobrescribir la base de datos del servidor de destino.|  
|**False**|No sobrescribir la base de datos del servidor de destino.|  
  
> [!CAUTION]  
>  Los datos de la base de datos del servidor de destino se sobrescribirán si especifica **True** para **DestinationOverwrite**, lo cual puede conllevar una pérdida de datos. Para evitar que ésta se produzca, realice una copia de seguridad de la base de datos del servidor de destino en otra ubicación antes de ejecutar la tarea Transferir bases de datos.  
  
 **Acción**  
 Permite especificar si la tarea **copiará** o **moverá** la base de datos al servidor de destino.  
  
 **Método**  
 Permite especificar si la tarea se ejecutará mientras la base de datos del servidor de origen esté en modo en línea o modo sin conexión.  
  
 Para transferir una base de datos en modo sin conexión, el usuario que ejecute el paquete debe ser miembro del rol fijo de servidor **sysadmin** .  
  
 Para transferir una base de datos en modo en línea, el usuario que ejecute el paquete debe ser miembro del rol fijo de servidor **sysadmin** o el propietario de la base de datos seleccionada (**dbo**).  
  
 **SourceDatabaseName**  
 Permite seleccionar el nombre de la base de datos que se va a copiar o mover.  
  
 **SourceDatabaseFiles**  
 Haga clic en el botón Examinar para seleccionar los archivos de la base de datos.  
  
 **ReattachSourceDatabase**  
 Permite especificar si la tarea intentará volver a adjuntar la base de datos de origen en caso de error.  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**True**|Volver a adjuntar la base de datos de origen.|  
|**False**|No volver a adjuntar la base de datos de origen.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Tareas de Integration Services](control-flow/integration-services-tasks.md)   
 [Editor de la base de datos de tarea de transferencia &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Página expresiones](expressions/expressions-page.md)   
 [Administrador de conexiones SMO](connection-manager/smo-connection-manager.md)  
  
  
