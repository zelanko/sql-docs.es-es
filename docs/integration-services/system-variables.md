---
description: Variables del sistema
title: Variables del sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], variables
- tasks [Integration Services], variables
- system variables [Integration Services]
- event handlers [Integration Services], variables
- variables [Integration Services], system
ms.assetid: efecd0d4-1489-4eba-a8fe-275d647058b8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 913345034da936d6ed7a0c9ea3678c427b4f34ef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495329"
---
# <a name="system-variables"></a>Variables del sistema

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona un conjunto de variables del sistema que almacenan información sobre el paquete en ejecución y sus objetos. Estas variables se pueden usar en expresiones y expresiones de propiedad para personalizar paquetes, contenedores, tareas y controladores de eventos.  
  
 Todas las variables (del sistema y definidas por el usuario) se pueden usar en los enlaces de parámetros que usa la tarea Ejecutar SQL para asignar variables a parámetros.  
  
## <a name="system-variables-for-packages"></a>Variables del sistema para paquetes  
 La siguiente tabla describe las variables del sistema que proporciona [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para paquetes.  
  
|Variable del sistema|Tipo de datos|Descripción|  
|---------------------|---------------|-----------------|  
|**CancelEvent**|Int32|Identificador de un objeto de evento de Windows que la tarea puede señalar para indicar que la tarea debe dejar de ejecutarse.|  
|**ContainerStartTime**|DateTime|Hora de inicio del contenedor.|  
|**CreationDate**|DateTime|Fecha en que se creó el paquete.|  
|**CreatorComputerName**|String|Equipo en el que se creó el paquete.|  
|**CreatorName**|String|Nombre de la persona que creó el paquete.|  
|**ExecutionInstanceGUID**|String|Identificador exclusivo de la instancia de ejecución de un paquete.|  
|**FailedConfigurations**|String|Nombres de las configuraciones de paquete que no se pudieron realizar.|  
|**IgnoreConfigurationsOnLoad**|Boolean|Indica si las configuraciones de paquete se omiten al cargar el paquete.|  
|**InteractiveMode**|Boolean|Indica si el paquete se ejecuta en modo interactivo. Si un paquete se ejecuta en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , esta propiedad se establece en **True**. Si un paquete se ejecuta con la utilidad de símbolo del sistema **DTExec** , la propiedad se establece en **False**.|  
|**LocaleId**|Int32|Configuración regional que usa el paquete.|  
|**MachineName**|String|Nombre del equipo en el que se está ejecutando el paquete.|  
|**OfflineMode**|Boolean|Indica si el paquete está en el modo sin conexión. El modo sin conexión no adquiere conexiones a orígenes de datos.|  
|**PackageID**|String|Identificador único del paquete.|  
|**PackageName**|String|Nombre del paquete.|  
|**StartTime**|DateTime|Hora a la que se inició la ejecución del paquete.|  
|**ServerExecutionID**|Int64|Identificador de ejecución para el paquete que se ejecuta en el servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .<br /><br /> El valor predeterminado es cero. El valor se cambia únicamente si el paquete lo ejecuta ISServerExec en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Cuando hay un paquete secundario, el valor se pasa desde el paquete primario al paquete secundario.|  
|**UserName**|String|Cuenta del usuario que inició el paquete. El nombre de usuario se encuentra calificado por el nombre de dominio.|  
|**VersionBuild**|Int32|Versión del paquete.|  
|**VersionComment**|String|Comentarios acerca de la versión del paquete.|  
|**VersionGUID**|String|Identificador único de la versión.|  
|**VersionMajor**|Int32|Versión principal del paquete.|  
|**VersionMinor**|Int32|Versión secundaria del paquete.|  
  
## <a name="system-variables-for-containers"></a>Variables del sistema para contenedores  
 La siguiente tabla describe las variables del sistema que proporciona [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para los contenedores de bucles For, Foreach y de secuencia.  
  
|Variable del sistema|Tipo de datos|Descripción|Contenedor|  
|---------------------|---------------|-----------------|---------------|  
|**LocaleId**|Int32|Configuración regional que usa el contenedor.|Contenedor de bucles For<br /><br /> Contenedor de bucles Foreach<br /><br /> contenedor de secuencias|  
  
## <a name="system-variables-for-tasks"></a>Variables del sistema para tareas  
 La siguiente tabla describe las variables del sistema que proporciona [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para tareas.  
  
|Variable del sistema|Tipo de datos|Descripción|  
|---------------------|---------------|-----------------|  
|**CreationName**|String|Nombre de la tarea.|  
|**LocaleId**|Int32|Configuración regional que usa la tarea.|  
|**TaskID**|String|Identificador único de una instancia de tarea.|  
|**TaskName**|String|Nombre de la instancia de tarea.|  
|**TaskTransactionOption**|Int32|Opción de transacción que usa la tarea.|  
  
## <a name="system-variables-for-event-handlers"></a>Variables del sistema para los controladores de eventos  
 La siguiente tabla describe las variables del sistema que proporciona [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para los controladores de eventos. No todas las variables están disponibles para todos los controladores de eventos.  
  
|Variable del sistema|Tipo de datos|Descripción|Controlador de eventos|  
|---------------------|---------------|-----------------|-------------------|  
|**Cancelar**|Boolean|Indica si el controlador de eventos deja de ejecutarse cuando se produce un error, advertencia o cancelación de consulta.|Controlador de eventos OnError<br /><br /> Controlador de eventos OnWarning<br /><br /> Controlador de eventos OnQueryCancel|  
|**ErrorCode**|Int32|Identificador del error.|Controlador de eventos OnError<br /><br /> Controlador de eventos OnInformation<br /><br /> Controlador de eventos OnWarning|  
|**ErrorDescription**|String|Descripción del error.|Controlador de eventos OnError<br /><br /> Controlador de eventos OnInformation<br /><br /> Controlador de eventos OnWarning|  
|**ExecutionStatus**|Boolean|Estado de ejecución actual.|Controlador de eventos OnExecStatusChanged|  
|**ExecutionValue**|DBNull|Valor de ejecución.|Controlador de eventos OnTaskFailed|  
|**LocaleId**|Int32|Configuración regional que usa el controlador de eventos.|Todos los controladores de eventos|  
|**PercentComplete**|Int32|Porcentaje de trabajo completado.|Controlador de eventos OnProgress|  
|**ProgressCountHigh**|Int32|Parte alta de un valor de 64 bits que indica la cantidad total de operaciones procesadas por el evento OnProgress.|Controlador de eventos OnProgress|  
|**ProgressCountLow**|Int32|Parte baja de un valor de 64 bits que indica la cantidad total de operaciones procesadas por el evento OnProgress.|Controlador de eventos OnProgress|  
|**ProgressDescription**|String|Descripción del progreso.|Controlador de eventos OnProgress|  
|**Propagate**|Boolean|Indica si el evento se propaga a un controlador de eventos de nivel más alto.<br /><br /> Nota: El valor de la variable **Propagate** se descarta durante la validación del paquete. Si establece **Propagate** en **False** en un paquete secundario, ello no evita que un evento se propague hasta el paquete primario.|Todos los controladores de eventos|  
|**SourceDescription**|String|Descripción del ejecutable en el controlador de eventos que provocó el evento.|Todos los controladores de eventos|  
|**SourceID**|String|Descripción del identificador único del ejecutable en el controlador de eventos que provocó el evento.|Todos los controladores de eventos|  
|**SourceName**|String|Nombre del ejecutable en el controlador de eventos que provocó el evento.|Todos los controladores de eventos|  
|**VariableDescription**|String|Descripción de la variable.|Controlador de eventos OnVariableValueChanged|  
|**VariableID**|String|Identificador único de la variable.|Controlador de eventos OnVariableValueChanged|  
  
## <a name="system-variables-in-parameter-bindings"></a>Variables del sistema en enlaces de parámetros  
 Con frecuencia resulta útil guardar los valores de variables del sistema en tablas cuando se ejecuta el paquete. Por ejemplo, un paquete que crea dinámicamente una tabla y escribe el GUID de la instancia de ejecución del paquete que creó la tabla en una columna de la tabla.  
  
 Si utiliza variables del sistema para asignar parámetros en la instrucción SQL que utiliza una tarea Ejecutar SQL, es importante que establezca el tipo de datos de cada parámetro enlazando al tipo de datos de la variable del sistema. De lo contrario, los valores de las variables del sistema se pueden traducir incorrectamente. Por ejemplo, si la variable del sistema **ExecutionInstanceGUID** , que tiene el tipo de datos de cadena y contiene una cadena que representa el GUID de la instancia de ejecución de un paquete, se usa en un enlace de parámetro con el tipo de datos del GUID, el GUID de la instancia del paquete se traducirá de manera incorrecta.  
  
 Esta regla se aplica también a las variables definidas por el usuario. No obstante, si bien los tipos de datos de las variables del sistema no se pueden cambiar y usted debe adaptar el uso de estas variables para que se ajusten a los tipos de datos, las variables definidas por el usuario son más flexibles. Las variables definidas por el usuario que se utilizan en enlaces de parámetros generalmente se definen con tipos de datos que son compatibles con los tipos de datos de parámetros a los que se asignan.  
  
## <a name="related-tasks"></a>Related Tasks  
 [asignar parámetros de consulta a variables en una tarea Ejecutar SQL](https://msdn.microsoft.com/library/6a164349-dfcf-4995-80bc-d4e7aee52a83)  
  
  
