---
title: Establecer las propiedades de paquetes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c7cb436d29f4401122daba5985558e3bb50e665f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198256"
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
  
-   [Establecer las propiedades de un paquete](../../2014/integration-services/set-the-properties-of-a-package.md)  
  
## <a name="properties-by-category"></a>Propiedades por categoría  
 Las siguientes tablas enumeran las propiedades de paquete por categoría.  
  
###  <a name="Checkpoints"></a> Puntos de comprobación  
 Puede usar las propiedades de esta categoría para reiniciar el paquete desde un punto de error en el flujo de control de paquetes, en lugar de volver a ejecutar el paquete desde el principio de su flujo de control. Para obtener más información, vea [Reiniciar paquetes de usando puntos de comprobación](packages/restart-packages-by-using-checkpoints.md).  
  
|Property|Descripción|  
|--------------|-----------------|  
|`CheckpointFileName`|Nombre del archivo que captura la información del punto de comprobación que permite que un paquete se reinicie. Cuando el paquete termina correctamente, se elimina este archivo.|  
|`CheckpointUsage`|Especifica cuándo se puede reiniciar un paquete. Los valores son `Never`, `IfExists`, y `Always`. El valor predeterminado de esta propiedad es `Never`, lo que indica que no se puede reiniciar el paquete. Para obtener más información, consulta <xref:Microsoft.SqlServer.Dts.Runtime.DTSCheckpointUsage>.|  
|`SaveCheckpoints`|Especifica si los puntos de comprobación se escriben en el archivo de punto de comprobación cuando se ejecuta el paquete. El valor predeterminado de esta propiedad es `False`.|  
  
> [!NOTE]  
>  La opción `/CheckPointing on` de dtexec es equivalente a establecer la propiedad `SaveCheckpoints` del paquete en True y la propiedad `CheckpointUsage` en Always. Para más información, consulte [dtexec Utility](packages/dtexec-utility.md).  
  
###  <a name="Execution"></a> Ejecución  
 Las propiedades en esta categoría configuran el comportamiento de tiempo de ejecución del objeto de paquete.  
  
|Property|Descripción|  
|--------------|-----------------|  
|`DelayValidation`|Indica si la validación del paquete se retrasa hasta que se ejecute el paquete. El valor predeterminado de esta propiedad es `False`.|  
|**Deshabilitar**|Indica si el paquete está deshabilitado. El valor predeterminado de esta propiedad es `False`.|  
|`DisableEventHandlers`|Especifica si se ejecutan los controladores de eventos del paquete. El valor predeterminado de esta propiedad es `False`.|  
|`FailPackageOnFailure`|Especifica si el paquete genera un error cuando se produce un error en un componente de paquete. El único valor válido de esta propiedad es `False`.|  
|`FailParentOnError`|Especifica si el contenedor principal genera un error cuando se produce un error en un contenedor secundario. El valor predeterminado de esta propiedad es `False`.|  
|`MaxConcurrentExecutables`|Cantidad de archivos ejecutables que el paquete puede ejecutar simultáneamente. El valor predeterminado de esta propiedad es **-1**, que indica que no hay límite.|  
|`MaximumErrorCount`|Cantidad máxima de errores que se pueden producir antes de que un paquete termine de ejecutarse. El valor predeterminado de esta propiedad es **1**.|  
|`PackagePriorityClass`|Clase de prioridad de subproceso Win32 del subproceso del paquete. Los valores son `Default`, `AboveNormal`, `Normal`, `BelowNormal`, `Idle`. El valor predeterminado de esta propiedad es `Default`. Para obtener más información, consulta <xref:Microsoft.SqlServer.Dts.Runtime.DTSPriorityClass>.|  
  
###  <a name="ForcedExecutionValue"></a> Valor de ejecución forzada  
 Las propiedades de esta categoría configuran un valor de ejecución opcional para el paquete.  
  
|Property|Descripción|  
|--------------|-----------------|  
|`ForcedExecutionValue`|Si se establece ForceExecutionValue en `True`, un valor que especifica el valor de ejecución opcional que devuelve el paquete. El valor predeterminado de esta propiedad es **0**.|  
|`ForcedExecutionValueType`|Tipo de datos de ForcedExecutionValue. El valor predeterminado de esta propiedad es `Int32`.|  
|`ForceExecutionValue`|Valor booleano que especifica si se debería forzar a que el valor de ejecución opcional del contenedor contenga un valor concreto. El valor predeterminado de esta propiedad es `False`.|  
  
###  <a name="Identification"></a> Identificación  
 Las propiedades de esta categoría proporcionan información como el identificador único y el nombre del paquete.  
  
|Property|Descripción|  
|--------------|-----------------|  
|`CreationDate`|Fecha en que se creó el paquete.|  
|`CreatorComputerName`|Nombre del equipo en el que creó el paquete.|  
|`CreatorName`|Nombre de la persona que creó el paquete.|  
|`Description`|Descripción de la funcionalidad del paquete.|  
|`ID`|GUID del paquete, que se asigna cuando se crea el paquete. Esta propiedad es de solo lectura. Para generar un nuevo valor aleatorio para el `ID` propiedad, seleccione  **\<generar nuevo Id. >** en la lista desplegable.|  
|`Name`|Nombre del paquete.|  
|`PackageType`|Tipo de paquete. Los valores son `Default`, `DTSDesigner`, `DTSDesigner100`, `DTSWizard`, `SQLDBMaint`, y `SQLReplication`. El valor predeterminado de esta propiedad es `Default`. Para obtener más información, consulta <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>.|  
  
###  <a name="Misc"></a> Varios  
 Las propiedades de esta categoría se usan para obtener acceso a las configuraciones y expresiones que usa un paquete y proporcionar información acerca de la configuración regional y modo de registro del paquete. Para obtener más información, vea [Usar expresiones de propiedad en paquetes](expressions/use-property-expressions-in-packages.md).  
  
|Property|Descripción|  
|--------------|-----------------|  
|`Configurations`|Colección de las configuraciones que usa el paquete. Haga clic en el botón para examinar **(…)** para ver y configurar las configuraciones de paquetes.|  
|`Expressions`|Haga clic en el botón para examinar **(…)** para crear expresiones para las propiedades de paquete.<br /><br /> Nota: Puede crear expresiones de propiedad para todas las propiedades de paquete que el objeto de modelo incluye, no solo las propiedades enumeradas en la ventana Propiedades.<br /><br /> Para obtener más información, vea [Usar expresiones de propiedad en paquetes](expressions/use-property-expressions-in-packages.md).<br /><br /> Para ver expresiones de propiedad existentes, expanda `Expressions`. Haga clic en el botón para examinar **(…)** en un cuadro de texto de expresión para modificar y evaluar una expresión.|  
|`ForceExecutionResult`|El resultado de la ejecución del paquete. Los valores son `None`, `Success`, `Failure`, y `Completion`. El valor predeterminado de esta propiedad es `None`. Para obtener más información, vea T:Microsoft.SqlServer.Dts.Runtime.DTSForcedExecResult.|  
|`LocaleId`|Una configuración regional de Microsoft Win32. El valor predeterminado de esta propiedad es la configuración regional del sistema operativo del equipo local.|  
|`LoggingMode`|Valor que especifica el comportamiento de registro del paquete. Los valores son `Disabled`, `Enabled`, y `UseParentSetting`. El valor predeterminado de esta propiedad es `UseParentSetting`. Para obtener más información, consulta <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>.|  
|`OfflineMode`|Indica si el paquete está en el modo sin conexión. Esta propiedad es de solo lectura. La propiedad se establece en el nivel de proyecto. Por lo general, el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] intenta conectarse a cada origen de datos utilizado por el paquete para validar los metadatos asociados a los orígenes y destinos. Es posible habilitar la opción **Trabajar sin conexión** en el menú **SSIS** , incluso antes de abrir un paquete, para evitar los intentos de conexión y los errores de validación provocados por esos intentos cuando los orígenes de datos no están disponibles. También se puede habilitar la opción **Trabajar sin conexión** para acelerar las operaciones en el diseñador, y deshabilitarla solo cuando se quiere validar el paquete.|  
|`SuppressConfigurationWarnings`|Indica si se suprimen las advertencias generadas por configuraciones. El valor predeterminado de esta propiedad es `False`.|  
|`UpdateObjects`|Indica si el paquete se actualiza para usar versiones más recientes de los objetos que contiene, si hay versiones más recientes disponibles. Por ejemplo, si esta propiedad se establece en `True`, un paquete que incluye una tarea inserción masiva se actualiza para usar la versión más reciente de la inserción masiva de tareas que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona. El valor predeterminado de esta propiedad es `False`.|  
  
###  <a name="Security"></a> Seguridad  
 Las propiedades en esta categoría se usan para configurar el nivel de protección del paquete. Para más información, consulte [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md).  
  
|Property|Descripción|  
|--------------|-----------------|  
|`PackagePassword`|La contraseña de los niveles de protección de paquetes (`EncryptSensitiveWithPassword` y `EncryptAllWithPassword`) que requieren contraseñas.|  
|`ProtectionLevel`|El nivel de protección del paquete. Los valores son `DontSaveSensitive`, `EncryptSensitiveWithUserKey`, `EncryptSensitiveWithPassword`, `EncryptAllWithPassword`, y **ServerStorage**. El valor predeterminado de esta propiedad es `EncryptSensitiveWithUserKey`. Para obtener más información, consulta <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel>.|  
  
###  <a name="Transactions"></a> Transactions  
 Las propiedades en esta categoría configuran el nivel de aislamiento y la opción de transacción del paquete. Para obtener más información, vea [Transacciones de Integration Services](integration-services-transactions.md).  
  
|Property|Descripción|  
|--------------|-----------------|  
|`IsolationLevel`|Nivel de aislamiento de la transacción del paquete.  El valor predeterminado de esta propiedad es `Serializable`. Los valores válidos son <br />`Unspecified`<br />`Chaos`<br />`ReadUncommitted`<br />`ReadCommitted`<br />`RepeatableRead`<br />`Serializable`<br />`Snapshot`.<br /><br /> El sistema aplica la propiedad `IsolationLevel` a las transacciones de paquete solamente cuando el valor de la propiedad `TransactionOption` se establece en `Required`.<br /><br /> El valor de la `IsolationLevel` por un contenedor secundario se solicitó una propiedad se omite cuando se cumplen las condiciones siguientes:<br /><br /> El valor de la propiedad `TransactionOption` del contenedor secundario es `Supported`.<br />El contenedor secundario combina la transacción de un contenedor primario.<br /><br /> El valor de la propiedad `IsolationLevel` solicitado por el contenedor se respeta solamente cuando el contenedor inicia una nueva transacción. Un contenedor inicia una nueva transacción cuando se cumplen las condiciones siguientes:<br /><br /> El valor del contenedor `TransactionOption` propiedad es `Required`.<br />El contenedor primario aún no ha iniciado una transacción.<br /><br /> <br /><br /> Nota: La `Snapshot` valor de la `IsolationLevel` propiedad no es compatible con las transacciones de paquete. Por lo tanto, no puede usar el `IsolationLevel` propiedad para establecer el nivel de aislamiento de transacciones de paquete para `Shapshot`. En su lugar, utilice una consulta SQL para establecer las transacciones de paquete en `Snapshot`. Para obtener más información, vea [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).<br /><br /> Para obtener más información sobre la propiedad `IsolationLevel`, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>.|  
|`TransactionOption`|Participación transaccional del paquete. Los valores son `NotSupported`, `Supported`, `Required`. El valor predeterminado de esta propiedad es `Supported`. Para obtener más información, consulta <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>.|  
  
###  <a name="Version"></a> Versión  
 Las propiedades de esta categoría proporcionan información sobre la versión del objeto de paquete.  
  
|Property|Descripción|  
|--------------|-----------------|  
|`VersionBuild`|Número de versión de la compilación del paquete.|  
|`VersionComments`|Comentarios acerca de la versión del paquete.|  
|`VersionGUID`|GUID de la versión del paquete. Esta propiedad es de solo lectura.|  
|`VersionMajor`|Última versión importante del paquete.|  
|`VersionMinor`|Última versión de menor importancia del paquete.|  
  
  
