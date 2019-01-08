---
title: Variables de Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- user-defined variables [Integration Services]
- scope [Integration Services]
- system variables [Integration Services]
- variables [Integration Services]
- variables [Integration Services], about variables
- values [Integration Services]
ms.assetid: c1e81ad6-628b-46d4-9b09-d2866517b6ca
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e6df40fef89955b792e31e0a7539a4adf9409d70
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52772577"
---
# <a name="integration-services-ssis-variables"></a>Variables de Integration Services (SSIS)
  Las variables almacenan valores que un paquete de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y sus contenedores, tareas y controladores de eventos pueden usar en tiempo de ejecución. Los scripts en la tarea Script y el componente Script también pueden usar variables. Las restricciones de precedencia que ordenan tareas y contenedores en un flujo de trabajo pueden usar variables cuando sus definiciones de restricciones incluyen expresiones.  
  
 Puede usar variables en paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para los siguientes fines:  
  
-   Actualizar propiedades de elementos de paquete en tiempo de ejecución. Por ejemplo, puede establecer dinámicamente el número de ejecutables simultáneos que admite un contenedor de bucles Foreach.  
  
-   Incluir una tabla de búsqueda almacenada en la memoria. Por ejemplo, un paquete puede ejecutar una tarea Ejecutar SQL que carga una variable con valores de datos.  
  
-   Cargar variables con valores de datos y usarlas posteriormente para especificar una condición de búsqueda en una cláusula WHERE. Por ejemplo, el script de una tarea Script puede actualizar el valor de una variable que utiliza una instrucción Transact-SQL en una tarea Ejecutar SQL.  
  
-   Cargar una variable con un número entero y luego usar el valor para controlar bucles dentro de un flujo de control de paquetes. Por ejemplo, puede utilizar una variable en la expresión de evaluación de un contenedor de bucles For para controlar la iteración.  
  
-   Llenar valores de parámetros para instrucciones Transact-SQL en tiempo de ejecución. Por ejemplo, un paquete puede ejecutar una tarea Ejecutar SQL y luego utilizar variables para establecer dinámicamente los parámetros en una instrucción Transact-SQL.  
  
-   Generar expresiones que incluyen valores de variable. Por ejemplo, la transformación Columna derivada puede llenar una columna con el resultado obtenido mediante la multiplicación de un valor de variable por un valor de columna.  
  
## <a name="system-and-user-defined-variables"></a>Variables del sistema y definidas por el usuario  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] admite dos tipos de variables: variables definidas por el usuario y variables del sistema. Las variables definidas por el usuario son definidas por los desarrolladores de paquetes y las variables del sistema son definidas por [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Puede crear la cantidad de variables definidas por el usuario que requiera un paquete, pero no puede crear variables del sistema adicionales.  
  
 Todas las variables (del sistema y definidas por el usuario) se pueden usar en los enlaces de parámetros que usa la tarea Ejecutar SQL para asignar variables a parámetros en instrucciones SQL. Para más información, vea [Tarea Ejecutar SQL](control-flow/execute-sql-task.md) y [Parámetros y códigos de retorno en la tarea Ejecutar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
> [!NOTE]  
>  Los nombres de variables definidas por el usuario y variables del sistema distinguen mayúsculas y minúsculas.  
  
 Puede crear variables definidas por el usuario para todos los tipos de contenedores de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] : paquetes, contenedores de bucles Foreach, contenedores de bucles For, contenedores de secuencias, tareas y controladores de eventos. Las variables definidas por el usuario son miembros de la colección de variables del contenedor.  
  
 Si crea el paquete mediante el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , puede ver los miembros de las colecciones de variables en las carpetas **Variables** en la pestaña **Explorador de paquetes** del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] . Las carpetas enumeran las variables definidas por el usuario y variables del sistema.  
  
 Puede configurar las variables definidas por el usuario de las maneras siguientes:  
  
-   Proporcionar un nombre y una descripción para la variable.  
  
-   Especificar un espacio de nombres para la variable.  
  
-   Indicar si la variable activa un evento cuando cambia su valor.  
  
-   Indicar si la variable es de solo lectura o de lectura/escritura.  
  
-   Usar el resultado de la evaluación de una expresión para configurar el valor de variable.  
  
-   Crear la variable en el ámbito del paquete o un objeto de paquete, como una tarea.  
  
-   Especificar el valor y el tipo de datos de la variable.  
  
 La única opción configurable en las variables del sistema es especificar si activan un evento cuando cambian de valor.  
  
 Hay disponible un conjunto diferente de variables del sistema para diferentes tipos de contenedor. Para obtener más información sobre las variables del sistema usadas por paquetes y sus elementos, vea [System Variables](system-variables.md).  
  
 Para obtener más información sobre escenarios de uso real para variables, vea [Usar variables en paquetes](../../2014/integration-services/use-variables-in-packages.md).  
  
## <a name="variable-properties"></a>Propiedades de variables  
 Puede configurar variables definidas por el usuario estableciendo las siguientes propiedades en la ventana **Variables** o en la ventana **Propiedades** . Algunas propiedades solo están disponibles en la ventana Propiedades.  
  
> [!NOTE]  
>  La única opción configurable en las variables del sistema es especificar si activan un evento cuando cambian de valor.  
  
 Descripción  
 Especifica la descripción de la variable.  
  
 EvaluateAsExpression  
 Cuando la propiedad se establece en `True`, la expresión especificada se usa para establecer el valor de la variable.  
  
 Expresión  
 Especifica la expresión asignada a la variable.  
  
 Nombre  
 Especifica el nombre de la variable.  
  
 Espacio de nombres  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona dos espacios de nombres, **User** y **System**. Como opción predeterminada, las variables personalizadas están en el espacio de nombres **User** y las variables del sistema están en el espacio de nombres **System** . Puede crear espacios de nombres adicionales para variables definidas por el usuario y cambiar el nombre del espacio de nombres **User**, pero no puede cambiar el nombre del espacio de nombres **System**, agregar variables al espacio de nombres **System** o asignar variables del sistema a un espacio de nombres diferente.  
  
 RaiseChangedEvent  
 Cuando la propiedad está establecida en `True`, se produce el evento de `OnVariableValueChanged` si el valor de la variable cambia.  
  
 Solo lectura  
 Cuando la propiedad está establecida en `False`, la variable es de lectura\escritura.  
  
 Ámbito  
 > [!NOTE]  
>  Para cambiar este valor de la propiedad, basta con hacer clic en **Mover variable** en la ventana **Variables** .  
  
 Una variable se crea dentro del ámbito de un paquete o dentro del ámbito de un contenedor, tarea o controlador de evento en el paquete. Dado que el contenedor del paquete se encuentra en la parte superior de la jerarquía de contenedores, las variables con ámbito de paquete funcionan como variables globales y pueden ser usadas por todos los contenedores en el paquete. De manera similar, las variables definidas dentro del ámbito de un contenedor, como el contenedor de bucles For, pueden ser usadas por todas las tareas o contenedores dentro del contenedor de bucles For.  
  
 Si un paquete ejecuta otros paquetes mediante la tarea Ejecutar paquete, las variables definidas en el ámbito del paquete que llama o la tarea Ejecutar paquete se pueden poner a disposición del paquete llamado usando el tipo de configuración de variable de paquete primario. Para más información, consulte [Package Configurations](../../2014/integration-services/package-configurations.md).  
  
 IncludeInDebugDump  
 Indica si el valor variable está incluido en los archivos de volcado de depuración.  
  
 Para variables definidas por el usuario y variables del sistema, el valor predeterminado para el **InclueInDebugDump** opción es `true`.  
  
 Sin embargo, para las variables definidas por el usuario, el sistema restablece la **IncludeInDebugDump** opción `false` cuando se cumplen las condiciones siguientes:  
  
-   Si el **EvaluateAsExpression** propiedad de la variable se establece en `true`, el sistema restablece la **IncludeInDebugDump** opción `false`.  
  
     Para incluir el texto de la expresión como el valor de la variable en los archivos de volcado de depuración, establezca el **IncludeInDebugDump** opción `true`.  
  
-   Si se cambia el tipo de datos en una cadena, el sistema restablece la **IncludeInDebugDump** opción `false`.  
  
 Cuando el sistema restablece la **IncludeInDebugDump** opción `false`, podría invalidarse el valor seleccionado por el usuario.  
  
 Valor  
 El valor de una variable definida por el usuario puede ser un literal o una expresión. Una variable incluye opciones para establecer el valor de la variable y el tipo de datos del valor. Las dos propiedades deben ser compatibles: por ejemplo, el uso de un valor de cadena junto con el tipo de datos de número entero no es válido.  
  
 Si la variable está configurada para evaluarse como una expresión, se debe proporcionar una expresión. En el tiempo de ejecución, se evalúa la expresión, y se establece la variable con el resultado de la evaluación. Por ejemplo, si una variable usa la expresión `DATEPART("month", GETDATE())` , el valor de la variable es el equivalente numérico del mes de la fecha actual. La expresión debe ser una expresión válida que use la sintaxis de gramática de expresiones de [!INCLUDE[ssIS](../includes/ssis-md.md)] . Cuando una expresión se usa con variables, la expresión puede usar literales y los operadores y funciones que proporciona la gramática de la expresión, pero la expresión no puede hacer referencia a las columnas desde un flujo de datos en el paquete. La longitud máxima de una expresión es 4000 caracteres. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 ValueType  
 > [!NOTE]  
>  El valor de la propiedad aparece en la columna **Tipo de datos** en la ventana **Variables** .  
  
 Especifica el tipo de datos del valor de la variable.  
  
## <a name="configuring-variables"></a>Configurar variables  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que puede configurar en el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , consulte [Ventana Variables](../../2014/integration-services/variables-window.md).  
  
 Para obtener más información sobre las propiedades de las variables, así como recabar obtener más información sobre la configuración mediante programación de estas propiedades, vea <xref:Microsoft.SqlServer.Dts.Runtime.Variable>.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Agregar, eliminar, cambiar el ámbito de la variable definida por el usuario en un paquete](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
 [Establecer las propiedades de una variable definida por el usuario](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
 [Uso de los valores de variables y parámetros en un paquete secundario](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
 [Asignar parámetros de consulta a variables en un componente de flujo de datos](data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
  
