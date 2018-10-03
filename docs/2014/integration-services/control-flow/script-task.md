---
title: Tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scripttask.f1
helpviewer_keywords:
- scripts [Integration Services], tasks
- Script task [Integration Services], about Script task
- Script task [Integration Services]
ms.assetid: f6cce7df-4bd6-4b75-9f89-6c37b4bb5558
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 38586615ce582ed4534bf23612bfca64b53af461
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224415"
---
# <a name="script-task"></a>Tarea Script
  La tarea Script proporciona código para realizar funciones que no están disponibles en las tareas integradas ni en las transformaciones proporcionadas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . La tarea Script también puede combinar funciones en un script, en lugar de usar múltiples tareas y transformaciones. La tarea Script sirve para trabajos que se deben realizar una sola vez en un paquete (o una vez por objeto enumerado), en lugar de una vez por fila de datos.  
  
 Puede usar la tarea Script para los siguientes fines:  
  
-   Tener acceso a datos mediante otras tecnologías incompatibles con los tipos de conexión integrados. Por ejemplo, un script puede usar interfaces del servicio Active Directory (ADSI) para tener acceso a los nombres de usuario de Active Directory y extraer dichos nombres.  
  
-   Crear un contador de rendimiento específico del paquete. Por ejemplo, un script puede crear un contador de rendimiento que se actualiza mientras se ejecuta una tarea compleja o de bajo rendimiento.  
  
-   Identificar si archivos específicos están vacíos o cuántas filas contienen y luego, en función de esa información, afectar el flujo de control de un paquete. Por ejemplo, si un archivo contiene cero filas, el valor de una variable se establece en 0, y una restricción de precedencia que evalúa el valor impide que una tarea Sistema de archivos copie el archivo.  
  
 Si tiene que utilizar el script para hacer el mismo trabajo en cada fila de datos de un conjunto, utilice el componente de script de la tarea Script. Por ejemplo, si desea evaluar si un valor de franqueo es razonable y omitir filas de datos con valores extremadamente altos o bajos, utilice un componente de script. Para más información, consulte [Script Component](../data-flow/transformations/script-component.md).  
  
 Si varios paquetes usan el script, considere la posibilidad de escribir una tarea personalizada en lugar de usar la tarea Script. Para más información, vea [Desarrollar una tarea personalizada](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
 Una vez que haya decidido que la tarea Script es la opción adecuada para el paquete, tiene que desarrollar el script que la tarea utiliza y configurar la propia tarea.  
  
## <a name="writing-and-running-the-script-that-the-task-uses"></a>Escribir y ejecutar el script que la tarea utiliza  
 La tarea Script usa [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools para Aplicaciones (VSTA) como entorno de escritura de los scripts y como motor que los ejecuta.  
  
 VSTA proporciona todas las características estándar del entorno [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] , como el editor de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] con códigos de color, IntelliSense y el **Explorador de objetos**. VSTA también utiliza el mismo depurador que usan otras herramientas de desarrollo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Los puntos de interrupción del script funcionan a la perfección con los puntos de interrupción de las tareas y los contenedores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . VSTA es compatible con los lenguajes de programación [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 Para ejecutar un script, debe tener VSTA instalado en el equipo en que se ejecute el paquete. Al ejecutar el paquete, la tarea carga el motor de script y ejecuta el script. Puede tener acceso a ensamblados .NET externos en scripts; para ello, debe agregar referencias a dichos ensamblados en el proyecto.  
  
> [!NOTE]  
>  A diferencia de las versiones anteriores en las que podía indicar si se precompilaban los scripts, todos los scripts se precompilan en [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] y versiones posteriores. Al precompilar el script, no se carga el motor del lenguaje en tiempo de ejecución, por lo que el paquete se ejecuta con mayor rapidez. Sin embargo, los archivos binarios precompilados utilizan una cantidad considerable de espacio en disco.  
  
## <a name="configuring-the-script-task"></a>Configurar la tarea Script  
 Puede configurar la tarea Script de las maneras siguientes:  
  
-   Proporcionar el script personalizado que ejecuta la tarea.  
  
-   Especifique el método del proyecto de VSTA que el módulo de ejecución de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] llama como punto de entrada en el código de la tarea Script.  
  
-   Especificar el lenguaje de script.  
  
-   Opcionalmente, proporcionar listas de variables de solo lectura/lectura y escritura para su uso en el script.  
  
 Puede establecer estas propiedades a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
### <a name="configuring-the-script-task-in-the-designer"></a>Configurar la tarea Script en el Diseñador  
 En la tabla siguiente se describe el evento `ScriptTaskLogEntry` que se puede registrar para la tarea Script. El `ScriptTaskLogEntry` se selecciona el evento para su registro en el **detalles** pestaña de la **configurar registros de SSIS** cuadro de diálogo. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) y [Mensajes personalizados para registro](../custom-messages-for-logging.md).  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`ScriptTaskLogEntry`|Informa sobre los resultados de la implementación del registro en el script. La tarea escribe una entrada de registro para cada llamada a la `Log` método de la `Dts` objeto. La tarea escribe estas entradas cuando se ejecuta el código. Para más información, consulte [Logging in the Script Task](../extending-packages-scripting/task/logging-in-the-script-task.md).|  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea los temas siguientes:  
  
-   [Editor de la tarea script &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de la tarea script &#40;página secuencia de comandos&#41;](../script-task-editor-script-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="configuring-the-script-task-programmatically"></a>Configurar la tarea Script mediante programación  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, vea el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask>  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Artículo técnico, [How to send email with delivery notification in C# (Enviar correo con notificación de entrega en C#)](http://go.microsoft.com/fwlink/?LinkId=237625), en shareourideas.com  
  
  
