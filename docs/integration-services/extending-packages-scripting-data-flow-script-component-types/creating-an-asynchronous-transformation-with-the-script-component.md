---
title: "Crear una transformación asincrónica con el componente de Script | Documentos de Microsoft"
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
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
caps.latest.revision: 63
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4da61e00337430a3eaef84e40f9f732a572cc45b
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>Crear una transformación asincrónica con el componente de script
  Un componente de transformación se utiliza en el flujo de datos de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para modificar y analizar los datos cuando pasan del origen al destino. Una transformación con salidas sincrónicas procesa cada fila de entrada a medida que pasa por el componente. Una transformación con salidas asincrónicas puede esperar a que se complete su procesamiento hasta que la transformación ha recibido todas las filas de entrada o la transformación puede generar algunas filas antes de haber recibido todas las filas de entrada. En este tema se describe una transformación asincrónica. Si el procesamiento requiere una transformación sincrónica, vea [crear una transformación sincrónica con el componente de secuencia de comandos](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md). Para obtener más información acerca de las diferencias entre los componentes sincrónicos y asincrónicos, vea [descripción sincrónico y transformaciones asincrónicas](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md).  
  
 Para obtener información general del componente de Script, consulte [extender el flujo de datos con el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 El componente de script y el código de infraestructura generado por dicho componente simplifican el proceso de desarrollo de un componente de flujo de datos personalizado. Sin embargo, para entender cómo funciona el componente de secuencia de comandos, quizá le resulte útil leer los pasos que debe seguir para desarrollar un componente de flujo de datos personalizados en el [desarrollar un componente de flujo de datos personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) sección, y especialmente [desarrollar un componente de transformación personalizado con salidas sincrónicas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md).  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>Introducción a un componente de transformación asincrónica  
 Al agregar un componente de Script a la pestaña flujo de datos de [!INCLUDE[ssIS](../../includes/ssis-md.md)] diseñador, el **seleccionar el tipo de componente de Script** aparece el cuadro de diálogo que le pide que preconfigure el componente como origen, transformación o destino. En este cuadro de diálogo, seleccione **transformación**.  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>Configurar un componente de transformación asincrónica en el modo de diseño de metadatos  
 Después de seleccionar la opción para crear un componente de transformación, configure el componente mediante el **Editor de transformación Script**. Para obtener más información, consulte [configurar el componente de Script en el Editor de componentes de secuencia de comandos](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Para seleccionar el lenguaje de script que se va a usar el componente de Script, establezca la **ScriptLanguage** propiedad en el **Script** página de la **Editor de transformación Script** cuadro de diálogo cuadro.  
  
> [!NOTE]  
>  Para establecer el idioma para el componente de Script de scripting predeterminado, utilice la **lenguaje de Scripting** opción el **General** página de la **opciones** cuadro de diálogo. Para obtener más información, vea [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
 Un componente de transformación de flujo de datos tiene una entrada y admite una o varias salidas. La configuración de la entrada y las salidas del componente es uno de los pasos que debe completar en el modo de diseño de metadatos, mediante la **Editor de transformación Script**, antes de escribir un script personalizado.  
  
### <a name="configuring-input-columns"></a>Configurar las columnas de entrada  
 Un componente de transformación creado mediante el componente de script tiene una única entrada.  
  
 En el **columnas de entrada** página de la **Editor de transformación Script**, la lista de columnas muestra las columnas disponibles de la salida del componente de nivel superior en el flujo de datos. Seleccione las columnas que desee transformar o las columnas a través de las que desee pasar. Marque todas las columnas que desee transformar en contexto como de columnas de lectura/escritura.  
  
 Para obtener más información sobre la **columnas de entrada** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; página columnas de entrada &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>Configurar entradas, salidas y columnas de salidas  
 Un componente de transformación admite una o más salidas.  
  
 A menudo, una transformación con salidas asincrónicas tiene dos salidas. Por ejemplo, al contar el número de direcciones ubicadas en una ciudad concreta, es posible que desee pasar los datos de dirección a una salida y enviar el resultado de la agregación a otra salida distinta. La salida de la agregación también requiere una nueva columna de salida.  
  
 En el **entradas y salidas** página de la **Editor de transformación Script**, verá que se ha creado una salida única de forma predeterminada, pero no se ha creado ninguna columna de salida. En esta página del editor, puede configurar los elementos siguientes:  
  
-   Es posible que desee crear una o más salidas adicionales, como una salida para el resultado de una agregación. Use la **agregar salida** y **quitar salida** botones para administrar las salidas del componente de transformación asincrónica. Establecer el **SynchronousInputID** propiedad de cada salida en cero para indicar que la salida no basta con pasar datos de un componente de nivel superior o transformarlos en contexto en las columnas y filas existentes. Este valor hace que las salidas sean asincrónicas con respecto a la entrada.  
  
-   Es posible que desee asignar un nombre descriptivo a la entrada y a las salidas. El componente de script utiliza estos nombres para generar las propiedades de descriptor de acceso con tipo que se usarán para hacer referencia a la entrada y las salidas en el script.  
  
-   A menudo, una transformación asincrónica agrega columnas al flujo de datos. Cuando el **SynchronousInputID** propiedad de una salida es cero, que indica que la salida no basta con pasar datos de un componente de nivel superior o transformarlos en contexto en las filas y columnas existentes, debe agregar y configurar columnas de salida explícitamente en la salida. Las columnas de salida no tienen por qué tener los mismos nombres que las columnas de entrada a las que están asignadas.  
  
-   Es posible que desee agregar más columnas para incluir información adicional. Debe escribir su propio código para rellenar de datos las columnas adicionales. Para obtener información acerca de cómo reproducir el comportamiento de una salida de error estándar, consulte [simular una salida de Error para el componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Para obtener más información sobre la **entradas y salidas** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; entradas y salidas de página &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Agregar variables  
 Si hay cualquier variables existentes cuyos valores desea utilizar en la secuencia de comandos, puede agregarlos en los campos de propiedades ReadOnlyVariables y ReadWriteVariables en el **Script** página de la **Editor de transformación de secuencia de comandos** .  
  
 Cuando agregue varias variables a los campos de propiedades, separe sus nombres con comas. También puede seleccionar varias variables, haga clic en el botón de puntos suspensivos (**...** ) situado junto a la **ReadOnlyVariables** y **ReadWriteVariables** campos de propiedades y, a continuación, seleccionar las variables en el **seleccionar variables** cuadro de diálogo.  
  
 Para obtener información general acerca de cómo usar variables con el componente de Script, consulte [usar Variables en el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Para obtener más información sobre la **Script** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; Página script &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>Crear script de un componente de transformación asincrónica en el modo de diseño de código  
 Después de haber configurado todos los metadatos para el componente, puede escribir un script personalizado. En el **Editor de transformación Script**, en la **Script** página, haga clic en **editar Script** para abrir el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools para aplicaciones (VSTA) IDE donde puede agregar un script personalizado. El lenguaje de scripting que utilice depende de si seleccionó [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# como lenguaje de script para la **ScriptLanguage** propiedad en el **Script** página.  
  
 Para obtener información importante que se aplica a todos los tipos de componentes creados mediante el componente de Script, consulte [codificar y depurar el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Descripción del código generado automáticamente  
 Al abrir el IDE de VSTA después de crear y configurar un componente de transformación, la editable **ScriptMain** clase aparece en el editor de código con código auxiliar para el ProcessInputRow y los métodos de CreateNewOutputRows. La clase ScriptMain es donde se va a escribir el código personalizado, y ProcessInputRow es el método más importante en un componente de transformación. El **CreateNewOutputRows** método más suele usarse en un componente de origen, que es como una transformación asincrónica de ambos componentes deben crear sus propias filas de salida.  
  
 Si abre la VSTA **el Explorador de proyectos** ventana, puede ver que el componente de Script también ha generado de solo lectura **BufferWrapper** y **ComponentWrapper** elementos de proyecto . La clase ScriptMain hereda de la clase UserComponent en el **ComponentWrapper** elemento de proyecto.  
  
 En tiempo de ejecución, el motor de flujo de datos llama el método PrimeOutput la **UserComponent** de la clase, lo que invalida el <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> método de la <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> clase primaria. El método PrimeOutput a su vez llama al método de CreateNewOutputRows.  
  
 A continuación, el motor de flujo de datos, invoca el método ProcessInput en la clase UserComponent, lo que invalida el <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> método de la <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> clase primaria. A su vez, el método ProcessInput recorre las filas del búfer de entrada y llama al método de ProcessInputRow una vez para cada fila.  
  
### <a name="writing-your-custom-code"></a>Escribir código personalizado  
 Para terminar de crear un componente de transformación asincrónica personalizado, debe usar el método ProcessInputRow invalidado para procesar los datos en cada fila del búfer de entrada. Dado que las salidas no son sincrónicas con respecto a la entrada, debe escribir filas de datos explícitamente para las salidas.  
  
 En una transformación asincrónica, puede usar el método AddRow para agregar filas a la salida según corresponda, desde los métodos ProcessInputRow o ProcessInput. No es necesario utilizar el método CreateNewOutputRows. Si está escribiendo una sola fila de resultados, como los resultados de agregación para una salida determinada, puede crear de antemano la fila de salida mediante el método CreateNewOutputRows y rellenar sus valores más adelante después de procesar todas las filas de entrada. Sin embargo no es útil crear varias filas en el método CreateNewOutputRows, ya que el componente de Script solo permite usar la fila actual en una entrada o salida. El método CreateNewOutputRows es más importante en un componente de origen donde no hay ninguna fila de entrada para procesar.  
  
 También puede invalidar el método ProcessInput propio, puede hacer lo preliminar o final otros procesamientos adicionales antes o después de ejecutar un bucle en el búfer de entrada y llamar a ProcessInputRow para cada fila. Por ejemplo, uno de los ejemplos de código de este tema invalida ProcessInput para contar el número de direcciones de una ciudad concreta como ProcessInputRow recorre filas**.** En el ejemplo se escribe el valor de resumen en la segunda salida después de que se han procesado todas las filas. En el ejemplo se completa la salida en ProcessInput porque los búferes de salida ya no están disponibles cuando se llama a PostExecute.  
  
 Dependiendo de los requisitos, también puede escribir script en los métodos de PreExecute y PostExecute disponibles en la clase ScriptMain para realizar cualquier procesamiento preliminar o final.  
  
> [!NOTE]  
>  Si estuviese desarrollando un componente de flujo de datos personalizado partiendo de cero, sería importante invalidar el método PrimeOutput en memoria caché las referencias a los búferes de salida para que pudiese agregar filas de datos a los búferes más adelante. En el componente de Script, esto no es necesario porque tiene una clase generada automáticamente que representa cada búfer de salida en el **BufferWrapper** elemento de proyecto.  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se muestra el código personalizado que se requiere en la clase ScriptMain para crear un componente de transformación asincrónica.  
  
> [!NOTE]  
>  Estos ejemplos utilizan la **Person.Address** tabla el **AdventureWorks** base de datos de ejemplo y pasar sus columnas primeros y cuarto, la **intAddressID** y  **nvarchar (30) Ciudad** columnas, a través del flujo de datos. Estos mismos datos se usan en los ejemplos de origen, transformación y destino de esta sección. Se documentan requisitos previos y suposiciones adicionales para cada ejemplo.  
  
 En este ejemplo se muestra un componente de transformación asincrónica con dos salidas. Esta transformación pasa a través de la **AddressID** y **City** columnas a una salida, mientras que cuenta el número de direcciones situadas en una ciudad concreta (Redmond, Washington, Estados Unidos) y, a continuación, las salidas del valor resultante en una segunda salida.  
  
 Si desea ejecutar este código de ejemplo, debe configurar el paquete y el componente de la siguiente forma:  
  
1.  Agregue un nuevo componente de script a la superficie del diseñador de flujo de datos y configúrelo como una transformación.  
  
2.  Conecte la salida de un origen o de otra transformación al nuevo componente de transformación en el diseñador. Esta salida debe proporcionar datos de la **Person.Address** tabla de la **AdventureWorks** base de datos de ejemplo que contiene al menos el **AddressID** y  **Ciudad** columnas.  
  
3.  Abra la **Editor de transformación Script**. En el **columnas de entrada** página, seleccione la **AddressID** y **City** columnas.  
  
4.  En el **entradas y salidas** página, agregue y configure el **AddressID** y **City** columnas en la primera salida de salida. Agregue una segunda salida y una columna de salida para el valor de resumen en la segunda salida. Establezca la propiedad SynchronousInputID de la primera salida en 0, porque este ejemplo copia cada fila de entrada explícitamente en la primera salida. La propiedad SynchronousInputID de la salida recién creada ya está establecida en 0.  
  
5.  Cambie el nombre de la entrada, las salidas y la nueva columna de salida por nombres más descriptivos. El ejemplo se utiliza **MyAddressInput** como el nombre de la entrada, **MyAddressOutput** y **MySummaryOutput** para las salidas, y **MyRedmondCount** para la columna de salida de la segunda salida.  
  
6.  En el **Script** página, haga clic en **editar Script** y escriba el script siguiente. A continuación, cierre el entorno de desarrollo de script y el **Editor de transformación Script**.  
  
7.  Crear y configurar un componente de destino para la primera salida que espera la **AddressID** y **City** columnas, como un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino o el componente de destino de ejemplo muestra en [crear un destino con el componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md),. A continuación, conecte la primera salida de transformación, **MyAddressOutput**, al componente de destino. Puede crear una tabla de destino ejecutando el siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] comando en el **AdventureWorks** base de datos:  
  
    ```sql
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
  
## <a name="see-also"></a>Vea también  
 [Descripción de las transformaciones sincrónicas y asincrónicas](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [Crear una transformación sincrónica con el componente de secuencia de comandos](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [Desarrollar un componente de transformación personalizado con salidas asincrónicas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  

