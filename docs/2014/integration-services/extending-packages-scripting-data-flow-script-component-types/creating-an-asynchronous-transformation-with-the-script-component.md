---
title: Crear una transformación asincrónica con el componente de script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1940405c6bde86364024e10694f9aaf1da24b06d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375023"
---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>Crear una transformación asincrónica con el componente de script
  Un componente de transformación se utiliza en el flujo de datos de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para modificar y analizar los datos cuando pasan del origen al destino. Una transformación con salidas sincrónicas procesa cada fila de entrada a medida que pasa por el componente. Una transformación con salidas asincrónicas puede esperar hasta haber recibido todas las filas de entrada para completar su procesamiento o puede generar algunas filas antes de haber recibido todas las filas de entrada. En este tema se describe una transformación asincrónica. Si el procesamiento requiere una transformación sincrónica, vea [Crear una transformación sincrónica con el componente de script](../data-flow/transformations/script-component.md). Para obtener más información acerca de las diferencias que existen entre los componentes sincrónicos y asincrónicos, vea [Understanding Synchronous and Asynchronous Transformations](../understanding-synchronous-and-asynchronous-transformations.md) (Descripción de las transformaciones sincrónicas y asincrónicas).  
  
 Para obtener una introducción al componente de script, vea [Extending the Data Flow with the Script Component](../extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md) (Extensión del Flujo de datos con el componente de script).  
  
 El componente de script y el código de infraestructura generado por dicho componente simplifican el proceso de desarrollo de un componente de flujo de datos personalizado. Sin embargo, para entender cómo funciona el componente de script, puede resultar útil leer los pasos que debe seguir para desarrollar un componente de flujo de datos personalizado en la sección [Developing a Custom Data Flow Component](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) (Desarrollo de un componente Flujo de datos personalizado) y, en especial, [Developing a Custom Transformation Component with Synchronous Outputs](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) (Desarrollo de un componente de transformación personalizado con salidas sincrónicas).  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>Introducción a un componente de transformación asincrónica  
 Al agregar un componente de script a la pestaña Flujo de datos del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)], se muestra el cuadro de diálogo **Seleccionar el tipo de componente de script**, que solicita al usuario que preconfigure el componente como un origen, una transformación o un destino. En este cuadro de diálogo, seleccione **Transformación**.  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>Configurar un componente de transformación asincrónica en el modo de diseño de metadatos  
 Después de seleccionar la opción para crear un componente de transformación, configure el componente mediante el **Editor de transformación Script**. Para obtener más información, consulte [Configuring the Script Component in the Script Component Editor](../extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) (Configurar el componente de script en el editor de componentes de script).  
  
 Para seleccionar el lenguaje de script que usará el componente de script, establezca la propiedad **ScriptLanguage** en la página **Script** del cuadro de diálogo **Editor de transformación Script**.  
  
> [!NOTE]  
>  Para establecer el lenguaje de scripting predeterminado para el componente de script, utilice la opción **Lenguaje de scripting** en la página **General** del cuadro de diálogo **Opciones**. Para obtener más información, vea[página General](../general-page-of-integration-services-designers-options.md).  
  
 Un componente de transformación de flujo de datos tiene una entrada y admite una o varias salidas. La configuración de la entrada y las salidas del componente es uno de los pasos que debe completar en el modo de diseño de metadatos, mediante el **Editor de transformación Script**, antes de escribir un script personalizado.  
  
### <a name="configuring-input-columns"></a>Configurar las columnas de entrada  
 Un componente de transformación creado mediante el componente de script tiene una única entrada.  
  
 En la página **Columnas de entrada** del **Editor de transformación Script**, la lista de columnas muestra las columnas disponibles de la salida del componente de nivel superior en el flujo de datos. Seleccione las columnas que desee transformar o las columnas a través de las que desee pasar. Marque todas las columnas que desee transformar en contexto como de columnas de lectura/escritura.  
  
 Para obtener más información acerca de la página **Columnas de entrada** del **Editor de transformación Script**, vea [Script Transformation Editor &#40;Input Columns Page&#41;](../script-transformation-editor-input-columns-page.md) (Editor de transformación Script [página Columnas de entrada]).  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>Configurar entradas, salidas y columnas de salidas  
 Un componente de transformación admite una o más salidas.  
  
 A menudo, una transformación con salidas asincrónicas tiene dos salidas. Por ejemplo, al contar el número de direcciones ubicadas en una ciudad concreta, es posible que desee pasar los datos de dirección a una salida y enviar el resultado de la agregación a otra salida distinta. La salida de la agregación también requiere una nueva columna de salida.  
  
 En la página **Entradas y salidas** del **Editor de transformación Script**, verá que se ha creado una única salida de forma predeterminada, pero que no se ha creado ninguna columna de salida. En esta página del editor, puede configurar los elementos siguientes:  
  
-   Es posible que desee crear una o más salidas adicionales, como una salida para el resultado de una agregación. Use los botones **Agregar salida** y **Quitar salida** para administrar las salidas del componente de transformación asincrónica. Establezca la propiedad `SynchronousInputID` de cada salida en cero para indicar que la salida no se limita a pasar datos de un componente de nivel superior ni a transformarlos en contexto en las filas y columnas existentes. Este valor hace que las salidas sean asincrónicas con respecto a la entrada.  
  
-   Es posible que desee asignar un nombre descriptivo a la entrada y a las salidas. El componente de script utiliza estos nombres para generar las propiedades de descriptor de acceso con tipo que se usarán para hacer referencia a la entrada y las salidas en el script.  
  
-   A menudo, una transformación asincrónica agrega columnas al flujo de datos. Cuando la propiedad `SynchronousInputID` de una salida es cero (lo que indica que la salida no se limita a pasar datos de un componente de nivel superior ni a transformarlos en contexto en las filas y columnas existentes), debe agregar y configurar columnas de salida explícitamente en la salida. Las columnas de salida no tienen por qué tener los mismos nombres que las columnas de entrada a las que están asignadas.  
  
-   Es posible que desee agregar más columnas para incluir información adicional. Debe escribir su propio código para rellenar de datos las columnas adicionales. Para obtener información sobre cómo reproducir el comportamiento de una salida de error estándar, consulte [Simulating an Error Output for the Script Component](../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md) (Simulación de una salida de error para el componente de script).  
  
 Para obtener más información acerca de la página **Entradas y salidas** del **Editor de transformación Script**, vea [Script Transformation Editor &#40;Inputs and Outputs Page&#41;](../script-transformation-editor-inputs-and-outputs-page.md) (Editor de transformación Script [página Entradas y salidas]).  
  
### <a name="adding-variables"></a>Agregar variables  
 Si hay variables existentes cuyos valores quiere usar en el script, puede agregarlas en los campos de propiedades ReadOnlyVariables y ReadWriteVariables de la página **Script** del **Editor de transformación Script**.  
  
 Cuando agregue varias variables a los campos de propiedades, separe sus nombres con comas. También puede seleccionar varias variables, haga clic en el botón de puntos suspensivos (**...** ) situado junto a la `ReadOnlyVariables` y `ReadWriteVariables` campos de propiedades y, a continuación, seleccionar las variables en el **seleccionar variables** cuadro de diálogo.  
  
 Para obtener información general sobre la forma de usar variables con el componente de script, vea [Using Variables in the Script Component](../extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md) (Uso de variables con el componente de script).  
  
 Para obtener más información acerca de la página **Script** del **Editor de transformación Script**, vea [Script Transformation Editor &#40;Script Page&#41;](../script-transformation-editor-script-page.md) (Editor de transformación Script [página Script]).  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>Crear script de un componente de transformación asincrónica en el modo de diseño de código  
 Después de haber configurado todos los metadatos para el componente, puede escribir un script personalizado. En la página **Script** del **Editor de transformación Script**, haga clic en **Editar script** para abrir el IDE de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA), donde puede agregar el script personalizado. El lenguaje de scripting que utilice dependerá de si ha seleccionado [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# como lenguaje de script para la propiedad **ScriptLanguage** en la página **Script**.  
  
 Para obtener información importante aplicable a todos los tipos de componentes creados mediante el componente de script, vea [Coding and Debugging the Script Component](../extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md) (Programación y depuración del componente de script).  
  
### <a name="understanding-the-auto-generated-code"></a>Descripción del código generado automáticamente  
 Al abrir el IDE de VSTA después de crear y configurar un componente de transformación, el texto editable `ScriptMain` clase aparece en el editor de código con código auxiliar para el ProcessInputRow y los métodos de CreateNewOutputRows. En la clase ScriptMain escribirá el código personalizado; ProcessInputRow es el método más importante de un componente de transformación. El método `CreateNewOutputRows` se utiliza con más frecuencia en un componente de origen, que es la forma en que una transformación asincrónica en los dos componentes mencionados debe crear sus propias filas de salida.  
  
 Si abre la VSTA **Explorador de proyectos** ventana, puede ver que el componente de Script también ha generado de solo lectura `BufferWrapper` y `ComponentWrapper` elementos de proyecto. La clase ScriptMain se hereda de la clase UserComponent en el `ComponentWrapper` elemento de proyecto.  
  
 En tiempo de ejecución, el motor de flujo de datos llama al método PrimeOutput la `UserComponent` clase, lo que invalida el <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost.PrimeOutput%2A> método de la <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> clase primaria. A su vez, el método PrimeOutput llama al método CreateNewOutputRows.  
  
 A continuación, el motor de flujo de datos invoca el método ProcessInput de la clase UserComponent, lo que invalida el método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> de la clase primaria <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. A su vez, el método ProcessInput usa un bucle para recorrer las filas del búfer de entrada y llama al método ProcessInputRow una vez por cada fila.  
  
### <a name="writing-your-custom-code"></a>Escribir código personalizado  
 Para terminar de crear un componente de transformación asincrónica personalizado, debe usar el método ProcessInputRow invalidado para procesar los datos de cada fila del búfer de entrada. Dado que las salidas no son sincrónicas con respecto a la entrada, debe escribir filas de datos explícitamente para las salidas.  
  
 En una transformación asincrónica, puede usar el método AddRow para agregar filas a la salida, según corresponda, desde los métodos ProcessInputRow o ProcessInput. No es necesario utilizar el método CreateNewOutputRows. Si escribe una sola fila de resultados (como resultados de agregación) para una salida determinada, puede crear la fila de salida de antemano con el método CreateNewOutputRows y rellenar sus valores más adelante, después de procesar todas las filas de entrada. Sin embargo, no resulta útil crear varias filas en el método CreateNewOutputRows, ya que el componente de script solamente permite usar la fila actual en una entrada o salida. El método CreateNewOutputRows es más importante en un componente de origen donde no hay filas de entrada que procesar.  
  
 Puede que también desee invalidar el propio método ProcessInput para poder realizar un procesamiento adicional preliminar o final, antes o después de usar un bucle para recorrer el búfer de entrada y llamar a ProcessInputRow para cada fila. Por ejemplo, uno de los ejemplos de código en este tema invalida ProcessInput para contar el número de direcciones de una ciudad concreta como ProcessInputRow recorre en bucle las filas`.` en el ejemplo se escribe el valor de resumen en la segunda salida después de han sido todas las filas puede procesar. El ejemplo completa la salida de ProcessInput porque los búferes de salida ya no están disponibles al llamar a PostExecute.  
  
 En función de sus requisitos, puede que también desee escribir script en los métodos PreExecute y PostExecute, disponibles en la clase ScriptMain, para realizar un procesamiento preliminar o final.  
  
> [!NOTE]  
>  Si estuviese desarrollando un componente de flujo de datos personalizado partiendo de cero, sería importante que invalidase el método PrimeOutput para almacenar en caché las referencias a los búferes de salida de forma que pudiese agregar filas de datos a los búferes más adelante. Esto no es necesario en el componente de script, ya que existe una clase que se genera automáticamente que representa cada búfer de salida en el elemento de proyecto `BufferWrapper`.  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se muestra el código personalizado que se requiere en la clase ScriptMain para crear un componente de transformación asincrónica.  
  
> [!NOTE]  
>  En estos ejemplos se usa la tabla **Person.Address** de la base de datos de ejemplo **AdventureWorks** y se pasan la primera y la cuarta columna, las columnas **intAddressID** y **nvarchar(30)City**, a través del flujo de datos. Estos mismos datos se usan en los ejemplos de origen, transformación y destino de esta sección. Se documentan requisitos previos y suposiciones adicionales para cada ejemplo.  
  
 En este ejemplo se muestra un componente de transformación asincrónica con dos salidas. Esta transformación pasa las columnas **AddressID** y **City** a una salida, al mismo tiempo que cuenta el número de direcciones situadas en una ciudad concreta (Redmond, Washington, EE. UU.) y, a continuación, genera el valor resultante en una segunda salida.  
  
 Si desea ejecutar este código de ejemplo, debe configurar el paquete y el componente de la siguiente forma:  
  
1.  Agregue un nuevo componente de script a la superficie del diseñador de flujo de datos y configúrelo como una transformación.  
  
2.  Conecte la salida de un origen o de otra transformación al nuevo componente de transformación en el diseñador. Esta salida debe proporcionar datos de la tabla **Person.Address** de la base de datos de ejemplo **AdventureWorks** que contiene al menos las columnas **AddressID** y **City**.  
  
3.  Abra el **Editor de transformación Script**. En la página **Columnas de entrada**, seleccione las columnas **AddressID** y **City**.  
  
4.  En la página **Entradas y salidas**, agregue y configure las columnas de salida **AddressID** y **City** en la primera salida. Agregue una segunda salida y una columna de salida para el valor de resumen en la segunda salida. Establezca la propiedad SynchronousInputID de la primera salida en 0, porque este ejemplo copia cada fila de entrada explícitamente en la primera salida. La propiedad SynchronousInputID de la salida recién creada ya está establecida en 0.  
  
5.  Cambie el nombre de la entrada, las salidas y la nueva columna de salida por nombres más descriptivos. En el ejemplo se usa **MyAddressInput** como nombre de la entrada, **MyAddressOutput** y **MySummaryOutput** para las salidas y **MyRedmondCount** para la columna de salida de la segunda salida.  
  
6.  En la página **Script**, haga clic en **Editar script** y escriba el script que se indica a continuación. A continuación, cierre el entorno de desarrollo de script y el **Editor de transformación Script**.  
  
7.  Cree y configure un componente de destino para la primera salida que espere las columnas **AddressID** y **City**, como un destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o el componente de destino de ejemplo que se muestra en [Creating a Destination with the Script Component](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md) (Crear un destino con el componente de script). A continuación, conecte la primera salida de transformación, **MyAddressOutput**, al componente de destino. Puede crear una tabla de destino ejecutando el siguiente comando [!INCLUDE[tsql](../../includes/tsql-md.md)] en la base de datos **AdventureWorks**:  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  Cree y configure otro componente de destino para la segunda salida. A continuación, conecte la segunda salida de transformación, **MySummaryOutput**, al componente de destino. Dado que la segunda salida escribe una única fila con un único valor, puede configurar fácilmente un destino con un administrador de conexiones de archivos planos que se conecta a un nuevo archivo que tiene una única columna. En el ejemplo, esta columna de destino se denomina **MyRedmondCount**.  
  
9. Ejecute el ejemplo.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Private myRedmondAddressCount As Integer  
  
    Public Overrides Sub CreateNewOutputRows()  
  
        MySummaryOutputBuffer.AddRow()  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInput(ByVal Buffer As MyAddressInputBuffer)  
  
        While Buffer.NextRow()  
            MyAddressInput_ProcessInputRow(Buffer)  
        End While  
  
        If Buffer.EndOfRowset Then  
            MyAddressOutputBuffer.SetEndOfRowset()  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount  
            MySummaryOutputBuffer.SetEndOfRowset()  
        End If  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With MyAddressOutputBuffer  
            .AddRow()  
            .AddressID = Row.AddressID  
            .City = Row.City  
        End With  
  
        If Row.City.ToUpper = "REDMOND" Then  
            myRedmondAddressCount += 1  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    private int myRedmondAddressCount;  
  
    public override void CreateNewOutputRows()  
    {  
  
        MySummaryOutputBuffer.AddRow();  
  
    }  
  
    public override void MyAddressInput_ProcessInput(MyAddressInputBuffer Buffer)  
    {  
  
        while (Buffer.NextRow())  
        {  
            MyAddressInput_ProcessInputRow(Buffer);  
        }  
  
        if (Buffer.EndOfRowset())  
        {  
            MyAddressOutputBuffer.SetEndOfRowset();  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount;  
            MySummaryOutputBuffer.SetEndOfRowset();  
        }  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            MyAddressOutputBuffer.AddRow();  
            MyAddressOutputBuffer.AddressID = Row.AddressID;  
            MyAddressOutputBuffer.City = Row.City;  
        }  
  
        if (Row.City.ToUpper() == "REDMOND")  
        {  
            myRedmondAddressCount += 1;  
        }  
  
    }  
  
}  
  
```  
  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Understanding Synchronous and Asynchronous Transformations](../understanding-synchronous-and-asynchronous-transformations.md)  (Descripción de las transformaciones sincrónicas y asincrónicas)  
 [Crear una transformación sincrónica con el componente de script](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
 [Desarrollar un componente de transformación personalizado con salidas asincrónicas](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  
