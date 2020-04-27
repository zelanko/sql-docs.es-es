---
title: Establecer las propiedades de paquetes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- checkpoints [Integration Services]
- execution properties [Integration Services]
- packages [Integration Services], properties
- identification properties [Integration Services]
- passwords [Integration Services]
- SSIS packages, properties
- transaction properties [Integration Services]
- updating package properties
- forced execution value properties [Integration Services]
- security properties [Integration Services]
- version properties [Integration Services]
- SQL Server Integration Services packages, properties
ms.assetid: 13f81c3e-2b18-4f83-b445-a2f4a2c560aa
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ea7f5f06816b6dd4ddf840f63119bebb0ebf80e8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62889218"
---
# <a name="set-package-properties"></a>Establecer las propiedades de paquetes
  Cuando se crea un paquete en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] mediante la interfaz gráfica proporcionada por [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , se configuran las propiedades del objeto de paquete en la ventana Propiedades.  
  
 La ventana **Propiedades** proporciona una lista categorizada y alfabética de propiedades. Para organizar la ventana **Propiedades** por categorías, haga clic en el icono Por categorías.  
  
 Cuando se organiza por categorías, la ventana **Propiedades** agrupa propiedades en las siguientes categorías:  
  
-   [Puntos de comprobación](#Checkpoints)  
  
-   [Ejecución](#Execution)  
  
-   [Valor de ejecución forzada](#ForcedExecutionValue)  
  
-   [Identificación](#Identification)  
  
-   [Varios](#Misc)  
  
-   [Seguridad](#Security)  
  
-   [Transactions](#Transactions)  
  
-   [Versión](#Version)  
  
 Para obtener información sobre propiedades adicionales de paquetes que no se pueden establecer en la ventana **Propiedades** , vea <xref:Microsoft.SqlServer.Dts.Runtime.Package>.  
  
### <a name="to-set-package-properties-in-the-properties-window"></a>Para establecer las propiedades del paquete en la ventana Propiedades.  
  
-   [Establecimiento de las propiedades de un paquete](../../2014/integration-services/set-the-properties-of-a-package.md)  
  
## <a name="properties-by-category"></a>Propiedades por categoría  
 Las siguientes tablas enumeran las propiedades de paquete por categoría.  
  
###  <a name="checkpoints"></a><a name="Checkpoints"></a> Puntos de comprobación  
 Puede usar las propiedades de esta categoría para reiniciar el paquete desde un punto de error en el flujo de control de paquetes, en lugar de volver a ejecutar el paquete desde el principio de su flujo de control. Para obtener más información, vea [Restart Packages by Using Checkpoints](packages/restart-packages-by-using-checkpoints.md).  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|`CheckpointFileName`|Nombre del archivo que captura la información del punto de comprobación que permite que un paquete se reinicie. Cuando el paquete termina correctamente, se elimina este archivo.|  
|`CheckpointUsage`|Especifica cuándo se puede reiniciar un paquete. Los valores son `Never`, `IfExists` y `Always`. El valor predeterminado de esta propiedad es `Never`, que indica que el paquete no puede reiniciarse. Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DTSCheckpointUsage>.|  
|`SaveCheckpoints`|Especifica si los puntos de comprobación se escriben en el archivo de punto de comprobación cuando se ejecuta el paquete. El valor predeterminado de esta propiedad es `False`.|  
  
> [!NOTE]  
>  La opción `/CheckPointing on` de dtexec es equivalente a establecer la propiedad `SaveCheckpoints` del paquete en True y la propiedad `CheckpointUsage` en Always. Para obtener más información, consulte [utilidad dtexec](packages/dtexec-utility.md).  
  
###  <a name="execution"></a>Ejecución de <a name="Execution"></a>  
 Las propiedades en esta categoría configuran el comportamiento de tiempo de ejecución del objeto de paquete.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|`DelayValidation`|Indica si la validación del paquete se retrasa hasta que se ejecute el paquete. El valor predeterminado de esta propiedad es `False`.|  
|**Deshabilitar**|Indica si el paquete está deshabilitado. El valor predeterminado de esta propiedad es `False`.|  
|`DisableEventHandlers`|Especifica si se ejecutan los controladores de eventos del paquete. El valor predeterminado de esta propiedad es `False`.|  
|`FailPackageOnFailure`|Especifica si el paquete genera un error cuando se produce un error en un componente de paquete. El único valor válido de esta propiedad es `False`.|  
|`FailParentOnError`|Especifica si el contenedor principal genera un error cuando se produce un error en un contenedor secundario. El valor predeterminado de esta propiedad es `False`.|  
|`MaxConcurrentExecutables`|Cantidad de archivos ejecutables que el paquete puede ejecutar simultáneamente. El valor predeterminado de esta propiedad es **-1**, que indica que no hay límite.|  
|`MaximumErrorCount`|Cantidad máxima de errores que se pueden producir antes de que un paquete termine de ejecutarse. El valor predeterminado de esta propiedad es **1**.|  
|`PackagePriorityClass`|Clase de prioridad de subproceso Win32 del subproceso del paquete. Los valores son `Default`, `AboveNormal`, `Normal`, `BelowNormal` y `Idle`. El valor predeterminado de esta propiedad es `Default`. Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DTSPriorityClass>.|  
  
###  <a name="forced-execution-value"></a><a name="ForcedExecutionValue"></a>Valor de ejecución forzada  
 Las propiedades de esta categoría configuran un valor de ejecución opcional para el paquete.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|`ForcedExecutionValue`|Si ForceExecutionValue se establece en `True`, valor que especifica el valor de ejecución opcional que devuelve el paquete. El valor predeterminado de esta propiedad es **0**.|  
|`ForcedExecutionValueType`|Tipo de datos de ForcedExecutionValue. El valor predeterminado de esta propiedad es `Int32`.|  
|`ForceExecutionValue`|Valor booleano que especifica si se debería forzar a que el valor de ejecución opcional del contenedor contenga un valor concreto. El valor predeterminado de esta propiedad es `False`.|  
  
###  <a name="identification"></a><a name="Identification"></a>Identificado  
 Las propiedades de esta categoría proporcionan información como el identificador único y el nombre del paquete.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|`CreationDate`|Fecha en que se creó el paquete.|  
|`CreatorComputerName`|Nombre del equipo en el que creó el paquete.|  
|`CreatorName`|Nombre de la persona que creó el paquete.|  
|`Description`|Descripción de la funcionalidad del paquete.|  
|`ID`|GUID del paquete, que se asigna cuando se crea el paquete. Esta propiedad es de solo lectura. Para generar un nuevo valor aleatorio para la `ID` propiedad, seleccione ** \<generar nuevo identificador>** en la lista desplegable.|  
|`Name`|Nombre del paquete.|  
|`PackageType`|Tipo de paquete. Los valores son `Default`, `DTSDesigner`, `DTSDesigner100`, `DTSWizard`, `SQLDBMaint` y `SQLReplication`. El valor predeterminado de esta propiedad es `Default`. Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>.|  
  
###  <a name="misc"></a><a name="Misc"></a>Variada  
 Las propiedades de esta categoría se usan para obtener acceso a las configuraciones y expresiones que usa un paquete y proporcionar información acerca de la configuración regional y modo de registro del paquete. Para más información, vea [Usar expresiones de propiedad en paquetes](expressions/use-property-expressions-in-packages.md).  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|`Configurations`|Colección de las configuraciones que usa el paquete. Haga clic en el botón Examinar **(…)** para ver y configurar las configuraciones de paquetes.|  
|`Expressions`|Haga clic en el botón Examinar **(…)** para crear expresiones para las propiedades del paquete.<br /><br /> Nota: puede crear expresiones de propiedad para todas las propiedades de paquete que incluye el modelo de objetos, no solo las propiedades que se muestran en el ventana Propiedades.<br /><br /> Para más información, vea [Usar expresiones de propiedad en paquetes](expressions/use-property-expressions-in-packages.md).<br /><br /> Para ver expresiones de propiedad existentes, expanda `Expressions`. Haga clic en el botón Examinar **(…)** en un cuadro de texto de expresión para modificar y evaluar una expresión.|  
|`ForceExecutionResult`|El resultado de la ejecución del paquete. Los valores son `None`, `Success`, `Failure` y `Completion`. El valor predeterminado de esta propiedad es `None`. Para obtener más información, vea T:Microsoft.SqlServer.Dts.Runtime.DTSForcedExecResult.|  
|`LocaleId`|Una configuración regional de Microsoft Win32. El valor predeterminado de esta propiedad es la configuración regional del sistema operativo del equipo local.|  
|`LoggingMode`|Valor que especifica el comportamiento de registro del paquete. Los valores son `Disabled`, `Enabled` y `UseParentSetting`. El valor predeterminado de esta propiedad es `UseParentSetting`. Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>.|  
|`OfflineMode`|Indica si el paquete está en el modo sin conexión. Esta propiedad es de solo lectura. La propiedad se establece en el nivel de proyecto. Por lo general, el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] intenta conectarse a cada origen de datos utilizado por el paquete para validar los metadatos asociados a los orígenes y destinos. Es posible habilitar la opción **Trabajar sin conexión** en el menú **SSIS** , incluso antes de abrir un paquete, para evitar los intentos de conexión y los errores de validación provocados por esos intentos cuando los orígenes de datos no están disponibles. También se puede habilitar la opción **Trabajar sin conexión** para acelerar las operaciones en el diseñador, y deshabilitarla solo cuando se quiere validar el paquete.|  
|`SuppressConfigurationWarnings`|Indica si se suprimen las advertencias generadas por configuraciones. El valor predeterminado de esta propiedad es `False`.|  
|`UpdateObjects`|Indica si el paquete se actualiza para usar versiones más recientes de los objetos que contiene, si hay versiones más recientes disponibles. Por ejemplo, si esta propiedad se establece en `True`, un paquete que incluye una tarea Inserción masiva se actualiza para usar una versión más reciente de la tarea Inserción masiva que proporciona [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. El valor predeterminado de esta propiedad es `False`.|  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 Las propiedades en esta categoría se usan para configurar el nivel de protección del paquete. Para más información, consulte [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md).  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|`PackagePassword`|La contraseña para los niveles de protección`EncryptSensitiveWithPassword` de `EncryptAllWithPassword`paquetes (y) que requieren contraseñas.|  
|`ProtectionLevel`|El nivel de protección del paquete. Los valores son `DontSaveSensitive`, `EncryptSensitiveWithUserKey`, `EncryptSensitiveWithPassword`, `EncryptAllWithPassword`y **ServerStorage**. El valor predeterminado de esta propiedad es `EncryptSensitiveWithUserKey`. Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel>.|  
  
###  <a name="transactions"></a><a name="Transactions"></a>Realizadas  
 Las propiedades en esta categoría configuran el nivel de aislamiento y la opción de transacción del paquete. Para más información, vea [Transacciones de Integration Services](integration-services-transactions.md).  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|`IsolationLevel`|Nivel de aislamiento de la transacción del paquete.  El valor predeterminado de esta propiedad es `Serializable`. Los valores válidos son <br />`Unspecified`<br />`Chaos`<br />`ReadUncommitted`<br />`ReadCommitted`<br />`RepeatableRead`<br />`Serializable`<br />`Snapshot`.<br /><br /> El sistema aplica la propiedad `IsolationLevel` a las transacciones de paquete solamente cuando el valor de la propiedad `TransactionOption` se establece en `Required`.<br /><br /> El valor de la propiedad `IsolationLevel` solicitado por un contenedor secundario se omite cuando se cumplen las condiciones siguientes:<br /><br /> El valor de la propiedad `TransactionOption` del contenedor secundario es `Supported`.<br />El contenedor secundario combina la transacción de un contenedor primario.<br /><br /> El valor de la propiedad `IsolationLevel` solicitado por el contenedor se respeta solamente cuando el contenedor inicia una nueva transacción. Un contenedor inicia una nueva transacción cuando se cumplen las condiciones siguientes:<br /><br /> El valor de la propiedad del `TransactionOption` contenedor es `Required`.<br />El contenedor primario aún no ha iniciado una transacción.<br /><br /> <br /><br /> Nota: El valor `Snapshot` de la propiedad `IsolationLevel` es incompatible con las transacciones de paquete. Por consiguiente, no puede utilizar la propiedad `IsolationLevel` para establecer el nivel de aislamiento de las transacciones de paquete en `Shapshot`. En su lugar, utilice una consulta SQL para establecer las transacciones de paquete en `Snapshot`. Para obtener más información, vea [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).<br /><br /> Para obtener más información sobre la propiedad `IsolationLevel`, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>.|  
|`TransactionOption`|Participación transaccional del paquete. Los valores son `NotSupported`, `Supported`, `Required`. El valor predeterminado de esta propiedad es `Supported`. Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>.|  
  
###  <a name="version"></a><a name="Version"></a>Versión  
 Las propiedades de esta categoría proporcionan información sobre la versión del objeto de paquete.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|`VersionBuild`|Número de versión de la compilación del paquete.|  
|`VersionComments`|Comentarios acerca de la versión del paquete.|  
|`VersionGUID`|GUID de la versión del paquete. Esta propiedad es de solo lectura.|  
|`VersionMajor`|Última versión importante del paquete.|  
|`VersionMinor`|Última versión de menor importancia del paquete.|  
  
  
