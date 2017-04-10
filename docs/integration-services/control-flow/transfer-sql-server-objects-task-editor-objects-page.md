---
title: "Editor de la tarea Transferir objetos de SQL Server (p&#225;gina Objetos) | Microsoft Docs"
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
  - "sql13.dts.designer.transfersqlserverobjects.objects.f1"
helpviewer_keywords: 
  - "Transferir objetos de SQL Server, editor de la tarea"
ms.assetid: 8cc09118-70ac-4013-8308-d87f8411ca0c
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Editor de la tarea Transferir objetos de SQL Server (p&#225;gina Objetos)
  Utilice la página **Objetos** del cuadro de diálogo **Editor de la tarea Transferir objetos de SQL Server** para especificar propiedades para copiar uno o más objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otra. Las tablas, las vistas, los procedimientos almacenados y las funciones definidas por el usuario son algunos ejemplos de objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que puede copiar. Para obtener más información acerca de esta tarea, vea [Transfer SQL Server Objects Task](../../integration-services/control-flow/transfer-sql-server-objects-task.md).  
  
> [!NOTE]  
>  El usuario que crea la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener suficientes permisos en los objetos del servidor de origen para seleccionarlos para la copia, además de permiso para tener acceso a la base de datos del servidor de destino donde se transferirán los objetos.  
  
## Opciones estáticas  
 **SourceConnection**  
 Seleccione un administrador de conexiones SMO de la lista o haga clic en **\<Nueva conexión…>** para crear una conexión al servidor de origen.  
  
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
  
|Value|Description|  
|-----------|-----------------|  
|**Reemplazar**|Se sobrescribirán los datos del servidor de destino.|  
|**Anexar**|Los datos copiados desde el servidor de origen se anexarán a los datos existentes en el servidor de destino.|  
  
> [!NOTE]  
>  La opción **ExistingData** solo está disponible cuando **CopyData** se establece en **True**.  
  
 **CopySchema**  
 Seleccione esta opción si el esquema se copia durante la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
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
  
## Opciones dinámicas  
  
### CopyAllObjects = False  
 **CopyAllTables**  
 Seleccione si la tarea copiará todas las tablas de la base de datos de origen especificada o solo las tablas seleccionadas.  
  
 **TablesList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar tablas**.  
  
 **CopyAllViews**  
 Seleccione si la tarea copiará todas las vistas de la base de datos de origen especificada o solo las vistas seleccionadas.  
  
 **ViewsList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar vistas**.  
  
 **CopyAllStoredProcedures**  
 Seleccione si la tarea copiará todos los procedimientos almacenados definidos por el usuario en la base de datos de origen especificada o solo los procedimientos seleccionados.  
  
 **StoredProceduresList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar procedimientos almacenados**.  
  
 **CopyAllUserDefinedFunctions**  
 Seleccione si la tarea copiará todas las funciones definidas por el usuario en la base de datos de origen especificada o solo las UDF seleccionadas.  
  
 **UserDefinedFunctionsList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar funciones definidas por el usuario**.  
  
 **CopyAllDefaults**  
 Seleccione si la tarea copiará todos los valores predeterminados de la base de datos de origen especificada o solo los valores predeterminados seleccionados.  
  
 **DefaultsList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar valores predeterminados**.  
  
 **CopyAllUserDefinedDataTypes**  
 Seleccione si la tarea copiará todos los tipos de datos definidos por el usuario en la base de datos de origen especificada o solo los tipos de datos definidos por el usuario seleccionados.  
  
 **UserDefinedDataTypesList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar tipos de datos definidos por el usuario**.  
  
 **CopyAllPartitionFunctions**  
 Seleccione si la tarea copiará todas las funciones de partición definidas por el usuario en la base de datos de origen especificada o solo las seleccionadas. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **PartitionFunctionsList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar funciones de partición**.  
  
 **CopyAllPartitionSchemes**  
 Seleccione si la tarea copiará todos los esquemas de partición de la base de datos de origen especificada o solo los seleccionados. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **PartitionSchemesList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar esquemas de partición**.  
  
 **CopyAllSchemas**  
 Seleccione si la tarea copiará todos los esquemas de la base de datos de origen especificada o solo los seleccionados. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **SchemasList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar esquemas**.  
  
 **CopyAllSqlAssemblies**  
 Seleccione si la tarea copiará todos los ensamblados de SQL de la base de datos de origen especificada o solo los seleccionados. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **SqlAssembliesList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar ensamblados de SQL**.  
  
 **CopyAllUserDefinedAggregates**  
 Seleccione si la tarea copiará todas las funciones de agregado definidas por el usuario en la base de datos de origen especificada o solo las seleccionadas. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **UserDefinedAggregatesList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar agregados definidos por el usuario**.  
  
 **CopyAllUserDefinedTypes**  
 Seleccione si la tarea copiará todos los tipos definidos por el usuario en la base de datos de origen especificada o solo los seleccionados. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **UserDefinedTypes**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar tipos definidos por el usuario**.  
  
 **CopyAllXmlSchemaCollections**  
 Seleccione si la tarea copiará todas las colecciones de esquemas XML de la base de datos de origen especificada o solo las seleccionadas. Esta opción solo es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **XmlSchemaCollectionsList**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Seleccionar colecciones de esquemas XML**.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor de la tarea Transferir objetos de SQL Server &#40;página General&#41;](../../integration-services/control-flow/transfer-sql-server-objects-task-editor-general-page.md)   
 [Página Expresiones](../../integration-services/expressions/expressions-page.md)   
 [Formatos de datos para importación en bloque o exportación masiva &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  