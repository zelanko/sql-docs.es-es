---
title: Tarea Transferir objetos de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfersqlserverobjectstask.f1
- sql13.dts.designer.transfersqlserverobjects.general.f1
- sql13.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6977e5934178ae17ce8d4469728af211ec2ec274
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727357"
---
# <a name="transfer-sql-server-objects-task"></a>Tarea Transferir objetos de SQL Server

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transfiere uno o varios tipos de objetos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por ejemplo, la tarea puede copiar tablas y procedimientos almacenados. Dependiendo de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se utilice como origen, hay diferentes tipos de objetos disponibles para copiar. Por ejemplo, solo en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se incluyen esquemas y agregados definidos por el usuario.  
  
## <a name="objects-to-transfer"></a>Objetos que se transferirán  
 Se pueden copiar roles de servidor, roles y usuarios de la base de datos especificada, así como los permisos para los objetos transferidos. Si copia los usuarios, roles y permisos asociados junto con los objetos, puede hacer que los objetos transferidos se puedan utilizar de inmediato en el servidor de destino.  
  
 En la tabla siguiente se muestra el tipo de objetos que se pueden copiar.  
  
|Objeto|  
|------------|  
|Tablas|  
|Vistas|  
|Procedimientos almacenados|  
|Funciones definidas por el usuario|  
|Valores predeterminados|  
|Tipos de datos definidos por el usuario|  
|Funciones de partición|  
|Esquemas de partición|  
|Esquemas|  
|Ensamblados|  
|Funciones de agregado definidas por el usuario|  
|Tipos definidos por el usuario|  
|Colección de esquemas XML|  
  
 Los tipos definidos por el usuario (UDT) que se han creado en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen dependencias en los ensamblados CLR (Common Language Runtime). Si utiliza la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para transferir UDT, también deberá configurar la tarea para transferir los objetos dependientes. Para transferir objetos dependientes, establezca la propiedad **IncludeDependentObjects** en **True**.  
  
### <a name="table-options"></a>Opciones de tabla  
 Al copiar tablas, puede indicar los tipos de elementos relacionados con la tabla que desee incluir en el proceso de copia. Puede copiar los siguientes tipos de elementos junto con la tabla relacionada:  
  
-   Índices  
  
-   Desencadenadores  
  
-   Índices de texto completo  
  
-   Claves principales  
  
-   Claves externas  
  
 También puede indicar si el script que genera la tarea está en formato Unicode.  
  
## <a name="destination-options"></a>Opciones de destino  
 Puede configurar la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que incluya nombres de esquema, datos, propiedades extendidas de los objetos transferidos y objetos dependientes en la transferencia. Si copia datos, puede reemplazar o anexar los datos existentes.  
  
 Algunas opciones únicamente se aplican a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por ejemplo, solo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite esquemas.  
  
## <a name="security-options"></a>Opciones de seguridad  
 La tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede incluir usuarios de nivel de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y roles del origen, inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los permisos para los objetos transferidos. Por ejemplo, la transferencia puede incluir los permisos en las tablas transferidas.  
  
## <a name="transfer-objects-between-instances-of-sql-server"></a>Transferencia de objetos entre instancias de SQL Server  
 La tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite un origen y un destino que sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventos  
 La tarea emite un evento de información que indica el objeto transferido y un evento de advertencia cuando se sobrescribe un objeto. También se emite un evento de información para acciones como el truncamiento de tablas de una base de datos.  
  
 La tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no indica el progreso incremental de la transferencia de objetos; solo indica 0% y 100%.  
  
## <a name="execution-value"></a>Valor de ejecución  
 El valor de ejecución, almacenado en la propiedad **ExecutionValue** de la tarea, devuelve el número de objetos transferidos. Si se asigna una variable definida por el usuario a la propiedad **ExecValueVariable** de la tarea Transferir objetos de SQL Server, se puede hacer que la información de la transferencia de objetos esté disponible para otros objetos del paquete. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Usar variables en paquetes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Entradas del registro  
 La tarea Transferir objetos de SQL Server incluye las siguientes entradas del registro personalizadas:  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects   Esta entrada del registro indica que se ha iniciado la transferencia. La entrada del registro incluye la hora de inicio.  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects    Esta entrada del registro indica que ha finalizado la transferencia. La entrada del registro incluye la hora de finalización.  
  
 Además, una entrada del registro para un evento **OnInformation** indica el número de objetos del tipo seleccionado para la transferencia, el número de objetos transferidos y acciones, como el truncamiento de tablas cuando se transfieren datos con tablas. Se escribe una entrada del registro para el evento **OnWarning** por cada objeto que se sobrescribe en el destino.  
  
## <a name="security-and-permissions"></a>Seguridad y permisos  
 El usuario debe tener permiso para examinar objetos en el servidor de origen, y para quitar y crear objetos en el servidor de destino; además, el usuario debe tener acceso a la base de datos especificada y a los objetos de la base de datos.  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>Configuración de la tarea Transferir objetos de SQL Server  
 La tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede configurar para que transfiera todos los objetos, todos los objetos de un tipo o solamente los objetos especificados de un tipo. Por ejemplo, puede copiar únicamente las tablas seleccionadas en la base de datos AdventureWorks.  
  
 Si la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transfiere tablas, puede especificar el tipo de objetos relacionados con las tablas que quiere copiar con las tablas. Por ejemplo, puede especificar que se copien las claves principales con las tablas.  
  
 Para mejorar aún más la funcionalidad de los objetos transferidos, puede configurar la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que incluya nombres de esquema, datos, propiedades extendidas de los objetos transferidos y objetos dependientes en la transferencia. Al copiar los datos, puede especificar si desea reemplazar o anexar los datos existentes.  
  
 Durante la ejecución, la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta con los servidores de origen y de destino utilizando dos administradores de conexión SMO. Los administradores de conexión SMO se configuran independientemente de la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y después se hace referencia a ellos en la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los administradores de conexión SMO especifican el servidor y el modo de autenticación que se utilizará para tener acceso al servidor. Para más información, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>Configuración mediante programación de la tarea Transferir objetos de SQL Server  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
## <a name="transfer-sql-server-objects-task-editor-general-page"></a>Editor de la tarea Transferir objetos de SQL Server (página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea Transferir objetos de SQL Server** para describir y asignar un nombre a la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  El usuario que crea la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener los permisos adecuados en los objetos del servidor de origen para seleccionarlos para copiar y permisos para tener acceso a la base de datos del servidor de destino al que se transferirán los objetos.  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Escriba un nombre único para la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="transfer-sql-server-objects-task-editor-objects-page"></a>Editor de la tarea Transferir objetos de SQL Server (página Objetos)
  Utilice la página **Objetos** del cuadro de diálogo **Editor de la tarea Transferir objetos de SQL Server** para especificar propiedades para copiar uno o más objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otra. Las tablas, las vistas, los procedimientos almacenados y las funciones definidas por el usuario son algunos ejemplos de objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que puede copiar.  
  
> [!NOTE]  
>  El usuario que crea la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener suficientes permisos en los objetos del servidor de origen para seleccionarlos para la copia, además de permiso para tener acceso a la base de datos del servidor de destino donde se transferirán los objetos.  
  
### <a name="static-options"></a>Opciones estáticas  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista, o bien haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de origen.  
  
 **SourceDatabase**  
 Seleccione una base de datos en el servidor de origen desde donde se copiarán los objetos.  
  
 **DestinationConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de destino.  
  
 **DestinationDatabase**  
 Seleccione una base de datos en el servidor de destino al que se copiarán los objetos.  
  
 **DropObjectsFirst**  
 Seleccione si los objetos seleccionados se quitarán primero del servidor de destino antes de la copia.  
  
 **IncludeExtendedProperties**  
 Seleccione si las propiedades extendidas se incluirán cuando se copien objetos desde el servidor de origen al de destino.  
  
 **CopyData**  
 Seleccione si los datos se incluirán cuando se copien objetos desde el servidor de origen al de destino.  
  
 **ExistingData**  
 Especifique cómo se copiarán los datos al servidor de destino. Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Reemplazar**|Se sobrescribirán los datos del servidor de destino.|  
|**Anexar**|Los datos copiados desde el servidor de origen se anexarán a los datos existentes en el servidor de destino.|  
  
> [!NOTE]  
>  La opción **ExistingData** solo está disponible cuando **CopyData** se establece en **True**.  
  
 **CopySchema**  
 Seleccione esta opción si el esquema se copia durante la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  **CopySchema** solo está disponible para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **UseCollation**  
 Seleccione esta opción si la transferencia de objetos debe incluir la intercalación especificada en el servidor de origen.  
  
 **IncludeDependentObjects**  
 Seleccione si la copia de los objetos seleccionados se realizará en cascada para incluir otros objetos que dependen de los objetos seleccionados para la copia.  
  
 **CopyAllObjects**  
 Seleccione si la tarea copiará todos los objetos de la base de datos de origen especificada o solo los objetos seleccionados.  Si esta opción se establece en False, puede seleccionar los objetos que se van a transferir y se muestran las opciones dinámicas de la sección **CopyAllObjects**.  
  
 **ObjectsToCopy**  
 Expanda **ObjectsToCopy** para especificar los objetos que se deben copiar desde la base de datos de origen a la base de datos de destino.  
  
> [!NOTE]  
>  **ObjectsToCopy** solo está disponible cuando **CopyAllObjects** se establece en **False**.  
  
 Las opciones para copiar los siguientes tipos de objetos solo son compatibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 Ensamblados  
  
 Funciones de partición  
  
 Esquemas de partición  
  
 Esquemas  
  
 Agregados definidos por el usuario  
  
 Tipos definidos por el usuario  
  
 Colecciones de esquemas XML  
  
 **CopyDatabaseUsers**  
 Especifique si los usuarios de la base de datos deben incluirse en la transferencia.  
  
 **CopyDatabaseRoles**  
 Especifique si los roles de la base de datos deben incluirse en la transferencia.  
  
 **CopySqlServerLogins**  
 Especifique si los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben incluirse en la transferencia.  
  
 **CopyObjectLevelPermissions**  
 Especifique si los permisos de objetos deben incluirse en la transferencia.  
  
 **CopyIndexes**  
 Especifique si los índices deben incluirse en la transferencia.  
  
 **CopyTriggers**  
 Especifique si los desencadenadores deben incluirse en la transferencia.  
  
 **CopyFullTextIndexes**  
 Especifique si los índices de texto completo deben incluirse en la transferencia.  
  
 **CopyPrimaryKeys**  
 Especifique si las claves principales deben incluirse en la transferencia.  
  
 **CopyForeignKeys**  
 Especifique si las claves externas deben incluirse en la transferencia.  
  
 **GenerateScriptsInUnicode**  
 Especifique si los scripts de transferencia generados están en formato Unicode.  
  
### <a name="dynamic-options"></a>Opciones dinámicas  
  
#### <a name="copyallobjects--false"></a>CopyAllObjects = False  
 **CopyAllTables**  
 Seleccione si la tarea copiará todas las tablas de la base de datos de origen especificada o solo las tablas seleccionadas.  
  
 **TablesList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar tablas** .  
  
 **CopyAllViews**  
 Seleccione si la tarea copiará todas las vistas de la base de datos de origen especificada o solo las vistas seleccionadas.  
  
 **ViewsList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar vistas** .  
  
 **CopyAllStoredProcedures**  
 Seleccione si la tarea copiará todos los procedimientos almacenados definidos por el usuario en la base de datos de origen especificada o solo los procedimientos seleccionados.  
  
 **StoredProceduresList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar procedimientos almacenados** .  
  
 **CopyAllUserDefinedFunctions**  
 Seleccione si la tarea copiará todas las funciones definidas por el usuario en la base de datos de origen especificada o solo las UDF seleccionadas.  
  
 **UserDefinedFunctionsList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar funciones definidas por el usuario** .  
  
 **CopyAllDefaults**  
 Seleccione si la tarea copiará todos los valores predeterminados de la base de datos de origen especificada o solo los valores predeterminados seleccionados.  
  
 **DefaultsList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar valores predeterminados** .  
  
 **CopyAllUserDefinedDataTypes**  
 Seleccione si la tarea copiará todos los tipos de datos definidos por el usuario en la base de datos de origen especificada o solo los tipos de datos definidos por el usuario seleccionados.  
  
 **UserDefinedDataTypesList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar tipos de datos definidos por el usuario** .  
  
 **CopyAllPartitionFunctions**  
 Seleccione si la tarea copiará todas las funciones de partición definidas por el usuario en la base de datos de origen especificada o solo las seleccionadas. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **PartitionFunctionsList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar funciones de partición** .  
  
 **CopyAllPartitionSchemes**  
 Seleccione si la tarea copiará todos los esquemas de partición de la base de datos de origen especificada o solo los seleccionados. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **PartitionSchemesList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar esquemas de partición** .  
  
 **CopyAllSchemas**  
 Seleccione si la tarea copiará todos los esquemas de la base de datos de origen especificada o solo los seleccionados. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **SchemasList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar esquemas** .  
  
 **CopyAllSqlAssemblies**  
 Seleccione si la tarea copiará todos los ensamblados de SQL de la base de datos de origen especificada o solo los seleccionados. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **SqlAssembliesList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar ensamblados de SQL** .  
  
 **CopyAllUserDefinedAggregates**  
 Seleccione si la tarea copiará todas las funciones de agregado definidas por el usuario en la base de datos de origen especificada o solo las seleccionadas. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **UserDefinedAggregatesList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar agregados definidos por el usuario** .  
  
 **CopyAllUserDefinedTypes**  
 Seleccione si la tarea copiará todos los tipos definidos por el usuario en la base de datos de origen especificada o solo los seleccionados. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **UserDefinedTypes**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar tipos definidos por el usuario** .  
  
 **CopyAllXmlSchemaCollections**  
 Seleccione si la tarea copiará todas las colecciones de esquemas XML de la base de datos de origen especificada o solo las seleccionadas. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **XmlSchemaCollectionsList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar colecciones de esquemas XML** .  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor de la tarea Transferir objetos de SQL Server &#40;página General&#41;](../../integration-services/control-flow/transfer-sql-server-objects-task-editor-general-page.md)   
 [Página Expresiones](../../integration-services/expressions/expressions-page.md)   
 [Formatos de datos para importación en bloque o exportación masiva &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
