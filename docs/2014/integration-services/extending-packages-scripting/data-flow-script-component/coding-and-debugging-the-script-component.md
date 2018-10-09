---
title: Programar y depurar el componente de script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c25b5b564f0fbe69d2559ae0c7c57d262c6646e0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177525"
---
# <a name="coding-and-debugging-the-script-component"></a>Codificar y depurar el componente de script
  En el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)], el componente Script tiene dos modos: modo de diseño de metadatos y modo de diseño de código. Al abrir el **Editor de transformación Script**, el componente escribe en modo de diseño de metadatos, en el que se configuran metadatos y se establecen las propiedades de componentes. Después de haber establecido las propiedades del componente de script y configurar la entrada y las salidas en modo de diseño de metadatos, se puede cambiar al modo de diseño de código para escribir un script personalizado. Para obtener más información acerca del modo de diseño de metadatos y el modo de diseño de código, vea [Configuring the Script Component in the Script Component Editor](configuring-the-script-component-in-the-script-component-editor.md) (Configurar el componente de script en el editor de componentes de script).  
  
## <a name="writing-the-script-in-code-design-mode"></a>Escribir el script en modo de diseño de código  
  
### <a name="script-component-development-environment"></a>Entorno de desarrollo del componente de script  
 Para escribir un script, haga clic en **Editar script** en la página **Script** del **Editor de transformación Script**, para abrir el IDE de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA). El IDE de VSTA incluye todas las características estándar del entorno de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] .NET, como el editor de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] con códigos de color, IntelliSense y el Explorador de objetos.  
  
 El código de script se escribe en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#. Puede especificar el lenguaje de script estableciendo la propiedad **ScriptLanguage** en el **Editor de transformación Script**. Si prefiere utilizar otro lenguaje de programación, puede desarrollar un ensamblado personalizado en el lenguaje seleccionado y utilizar su funcionalidad en el código del componente de script.  
  
 El script que crea en el componente de script se almacena en la definición de paquete. No hay un archivo de script independiente. Por consiguiente, el uso del componente de script no afecta a la implementación del paquete.  
  
> [!NOTE]  
>  Mientras diseña el paquete, el código de script se escribe temporalmente en un archivo de proyecto. Dado que almacenar información confidencial en un archivo supone un riesgo potencial para la seguridad, recomendamos que no incluya información confidencial como contraseñas en el código de script.  
  
 De forma predeterminada, `Option Strict` está deshabilitada en el IDE.  
  
### <a name="script-component-project-structure"></a>Estructura del proyecto del componente de script  
 La eficacia del componente de script reside en que puede generar código de infraestructura que reduce la cantidad de código que se debe escribir. Esta característica se basa en el hecho de que las entradas y salidas, y sus columnas y propiedades, son fijas y se conocen previamente. Por consiguiente, cualquier cambio subsiguiente que se realiza en los metadatos del componente puede invalidar el código que se ha escrito. Esto produce errores de compilación durante la ejecución del paquete.  
  
#### <a name="project-items-and-classes-in-the-script-component-project"></a>Elementos y clases de proyecto en el proyecto del componente de script  
 Al cambiar al modo de diseño de código, el IDE de VSTA se abre y muestra el elemento de proyecto `ScriptMain`. El elemento de proyecto `ScriptMain` contiene la clase `ScriptMain` modificable, que actúa como el punto de entrada para el script y que es donde se escribe el código. Los elementos de código de la clase varían, dependiendo del lenguaje de programación seleccionado para la tarea Script.  
  
 El proyecto de script contiene dos elementos de proyecto adicionales de solo lectura generados automáticamente:  
  
-   El elemento de proyecto `ComponentWrapper`, que contiene tres clases:  
  
    -   La clase `UserComponent`, que hereda de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> y que contiene los métodos y propiedades que se usarán para procesar datos e interactuar con el paquete. La clase `ScriptMain` hereda de la clase `UserComponent`.  
  
    -   Una clase de colección `Connections` que contiene referencias a las conexiones seleccionadas en la página Administrador de conexiones del Editor de Script de transformación.  
  
    -   Un `Variables` clase de colección que contiene referencias a las variables especificadas en el `ReadOnlyVariable` y `ReadWriteVariables` propiedades en el **Script** página de la **Editor de transformación Script**.  
  
-   El `BufferWrapper` elemento de proyecto contiene una clase que hereda de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> para cada entrada y salida configurada en el **entradas y salidas** página de la **Editor de transformación Script**. Cada una de estas clases contiene las propiedades de descriptor de acceso con tipo, que corresponden a las columnas de entrada y salida configuradas, y los búferes de flujo de datos que contienen las columnas.  
  
 Para obtener información sobre cómo usar estos objetos, métodos y propiedades, vea [Understanding el Model]((understanding-the-script-component-object-model.md) de objeto de componente de Script. Para obtener información acerca de cómo usar los métodos y propiedades de estas clases en un tipo determinado del componente de script, vea la sección [Additional Script Component Examples](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md) (Ejemplos de componente de script adicionales). Los temas de ejemplo también contienen ejemplos de código completos.  
  
 Al configurar el componente de script como una transformación, el elemento de proyecto `ScriptMain` contiene el siguiente código generado automáticamente. La plantilla de código también proporciona información general sobre el componente Script, así como información adicional sobre cómo recuperar y manipular objetos SSIS, como variables, eventos y conexiones.  
  
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
 El proyecto del componente de script puede incluir elementos distintos del elemento `ScriptMain` predeterminado. Puede agregar clases, módulos, archivos de código y carpetas al proyecto; además puede usar las carpetas para organizar los grupos de elementos.  
  
 Todos los elementos que se agregan se conservan dentro del paquete.  
  
#### <a name="references-in-the-script-component-project"></a>Referencias en el proyecto del componente de script  
 Para agregar referencias a los ensamblados administrados, haga clic con el botón derecho en el proyecto de la tarea Script en el **Explorador de proyectos** y, después, haga clic en **Agregar referencia**. Para obtener más información, consulte [Hacer referencia a otros ensamblados en soluciones de scripting](../referencing-other-assemblies-in-scripting-solutions.md).  
  
> [!NOTE]  
>  Puede ver las referencias de proyecto en el IDE de VSTA en la **Vista de clases** o en el **Explorador de proyectos**. Puede abrir cualquiera de estas ventanas en el menú **Ver**. Puede agregar una referencia nueva en el menú **Proyecto**, en el **Explorador de proyectos** o en **Vista de clases**.  
  
## <a name="interacting-with-the-package-in-the-script-component"></a>Interactuar con el paquete en el componente de script  
 El script personalizado que escribe en el componente de script puede obtener acceso y usar variables y administradores de conexión del paquete contenedor, a través de los descriptores de acceso con establecimiento inflexible de tipos en las clases base generadas automáticamente. Sin embargo, debe configurar tanto las variables como los administradores de conexión antes de escribir en modo de diseño de código, si desea que estén disponibles en su script. Puede también provocar eventos y realizar registros desde su código del componente de script.  
  
 Los elementos de proyecto generados automáticamente en el proyecto del componente de script, proporcionan los siguientes objetos, métodos y propiedades para que interactúen con el paquete.  
  
|Característica del paquete|Método de acceso|  
|---------------------|-------------------|  
|Variables|Usa las propiedades de descriptor de acceso con nombre y tipo en la clase de colección `Variables` del elemento de proyecto `ComponentWrapper`, expuesto a través de la propiedad `Variables` de la clase `ScriptMain`.<br /><br /> El método `PreExecute` únicamente puede tener acceso a variables de solo lectura. El método `PostExecute` puede tener acceso a variables de solo lectura y de lectura/escritura.|  
|Conexiones|Usa las propiedades de descriptor de acceso con nombre y tipo en la clase de colección `Connections` del elemento de proyecto `ComponentWrapper`, expuesto a través de la propiedad `Connections` de la clase `ScriptMain`.|  
|Eventos|Provocan eventos mediante el <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> propiedad de la `ScriptMain` clase y el **Fire\<X >** métodos de la <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> interfaz.|  
|Registro|Realiza registros mediante el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> de la clase `ScriptMain`.|  
  
## <a name="debugging-the-script-component"></a>Depurar el componente de script  
 Para depurar el código del componente Script, establezca al menos un punto de interrupción en el código y, a continuación, cierre el IDE de VSTA para ejecutar el paquete en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Cuando la ejecución del paquete entra en el componente Script, el IDE de VSTA se vuelve a abrir y muestra el código en modo de solo lectura. Después de que la ejecución llega al punto de interrupción, puede examinar los valores de variable y completar el código restante.  
  
> [!NOTE]  
>  No puede depurar un componente Script al ejecutar este último como parte de un paquete secundario que se ejecuta desde una tarea Ejecutar paquete. Los puntos de interrupción establecidos en el componente Script del paquete secundario se descartan en estas circunstancias. Puede depurar el paquete secundario ejecutándolo normalmente por separado.  
  
> [!NOTE]  
>  Al depurar un paquete que contiene varios componentes Script, el depurador depura un componente Script. El sistema puede depurar otro componente Script si el depurador se completa, como en el caso de un bucle Foreach o un contenedor de bucles For.  
  
 También puede supervisar la ejecución del componente Script con los métodos siguientes:  
  
-   Interrumpa la ejecución y muestre un mensaje modal mediante el uso de la `MessageBox.Show` método en el **System.Windows.Forms** espacio de nombres. (Quite este código después de completar el proceso de depuración.)  
  
-   Provoque eventos para los mensajes informativos, advertencias y errores. Los métodos FireInformation, FireWarning y FireError muestran la descripción del evento en la ventana **Resultados** de Visual Studio. Sin embargo, el método FireProgress, el método Console.Write y el método Console.WriteLine no muestran ninguna información en la ventana **Resultados**. Los mensajes del evento FireProgress aparecen en la pestaña **Progreso** del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Para obtener más información, consulte [Raising Events in the Script Component](../../data-flow/transformations/script-component.md) (Provocar eventos en el componente de script).  
  
-   Registre eventos o mensajes definidos por el usuario para los proveedores de registro habilitados. Para obtener más información, consulte [registro en la secuencia de comandos de Component]((logging-in-the-script-component.md).  
  
 Si solamente desea examinar la salida de un componente de script configurado como un origen o como una transformación, sin guardar los datos en un destino, puede detener el flujo de datos con una [transformación de recuento de filas](../../data-flow/transformations/row-count-transformation.md) y adjuntar un visor de datos a la salida del componente de script. Para obtener información acerca de los visores de datos, vea [Depurar el flujo de datos](../../troubleshooting/debugging-data-flow.md).  
  
## <a name="in-this-section"></a>En esta sección  
 Para obtener más información acerca de cómo codificar el componente de script, consulte los temas siguientes en esta sección.  
  
 [Descripción del modelo de objetos del componente de script](understanding-the-script-component-object-model.md)  
 Explica cómo usar los objetos, métodos y propiedades disponibles en el componente de script.  
  
 [Hacer referencia a otros ensamblados en soluciones de scripting](../referencing-other-assemblies-in-scripting-solutions.md)  
 Explica cómo hacer referencia a los objetos de la biblioteca de clases [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] en el componente de script.  
  
 [Simular una salida de error para el componente de script](../../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 Explica cómo simular una salida de error en las filas que provocan errores durante el procesamiento por el componente de script.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [VSTA setup and configuration troubles for SSIS 2008 and R2 installations](http://go.microsoft.com/fwlink/?LinkId=215661) (Problemas de instalación y configuración de VSTA en instalaciones de SSIS 2008 y R2), en blogs.msdn.com.  
  
![Icono de Integration Services (pequeño)](../../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services** <br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Configurar el componente de script en el editor de componentes de script](configuring-the-script-component-in-the-script-component-editor.md)  
  
  
