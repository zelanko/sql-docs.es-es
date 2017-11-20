---
title: Usar expresiones de propiedad en paquetes | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- packages [Integration Services], expressions
- Integration Services packages, expressions
- SQL Server Integration Services packages, expressions
- dynamic properties
- updating package properties
- SSIS packages, expressions
- expressions [Integration Services], property expressions
- property expressions [Integration Services]
ms.assetid: a4bfc925-3ef6-431e-b1dd-7e0023d3a92d
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7f1a931e20a1ab0bafae0e014b174cf718e9a69f
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="use-property-expressions-in-packages"></a>Usar expresiones de propiedad en paquetes
  Una expresión de propiedad es una expresión asignada a una propiedad para permitir la actualización dinámica de la propiedad en tiempo de ejecución. Por ejemplo, una expresión de propiedad puede actualizar la línea Para que utiliza una tarea Enviar correo, insertando una dirección de correo electrónico almacenada en una variable.  
  
 Se puede agregar una expresión a un paquete, tarea, bucle ForEach, bucle For, secuencia, enumerador ForEach, controlador de eventos, administrador de conexiones de paquetes o proyectos, o proveedor de registro. Cualquier propiedad de estos objetos que sea de lectura/escritura puede implementa una expresión de propiedad. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] también admite el uso de expresiones de propiedad en algunas propiedades personalizadas de los componentes de flujo de datos. Las variables y restricciones de precedencia no admiten expresiones de propiedad, pero incluyen propiedades especiales en las que puede utilizar expresiones.  
  
 Las expresiones de propiedad se pueden actualizar de diferentes maneras:  
  
-   Las variables definidas por el usuario se pueden incluir en configuraciones de paquetes y actualizar al implementar el paquete. Durante la ejecución, la expresión de propiedad se evalúa con el valor actualizado de la variable.  
  
-   Las variables del sistema incluidas en expresiones se actualizan en tiempo de ejecución y esto cambia los resultados de la evaluación de la propiedad.  
  
-   Las funciones de fecha y hora se evalúan en tiempo de ejecución y proporcionan los valores actualizados para las expresiones de propiedad.  
  
-   Los scripts ejecutados por la tarea Script y el componente de script pueden actualizar las variables de las expresiones.  
  
 Las expresiones se generan con el lenguaje de expresiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Las expresiones pueden utilizar variables del sistema o definidas por el usuario, junto con los operadores, funciones y conversiones de tipo que proporciona el lenguaje de expresiones.  
  
> [!NOTE]  
>  Los nombres están definidos por el usuario y las variables del sistema distinguen mayúsculas y minúsculas.  
  
 Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 Un uso importante de las expresiones de propiedad es para personalizar las configuraciones de cada instancia implementada de un paquete. Esto permite actualizar de forma dinámica las propiedades del paquete para diferentes entornos. Por ejemplo, puede crear una expresión de propiedad que asigne una variable a la cadena de conexión de un administrador de conexiones y, después, actualizar la variable cuando se implemente el paquete, asegurándose de que la cadena de conexión sea correcta en tiempo de ejecución. Las configuraciones de paquetes se cargan antes de evaluar las expresiones de propiedad.  
  
 Una propiedad solo puede utilizar una expresión de propiedad, y una expresión de propiedad solo se puede aplicar a una propiedad. Sin embargo, puede generar varias expresiones de propiedad idénticas y asignarlas a diferentes propiedades.  
  
 Algunas propiedades se establecen mediante el uso de valores provenientes de enumeradores. Cuando hace referencia al miembro enumerador en una expresión de propiedad, debe utilizar el valor numérico equivalente al nombre descriptivo del miembro enumerador. Por ejemplo, si una expresión de propiedad establece la propiedad **LoggingMode** , que utiliza un valor de la enumeración **DTSLoggingMode** , la expresión de propiedad debe utilizar 0, 1 o 2 en lugar de los nombres descriptivos **Enabled**, **Disabled**o **UseParentSetting**. Para más información, vea [Constantes enumeradas en expresiones de propiedad](../../integration-services/expressions/enumerated-constants-in-property-expressions.md).  
  
## <a name="property-expression-user-interface"></a>Interfaz de usuario de las expresiones de propiedad  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona un conjunto de herramientas para generar y administrar expresiones de propiedad.  
  
-   La página **Expresiones** , que se encuentra en los editores personalizados de tareas, el contenedor de bucles For y los contenedores ForEach. La página **Expresiones** permite modificar expresiones y ver una lista de las expresiones de propiedad que utiliza una tarea, un bucle ForEach o un bucle For.  
  
-   La ventana **Propiedades** , para modificar expresiones y ver una lista de las expresiones de propiedad que utilizadas por un paquete o por los objetos de un paquete.  
  
-   El cuadro de diálogo **Editor de expresiones de propiedad** , para crear, actualizar y eliminar expresiones de propiedad.  
  
-   El cuadro de diálogo **Generador de expresiones** , para crear una expresión con las herramientas gráficas. En el cuadro de diálogo **Generador de expresiones** se pueden evaluar expresiones para que las revise, sin asignar el resultado de la evaluación a la propiedad.  
  
 El diagrama siguiente muestra las interfaces de usuario que sirven para agregar, cambiar y quitar expresiones de propiedad.  
  
 ![La interfaz de usuario para las expresiones de propiedad](../../integration-services/expressions/media/ssis-propertyexpressionui.gif "la interfaz de usuario para las expresiones de propiedad")  
  
 En la ventana **Propiedades** y en la página **Expresiones** , haga clic en el botón Examinar **(…)** en el nivel de la colección de **Expresiones** para abrir el cuadro de diálogo **Editor de expresiones de propiedad** . El Editor de expresiones de propiedad le permite asignar una propiedad a una expresión y escribir una expresión de propiedad. Si quiere usar las herramientas gráficas de expresiones para crear y validar la expresión, haga clic en el botón Examinar **(…)** en el nivel de expresión para abrir el cuadro de diálogo **Generador de expresiones** y, después, cree o modifique la expresión (y, de manera opcional, valídela).  
  
 También puede abrir el cuadro de diálogo **Generador de expresiones** desde el cuadro de diálogo **Editor de expresiones de propiedad** .  
  
#### <a name="to-work-with-property-expressions"></a>Para trabajar con expresiones de propiedad  
  
-   [Agregar o cambiar una expresión de propiedad](../../integration-services/expressions/add-or-change-a-property-expression.md)  
  
### <a name="setting-property-expressions-of-data-flow-components"></a>Establecer expresiones de propiedad de componentes de flujo de datos  
 Si genera un paquete en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], las propiedades de los componentes de flujo de datos que admiten expresiones de propiedad se muestran en la tarea Flujo de datos a la que pertenecen. Para agregar, cambiar y quitar las expresiones de propiedad de componentes de flujo de datos, haga clic con el botón derecho en la tarea Flujo de datos del flujo de datos al que pertenecen los componentes de flujo de datos y haga clic en **Propiedades**. La ventana Propiedades enumera las propiedades de los componentes de flujo de datos con los que puede utilizar expresiones de propiedad. Por ejemplo, para crear o modificar una expresión de propiedad para la propiedad SamplingValue de una transformación Muestreo de fila en un flujo de datos denominado SampleCustomer, haga clic con el botón derecho en la tarea Flujo de datos del flujo de datos al que pertenece la transformación Muestreo de fila y haga clic en **Propiedades**. La propiedad SamplingValue se muestra en la ventana Propiedades y tiene el formato [SampleCustomer].[SamplingValue].  
  
 En la ventana Propiedades, puede agregar, cambiar y quitar expresiones de propiedad para componentes de flujo de datos de la misma manera que las expresiones de propiedad para otros tipos de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . La ventana Propiedades también proporciona acceso a varios cuadros de diálogo y generadores que sirven para agregar, cambiar o quitar expresiones de propiedad para componentes de flujo de datos. Para obtener más información sobre las propiedades de componentes de flujo de datos que se pueden actualizar a través de expresiones de propiedad, vea [Transformation Custom Properties](../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
## <a name="loading-property-expressions"></a>Cargar expresiones de propiedad  
 No se puede especificar ni controlar el momento en que se cargan las expresiones. Las expresiones de propiedad se evalúan y cargan cuando se validan el paquete y los objetos de paquete. La validación se produce cuando se guarda el paquete, se abre en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] y se ejecuta.  
  
 Por lo tanto, no verá los valores actualizados de las propiedades de los objetos de paquete que utilizan expresiones de propiedad en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] hasta que guarde el paquete, lo ejecute o lo vuelva a abrir después de agregarle las expresiones de propiedad.  
  
 Las expresiones de propiedad asociadas con los diferentes tipos de objetos (administradores de conexión, proveedores de registro y enumeradores) también se cargan cuando se llama a métodos específicos para ese tipo de objeto. Por ejemplo, las propiedades de administradores de conexión se cargan antes de que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una instancia de la conexión.  
  
 Las expresiones de propiedad se cargan una vez que se han cargado las configuraciones de paquete. Por ejemplo, las variables se actualizan primero con sus configuraciones, y luego se evalúan y cargan las expresiones de propiedad que utilizan las variables. Esto significa que las expresiones de propiedad siempre utilizan los valores de variables establecidas con configuraciones.  
  
> [!NOTE]  
>  No se puede usar la opción **Set** de la utilidad **dtexec** para rellenar una expresión de propiedad.  
  
 La tabla siguiente resume cuándo se evalúan y cargan las expresiones de propiedad de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
|Tipo de objeto|Carga y evaluación|  
|-----------------|-----------------------|  
|Paquete, bucle Foreach, bucle For, secuencia, tareas y componentes de flujo de datos|Tras la carga de configuraciones<br /><br /> Antes de la validación<br /><br /> Antes de la ejecución|  
|Administradores de conexión|Tras la carga de configuraciones<br /><br /> Antes de la validación<br /><br /> Antes de la ejecución<br /><br /> Antes de la creación de una instancia de conexión|  
|Proveedores de registro|Tras la carga de configuraciones<br /><br /> Antes de la validación<br /><br /> Antes de la ejecución<br /><br /> Antes de la apertura de registros|  
|Enumeradores Foreach|Tras la carga de configuraciones<br /><br /> Antes de la validación<br /><br /> Antes de la ejecución<br /><br /> Antes de cada enumeración del bucle|  
  
## <a name="using-property-expressions-in-the-foreach-loop"></a>Usar expresiones de propiedad en el bucle Foreach  
 A menudo, es útil implementar una expresión de propiedad para establecer el valor de la propiedad **ConnectionString** de los administradores de conexión que se utilizan dentro del contenedor de bucles Foreach. Después de que el enumerador asigne su valor actual a una variable en cada iteración del bucle, la expresión de propiedad puede usar el valor de esa variable para actualizar el valor de la propiedad **ConnectionString** de forma dinámica.  
  
 Si desea utilizar expresiones de propiedad con la propiedad **ConnectionString** de administradores de conexión de archivos, varios archivos, archivos planos y varios archivos planos que utiliza un bucle Foreach, deberá tener en cuenta varios aspectos. Un paquete se puede configurar para ejecutar varios ejecutables de manera simultánea si se establece la propiedad **MaxConcurrentExecutables** en un valor mayor que 1 o en el valor -1. El valor de -1 permite que el número máximo de ejecutables en ejecución simultánea sea igual al número de procesadores más dos. Para evitar las consecuencias negativas de la ejecución paralela de ejecutables, el valor de **MaxConcurrentExecutables** se debe establecer en 1. Si **MaxConcurrentExecutables** no se establece en 1, el valor de la propiedad **ConnectionString** no se puede garantizar y se pueden obtener resultados impredecibles.  
  
 Por ejemplo, suponga que un bucle Foreach que enumera los archivos de una carpeta recupera los nombres de archivo y luego utiliza la tarea Ejecutar SQL para insertar cada nombre de archivo en una tabla. Si **MaxConcurrentExecutables** no se establece en 1, es posible que se produzcan conflictos de escritura si dos instancias de la tarea Ejecutar SQL intentan escribir en la tabla al mismo tiempo.  
  
## <a name="sample-property-expressions"></a>Ejemplo de expresiones de propiedad  
 En las siguientes expresiones de ejemplo se muestra cómo utilizar variables del sistema, operadores, funciones y literales de cadena en las expresiones de propiedad.  
  
### <a name="property-expression-for-the-loggingmode-property-of-a-package"></a>Expresión de propiedad para la propiedad LoggingMode de un paquete  
 Se puede usar la siguiente expresión de propiedad para establecer la propiedad LoggingMode de un paquete. La expresión utiliza las funciones DAY y GETDATE para obtener un entero que representa la parte de la fecha correspondiente al día de la fecha. Si el día es el 1 o el 15, se habilita el registro; de lo contrario, el registro se deshabilita. El valor 1 es el entero equivalente del miembro **Enabled**del enumerador LoggingMode, mientras que el valor 2 es el entero equivalente del miembro **Disabled**. Debe utilizar el valor numérico en lugar del nombre del miembro enumerador en la expresión.  
  
 `DAY((DT_DBTIMESTAMP)GETDATE())==1||DAY((DT_DBTIMESTAMP)GETDATE())==15?1:2`  
  
### <a name="property-expression-for-the-subject-of-an-e-mail-message"></a>Expresión de propiedad para el asunto de un mensaje de correo electrónico  
 Se puede usar la siguiente expresión de propiedad para establecer la propiedad Subject de una tarea Enviar correo y proporcionar un asunto de correo electrónico útil. La expresión utiliza una combinación de literales de cadena, variables del sistema, operadores de concatenación (+) y conversión, y las funciones DATEDIFF y GETDATE. Las variables del sistema son las variables `PackageName` y `StartTime` .  
  
 `"PExpression-->Package: (" + @[System::PackageName] + ") Started:"+  (DT_WSTR, 30) @[System::StartTime] + " Duration:"  +  (DT_WSTR,10) (DATEDIFF( "ss", @[System::StartTime] , GETDATE()  )) + " seconds"`  
  
 Si el nombre del paquete es EmailRowCountPP, se ejecutó el 4 de marzo de 2005 y la duración de la ejecución fue de 9 segundos, la expresión se evalúa como la cadena siguiente.  
  
 PExpression-->Package: (EmailRowCountPP) Started:3/4/2005 11:06:18 AM Duration:9 seconds.  
  
### <a name="property-expression-for-the-message-of-an-e-mail-message"></a>Expresión de propiedad para el cuerpo de un mensaje de correo electrónico  
 Se puede usar la siguiente expresión de propiedad para establecer la propiedad MessageSource de una tarea Enviar correo. La expresión utiliza una combinación de literales de cadena, variables definidas por el usuario y el operador de concatenación (+). Las variables definidas por el usuario se denominan `nasdaqrawrows`, `nyserawrows`y `amexrawrows`. La cadena "\n" indica un retorno de carro.  
  
 `"Rows Processed: "  +   "\n" +"   NASDAQ: "  +   (dt_wstr,9)@[nasdaqrawrows]   + "\n" + "   NYSE: "  +  (dt_wstr,9)@[nyserawrows]  + "\n" + "   Amex: "  +  (dt_wstr,9)@[amexrawrows]`  
  
 Si `nasdaqrawrows` es 7058, `nyserawrows` es 3528 y `amexrawrows` es 1102, la expresión se evalúa como la cadena siguiente.  
  
 Rows Processed:  
  
 NASDAQ: 7058  
  
 NYSE: 3528  
  
 AMEX: 1102  
  
### <a name="property-expression-for-the-executable-property-of-an-execute-process-task"></a>Expresión de propiedad para la propiedad Ejecutable de una tarea Ejecutar proceso  
 Se puede usar la siguiente expresión de propiedad para establecer la propiedad Executable de una tarea Ejecutar proceso. La expresión utiliza una combinación de literales de cadena, operadores y funciones. La expresión utiliza las funciones DATEPART y GETDATE y el operador condicional.  
  
 `DATEPART("weekday", GETDATE()) ==2?"notepad.exe":"mspaint.exe"`  
  
 Si es el segundo día de la semana, la tarea Ejecutar proceso ejecuta notepad.exe, de lo contrario, ejecuta mspaint.exe.  
  
### <a name="property-expression-for-the-connectionstring-property-of-a-flat-file-connection-manager"></a>Expresión de propiedad para la propiedad ConnectionString de un administrador de conexiones de archivos planos  
 Se puede usar la siguiente expresión de propiedad para establecer la propiedad ConnectionString de un administrador de conexiones de archivos planos. La expresión utiliza una sola variable definida por el usuario, `myfilenamefull`, que contiene la ruta de acceso a un archivo de texto.  
  
 `@[User::myfilenamefull]`  
  
> [!NOTE]  
>  Solo se puede tener acceso a las expresiones de propiedad para los administradores de conexión a través de la ventana Propiedades. Para ver las propiedades de un administrador de conexiones, seleccione el administrador de conexiones en el área **Administradores de conexiones** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] cuando la ventana Propiedades esté abierta, o bien haga clic con el botón derecho en el administrador de conexiones y seleccione **Propiedades**.  
  
### <a name="property-expression-for-the-configstring-property-of-a-text-file-log-provider"></a>Expresión de propiedad para la propiedad ConfigString de un proveedor de registro de archivos de texto  
 Se puede usar la siguiente expresión de propiedad para establecer la propiedad ConfigString de un proveedor de registro de archivos de texto. La expresión usa una sola variable definida por el usuario, `varConfigString`, que contiene el nombre del administrador de conexiones de archivos que se va a usar. El administrador de conexiones de archivos especifica la ruta de acceso del archivo de texto en el que se escriben las entradas del registro.  
  
 `@[User::varConfigString]`  
  
> [!NOTE]  
>  Solo se puede tener acceso a las expresiones de propiedad para los administradores de registro a través de la ventana Propiedades. Para ver las propiedades de un proveedor de registro, seleccione el proveedor de registro en la pestaña **Explorador de paquetes** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] cuando la ventana Propiedades esté abierta, o bien haga clic con el botón derecho en el proveedor de registro (en el Explorador de paquetes) y haga clic en **Propiedades**.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   [Marcador de resaltado de expresión y configuración (proyecto de CodePlex)](http://go.microsoft.com/fwlink/?LinkId=146625)  
  
-   Artículo técnico, sobre [ejemplos de expresiones SSIS](http://go.microsoft.com/fwlink/?LinkId=220761), en social.technet.microsoft.com  
  
## <a name="see-also"></a>Vea también  
 [Usar variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  

