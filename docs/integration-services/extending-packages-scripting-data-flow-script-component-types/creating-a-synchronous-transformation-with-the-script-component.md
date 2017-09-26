---
title: "Crear una transformación sincrónica con el componente de Script | Documentos de Microsoft"
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
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: aa1bee1a-ab06-44d8-9944-4bff03d73016
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3d4a507c31f77449aba7eb884c39bf68c7c78581
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-synchronous-transformation-with-the-script-component"></a>Crear una transformación sincrónica con el componente de script
  Un componente de transformación se utiliza en el flujo de datos de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para modificar y analizar los datos cuando pasan del origen al destino. Una transformación con salidas sincrónicas procesa cada fila de entrada a medida que pasa por el componente. Una transformación con salidas asincrónicas espera hasta que haya recibido todas las filas de entrada para completar su procesamiento. En este tema se describe una transformación sincrónica. Para obtener información acerca de las transformaciones asincrónicas, vea [crear una transformación asincrónica con el componente de secuencia de comandos](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md). Para obtener más información acerca de las diferencias entre los componentes sincrónicos y asincrónicos, vea [descripción sincrónico y transformaciones asincrónicas](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md).  
  
 Para obtener información general del componente de Script, consulte [extender el flujo de datos con el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 El componente de script y el código de infraestructura que genera simplifican considerablemente el proceso de desarrollo de un componente de flujo de datos personalizado. Sin embargo, para entender cómo funciona el componente de secuencia de comandos, quizá le resulte útil leer los pasos que debe seguir para desarrollar un componente de flujo de datos personalizados en la sección en [desarrollar un componente de flujo de datos personalizada](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)y sobre todo [Desarrollar un componente de transformación personalizado con salidas sincrónicas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md).  
  
## <a name="getting-started-with-a-synchronous-transformation-component"></a>Introducción a un componente de transformación sincrónica  
 Al agregar un componente de Script al panel flujo de datos de [!INCLUDE[ssIS](../../includes/ssis-md.md)] diseñador, el **seleccionar el tipo de componente de Script** cuadro de diálogo se abre y le pide que seleccione un tipo de componente de origen, destino o transformación. En este cuadro de diálogo, seleccione **transformación**.  
  
## <a name="configuring-a-synchronous-transformation-component-in-metadata-design-mode"></a>Configurar un componente de transformación sincrónica en modo de diseño de metadatos  
 Después de seleccionar la opción para crear un componente de transformación, configure el componente mediante el **Editor de transformación Script**. Para obtener más información, consulte [configurar el componente de Script en el Editor de componentes de secuencia de comandos](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Para establecer el lenguaje de script para el componente de Script, establezca la **ScriptLanguage** propiedad en el **Script** página de la **Editor de transformación Script**.  
  
> [!NOTE]  
>  Para establecer el idioma para el componente de Script de scripting predeterminado, utilice la **lenguaje de Scripting** opción el **General** página de la **opciones** cuadro de diálogo. Para obtener más información, consulte [generales página](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
 Un componente de transformación de flujo de datos tiene una entrada y admite una o más salidas. Configuración de la entrada y las salidas del componente es uno de los pasos que debe completar en el modo de diseño de metadatos, mediante la **Editor de transformación Script**, antes de escribir un script personalizado.  
  
### <a name="configuring-input-columns"></a>Configurar las columnas de entrada  
 Un componente de transformación tiene una entrada.  
  
 En el **columnas de entrada** página de la **Editor de transformación de Script,** la lista de columnas muestra las columnas disponibles de la salida del componente de nivel superior en el flujo de datos. Seleccione las columnas que desee transformar o las columnas a través de las que desee pasar. Marque todas las columnas que desee transformar en contexto como de columnas de lectura/escritura.  
  
 Para obtener más información sobre la **columnas de entrada** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; página columnas de entrada &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>Configurar entradas, salidas y columnas de salidas  
 Un componente de transformación admite una o más salidas.  
  
 En el **entradas y salidas** página de la **Editor de transformación Script**, puede ver que se ha creado una salida única, pero la salida no tiene ninguna columna. En esta página del editor, quizá necesite o desee configurar los elementos siguientes.  
  
-   Cree una o varias salidas adicionales, como una salida de error simulada para las filas que contienen valores inesperados. Use la **agregar salida** y **quitar salida** botones para administrar las salidas del componente de transformación sincrónica. Todas las filas de entrada se dirigen a todas las salidas disponibles a menos que indique que desea redirigir cada fila a una salida u otra. Indicar que desea redirigir filas especificando un valor entero distinto de cero para la **ExclusionGroup** propiedad en las salidas. El valor entero concreto escrito en **ExclusionGroup** identificar las salidas no es significativo, pero debe utilizar el mismo entero de forma coherente para el grupo de salidas especificado.  
  
    > [!NOTE]  
    >  También puede utilizar un elemento que es distinto de cero **ExclusionGroup** valor de propiedad con una salida única si no desea todas las filas de salida. Sin embargo, en este caso, debe llamar explícitamente a la **DirectRowTo\<outputbuffer >** método para cada fila que se desea enviar a la salida.  
  
-   Asigne un nombre más descriptivo a la entrada y las salidas. El componente de script utiliza estos nombres para generar las propiedades de descriptor de acceso con tipo que se usarán para hacer referencia a la entrada y las salidas en el script.  
  
-   Deje las columnas tal como están para las transformaciones sincrónicas. Normalmente una transformación sincrónica no agrega columnas al flujo de datos. Se modifican los datos in situ en el búfer y se pasa el contenido del búfer al componente siguiente del flujo de datos. Si éste es el caso, no tiene que agregar y configurar explícitamente las columnas de resultados en las salidas de la transformación. Las salidas aparecen en el editor sin las columnas definidas explícitamente.  
  
-   Agregue las nuevas columnas a las salidas de error simuladas para los errores de fila. Normalmente, varias salidas en la misma **ExclusionGroup** tienen el mismo conjunto de columnas de salida. Sin embargo, si crea una salida de error simulada, quizá desee agregar más columnas que contengan información de error. Para obtener información acerca de cómo el flujo de datos motor procesa las filas de error, consulte [uso de salidas de Error en un componente de flujo de datos](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md). Observe que en el componente de script debe escribir su propio código para llenar las columnas adicionales con la información de error adecuada. Para obtener más información, consulte [simular una salida de Error para el componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Para obtener más información sobre la **entradas y salidas** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; entradas y salidas de página &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Agregar variables  
 Si desea utilizar variables existentes en el script, puede agregarlos en el **ReadOnlyVariables** y **ReadWriteVariables** campos de propiedades en el **Script** página de la **Editor de transformación script**.  
  
 Cuando agregue varias variables a los campos de propiedades, separe sus nombres con comas. También puede seleccionar varias variables, haga clic en el botón de puntos suspensivos (**... **) situado junto a la **ReadOnlyVariables** y **ReadWriteVariables** campos de propiedades y, a continuación, seleccionar las variables en el **seleccionar variables** cuadro de diálogo.  
  
 Para obtener información general acerca de cómo usar variables con el componente de Script, consulte [usar Variables en el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Para obtener más información sobre la **Script** página de la **Editor de transformación Script**, consulte [Editor de transformación Script &#40; Página script &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-synchronous-transformation-component-in-code-design-mode"></a>Scripting de un componente de transformación sincrónica en el modo de diseño de código  
 Después de haber configurado los metadatos para el componente, puede escribir un script personalizado. En el **Editor de transformación Script**, en la **Script** página, haga clic en **editar Script** para abrir el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools para aplicaciones (VSTA) IDE donde puede agregar un script personalizado. El lenguaje de scripting que utilice depende de si seleccionó [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# como lenguaje de script para la **ScriptLanguage** propiedad en el **Script** página.  
  
 Para obtener información importante que se aplica a todos los tipos de componentes creados mediante el componente de Script, consulte [codificar y depurar el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Descripción del código generado automáticamente  
 Cuando se abre el IDE de VSTA después de crear y configurar un componente de transformación, la editable **ScriptMain** clase aparece en el editor de código con un código auxiliar para la **ProcessInputRow** método. El **ScriptMain** clase es donde se escribirá el código personalizado, y **ProcessInputRow** es el método más importante en un componente de transformación.  
  
 Si abre el **el Explorador de proyectos** ventana en VSTA, puede ver que el componente de Script también ha generado de solo lectura **BufferWrapper** y **ComponentWrapper** proyecto elementos. El **ScriptMain** clase hereda de la **UserComponent** clase en el **ComponentWrapper** elemento de proyecto.  
  
 En tiempo de ejecución, el motor de flujo de datos, se invoca el **ProcessInput** método en el **UserComponent** de la clase, lo que invalida el <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> método de la <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> clase primaria. El **ProcessInput** método a su vez recorre las filas en el búfer de entrada y llama el **ProcessInputRow** método una vez por cada fila.  
  
### <a name="writing-your-custom-code"></a>Escribir código personalizado  
 Un componente de transformación con salidas sincrónicas es el más sencillo de escribir de todos los componentes de flujo de datos. Por ejemplo, el ejemplo de salida única mostrado más adelante en este tema consta del código personalizado siguiente:  
  
```vb  
Row.City = UCase(Row.City)  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
```  
  
 Para terminar de crear un componente de transformación sincrónica personalizado, use el invalidado **ProcessInputRow** método para transformar los datos en cada fila del búfer de entrada. El motor de flujo de datos pasa este búfer, cuando está lleno, al componente siguiente del flujo de datos.  
  
 Dependiendo de los requisitos, también puede escribir script en el **PreExecute** y **PostExecute** métodos disponibles en la **ScriptMain** (clase), para realizar procesamiento preliminar o final.  
  
### <a name="working-with-multiple-outputs"></a>Trabajar con varias salidas  
 Dirigir las filas de entrada a una de dos o más posibles salidas no requiere mucho más código personalizado que el caso de ejemplo de salida única descrito anteriormente. Por ejemplo, el ejemplo de dos salidas mostrado más adelante en este tema consta del código personalizado siguiente:  
  
```vb  
Row.City = UCase(Row.City)  
If Row.City = "REDMOND" Then  
    Row.DirectRowToMyRedmondAddresses()  
Else  
    Row.DirectRowToMyOtherAddresses()  
End If  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
if (Row.City=="REDMOND")  
{  
    Row.DirectRowToMyRedmondAddresses();  
}  
else  
{  
    Row.DirectRowToMyOtherAddresses();  
}  
```  
  
 En este ejemplo, el componente de Script genera la **DirectRowTo\<OutputBufferX >** métodos automáticamente, basándose en los nombres de las salidas que configuró. Puede utilizar un código similar para dirigir las filas de errores a una salida de error simulada.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran el código personalizado que se requiere en el **ScriptMain** clase para crear un componente de transformación sincrónica.  
  
> [!NOTE]  
>  Estos ejemplos utilizan la **Person.Address** tabla el **AdventureWorks** base de datos de ejemplo y pasar sus columnas primeros y cuarto, la **intAddressID** y ** nvarchar (30) Ciudad** columnas, a través del flujo de datos. Estos mismos datos se usan en los ejemplos de origen, transformación y destino de esta sección. Se documentan requisitos previos y suposiciones adicionales para cada ejemplo.  
  
### <a name="single-output-synchronous-transformation-example"></a>Ejemplo de transformación sincrónica de salida única  
 En este ejemplo se muestra un componente de transformación sincrónica con una salida única. Esta transformación pasa a través de la **AddressID** columna y convierte la **City** columna a mayúsculas.  
  
 Si desea ejecutar este código de ejemplo, debe configurar el paquete y el componente de la siguiente forma:  
  
1.  Agregue un nuevo componente de script a la superficie del diseñador de flujo de datos y configúrelo como una transformación.  
  
2.  Conecte la salida de un origen o de otra transformación al nuevo componente de transformación en el diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Esta salida debe proporcionar datos de la **Person.Address** tabla de la **AdventureWorks** base de datos de ejemplo que contiene el **AddressID** y **ciudad ** columnas.  
  
3.  Abra la **Editor de transformación Script**. En el **columnas de entrada** página, seleccione la **AddressID** y **City** columnas. Marca el **City** columna como de lectura/escritura.  
  
4.  En el **entradas y salidas** página, cambiar el nombre de la entrada y salida por nombres más descriptivos, como **MyAddressInput** y **MyAddressOutput**. Tenga en cuenta que la **SynchronousInputID** de la salida corresponde a la **ID** de la entrada. Por consiguiente no tiene que agregar y configurar las columnas de resultados.  
  
5.  En el **Script** página, haga clic en **editar Script** y escriba el script siguiente. A continuación, cierre el entorno de desarrollo de script y el **Editor de transformación Script**.  
  
6.  Crear y configurar un componente de destino que espera la **AddressID** y **City** columnas, como un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino o el componente de destino de ejemplo se muestra en [Crear un destino con el componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). A continuación, conecte la salida de transformación al componente de destino. Puede crear una tabla de destino ejecutando el siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] comando en el **AdventureWorks** base de datos:  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  Ejecute el ejemplo.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
    }  
  
}  
```  
  
### <a name="two-output-synchronous-transformation-example"></a>Ejemplo de transformación sincrónica de dos salidas  
 En este ejemplo se muestra un componente de transformación sincrónica con dos salidas. Esta transformación pasa a través de la **AddressID** columna y convierte la **City** columna a mayúsculas. Si el nombre de la ciudad es Redmond, dirige la fila a una salida; dirige todas las demás filas a otra salida.  
  
 Si desea ejecutar este código de ejemplo, debe configurar el paquete y el componente de la siguiente forma:  
  
1.  Agregue un nuevo componente de script a la superficie del diseñador de flujo de datos y configúrelo como una transformación.  
  
2.  Conecte la salida de un origen o de otra transformación al nuevo componente de transformación en el diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Esta salida debe proporcionar datos de la **Person.Address** tabla de la **AdventureWorks** base de datos de ejemplo que contiene al menos el **AddressID** y ** Ciudad** columnas.  
  
3.  Abra la **Editor de transformación Script**. En el **columnas de entrada** página, seleccione la **AddressID** y **City** columnas. Marca el **City** columna como de lectura/escritura.  
  
4.  En el **entradas y salidas** página, cree una segunda salida. Después de agregar la nueva salida, asegúrese de establecer su **SynchronousInputID** a la **ID** de la entrada. Esta propiedad ya está establecida en la primera salida, que se crea de forma predeterminada. Para cada salida, establezca el **ExclusionGroup** propiedad en el mismo valor distinto de cero para indicar que dividirá las filas de entrada entre dos salidas mutuamente excluyentes. No tiene que agregar ninguna columna de resultados a las salidas.  
  
5.  Cambiar el nombre de la entrada y las salidas con nombres más descriptivos, como **MyAddressInput**, **MyRedmondAddresses**, y **MyOtherAddresses**.  
  
6.  En el **Script** página, haga clic en **editar Script** y escriba el script siguiente. A continuación, cierre el entorno de desarrollo de script y el **Editor de transformación Script**.  
  
7.  Cree y configure dos componentes de destino que espera la **AddressID** y **City** columnas, como un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino, un destino de archivo sin formato o el componente de destino de ejemplo muestra en [crear un destino con el componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). A continuación, conecte cada una de las salidas de la transformación a uno de los componentes de destino. Puede crear tablas de destino mediante la ejecución de un [!INCLUDE[tsql](../../includes/tsql-md.md)] comando similar al siguiente (con nombres de tabla única) en la **AdventureWorks** base de datos:  
  
    ```  
    CREATE TABLE [Person].[Address2](  
        [AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL  
    ```  
  
8.  Ejecute el ejemplo.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
        If Row.City = "REDMOND" Then  
            Row.DirectRowToMyRedmondAddresses()  
        Else  
            Row.DirectRowToMyOtherAddresses()  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
        if (Row.City == "REDMOND")  
        {  
            Row.DirectRowToMyRedmondAddresses();  
        }  
        else  
        {  
            Row.DirectRowToMyOtherAddresses();  
        }  
  
    }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Descripción de las transformaciones sincrónicas y asincrónicas] (~/integration-services/understanding-synchronous-and-asynchronous-transformations.md   
 [Crear una transformación asincrónica con el componente de Script] (~/integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md   
 [Desarrollo de un componente de transformación personalizado con salidas sincrónicas] (~/integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md  
  
  



