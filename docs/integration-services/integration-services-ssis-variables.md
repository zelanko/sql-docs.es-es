---
title: Variables de Integration Services (SSIS) | Microsoft Docs
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
- variables [Integration Services], passing between packages
- user-defined variables [Integration Services]
- scope [Integration Services]
- system variables [Integration Services]
- variables [Integration Services]
- variables [Integration Services], about variables
- values [Integration Services]
ms.assetid: c1e81ad6-628b-46d4-9b09-d2866517b6ca
caps.latest.revision: 60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0581f31841e370799039d609501c0a9e76323653
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35408827"
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
  
 Todas las variables, del sistema y definidas por el usuario, se pueden utilizar en los enlaces de parámetros que utiliza la tarea Ejecutar SQL para asignar variables a parámetros en instrucciones SQL. Para obtener más información, vea [Tarea Ejecutar SQL](../integration-services/control-flow/execute-sql-task.md) y [Parámetros y códigos de retorno en la tarea Ejecutar SQL](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).  
  
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
  
 Hay disponible un conjunto diferente de variables del sistema para diferentes tipos de contenedor. Para obtener más información sobre las variables del sistema usadas por paquetes y sus elementos, vea [System Variables](../integration-services/system-variables.md).  
  
 Para obtener más información sobre escenarios de uso real para variables, vea [Usar variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="properties-of-variables"></a>Propiedades de las variables  
 Puede configurar variables definidas por el usuario estableciendo las siguientes propiedades en la ventana **Variables** o en la ventana **Propiedades** . Algunas propiedades solo están disponibles en la ventana Propiedades.  
  
> [!NOTE]  
>  La única opción configurable en las variables del sistema es especificar si activan un evento cuando cambian de valor.  
  
 **Description**    
 Especifica la descripción de la variable.  
  
 **EvaluateAsExpression**    
 Cuando la propiedad está establecida en **True**, la expresión especificada se usa para establecer el valor de la variable.  
  
 **Expresión**    
 Especifica la expresión asignada a la variable.  
  
 **Nombre**    
 Especifica el nombre de la variable.  
  
 **Espacio de nombres**  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona dos espacios de nombres, **User** y **System**. Como opción predeterminada, las variables personalizadas están en el espacio de nombres **User** y las variables del sistema están en el espacio de nombres **System** . Puede crear espacios de nombres adicionales para variables definidas por el usuario y cambiar el nombre del espacio de nombres **User** , pero no puede cambiar el nombre del espacio de nombres **System** , agregar variables al espacio de nombres **System** o asignar variables del sistema a un espacio de nombres diferente.  
  
**RaiseChangedEvent**  
 Cuando la propiedad está establecida en **True**, se produce el evento **OnVariableValueChanged** si el valor de la variable cambia.  
  
 **Solo lectura**  
 Cuando la propiedad está establecida en **False**, la variable es de lectura/escritura.  
  
**Ámbito**    
 > [!NOTE]  
>  Para cambiar este valor de la propiedad, basta con hacer clic en **Mover variable** en la ventana **Variables** .  
  
 Una variable se crea dentro del ámbito de un paquete o dentro del ámbito de un contenedor, tarea o controlador de evento en el paquete. Dado que el contenedor del paquete se encuentra en la parte superior de la jerarquía de contenedores, las variables con ámbito de paquete funcionan como variables globales y pueden ser usadas por todos los contenedores en el paquete. De manera similar, las variables definidas dentro del ámbito de un contenedor, como el contenedor de bucles For, pueden ser usadas por todas las tareas o contenedores dentro del contenedor de bucles For.  
  
 Si un paquete ejecuta otros paquetes mediante la tarea Ejecutar paquete, las variables definidas en el ámbito del paquete que llama o la tarea Ejecutar paquete se pueden poner a disposición del paquete llamado usando el tipo de configuración de variable de paquete primario. Para más información, consulte [Package Configurations](../integration-services/packages/package-configurations.md).  
  
**IncludeInDebugDump**  
 Indica si el valor variable está incluido en los archivos de volcado de depuración.  
  
 Para las variables definidas por el usuario y las variables del sistema, el valor predeterminado de la opción **InclueInDebugDump** es **true**.  
  
 Pero para las variables definidas por el usuario, el sistema restablece la opción **IncludeInDebugDump** en **false** cuando se cumplen las condiciones siguientes:  
  
-   Si la propiedad de variable **EvaluateAsExpression** está establecida en **true**, el sistema restablece la opción **IncludeInDebugDump** en **false**.  
  
     Para incluir el texto de la expresión como el valor de la variable en los archivos de volcado de depuración, establezca la opción **IncludeInDebugDump** en **true**.  
  
-   Si el tipo de datos de la variable se cambia a una cadena, el sistema restablece la opción **IncludeInDebugDump** en **false**.  
  
 Cuando el sistema restablece la opción **IncludeInDebugDump** en **false**, podría invalidarse el valor seleccionado por el usuario.  
  
**Value**    
El valor de una variable definida por el usuario puede ser un literal o una expresión. El valor de una variable no puede ser null. Las variables tienen los siguientes valores predeterminados:

| Tipo de datos | Valor predeterminado |
|---|---|
| Boolean | False |
| Tipos de datos numeric y binary | 0 (cero) |
| Tipos de datos char y string | (cadena vacía) |
| Objeto | System.Object |
| | |

Una variable tiene opciones para establecer el valor de la variable y el tipo de datos del valor. Las dos propiedades deben ser compatibles: por ejemplo, el uso de un valor de cadena junto con el tipo de datos de número entero no es válido.  
  
 Si la variable está configurada para evaluarse como una expresión, se debe proporcionar una expresión. En el tiempo de ejecución, se evalúa la expresión, y se establece la variable con el resultado de la evaluación. Por ejemplo, si una variable usa la expresión `DATEPART("month", GETDATE())` , el valor de la variable es el equivalente numérico del mes de la fecha actual. La expresión debe ser una expresión válida que use la sintaxis de gramática de expresiones de [!INCLUDE[ssIS](../includes/ssis-md.md)] . Cuando una expresión se usa con variables, la expresión puede usar literales y los operadores y funciones que proporciona la gramática de la expresión, pero la expresión no puede hacer referencia a las columnas desde un flujo de datos en el paquete. La longitud máxima de una expresión es 4000 caracteres. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
**ValueType**    
 > [!NOTE]  
>  El valor de la propiedad aparece en la columna **Tipo de datos** en la ventana **Variables** .  
  
 Especifica el tipo de datos del valor de la variable.  

## <a name="scenarios-for-using-variables"></a>Escenarios de utilización de variables  
 Las variables se usan de muchas formas distintas en los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Es probable que observe que el desarrollo de un paquete no avanza mucho antes de que tenga que agregar al paquete una variable definida por el usuario para lograr la flexibilidad y facilidad de uso que requiere la solución. Según el escenario de que se trate, las variables del sistema también se usan a menudo.  
  
 **Expresiones de propiedad** Use variables para proporcionar valores en las expresiones de propiedad que definen las propiedades de los paquetes y los objetos de paquete. Por ejemplo, la expresión `SELECT * FROM @varTableName` contiene la variable `varTableName` , que actualiza la instrucción SQL ejecutada por la tarea Ejecutar SQL. La expresión `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`actualiza el paquete ejecutado por la tarea Ejecutar paquete, mediante la ejecución del paquete especificado en la variable `varPackageFirst` el primer día de cada mes y la ejecución del paquete especificado en la variable `varPackageOther` los demás días. Para obtener más información, vea [Usar expresiones de propiedad en paquetes](../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 **Expresiones de flujo de datos** Use variables para proporcionar los valores de las expresiones utilizadas por las transformaciones Columna derivada y División condicional para llenar columnas o dirigir filas de datos a distintas salidas de transformación. Por ejemplo, la expresión `@varSalutation + LastName`concatena el valor de la variable `VarSalutation` y el de la columna `LastName` . La expresión `Income < @HighIncome`dirige a un resultado las filas de datos cuyo valor de la columna `Income` es menor que el valor de la variable `HighIncome` . Para obtener más información, vea [Transformación Columna derivada](../integration-services/data-flow/transformations/derived-column-transformation.md), [Transformación División condicional](../integration-services/data-flow/transformations/conditional-split-transformation.md) y [Expresiones de Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 **Expresiones de restricción de precedencia** Se deben proporcionar valores para su uso en restricciones de precedencia para determinar si se ejecuta el ejecutable restringido. Las expresiones se pueden usar con un resultado de la ejecución (satisfactoria, errónea, terminada), o en lugar de un resultado de la ejecución. Por ejemplo, si la expresión `@varMax > @varMin`se evalúa como **true**, se ejecuta el ejecutable. Para obtener más información, vea [Agregar expresiones a las restricciones de precedencia](http://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1).  
  
 **Parámetros y códigos de retorno** Se deben proporcionar valores para los parámetros de entrada, o almacenar los valores de los parámetros de salida y los códigos de retorno. Para ello, se asignan las variables a los parámetros y códigos de retorno. Por ejemplo, si se establece la variable `varProductId` en 23 y se ejecuta la instrucción SQL `SELECT * from Production.Product WHERE ProductID = ?`, la consulta recupera el producto cuyo `ProductID` sea 23. Para obtener más información, vea [Tarea Ejecutar SQL](../integration-services/control-flow/execute-sql-task.md) y [Parámetros y códigos de retorno en la tarea Ejecutar SQL](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).  
  
 **Expresiones del bucle For** Se deben proporcionar valores para su uso en las expresiones de inicialización, evaluación y asignación del bucle For. Por ejemplo, si la variable `varCount` es 2 y `varMaxCount` es 10, la expresión de inicialización es `@varCount`, la expresión de evaluación es  `@varCount < @varMaxCount`y la expresión de asignación es `@varCount =@varCount +1`, el bucle se repite 8 veces. Para más información, consulte [For Loop Container](../integration-services/control-flow/for-loop-container.md).  
  
 **Configuraciones de variables de paquete primario** Los valores de los paquetes primarios se deben pasar a los paquetes secundarios. Los paquetes secundarios pueden tener acceso a las variables del paquete primario utilizando configuraciones de variables de paquete primario. Por ejemplo, si el paquete secundario debe usar los mismos datos que el paquete primario, el secundario puede definir una configuración de variables de paquete primario que especifique una variable establecida por la función GETDATE en el paquete primario. Para obtener más información, consulte [Execute Package Task](../integration-services/control-flow/execute-package-task.md) y [Package Configurations](../integration-services/packages/package-configurations.md).  
  
 **Tarea Script y componente de script** Se debe proporcionar a la tarea Script o al componente de script una lista de variables de solo lectura o lectura/escritura, actualizar las variables de lectura/escritura del script y, después, usar los valores actualizados dentro o fuera del script. Por ejemplo, en el código `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`, la variable de script `numberOfCars` se actualiza con el valor de la variable `NumberOfCars`. Para más información, consulte [Using Variables in the Script Task](../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md).  

## <a name="add-a-variable"></a>Agregar una variable  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] con el que desea trabajar.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , siga uno de estos procedimientos para definir el ámbito de la variable:  
  
    -   Para establecer el ámbito en el paquete, haga clic en cualquier lugar de la superficie de diseño de la pestaña **Flujo de control** .  
  
    -   Para establecer el ámbito en un controlador de eventos, seleccione un ejecutable y un controlador de eventos en la superficie de diseño de la pestaña **Controlador de eventos** .  
  
    -   Para establecer el ámbito en una tarea o un contenedor, en la superficie de diseño de la pestaña **Flujo de control** o **Controlador de eventos** , haga clic en una tarea o un contenedor.  
  
4.  En el menú **SSIS** , haga clic en **Variables**. También puede ver la ventana **Variables** si asigna el comando View.Variables a una combinación de teclas que desee en la página **Teclado** del cuadro de diálogo **Opciones** .  
  
5.  En la ventana **Variables** , haga clic en el icono **Agregar variable** . Se agregará la nueva variable a la lista.  
  
6.  Opcionalmente, haga clic en el icono **Opciones de cuadrícula** , seleccione las columnas adicionales que desee mostrar en el cuadro de diálogo **Opciones de cuadrícula de variables** y haga clic en **Aceptar**.  
  
7.  O bien, establezca las propiedades de una variable. Para obtener más información, vea [Establecer las propiedades de una variable definida por el usuario](http://msdn.microsoft.com/library/f98ddbec-f668-4dba-a768-44ac3ae0536f).  
  
8.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  

### <a name="add-variable-dialog-box"></a>Agregar variable, cuadro de diálogo
Utilice el cuadro de diálogo **Agregar variable** para especificar las propiedades de una nueva variable.  
  
#### <a name="options"></a>Opciones  
 **Contenedor**  
 Seleccione un contenedor de la lista. El contenedor define el ámbito de la variable. El contenedor puede ser el paquete o un ejecutable del mismo.  
  
 **Nombre**  
 Escriba el nombre de la variable.  
  
 **Espacio de nombres**  
 Especifique el espacio de nombres de la variable. De forma predeterminada, las variables definidas por el usuario se encuentran en el espacio de nombres **Usuario** .  
  
 **Tipo de valor**  
 Seleccione un tipo de datos.  
  
 **Value**  
 Escriba un valor. El valor debe ser compatible con el tipo de datos especificado en la opción **Tipo de valor** .  
  
 **Solo lectura**  
 Seleccione esta opción para cambiar la variable a solo lectura.  
   
## <a name="delete-a-variable"></a>Eliminación de una variable  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga clic con el botón secundario en el paquete para abrirlo.  
  
3.  En el menú **SSIS** , haga clic en **Variables**. También puede ver la ventana **Variables** si asigna el comando View.Variables a una combinación de teclas que desee en la página **Teclado** del cuadro de diálogo **Opciones** .  
  
4.  Seleccione la variable que desee eliminar y haga clic en **Eliminar variable**.  
  
     Si no ve la variable en la ventana Variables, haga clic en **Opciones de cuadrícula** y seleccione **Mostrar variables de todos los ámbitos**.  
  
5.  Si se abre el cuadro de diálogo **Confirmar eliminación de variables** , haga clic en **Sí** para confirmar.  
  
6.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="change-the-scope-of-a-variable"></a>Cambio del ámbito de una variable  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga clic con el botón secundario en el paquete para abrirlo.  
  
3.  En el menú **SSIS** , haga clic en **Variables**. También puede ver la ventana **Variables** si asigna el comando View.Variables a una combinación de teclas que desee en la página **Teclado** del cuadro de diálogo **Opciones** .  
  
4.  Seleccione la variable y haga clic en **Mover variable**.  
  
     Si no ve la variable en la ventana Variables, haga clic en **Opciones de cuadrícula** y seleccione **Mostrar variables de todos los ámbitos**.  
  
5.  En el cuadro de diálogo **Seleccionar nuevo ámbito** , seleccione el paquete o un contenedor, una tarea o un controlador de eventos en el paquete, para cambiar el ámbito de la variable.  
  
6.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  

## <a name="set-the-properties-of-a-user-defined-variable"></a>Establecer las propiedades de una variable definida por el usuario
 Para establecer las propiedades de una variable definida por el usuario en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], puede utilizar una de las características siguientes:  
  
-   Ventana Variables.  
  
-   Ventana Propiedades. En la ventana **Propiedades** se muestra una lista de propiedades para configurar variables que no están disponibles en la ventana **Variables** : Description, EvaluateAsExpression, Expression, ReadOnly, ValueType yIncludeInDebugDump.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] también proporciona un conjunto de variables del sistema cuyas propiedades no se pueden actualizar, excepto la propiedad de RaiseChangedEvent.  
  
### <a name="set-expressions-on-variables"></a>Establecimiento de las expresiones de valor en variables  
  
 Cuando se usa la ventana **Propiedades** para establecer expresiones en una variable definida por el usuario:  
  
-   El valor de una variable se puede establecer por las propiedades Value o Expression. De forma predeterminada, la propiedad EvaluateAsExpression se establece en **False** y la propiedad Value establece el valor de la variable. Para usar una expresión para establecer el valor, primero necesita establecer EvaluateAsExpression en **True**y, después, proporcionar una expresión en la propiedad Expression. La propiedad Value se establece automáticamente en el resultado de la evaluación de la expresión.  
  
-   La propiedad ValueType contiene el tipo de datos del valor de la propiedad Value. Si Value se establece con una expresión, ValueType se actualiza automáticamente a un tipo de datos compatible con el resultado de la evaluación de la expresión. Por ejemplo, si Value contiene 0 y la propiedad ValueType contiene **Int32** y, después, establece Expression en GETDATE(), Value contendrá la fecha y hora actuales y ValueType se establecerá en **DateTime**.  
  
-   La ventana **Propiedades** de la variable proporciona acceso al cuadro de diálogo **Generador de expresiones** . Esta herramienta se puede usar para generar, validar y evaluar expresiones. Para más información, vea [Generador de expresiones](../integration-services/expressions/expression-builder.md) y [Expresiones de Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 Cuando se usa la ventana **Variables** para establecer expresiones en una variable definida por el usuario:  
  
-   Para usar una expresión para establecer el valor de la variable, primero confirme que el tipo de datos variant es compatible con el resultado de la evaluación de la expresión y después escriba una expresión en la columna **Expresión** de la ventana **Variables** . La propiedad EvaluateAsExpression de la ventana **Propiedades** se establece automáticamente en **True**.  
  
-   Cuando asigne una expresión a una variable, un marcador especial de icono se muestra junto a la variable. Este marcador de icono especial también aparece junto a los administradores de conexiones y las tareas con expresiones establecidas.  
  
-   La ventana **Variables** de la variable proporciona acceso al cuadro de diálogo **Generador de expresiones** . Esta herramienta se puede usar para generar, validar y evaluar expresiones. Para más información, vea [Generador de expresiones](../integration-services/expressions/expression-builder.md) y [Expresiones de Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 En **Variables** y la ventana de **Propiedades** , si asigna una expresión a la variable y **EvaluateAsExpression** se establece en **True**, no puede cambiar el tipo de datos variant.  
  
### <a name="set-the-namespace-and-name-properties"></a>Establecimiento de las propiedades Namespace y Name
  
 Los valores de las propiedades **Nombre** y **Espacio de nombres** deben empezar con una letra, como se define en el Estándar Unicode 2.0, o un carácter de subrayado (_). Los caracteres siguientes pueden ser letras o números, tal como se define en el Estándar Unicode 2.0, o el carácter de subrayado (\_).  
  
### <a name="set-variable-properties-in-the-variables-window"></a>Establecimiento de las propiedades de variables en la ventana Variables   
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga clic con el botón secundario en el paquete para abrirlo.  
  
3.  En el menú **SSIS** , haga clic en **Variables**.  
  
     También puede ver la ventana **Variables** si asigna el comando View.Variables a una combinación de teclas que desee en la página **Teclado** del cuadro de diálogo **Opciones** .  
  
4.  Opcionalmente, haga clic en **Opciones de cuadrícula** de la ventana **Variables**, seleccione las columnas que aparecen en la ventana **Variables** y seleccione filtros para aplicarlos a la lista de variables.  
  
5.  Seleccione la variable de la lista y actualice los valores en las columnas **Nombre**, **Tipo de datos**, **Valor**, **Espacio de nombres**, **Generar evento de cambios**, **Descripción** y **Expresión** .  
  
6.  Seleccione la variable en la lista y haga clic en **Mover variable** para cambiar el ámbito.  
  
7.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  
  
### <a name="set-variable-properties-in-the-properties-window"></a>Establecimiento de las propiedades de variables en la ventana Propiedades  

1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga clic con el botón secundario en el paquete para abrirlo.  
  
3.  En el menú **Ver** , haga clic en **Ventana de propiedades**.  
  
4.  En el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en la pestaña **Explorador de paquetes** y expanda el nodo Paquete.  
  
5.  Para modificar variables en el ámbito de paquete, expanda el nodo Variables; también puede expandir los nodos Controladores de eventos o Ejecutables hasta localizar el nodo Variables que contiene la variable que desea modificar.  
  
6.  Haga clic en la variable cuyas propiedades desee modificar.  
  
7.  En la ventana **Propiedades** , actualice las propiedades de la variable de lectura y escritura. Algunas propiedades son solo de lectura/escritura para las variables definidas por el usuario.  
  
     Para más información sobre las propiedades, vea [Integration Services &#40;SSIS&#41; Variables](../integration-services/integration-services-ssis-variables.md).  
  
8.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  

## <a name="update-a-variable-dynamically-with-configurations"></a>Actualización dinámica de una variable mediante configuraciones  
 Para actualizar dinámicamente las variables, puede crear configuraciones para las variables, implementar las configuraciones con el paquete y después, actualizar los valores de las variables en el archivo de configuración al implementar los paquetes. El paquete utiliza los valores actualizados de las variables en tiempo de ejecución. Para obtener más información, vea [Crear configuraciones de paquetes](../integration-services/packages/create-package-configurations.md).  

## <a name="related-tasks"></a>Related Tasks  
 [Usar los valores de variables y parámetros en un paquete secundario](../integration-services/packages/legacy-package-deployment-ssis.md#child)  
  
 [Asignar parámetros de consulta a variables en un componente de flujo de datos](../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
