---
title: Constantes enumeradas en expresiones de propiedad | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], expressions
- dynamic properties
- updating package properties
- enumerated constants [Integration Services]
- property expressions [Integration Services]
ms.assetid: a4418315-38e2-4ad3-8784-576163b25d6f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b22e25ad9053ed4da0187035cff00ff7e3ca70af
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58386573"
---
# <a name="enumerated-constants-in-property-expressions"></a>Constantes enumeradas en expresiones de propiedad
  Si las expresiones de propiedad incluyen valores de una lista de miembros enumeradores, la expresión debe utilizar el valor numérico del miembro enumerador en lugar del nombre descriptivo del miembro. Por ejemplo, si una expresión establece la propiedad `LoggingMode`, debe utilizar el valor 2 en lugar del nombre descriptivo Deshabilitado.  
  
 Este tema enumera solo los valores numéricos equivalentes a los nombres descriptivos de los enumeradores cuyos miembros se utilizan generalmente en expresiones de propiedad. El modelo de objetos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye varios enumeradores adicionales que puede utilizar cuando programa el modelo de objetos para generar paquetes mediante programación o elementos de paquete de código personalizado tales como tareas y componentes de flujo de datos.  
  
 Además de las propiedades personalizadas de los paquetes y objetos de paquetes, la ventana Propiedades de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] incluye un conjunto de propiedades disponibles para paquetes, tareas, y los contenedores de secuencias, de bucles Foreach y de bucles For. Las propiedades comunes establecidas por valores de enumeradores -`ForceExecutionResult`, `LoggingMode`, `IsolationLevel`, y `Transaction Option`-se muestran en la sección Propiedades comunes.  
  
 Las siguientes secciones proporcionan información sobre constantes enumeradas:  
  
 [Paquete](#Package)  
  
 [Enumeradores de bucle Foreach](#Foreach)  
  
 [Tareas](#Tasks)  
  
 [Tareas del plan de mantenimiento](#MaintenancePlanTasks)  
  
 [Propiedades comunes](#CommonProperties)  
  
##  <a name="Package"></a> Paquete  
 Las siguientes tablas enumeran los nombres descriptivos y los equivalentes de valores numéricos de las propiedades de paquetes que se establecen utilizando valores de un enumerador.  
  
 `PackageType` Conjunto de propiedades con valores de la `DTSPackageType` enumeración.  
  
|Nombre descriptivo en DTSPackageType|Valor numérico|  
|-------------------------------------|-------------------|  
|Default|0|  
|DTSWizard|1|  
|DTSDesigner|2|  
|SQLReplication|3|  
|DTSDesigner100|5|  
|SQLDBMaint|6|  
  
 `CheckpointUsage` Conjunto de propiedades con valores de la `DTSCheckpointUsage` enumeración.  
  
|Nombre descriptivo en DTSCheckpointUsage|Valor numérico|  
|-----------------------------------------|-------------------|  
|Never|0|  
|IfExists|1|  
|Always|2|  
  
 `PackagePriorityClass` Conjunto de propiedades con valores de la `DTSPriorityClass` enumeración.  
  
|Nombre descriptivo en DTSPriorityClass|Valor numérico|  
|---------------------------------------|-------------------|  
|Default|0|  
|AboveNormal|1|  
|Normal|2|  
|BelowNormal|3|  
|Idle|4|  
  
 `ProtectionLevel` Conjunto de propiedades con valores de la `DTSProtectionLevel` enumeración.  
  
|Nombre descriptivo en DTSProtectionLevel|Valor numérico|  
|-----------------------------------------|-------------------|  
|DontSaveSensitive|0|  
|EncryptSensitiveWithUserKey|1|  
|EncryptSensitiveWithPassword|2|  
|EncryptAllWithPassword|3|  
|EncryptAllWithUserKey|4|  
|ServerStorage|5|  
  
##  <a name="PrecedenceConstraints"></a> Restricciones de precedencia  
 `EvalOp` Conjunto de propiedades con valores de la `DTSPrecedenceEvalOp` enumeración.  
  
|Nombre descriptivo en DTSPrecedenceEvalOp|Valor numérico|  
|------------------------------------------|-------------------|  
|Expresión|1|  
|Restricción|2|  
|ExpressionAndConstraint|3|  
|ExpressionOrConstraint|4|  
  
 `Value` Conjunto de propiedades con valores de la `DTSExecResult` enumeración.  
  
|Nombre descriptivo|Valor numérico|  
|-------------------|-------------------|  
|Correcto|0|  
|Failure|1|  
|Completion|2|  
|Canceled|3|  
  
##  <a name="Foreach"></a> Enumeradores de bucle Foreach  
 El bucle Foreach incluye un conjunto de enumeradores con propiedades que se pueden establecer a partir de expresiones de propiedad.  
  
### <a name="foreach-ado-enumerator"></a>Enumerador de ADO para Foreach  
 `Type` Conjunto de propiedades con valores de la `ADOEnumerationType` enumeración.  
  
|Nombre descriptivo en ADOEnumerationType|Valor numérico|  
|-----------------------------------------|-------------------|  
|EnumerateTables|0|  
|EnumerateAllRows|1|  
|EnumerateRowsInFirstTable|2|  
  
### <a name="foreach-nodelist-enumerator"></a>Enumerador de lista de nodos para Foreach  
 `SourceDocumentType`, `InnerXPathStringSourceType`, y **OuterXPathStringSourceType** conjunto de propiedades con valores de la `SourceType` enumeración.  
  
|Nombre descriptivo en SourceType|Valor numérico|  
|---------------------------------|-------------------|  
|FileConnection|0|  
|Variable|1|  
|DirectInput|2|  
  
 `EnumerationType` Conjunto de propiedades con valores de la `EnumerationType` enumeración.  
  
|Nombre descriptivo en EnumerationType|Valor numérico|  
|--------------------------------------|-------------------|  
|Navigator|0|  
|Nodo|1|  
|NodeText|2|  
|ElementCollection|3|  
  
 `InnerElementType` Conjunto de propiedades con valores de la `InnerElementType` enumeración.  
  
|Nombre descriptivo en InnerElementType|Valor numérico|  
|---------------------------------------|-------------------|  
|Navigator|0|  
|Nodo|1|  
|NodeText|2|  
  
##  <a name="Tasks"></a> Tareas  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye numerosas tareas con propiedades que se establecen a partir de expresiones de propiedad.  
  
### <a name="analysis-services-execute-ddl-task"></a>Tarea Ejecutar DDL de Analysis Services  
 `SourceType` Conjunto de propiedades con valores de la `DDLSourceType` enumeración.  
  
|Nombre descriptivo en DDLSourceType|Valor numérico|  
|------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|Variable|2|  
  
### <a name="bulk-insert-task"></a>Inserción masiva, tarea  
 `DataFileType` Conjunto de propiedades con valores de la `DTSBulkInsert_DataFileType` enumeración.  
  
|Nombre descriptivo en DTSBulkInsert_DataFileType|Valor numérico|  
|--------------------------------------------------|-------------------|  
|DTSBulkInsert_DataFileType_Char|0|  
|DTSBulkInsert_DataFileType_Native|1|  
|DTSBulkInsert_DataFileType_WideChar|2|  
|DTSBulkInsert_DataFileType_WideNative|3|  
  
### <a name="execute-sql-task"></a>Tarea Ejecutar SQL  
 `ResultSetType` Conjunto de propiedades con valores de la `ResultSetType` enumeración.  
  
|Nombre descriptivo en ResultSetType|Valor numérico|  
|------------------------------------|-------------------|  
|ResultSetType_None|1|  
|ResultSetType_SingleRow|2|  
|ResultSetType_Rowset|3|  
|ResultSetType_XML|4|  
  
 `SqlStatementSourceType` Conjunto de propiedades con valores de la `SqlStatementSourceType` enumeración.  
  
|Nombre descriptivo en SqlStatementSourceType|Valor numérico|  
|---------------------------------------------|-------------------|  
|DirectInput|1|  
|FileConnection|2|  
|Variable|3|  
  
### <a name="file-system-task"></a>Tarea Sistema de archivos  
 `Operation` Conjunto de propiedades con valores de la `DTSFileSystemOperation` enumeración.  
  
|Nombre descriptivo en DTSFileSystemOperation|Valor numérico|  
|---------------------------------------------|-------------------|  
|CopyFile|0|  
|MoveFile|1|  
|DeleteFile|2|  
|RenameFile|3|  
|SetAttributes|4|  
|CreateDirectory|5|  
|CopyDirectory|6|  
|MoveDirectory|7|  
|DeleteDirectory|8|  
|DeleteDirectoryContent|9|  
  
 `Attributes` Conjunto de propiedades con valores de la `DTSFileSystemAttributes` enumeración.  
  
|Nombre descriptivo en DTSFileSystemAttributes|Valor numérico|  
|----------------------------------------------|-------------------|  
|Normal|0|  
|Archive|1|  
|Hidden|2|  
|Solo lectura|4|  
|Sistema|8|  
  
### <a name="ftp-task"></a>Tarea FTP  
 `Operation` Conjunto de propiedades con valores de la `DTSFTPOp` enumeración.  
  
|Nombre descriptivo en DTSFTPOp|Valor numérico|  
|-------------------------------|-------------------|  
|Send|0|  
|Receive|1|  
|DeleteLocal|2|  
|DeleteRemote|3|  
|MakeDirLocal|4|  
|MakeDirRemote|5|  
|RemoveDirLocal|6|  
|RemoveDirRemote|7|  
  
### <a name="message-queue-task"></a>Message Queue Task  
 `MessageType` Conjunto de propiedades con valores de la `MQMessageType` enumeración.  
  
|Nombre descriptivo en MQMessageType|Valor numérico|  
|------------------------------------|-------------------|  
|DTSMQMessageType_String|0|  
|DTSMQMessageType_DataFile|1|  
|DTSMQMessageType_Variables|2|  
|DTSMQMessagType_StringMessageToVariable|3|  
  
 `StringCompareType` Conjunto de propiedades con valores de la `MQStringMessageCompare` enumeración.  
  
|Nombre descriptivo en MQStringMessageCompare|Valor numérico|  
|---------------------------------------------|-------------------|  
|DTSMQStringMessageCompare_None|0|  
|DTSMQStringMessageCompare_Exact|1|  
|DTSMQStringMessageCompare_IgnoreCase|2|  
|DTSMQStringMessageCompare_Contains|3|  
  
 `TaskType` Conjunto de propiedades con valores de la `MQType` enumeración.  
  
|Nombre descriptivo en MQType|Valor numérico|  
|-----------------------------|-------------------|  
|DTSMQType_Sender|0|  
|DTSMQType_Receiver|1|  
  
### <a name="send-mail-task"></a>Enviar correo, tarea  
 `MessageSourceType` Conjunto de propiedades con valores de la `SendMailMessageSourceType` enumeración.  
  
|Nombre descriptivo en SendMailMessageSourceType|Valor numérico|  
|------------------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|Variable|2|  
  
 `Priority` Conjunto de propiedades con valores de la `MailPriority` enumeración.  
  
|Nombre descriptivo en MailPriority|Valor numérico|  
|-----------------------------------|-------------------|  
|Alta|1|  
|Normal|3|  
|Baja|5|  
  
### <a name="transfer-database-task"></a>Tarea Transferir bases de datos  
 `Action` Conjunto de propiedades con valores de la `TransferAction` enumeración.  
  
|Nombre descriptivo en TransferAction|Valor numérico|  
|-------------------------------------|-------------------|  
|Copiar|0|  
|Mover|1|  
  
 `Method` Conjunto de propiedades con valores de la `TransferMethod` enumeración.  
  
|Nombre descriptivo en TransferMethod|Valor numérico|  
|-------------------------------------|-------------------|  
|DatabaseOffline|0|  
|DatabaseOnline|1|  
  
### <a name="transfer-error-messages-task"></a>Tarea Transferir mensajes de error  
 `IfObjectExists` Conjunto de propiedades con valores de la `IfObjectExists` enumeración.  
  
|Nombre descriptivo en IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Sobrescribir|1|  
|Omitir|2|  
  
### <a name="transfer-jobs-task"></a>Tarea Transferir trabajos  
 `IfObjectExists` Conjunto de propiedades con valores de la `IfObjectExists` enumeración.  
  
|Nombre descriptivo en IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Sobrescribir|1|  
|Omitir|2|  
  
### <a name="transfer-logins-task"></a>Tarea Transferir inicios de sesión  
 `IfObjectExists` Conjunto de propiedades con valores de la `IfObjectExists` enumeración.  
  
|Nombre descriptivo en IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Sobrescribir|1|  
|Omitir|2|  
  
 `LoginsToTransfer` Conjunto de propiedades con valores de la `LoginsToTransfer` enumeración.  
  
|Nombre descriptivo en LoginsToTransfer|Valor numérico|  
|---------------------------------------|-------------------|  
|AllLogins|0|  
|SelectedLogins|1|  
|AllLoginsFromSelectedDatabases|2|  
  
### <a name="transfer-master-stored-procedures-task"></a>Tarea Transferir procedimientos almacenados principales  
 `IfObjectExists` Conjunto de propiedades con valores de la `IfObjectExists` enumeración.  
  
|Nombre descriptivo en IfObjectExists|Valor numérico|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Sobrescribir|1|  
|Omitir|2|  
  
### <a name="transfer-sql-server-objects-task"></a>Tarea Transferir objetos de SQL Server  
 `ExistingData` Conjunto de propiedades con valores de la `ExistingData` enumeración.  
  
|Nombre descriptivo en ExistingData|Valor numérico|  
|-----------------------------------|-------------------|  
|Reemplazar|0|  
|Anexar|1|  
  
### <a name="web-service-task"></a>Tarea Servicio web  
 `OutputType` Conjunto de propiedades con valores de la `DTSOutputType` enumeración.  
  
|Nombre descriptivo en DTSOutputType|Valor numérico|  
|------------------------------------|-------------------|  
|Archivo|0|  
|Variable|1|  
  
### <a name="wmi-data-reader-task"></a>Tarea Lector de datos WMI  
 `OverwriteDestination` Conjunto de propiedades con valores de la `OverwriteDestination` enumeración.  
  
|Nombre descriptivo en OverwriteDestination|Valor numérico|  
|-------------------------------------------|-------------------|  
|OverwriteDestination|0|  
|AppendToDestination|1|  
|KeepOriginal|2|  
  
 `OutputType` Conjunto de propiedades con valores de la `OutputType` enumeración.  
  
|Nombre descriptivo en OutputType|Valor numérico|  
|---------------------------------|-------------------|  
|DataTable|0|  
|PropertyValue|1|  
|PropertyNameAndValue|2|  
  
 `DestinationType` Conjunto de propiedades con valores de la `DestinationType` enumeración.  
  
|Nombre descriptivo en DestinationType|Valor numérico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|Variable|1|  
  
 `WqlQuerySourceType` Conjunto de propiedades con valores de la `QuerySourceType` enumeración.  
  
|Nombre descriptivo en QuerySourceType|Valor numérico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|Variable|2|  
  
 Monitor de eventos WMI `ActionAtEvent` conjunto de propiedades con valores de la `ActionAtEvent` enumeración.  
  
|Nombre descriptivo en ActionAtEvent|Valor numérico|  
|------------------------------------|-------------------|  
|LogTheEventAndFireDTSEvent|0|  
|LogTheEvent|1|  
  
 `ActionAtTimeout` Conjunto de propiedades con valores de la `ActionAtTimeout` enumeración.  
  
|Nombre descriptivo en ActionAtTimeout|Valor numérico|  
|--------------------------------------|-------------------|  
|LogTimeoutAndFireDTSEvent|0|  
|LogTimeout|1|  
  
 `AfterEvent` Conjunto de propiedades con valores de la `AfterEvent` enumeración.  
  
|Nombre descriptivo en AfterEvent|Valor numérico|  
|---------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 `AfterTimeout` Conjunto de propiedades con valores de la `AfterTimeout` enumeración.  
  
|Nombre descriptivo en AfterTimeout|Valor numérico|  
|-----------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 `WqlQuerySourceType` Conjunto de propiedades con valores de la `QuerySourceType` enumeración.  
  
|Nombre descriptivo en QuerySourceType|Valor numérico|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|Variable|2|  
  
### <a name="xml-task"></a>Tarea XML  
 `OperationType` Conjunto de propiedades con valores de la `DTSXMLOperation` enumeración.  
  
|Nombre descriptivo en DTSXMLOperation|Valor numérico|  
|--------------------------------------|-------------------|  
|Validar|0|  
|XSLT|1|  
|XPATH|2|  
|Mezcla|3|  
|Diferencias|4|  
|Revisión|5|  
  
 `SourceType`, `SecondOperandType`, y `XPathSourceType` conjunto de propiedades con valores de la `DTSXMLSourceType` enumeración.  
  
|Nombre descriptivo en DTSXMLSourceType|Valor numérico|  
|---------------------------------------|-------------------|  
|FileConnection|0|  
|Variable|1|  
|DirectInput|2|  
  
 `DestinationType` y **DiffGramDestinationType** conjunto de propiedades con valores de la `DTSXMLSaveResultTo` enumeración.  
  
|Nombre descriptivo en DTSXMLSaveResultTo|Valor numérico|  
|-----------------------------------------|-------------------|  
|FileConnection|0|  
|Variable|1|  
  
 `ValidationType` Conjunto de propiedades con valores de la `DTSXMLValidationType` enumeración.  
  
|Nombre descriptivo en DTSXMLValidationType|Valor numérico|  
|-------------------------------------------|-------------------|  
|DTD|0|  
|XSD|1|  
  
 `XPathOperation` Conjunto de propiedades con valores de la `DTSXMLXPathOperation` enumeración.  
  
|Nombre descriptivo en DTSXMLXPathOperation|Valor numérico|  
|-------------------------------------------|-------------------|  
|Evaluation|0|  
|Valores|1|  
|NodeList|2|  
  
 `DiffOptions` Conjunto de propiedades con valores de la `DTSXMLDiffOptions` enumeración. Las opciones de este enumerador no se excluyen mutualmente. Para utilizar varias opciones, proporcione una lista separada por comas de las opciones que se deben aplicar.  
  
|Nombre descriptivo en DTSXMLDiffOptions|Valor numérico|  
|----------------------------------------|-------------------|  
|None|0|  
|IgnoreChildOrder|1|  
|IgnoreComments|2|  
|IgnorePI|4|  
|IgnoreWhitespace|8|  
|IgnoreNameSpaces|16|  
|IgnorePrefixes|32|  
|IgnoreXmlDecl|64|  
|IgnoreDtd|128|  
  
 `DiffAlgorithm` Conjunto de propiedades con valores de la `DTSXMLDiffAlgorithm` enumeración.  
  
|Nombre descriptivo en DTSXMLDiffAlgorithm|Valor numérico|  
|------------------------------------------|-------------------|  
|Auto|0|  
|Rápido|1|  
|Preciso|2|  
  
##  <a name="MaintenancePlanTasks"></a> Tareas del plan de mantenimiento  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye un conjunto de tareas que realiza tareas de SQL Server para utilizar en planes de mantenimiento y paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite el trabajo con estas tareas mediante programación y la documentación de referencia de programación no incluye documentación de API de estas tareas y sus enumeradores.  
  
### <a name="all-maintenance-tasks"></a>Todas las tareas de mantenimiento  
 Todas las tareas de mantenimiento utilizan las siguientes enumeraciones para establecer las propiedades especificadas.  
  
 `DatabaseSelectionType` Conjunto de propiedades con valores de la `DatabaseSelection` enumeración.  
  
|Nombre descriptivo en DatabaseSelection|Valor numérico|  
|----------------------------------------|-------------------|  
|None|0|  
|All|1|  
|Sistema|2|  
|Usuario|3|  
|Specific|4|  
  
 `TableSelectionType` Conjunto de propiedades con valores de la `TableSelection` enumeración.  
  
|Nombre descriptivo en TableSelection|Valor numérico|  
|-------------------------------------|-------------------|  
|None|0|  
|All|1|  
|Specific|2|  
  
 `ObjectTypeSelection` Conjunto de propiedades con valores de la `ObjectType` enumeración.  
  
|Nombre descriptivo en ObjectType|Valor numérico|  
|---------------------------------|-------------------|  
|Table|0|  
|Ver|1|  
|TableView|2|  
  
### <a name="back-up-database-task"></a>Tarea Copia de seguridad de la base de datos  
 `DestinationCreationType` Conjunto de propiedades con valores de la `DestinationType` enumeración.  
  
|Nombre descriptivo en DestinationType|Valor numérico|  
|--------------------------------------|-------------------|  
|Auto|0|  
|Manual|1|  
  
 `ExistingBackupsAction` Conjunto de propiedades con valores de la `ActionForExistingBackups` enumeración.  
  
|Nombre descriptivo en ActionForExistingBackups|Valor numérico|  
|-----------------------------------------------|-------------------|  
|Anexar|0|  
|Sobrescribir|1|  
  
 `BackupAction` Conjunto de propiedades con valores de la `BackupTaskType` enumeración. Esta propiedad trabaja con la propiedad `BackupIsIncremental` para definir el tipo de copia de seguridad que realiza la tarea.  
  
|Nombre descriptivo en BackupTaskType|Valor numérico|  
|-------------------------------------|-------------------|  
|Base de datos|0|  
|Archivos|1|  
|Log|2|  
  
 `BackupDevice` Conjunto de propiedades con valores de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) `DeviceType` enumeración.  
  
|Nombre descriptivo en DeviceType|Valor numérico|  
|---------------------------------|-------------------|  
|LogicalDevice|0|  
|Cinta|1|  
|Archivo|2|  
|Pipe|3|  
|VirtualDevice|4|  
  
### <a name="maintenance-cleanup-task"></a>tarea, Limpieza de mantenimiento  
 `FileTypeSelected` Conjunto de propiedades con valores de la `FileType` enumeración.  
  
|Nombre descriptivo en FileType|Valor numérico|  
|-------------------------------|-------------------|  
|FileBackup|0|  
|FileReport|1|  
  
 `OlderThanTimeUnitType` Conjunto de propiedades con valores de la `TimeUnitType` enumeración.  
  
|Nombre descriptivo en TimeUnitType|Valor numérico|  
|-----------------------------------|-------------------|  
|Day|0|  
|Semana|1|  
|Month|2|  
|Year|3|  
  
### <a name="update-statistics-task"></a>Tarea Actualizar estadísticas  
 `UpdateType` Conjunto de propiedades con valores de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) `StatisticsTarget` enumeración.  
  
|Nombre descriptivo en StatisticsTarget|Valor numérico|  
|---------------------------------------|-------------------|  
|columna|1|  
|Índice|2|  
|All|3|  
  
##  <a name="CommonProperties"></a> Propiedades comunes  
 Los paquetes, tareas, y los contenedores de secuencias, de bucles Foreach y de bucles For pueden utilizar las siguientes enumeraciones para establecer las propiedades especificadas.  
  
 `ForceExecutionResult` Conjunto de propiedades con valores de la `DTSForcedExecResult` enumeración.  
  
|Nombre descriptivo en DTSForcedExecResult|Valor numérico|  
|------------------------------------------|-------------------|  
|None|-1|  
|Correcto|0|  
|Failure|1|  
|Completion|2|  
  
 `IsolationLevel` Conjunto de propiedades por .NET Framework `IsolationLevel` enumeración. Para obtener más información, vea la biblioteca de clases de .NET Framework. en [MSDN Library](https://go.microsoft.com/fwlink?LinkId=17313).  
  
 `LoggingMode` Conjunto de propiedades con valores de la `DTSLoggingMode` enumeración.  
  
|Nombre descriptivo en DTSLoggingMode|Valor numérico|  
|-------------------------------------|-------------------|  
|UseParentSetting|0|  
|Habilitado|1|  
|Deshabilitado|2|  
  
 `TransactionOption` Conjunto de propiedades con valores de la `DTSTransactionOption` enumeración.  
  
|Nombre descriptivo en DTSTransactionOption|Valor numérico|  
|-------------------------------------------|-------------------|  
|NotSupported|0|  
|Admitida|1|  
|Obligatorio|2|  
  
## <a name="related-tasks"></a>Related Tasks  
 [Agregar o cambiar una expresión de propiedad](add-or-change-a-property-expression.md)  
  
## <a name="see-also"></a>Vea también  
 [Usar expresiones de propiedad en paquetes](use-property-expressions-in-packages.md)   
 [Paquetes de Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md)   
 [Contenedores de Integration Services](../control-flow/integration-services-containers.md)   
 [Tareas de Integration Services](../control-flow/integration-services-tasks.md)   
 [Restricciones de precedencia](../control-flow/precedence-constraints.md)  
  
  
