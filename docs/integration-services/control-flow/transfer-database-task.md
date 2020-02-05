---
title: Tarea Transferir base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferdatabasetask.f1
- sql13.dts.designer.transferdatabasetask.general.f1
- sql13.dts.designer.transferdatabasetask.database.f1
- sql13.dts.designer.transferdatabasetask.sourcedbfiles.f1
- sql13.dts.designer.transferdatabasetask.destdbfiles.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8badd727143d80db08eed45ddbf5102c635ddeeb
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71293899"
---
# <a name="transfer-database-task"></a>Tarea Transferir bases de datos

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La tarea Transferir bases de datos transfiere una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre dos instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A diferencia de otras tareas que solo transfieren objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] copiándolos, la tarea Transferir bases de datos puede copiar o mover una base de datos. Esta tarea también puede utilizarse para copiar una base de datos en el mismo servidor.  
  
## <a name="offline-and-online-modes"></a>Modo sin conexión y en línea  
 La base de datos se puede transferir en modo en línea o sin conexión. Cuando se utiliza el modo en línea, la base de datos permanece adjunta y se transfiere utilizando el Objeto de administración de SQL (SMO) para copiar los objetos de la base de datos. Cuando se utiliza el modo sin conexión, la base de datos se separa, los archivos de la base de datos se copian o se mueven, y la base de datos se adjunta en el destino cuando finaliza la transferencia correctamente. Si la base de datos se copia, se vuelve a adjuntar automáticamente al origen después de que la copia se lleve a cabo correctamente. En el modo sin conexión, la base de datos se copia más rápidamente, pero no está disponible para los usuarios durante la transferencia.  
  
 El modo sin conexión requiere que se especifiquen los recursos compartidos de archivos de red en los servidores de origen y de destino que contienen los archivos de la base de datos. Si la carpeta está compartida y el usuario tiene acceso a ella, puede hacer referencia al recurso compartido de red con la sintaxis \\\nombreDeEquipo\Archivos de programa\miCarpeta\\. De lo contrario, debe usar la sintaxis \\\nombreDeEquipo\c$\Archivos de programa\miCarpeta\\. Para utilizar esta última sintaxis, el usuario debe tener acceso de escritura a los recursos compartidos de red en el origen y en el destino.  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a>Transferencia de bases de datos entre versiones de SQL Server  
 La tarea Transferir bases de datos puede transferir una base de datos entre instancias de versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferentes.  
  
## <a name="events"></a>Eventos  
 La tarea Transferir bases de datos no indica el progreso incremental de la transferencia del mensaje de error; solo indica 0% y 100%.  
  
## <a name="execution-value"></a>Valor de ejecución  
 El valor de ejecución, definido en la propiedad **ExecutionValue** de la tarea, devuelve el valor 1, ya que a diferencia de otras tareas de transferencia, la tarea Transferir bases de datos solo puede transferir una base de datos.  
  
 Si se asigna una variable definida por el usuario a la propiedad **ExecValueVariable** de la tarea Transferir bases de datos, se puede hacer que la información de la transferencia del mensaje de error esté disponible para otros objetos del paquete. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Usar variables en paquetes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Entradas del registro  
 La tarea Transferir bases de datos incluye las siguientes entradas del registro personalizadas:  
  
-   SourceSQLServer    Esta entrada del registro muestra el nombre del servidor de origen.  
  
-   DestSQLServer    Esta entrada del registro muestra el nombre del servidor de destino.  
  
-   SourceDB    Esta entrada del registro muestra el nombre de la base de datos que se transfiere.  
  
 Además, se escribe una entrada del registro para el evento **OnInformation** cuando se sobrescribe la base de datos de destino.  
  
## <a name="security-and-permissions"></a>Seguridad y permisos  
 Para transferir una base de datos en el modo sin conexión, el usuario que ejecuta el paquete debe ser miembro del rol de servidor sysadmin.  
  
 Para transferir una base de datos en el modo en línea, el usuario que ejecuta el paquete debe ser miembro del rol de servidor sysadmin o el propietario (dbo) de la base de datos seleccionada.  
  
## <a name="configuration-of-the-transfer-database-task"></a>Configuración de la tarea Transferir bases de datos  
 Puede especificar si la tarea debe intentar volver a adjuntar la base de datos de origen si la transferencia de la base de datos no se realiza.  
  
 La tarea Transferir bases de datos también se puede configurar para que permita sobrescribir y reemplazar una base de datos de destino con el mismo nombre.  
  
 Asimismo, es posible cambiar el nombre de la base de datos de origen como parte del proceso de transferencia. Si desea transferir una base de datos a una instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ya contenga una base de datos con el mismo nombre, puede cambiar el nombre de la base de datos de origen para poder transferirla. Sin embargo, el nombre de los archivos de base de datos también deben ser distintos; si en el destino ya existen archivos de base de datos con el mismo nombre, la tarea generará un error.  
  
 Al copiar una base de datos, su tamaño no puede ser menor que el tamaño de la base de datos **model** del servidor de destino. Se puede aumentar el tamaño de la base de datos que se va a copiar o reducir el tamaño de **modelo**.  
  
 Durante la ejecución, la tarea Transferir bases de datos se conecta a los servidores de origen y de destino utilizando uno o dos administradores de conexión SMO. Cuando se crea una copia de la base de datos en el mismo servidor, solo se requiere un administrador de conexiones SMO. Los administradores de conexión SMO se configuran independientemente de la tarea Transferir bases de datos y después se hace referencia a ellos en dicha tarea. Los administradores de conexión SMO especifican el servidor y el modo de autenticación que se utilizan cuando la tarea tiene acceso al servidor. Para más información, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>Configuración mediante programación de la tarea Transferir bases de datos  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
## <a name="transfer-database-task-editor-general-page"></a>Editor de la tarea Transferir bases de datos (página General)
  Utilice la página **General** del cuadro de diálogo **Editor de la tarea Transferir bases de datos** para asignar un nombre y una descripción a la tarea Transferir bases de datos. La tarea Transferir bases de datos copia o mueve una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre dos instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta tarea también puede utilizarse para copiar una base de datos en el mismo servidor.   
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Escriba un nombre único para la tarea Transferir bases de datos. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Transferir bases de datos.  
  
## <a name="transfer-database-task-editor-databases-page"></a>Editor de la tarea Transferir bases de datos (página Bases de datos)
  Utilice la página **Bases de datos** del cuadro de diálogo **Editor de la tarea Transferir bases de datos** para especificar propiedades para las bases de datos de origen y destino implicadas en la tarea Transferir bases de datos. La tarea Transferir bases de datos copia o mueve una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre dos instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta tarea también puede utilizarse para copiar una base de datos en el mismo servidor.  
  
### <a name="options"></a>Opciones  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista, o bien haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de origen.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de destino.  
  
 **DestinationDatabaseName**  
 Especifique el nombre de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el servidor de destino.  
  
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
  
|Value|Descripción|  
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
  
|Value|Descripción|  
|-----------|-----------------|  
|**True**|Volver a adjuntar la base de datos de origen.|  
|**False**|No volver a adjuntar la base de datos de origen.|  

## <a name="source-database-files"></a>Archivos de base de datos de origen
  Utilice el cuadro de diálogo **Archivos de base de datos de origen** para ver los nombres y las ubicaciones de los archivos de la base de datos en el servidor de origen o para especificar una ubicación del recurso compartido de archivos de red para la tarea Transferir bases de datos.   
  
 Para llenar este cuadro de diálogo con los nombres y las ubicaciones de los archivos de la base de datos del servidor de origen, especifique **SourceConnection** y **SourceDatabaseName** primero en la página **Bases de datos** del cuadro de diálogo **Editor de la tarea Transferir bases de datos** .  
  
### <a name="options"></a>Opciones  
 **Archivo de origen**  
 Nombres de los archivos de la base de datos del servidor de origen que se van a transferir. El**Archivo de origen** es de solo lectura.  
  
 **Carpeta de origen**  
 Carpeta del servidor de origen en la que se encuentran los archivos de la base de datos que se van a transferir. La**Carpeta de origen** es de solo lectura.  
  
 **Recurso compartido de archivos de red**  
 Carpeta compartida de red del servidor de origen desde donde se transferirán los archivos de la base de datos. Utilice **Recurso compartido de archivos de red** cuando transfiera una base de datos en el modo sin conexión especificando el **Método** **DatabaseOffline** en la página **Bases de datos** del cuadro de diálogo **Editor de la tarea Transferir bases de datos** .  
  
 Especifique la ubicación del recurso compartido de archivos de red, o bien haga clic en el botón Examinar **(…)** para buscar la ubicación del recurso compartido de archivos de red.  
  
 Cuando transfiere una base de datos en modo sin conexión, los archivos de la base de datos se copian a la ubicación **Recurso compartido de archivos de red** del servidor de origen antes de ser transferidos al servidor de destino.  

## <a name="destination-database-files"></a>Archivos de la base de datos de destino
  Utilice el cuadro de diálogo **Archivos de la base de datos de destino** para ver o cambiar las ubicaciones y los nombres de archivos de la base de datos en el servidor de destino o para especificar una ubicación de archivo de red para la tarea Transferir bases de datos.  
  
 Para rellenar automáticamente este cuadro de diálogo con las ubicaciones y los nombres de archivos de la base de datos en el servidor de origen, especifique primero **SourceConnection**, **SourceDatabaseName**y **SourceDatabaseFiles** en la página **Bases de datos** del cuadro de diálogo **Editor de la tarea Transferir bases de datos** .  
  
### <a name="options"></a>Opciones  
 **Archivo de destino**  
 Nombres de los archivos de base de datos transferidos en el servidor de destino.  
  
 Escriba el nombre del archivo o haga clic en el nombre para editarlo.  
  
 **Carpeta de destino**  
 Carpeta del servidor de destino a la que se transferirán los archivos de la base de datos.  
  
 Escriba la ruta a la carpeta, haga clic en la ruta para editarla o bien, haga clic para examinar y buscar la carpeta donde desea transferir los archivos de la base de datos en el servidor de destino.  
  
 **Recurso compartido de archivos de red**  
 Carpeta compartida de red en el servidor de destino a la que se transferirán los archivos de la base de datos. Utilice **Recurso compartido de archivos de red** cuando transfiera una base de datos en el modo sin conexión especificando el **Método** **DatabaseOffline** en la página **Bases de datos** del cuadro de diálogo **Editor de la tarea Transferir bases de datos** .  
  
 Escriba la ubicación del recurso compartido de archivos de red o haga clic para examinar y buscar la ubicación del recurso compartido del archivo de red.  
  
 Cuando transfiera una base de datos en el modo sin conexión, los archivos se copian en la ubicación **Recurso compartido de archivos de red** antes de transferirlos a la ubicación **Carpeta de destino** .  
