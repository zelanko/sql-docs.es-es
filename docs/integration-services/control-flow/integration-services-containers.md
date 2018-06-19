---
title: Contenedores de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SSIS containers
- containers [Integration Services]
- containers [Integration Services], about containers
- control flow [Integration Services], containers
- SQL Server Integration Services containers
ms.assetid: 1b725922-ec59-4a47-9d55-e079463058f3
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1d27f27154fe4faa1f028c53aafd7db40f20e938
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35333279"
---
# <a name="integration-services-containers"></a>Contenedores de Integration Services
  Los contenedores son objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que proporcionan estructura a los paquetes y servicios a las tareas. Permiten repetir flujos de control en paquetes y agrupan tareas y contenedores en unidades de trabajo significativas. Los contenedores pueden incluir otros contenedores, además de tareas.  
  
 Los paquetes usan contenedores para los siguientes fines:  
  
-   Repetir tareas para cada elemento de una colección, como archivos de una carpeta, esquemas u objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO). Por ejemplo, un paquete puede ejecutar instrucciones de Transact-SQL almacenadas en varios archivos.  
  
-   Repetir las tareas hasta que una expresión especificada se evalúe como **false**. Por ejemplo, un paquete puede enviar un mensaje de correo electrónico distinto siete veces, una vez cada día de la semana.  
  
-   Agrupar tareas y contenedores que deben completarse correctamente o no completarse como una unidad (todas o ninguna). Por ejemplo, un paquete puede agrupar tareas que eliminan y agregan filas de una tabla de base de datos, y confirmar o revertir todas las tareas si una no se completa correctamente.  
  
## <a name="container-types"></a>Tipos de contenedor  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona cuatro tipos de contenedores para generar paquetes. En la tabla siguiente se muestran los tipos de contenedor.  
  
|Contenedor|Descripción|  
|---------------|-----------------|  
|[Contenedor Foreach Loop](../../integration-services/control-flow/foreach-loop-container.md)|Ejecuta un flujo de control repetidamente mediante un enumerador.|  
|[Contenedor de bucles For](../../integration-services/control-flow/for-loop-container.md)|Ejecuta un flujo de control repetidamente probando una condición.|  
|[Contenedor de secuencias](../../integration-services/control-flow/sequence-container.md)|Agrupa tareas y contenedores en flujos de control que son subconjuntos del flujo de control del paquete.|  
|[Contenedor de tarea](../../integration-services/control-flow/task-host-container.md)|Proporciona servicios a una tarea individual.|  
  
 Los paquetes y los controladores de eventos también son tipos de contenedores. Para obtener información, vea [Paquetes de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md) y [Controladores de eventos de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md).  
  
### <a name="summary-of-container-properties"></a>Resumen de propiedades de contenedor  
 Todos los tipos de contenedor tienen un conjunto de propiedades comunes. Si se crean paquetes con las herramientas gráficas de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , en la ventana Propiedades se enumeran las siguientes propiedades de los contenedores de bucles Foreach, bucles For y secuencias. Las propiedades del contenedor del host de la tarea se configuran como parte de la configuración de la tarea que el host de la tarea encapsula. Las propiedades del host de la tarea se establecen al configurar la tarea.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|**DelayValidation**|Valor booleano que indica si la validación del contenedor se retrasa hasta el tiempo de ejecución. El valor predeterminado de esta propiedad es **False**.<br /><br /> Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.DelayValidation%2A>.|  
|**Descripción**|Descripción del contenedor. La propiedad contiene una cadena, pero puede estar en blanco.<br /><br /> Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Description%2A>.|  
|**Deshabilitar**|Valor booleano que indica si el contenedor se ejecuta. El valor predeterminado de esta propiedad es **False**.<br /><br /> Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Disable%2A>.|  
|**DisableEventHandlers**|Valor booleano que indica si los controladores de eventos asociados al contenedor se ejecutan. El valor predeterminado de esta propiedad es **False**.|  
|**FailPackageOnFailure**|Valor booleano que especifica si el paquete genera un error cuando se produce un error en el contenedor. El valor predeterminado de esta propiedad es **False**.<br /><br /> Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailPackageOnFailure%2A>.|  
|**FailParentOnFailure**|Valor booleano que especifica si el contenedor primario genera un error cuando se produce un error en el contenedor. El valor predeterminado de esta propiedad es **False**.<br /><br /> Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailParentOnFailure%2A>.|  
|**ForcedExecutionValue**|Si **ForceExecutionValue** se configura como **True**, objeto que contiene el valor de ejecución opcional del contenedor. El valor predeterminado de esta propiedad es **0**.<br /><br /> Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForcedExecutionValue%2A>.|  
|**ForcedExecutionValueType**|El tipo de datos de **ForcedExecutionValue**. El valor predeterminado de esta propiedad es **Int32**.|  
|**ForceExecutionResult**|Valor que especifica el resultado forzado de la ejecución del paquete o contenedor. Los valores son **None**, **Success**, **Failure**y **Completion**. El valor predeterminado de esta propiedad es **None**.<br /><br /> Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionResult%2A>.|  
|**ForceExecutionValue**|Valor booleano que especifica si se debería forzar a que el valor de ejecución opcional del contenedor contenga un valor concreto. El valor predeterminado de esta propiedad es **False**.<br /><br /> Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionValue%2A>.|  
|**ID**|GUID del contenedor, que se asigna cuando se crea el paquete. Esta propiedad es de solo lectura.<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ID%2A>.|  
|**IsolationLevel**|Nivel de aislamiento de la transacción del contenedor. Los valores son **Unspecified**, **Chaos**, **ReadUncommitted**, **ReadCommitted**, **RepeatableRead**, **Serializable**y **Snapshot**. El valor predeterminado de esta propiedad es **Serializable**. Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>.|  
|**LocaleID**|Una configuración regional de Microsoft Win32. El valor predeterminado de esta propiedad es la configuración regional del sistema operativo del equipo local.<br /><br /> Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LocaleID%2A>.|  
|**LoggingMode**|Valor que especifica el comportamiento de registro del contenedor. Los valores son **Disabled**, **Enabled**y **UseParentSetting**. El valor predeterminado de esta propiedad es **UseParentSetting**. Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>.|  
|**MaximumErrorCount**|Cantidad máxima de errores que se pueden producir antes de que un contenedor deje de ejecutarse. El valor predeterminado de esta propiedad es **1**.<br /><br /> Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.MaximumErrorCount%2A>.|  
|**Nombre**|Nombre del contenedor.<br /><br /> Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Name%2A>.|  
|**TransactionOption**|Participación transaccional del contenedor. Los valores son **NotSupported**, **Supported**y **Required**. El valor predeterminado de esta propiedad es **Supported**. Para obtener más información, vea <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>.|  
  
 Para obtener información sobre todas las propiedades disponibles para los contenedores de bucles Foreach, bucles For, secuencias y host de la tarea cuando se configuran mediante programación, vea los siguientes temas de la API de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] :  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForEachLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.Sequence  
  
-   T:Microsoft.SqlServer.Dts.Runtime.TaskHost  
  
## <a name="objects-that-extend-container-functionality"></a>Objetos que extienden la funcionalidad de un contenedor  
 Los contenedores incluyen flujos de control formados por ejecutables y restricciones de precedencia, y pueden usar controladores de eventos y variables. El contenedor del host de la tarea es una excepción: puesto que este contenedor encapsula una única tarea, no utiliza las restricciones de precedencia.  
  
### <a name="executables"></a>Ejecutables  
 Los ejecutables hacen referencia a las tareas de nivel de contenedor y a cualquier contenedor contenido en el contenedor. Un ejecutable puede ser una de las tareas y los contenedores proporcionados por [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , o una tarea personalizada. Para más información, consulte [Integration Services Tasks](../../integration-services/control-flow/integration-services-tasks.md).  
  
### <a name="precedence-constraints"></a>Restricciones de precedencia  
 Las restricciones de precedencia vinculan los contenedores y las tareas del mismo contenedor principal en un flujo de control ordenado. Para obtener más información, vea [Restricciones de precedencia](../../integration-services/control-flow/precedence-constraints.md).  
  
### <a name="event-handlers"></a>Controladores de eventos  
 Los controladores de eventos de nivel de contenedor responden a eventos provocados por el contenedor o por los objetos que incluye. Para obtener más información, vea [Controladores de eventos de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md).  
  
### <a name="variables"></a>Variables  
 Las variables que se usan en contenedores incluyen las variables del sistema de nivel de contenedor proporcionadas por [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y las variables definidas por el usuario usadas por el contenedor. Para obtener más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="break-points"></a>Puntos de interrupción  
 Al establecer un punto de interrupción en un contenedor y si la condición de interrupción es **Salto cuando el contenedor recibe el evento OnVariableValueChanged**, defina la variable en el ámbito del contenedor.  
  
## <a name="see-also"></a>Ver también  
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  
