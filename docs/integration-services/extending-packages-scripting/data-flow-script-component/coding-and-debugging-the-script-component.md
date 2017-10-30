---
title: Codificar y depurar el componente de Script | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, development environment
- Script component [Integration Services], debugging
- Script component [Integration Services], coding
- SSIS Script component, debugging
- Script component [Integration Services], development environment
- debugging [Integration Services], scripts
- SSIS Script component, coding
- VSTA
ms.assetid: c3913c15-66aa-4b61-89b5-68488fa5f0a4
caps.latest.revision: 66
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ff6c9814547a83439717f8a88d3bd52be80c4ca5
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="coding-and-debugging-the-script-component"></a>Codificar y depurar el componente de script
  En el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)], el componente Script tiene dos modos: modo de diseño de metadatos y modo de diseño de código. Cuando se abre la **Editor de transformación Script**, el componente entra en modo de diseño de metadatos, en el que se configuran metadatos y establecer las propiedades de componente. Después de haber establecido las propiedades del componente de script y configurar la entrada y las salidas en modo de diseño de metadatos, se puede cambiar al modo de diseño de código para escribir un script personalizado. Para obtener más información acerca del modo de diseño de metadatos y modo de diseño de código, vea [configurar el componente de Script en el Editor de componentes de secuencia de comandos](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
## <a name="writing-the-script-in-code-design-mode"></a>Escribir el script en modo de diseño de código  
  
### <a name="script-component-development-environment"></a>Entorno de desarrollo del componente de script  
 Para escribir la secuencia de comandos, haga clic en **editar Script** en el **Script** página de la **Editor de transformación Script** para abrir el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools para aplicaciones (VSTA) IDE. El IDE de VSTA incluye todas las características estándar del entorno de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] .NET, como el editor de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] con códigos de color, IntelliSense y el Explorador de objetos.  
  
 El código de script se escribe en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#. Especificar el lenguaje de script estableciendo la **ScriptLanguage** propiedad en el **Editor de transformación Script**. Si prefiere utilizar otro lenguaje de programación, puede desarrollar un ensamblado personalizado en el lenguaje seleccionado y utilizar su funcionalidad en el código del componente de script.  
  
 El script que crea en el componente de script se almacena en la definición de paquete. No hay un archivo de script independiente. Por consiguiente, el uso del componente de script no afecta a la implementación del paquete.  
  
> [!NOTE]  
>  Mientras diseña el paquete, el código de script se escribe temporalmente en un archivo de proyecto. Dado que almacenar información confidencial en un archivo es un riesgo de seguridad, se recomienda que no incluyen información confidencial como contraseñas en el código de script.  
  
 De forma predeterminada, **Option Strict** está deshabilitado en el IDE.  
  
### <a name="script-component-project-structure"></a>Estructura del proyecto del componente de script  
 La eficacia del componente de script reside en que puede generar código de infraestructura que reduce la cantidad de código que se debe escribir. Esta característica se basa en el hecho de que las entradas y salidas, y sus columnas y propiedades, son fijas y se conocen previamente. Por consiguiente, cualquier cambio subsiguiente que se realiza en los metadatos del componente puede invalidar el código que se ha escrito. Esto produce errores de compilación durante la ejecución del paquete.  
  
#### <a name="project-items-and-classes-in-the-script-component-project"></a>Elementos y clases de proyecto en el proyecto del componente de script  
 Cuando cambie al modo de diseño de código, el IDE de VSTA se abre y muestra el **ScriptMain** elemento de proyecto. El **ScriptMain** elemento de proyecto contiene el editable **ScriptMain** (clase), que actúa como la entrada de punto de la secuencia de comandos y que es donde se escribe el código. Los elementos de código de la clase varían, dependiendo del lenguaje de programación seleccionado para la tarea Script.  
  
 El proyecto de script contiene dos elementos de proyecto adicionales de solo lectura generados automáticamente:  
  
-   El **ComponentWrapper** elemento de proyecto contiene tres clases:  
  
    -   El **UserComponent** (clase), que se hereda de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> y contiene los métodos y propiedades que se va a usar para procesar los datos e interactuar con el paquete. El **ScriptMain** clase hereda de la **UserComponent** clase.  
  
    -   A **conexiones** clase de colección que contiene referencias a las conexiones seleccionadas en la página Administrador de conexiones del Editor de transformación de secuencia de comandos.  
  
    -   A **Variables** clase de colección que contiene referencias a las variables escritas en el **ReadOnlyVariable** y **ReadWriteVariables** propiedades en el **Script** página de la **Editor de transformación Script**.  
  
-   El **BufferWrapper** elemento de proyecto contiene una clase que hereda de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> para cada entrada y salida configurada en el **entradas y salidas** página de la **Editor de transformación Script**. Cada una de estas clases contiene las propiedades de descriptor de acceso con tipo, que corresponden a las columnas de entrada y salida configuradas, y los búferes de flujo de datos que contienen las columnas.  
  
 Para obtener información sobre cómo usar estos objetos, métodos y propiedades, vea [entender el modelo de objetos de componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md). Para obtener información sobre cómo usar los métodos y propiedades de estas clases en un determinado tipo de componente de Script, vea la sección [Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md). Los temas de ejemplo también contienen ejemplos de código completos.  
  
 Al configurar el componente de Script como una transformación, el **ScriptMain** elemento de proyecto contiene el siguiente código generado automáticamente. La plantilla de código también proporciona información general sobre el componente Script, así como información adicional sobre cómo recuperar y manipular objetos SSIS, como variables, eventos y conexiones.  
  
```vb  
' Microsoft SQL Server Integration Services Script Component  
' Write scripts using Microsoft Visual Basic 2008.  
' ScriptMain is the entry point class of the script.  
  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
<Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute> _  
<CLSCompliant(False)> _  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub PreExecute()  
        MyBase.PreExecute()  
        '  
        ' Add your code here for preprocessing or remove if not needed  
        '  
    End Sub  
  
    Public Overrides Sub PostExecute()  
        MyBase.PostExecute()  
        '  
        ' Add your code here for postprocessing or remove if not needed  
        ' You can set read/write variables here, for example:  
        ' Me.Variables.MyIntVar = 100  
        '  
    End Sub  
  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
        '  
        ' Add your code here  
        '  
    End Sub  
  
End Class  
```  
  
```csharp  
/* Microsoft SQL Server Integration Services user script component  
*  Write scripts using Microsoft Visual C# 2008.  
*  ScriptMain is the entry point class of the script.*/  
  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
[Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute]  
public class ScriptMain : UserComponent  
{  
  
    public override void PreExecute()  
    {  
        base.PreExecute();  
        /*  
          Add your code here for preprocessing or remove if not needed  
        */  
    }  
  
    public override void PostExecute()  
    {  
        base.PostExecute();  
        /*  
          Add your code here for postprocessing or remove if not needed  
          You can set read/write variables here, for example:  
          Variables.MyIntVar = 100  
        */  
    }  
  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
        /*  
          Add your code here  
        */  
    }  
  
}  
```  
  
#### <a name="additional-project-items-in-the-script-component-project"></a>Elementos de proyecto adicionales del proyecto del componente de script  
 El proyecto de componente de Script puede incluir elementos que no sea el valor predeterminado **ScriptMain** elemento. Puede agregar clases, módulos, archivos de código y carpetas al proyecto; además puede usar las carpetas para organizar los grupos de elementos.  
  
 Todos los elementos que se agregan se conservan dentro del paquete.  
  
#### <a name="references-in-the-script-component-project"></a>Referencias en el proyecto del componente de script  
 También puede agregar referencias a los ensamblados administrados haciendo clic en el proyecto de la tarea de secuencia de comandos en **el Explorador de proyectos**y, a continuación, haga clic en **Agregar referencia**. Para obtener más información, consulte [que hacen referencia a otros ensamblados en las soluciones de Scripting](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md).  
  
> [!NOTE]  
>  Puede ver las referencias del proyecto en el IDE de VSTA en **vista de clases** o en **el Explorador de proyectos**. Puede abrir cualquiera de estas ventanas en el **vista** menú. Puede agregar una nueva referencia de la **proyecto** menú, de **el Explorador de proyectos**, o de **vista de clases**.  
  
## <a name="interacting-with-the-package-in-the-script-component"></a>Interactuar con el paquete en el componente de script  
 El script personalizado que escribe en el componente de script puede obtener acceso y usar variables y administradores de conexión del paquete contenedor, a través de los descriptores de acceso con establecimiento inflexible de tipos en las clases base generadas automáticamente. Sin embargo, debe configurar tanto las variables como los administradores de conexión antes de escribir en modo de diseño de código, si desea que estén disponibles en su script. Puede también provocar eventos y realizar registros desde su código del componente de script.  
  
 Los elementos de proyecto generados automáticamente en el proyecto del componente de script, proporcionan los siguientes objetos, métodos y propiedades para que interactúen con el paquete.  
  
|Característica del paquete|Método de acceso|  
|---------------------|-------------------|  
|Variables|Utilizar las propiedades de descriptor de acceso con nombre y tipo de la **Variables** clase de colección en el **ComponentWrapper** elemento de proyecto, expuesta a través de la **Variables** propiedad de la **ScriptMain** clase.<br /><br /> El **PreExecute** método puede tener acceso a solo las variables de solo lectura. El **PostExecute** método puede tener acceso de solo lectura y las variables de lectura/escritura.|  
|Conexiones|Utilizar las propiedades de descriptor de acceso con nombre y tipo de la **conexiones** clase de colección en el **ComponentWrapper** elemento de proyecto, expuesta a través de la **conexiones** propiedad de la **ScriptMain** clase.|  
|Eventos|Generar eventos mediante el <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> propiedad de la **ScriptMain** clase y la **activan\<X >** métodos de la <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> interfaz.|  
|Registro|Realizar el registro mediante el uso de la <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> método de la **ScriptMain** clase.|  
  
## <a name="debugging-the-script-component"></a>Depurar el componente de script  
 Para depurar el código del componente Script, establezca al menos un punto de interrupción en el código y, a continuación, cierre el IDE de VSTA para ejecutar el paquete en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Cuando la ejecución del paquete entra en el componente Script, el IDE de VSTA se vuelve a abrir y muestra el código en modo de solo lectura. Después de que la ejecución llega al punto de interrupción, puede examinar los valores de variable y completar el código restante.  
  
> [!NOTE]  
>  No puede depurar un componente Script al ejecutar este último como parte de un paquete secundario que se ejecuta desde una tarea Ejecutar paquete. Los puntos de interrupción establecidos en el componente Script del paquete secundario se descartan en estas circunstancias. Puede depurar el paquete secundario ejecutándolo normalmente por separado.  
  
> [!NOTE]  
>  Al depurar un paquete que contiene varios componentes Script, el depurador depura un componente Script. El sistema puede depurar otro componente Script si el depurador se completa, como en el caso de un bucle Foreach o un contenedor de bucles For.  
  
 También puede supervisar la ejecución del componente Script con los métodos siguientes:  
  
-   Interrumpa la ejecución y mostrar un mensaje modal mediante el **MessageBox.Show** método en el **System.Windows.Forms** espacio de nombres. (Quite este código después de completar el proceso de depuración.)  
  
-   Provoque eventos para los mensajes informativos, advertencias y errores. Los métodos FireInformation, FireWarning y FireError mostrar la descripción del evento en Visual Studio **salida** ventana. Sin embargo, el método FireProgress, el Console.Write (método) y Console.WriteLine (método) no muestran toda la información en el **salida** ventana. Mensajes desde el evento FireProgress aparecen en la **progreso** ficha de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] diseñador. Para obtener más información, consulte [provocar eventos en el componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md).  
  
-   Registre eventos o mensajes definidos por el usuario para los proveedores de registro habilitados. Para obtener más información, consulte [el componente de Script de inicio de sesión](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md).  
  
 Si desea examinar la salida de un componente de Script configurado como origen o como una transformación, sin guardar los datos en un destino, puede detener el flujo de datos con un [transformación recuento de filas](../../../integration-services/data-flow/transformations/row-count-transformation.md) y adjuntar un visor de datos a la salida del componente de Script. Para obtener información acerca de los visores de datos, vea [Debugging Data Flow](../../../integration-services/troubleshooting/debugging-data-flow.md).  
  
## <a name="in-this-section"></a>En esta sección  
 Para obtener más información acerca de cómo codificar el componente de script, consulte los temas siguientes en esta sección.  
  
 [Descripción del modelo de objetos de componentes de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 Explica cómo usar los objetos, métodos y propiedades disponibles en el componente de script.  
  
 [Hacer referencia a otros ensamblados en soluciones de Scripting](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)  
 Explica cómo hacer referencia a los objetos de la biblioteca de clases [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] en el componente de script.  
  
 [Simular una salida de Error para el componente de Script](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 Explica cómo simular una salida de error en las filas que provocan errores durante el procesamiento por el componente de script.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [problemas de instalación y configuración de VSTA para las instalaciones de SSIS 2008 y R2](http://go.microsoft.com/fwlink/?LinkId=215661), en blogs.msdn.com.  
  
## <a name="see-also"></a>Vea también  
 [Configurar el componente de Script en el Editor de componentes de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
  
  

