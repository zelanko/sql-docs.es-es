---
title: Configurar el componente de script en el editor de componentes de script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 40f354f190093c0c689e708301bed9fcba8c87c3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176234"
---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>Configurar el componente de script en el editor de componentes de script
  Antes de escribir código personalizado en el componente de script, tiene que seleccionar el tipo de componente de flujo de datos que quiere crear (origen, transformación o destino) y, después, configurar los metadatos y las propiedades del componente en el **Editor de transformación Script**.

## <a name="selecting-the-type-of-component-to-create"></a>Seleccionar el tipo de componente que se va a crear
 Al agregar un componente de script al panel Flujo de datos del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)], aparece el cuadro de diálogo **Seleccionar el tipo de componente de script**. En él preconfigura el componente como un origen, transformación o destino. Después de realizar esta selección inicial, puede continuar configurando el componente en el **Editor de transformación Script**.

 Para establecer el lenguaje de script predeterminado para el componente de script, utilice la opción **Lenguaje de scripting** de la página **General** del cuadro de diálogo **Opciones**. Para obtener más información, vea [General Page](../../general-page-of-integration-services-designers-options.md).

## <a name="understanding-the-two-design-time-modes"></a>Descripción de los dos modos en tiempo de diseño
 En el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)], el componente Script tiene dos modos: modo de diseño de metadatos y modo de diseño de código.

 Al abrir el **Editor de transformación Script**, el componente activa el modo de diseño de metadatos. En este modo, puede seleccionar columnas de entrada y agregar o configurar salidas y columnas de salida, pero no puede escribir código. Una vez configurados los metadatos del componente, puede cambiar al modo de diseño de código para escribir el script.

 Al hacer clic en **Editar script** para cambiar al modo de diseño de código, el componente de script bloquea los metadatos para evitar cambios adicionales y, a continuación, genera automáticamente código base a partir de los metadatos de las entradas y salidas. Después de que finaliza el código generado automáticamente, puede escribir código personalizado. Este código utiliza las clases base generadas automáticamente para procesar las filas de entrada, para tener acceso a los búferes y columnas de los búferes y para recuperar administradores de conexión y variables del paquete, todos como objetos con establecimiento inflexible de tipos.

 Después de escribir el código personalizado en modo de diseño de código, puede volver a cambiar al modo de diseño de metadatos. Esto no elimina el código que haya escrito; sin embargo, los cambios subsiguientes a los metadatos provocan que se vuelva a generar la clase base. Posteriormente el componente puede producir un error en la validación ya que es posible que los objetos a los que hace referencia el código personalizado no existan o se hayan modificado. En este caso, debe corregir manualmente el código para que se pueda compilar correctamente en la clase base regenerada.

## <a name="configuring-the-component-in-metadata-design-mode"></a>Configurar el componente en modo de diseño de metadatos
 En el modo de diseño de metadatos, puede seleccionar columnas de entrada y agregar y configurar salidas y columnas de salida, pero no puede escribir código. Una vez configurados los metadatos del componente, cambie al modo de diseño de código para escribir el script.

 Las propiedades que debe configurar en el editor personalizado dependen del uso del componente de script. Este componente se puede configurar como origen, transformación o destino. Según la forma en que se usa el componente, admite una entrada o salidas, o ambas cosas. El código personalizado que escribirá procesa las filas y columnas de entrada y salida.

### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>Página Columnas de entrada del Editor de Script de transformación
 La página **Columnas de entrada** del **Editor de transformación Script** se muestra para las transformaciones y los destinos, pero no para los orígenes. En esta página, selecciona las columnas de entrada disponibles que desea que estén disponibles en el script personalizado y especifica el acceso de solo lectura o de lectura y escritura a ellas.

 En el proyecto de código que se generará en función de estos metadatos, el elemento de proyecto BufferWrapper contiene una clase para cada entrada, y esta clase contiene propiedades de descriptor de acceso con tipo para cada columna de entrada seleccionada. Por ejemplo, si selecciona una columna **CustomerID** de entero y una columna **CustomerName** de cadena de una entrada denominada `CustomerInput`, el elemento de proyecto BufferWrapper contendrá `CustomerInput` una clase que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>y la `CustomerInput` clase expondrá una propiedad de entero denominada **CustomerID** y una propiedad de cadena denominada **customername**. Esta convención hace posible escribir código con comprobación de tipos como el siguiente:

```vb
Dim currentCustomerID as Integer = CustomerInput.CustomerID
Dim currentCustomerName as String = CustomerInput.CustomerName
```

 Para obtener más información sobre cómo configurar columnas de entrada para un tipo específico de componente de flujo de datos, vea el ejemplo correspondiente en [Developing Specific Types of Script Components](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md) (Desarrollar tipos de componentes de script específicos).

### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>Página Entradas y salidas del Editor de Script de transformación
 La página **Entradas y salidas** del **Editor de transformación Script** se muestra para orígenes, transformaciones y destinos. En esta página, agrega, quita y configura entradas, salidas y columnas de salida que desea utilizar en el script personalizado, con las limitaciones siguientes:

-   Si se usa como origen, el componente de script no tiene ninguna entrada y admite varias salidas.

-   Si se usa como transformación, el componente de script admite una entrada y varias salidas.

-   Si se usa como destino, el componente de script admite una entrada y no tiene ninguna salida.

 En el proyecto de código que se generará en función de estos metadatos, el elemento de proyecto BufferWrapper contiene una clase para cada entrada y salida. Por ejemplo `CustomerOutput`, si crea una salida denominada, el elemento de proyecto BufferWrapper contendrá una `CustomerOutput` clase que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>y la `CustomerOutput` clase contendrá las propiedades de descriptor de acceso con tipo para cada columna de salida creada.

 Solamente puede configurar columnas de salida en la página **Entradas y salidas**. Puede seleccionar columnas de entrada para las transformaciones y los destinos en la página **Columnas de entrada**. Las propiedades de descriptor de acceso con tipo creadas en el elemento de proyecto BufferWrapper serán de solo escritura para las columnas de salida. Las propiedades de descriptor de acceso para las columnas de entrada serán de solo lectura, o de lectura y escritura dependiendo del tipo de uso seleccionado para cada columna en la página **Columnas de entrada**.

 Para obtener más información sobre la configuración de entradas y salidas para un tipo específico de componente de flujo de datos, vea el ejemplo correspondiente en [Developing Specific Types of Script Components](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md) (Desarrollar tipos de componentes de script específicos).

> [!NOTE]
>  Aunque no puede configurar directamente una salida como una salida de error en el componente de script para el control automático de filas del error, puede reproducir la funcionalidad de una salida de error mediante la creación de una salida adicional y la utilización de script para dirigir las filas a esta salida cuando corresponda. Para obtener más información, vea [Simulating an Error Output for the Script Component](../../data-flow/transformations/script-component.md) (Simular una salida de error para el componente de script).

#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>Propiedades ExclusionGroup y SynchronousInputID de las salidas
 La propiedad `ExclusionGroup` solamente tiene un valor distinto de cero en transformaciones con salidas sincrónicas, donde el código realiza el filtrado o la bifurcación y dirige cada fila a una de las salidas que comparten el mismo valor de `ExclusionGroup` distinto de cero. Por ejemplo, la transformación puede dirigir las filas a la salida predeterminada o a una salida de error. Al crear salidas adicionales para este escenario, asegúrese de establecer el valor de la propiedad `SynchronousInputID` en el entero que coincide con el valor `ID` de la entrada del componente.

 La propiedad `SynchronousInputID` solamente tiene un valor distinto de cero en transformaciones con salidas sincrónicas. Si el valor de esta propiedad es cero, significa que la salida es asincrónica. En una salida sincrónica, donde las filas pasan a la salida o salidas seleccionadas sin agregar nuevas filas, esta propiedad debe contener el valor `ID` de la entrada del componente.

> [!NOTE]
>  Cuando el **Editor de script de transformación** crea la primera salida, el editor `SynchronousInputID` establece la propiedad de la salida `ID` en el de la entrada del componente. Sin embargo, cuando el editor crea las salidas subsiguientes, el editor establece las propiedades `SynchronousInputID` de estas salidas en cero.
> 
>  Si está creando un componente con salidas sincrónicas, cada salida debe tener su `SynchronousInputID` propiedad establecida en el `ID` valor de la entrada del componente. Por tanto, en cada salida que el editor crea después de la primera salida, su valor `SynchronousInputID` debe cambiar de cero al valor `ID` de la entrada del componente.
> 
>  Si crea un componente con salidas asincrónicas, la propiedad `SynchronousInputID` de cada salida debe estar establecida en cero. Por lo tanto, la primera salida debe `SynchronousInputID` tener su valor cambiado `ID` de la entrada del componente a cero.

 Para obtener un ejemplo de dirección de filas a una de las dos salidas sincrónicas del componente de script, consulte [Crear una transformación sincrónica con el componente de script](../../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md).

### <a name="object-names-in-generated-script"></a>Nombres de objeto en el script generado
 El componente de script analiza los nombres de las entradas y salidas y analiza los nombres de las columnas en las entradas y salidas; basándose en estos nombres, genera clases y propiedades en el elemento de proyecto BufferWrapper. Si los nombres que se encuentran incluyen caracteres que no pertenecen a las categorías Unicode `UppercaseLetter`, `LowercaseLetter`, `TitlecaseLetter`, `ModifierLetter`, `OtherLetter` o `DecimalDigitLetter`, los caracteres no válidos se quitan de los nombres generados. Por ejemplo, se quitan los espacios, por lo que dos columnas de entrada con los nombres **FirstName** y [**First Name**] se interpretan con el nombre de columna **FirstName**, lo que produce resultados imprevisibles. Para evitar esta situación, los nombres de entradas y salidas y de columnas de entrada y salida que utiliza el componente de script solamente deben contener caracteres de las categorías Unicode indicadas en esta sección.

### <a name="script-page-of-the-script-transformation-editor"></a>Página Script del Editor de Script de transformación
 En la página **Script** del **Editor de la tarea Script**, asigna un nombre único y una descripción a la tarea Script. También puede asignar valores a las propiedades siguientes.

> [!NOTE]
>  En [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] y versiones posteriores, se recompilan todos los scripts. En versiones anteriores, especificaba si los scripts se precompilaban o no estableciendo una propiedad `Precompile` para la tarea.

#### <a name="validateexternalmetadata-property"></a>Propiedad ValidateExternalMetadata
 El valor booleano de la propiedad `ValidateExternalMetadata` especifica si el componente debe realizar la validación en los orígenes de datos externos en tiempo de diseño o si debe posponer la validación hasta el tiempo de ejecución. De forma predeterminada, el valor de esta propiedad es `True`; es decir, los metadatos externos se validan en tiempo de diseño y en tiempo de ejecución. Puede establecer el valor de esta propiedad en `False` cuando un origen de datos externo no esté disponible en tiempo de diseño: por ejemplo, cuando el paquete descarga el origen o crea el destino solamente en tiempo de ejecución.

#### <a name="readonlyvariables-and-readwritevariables-properties"></a>Propiedades ReadOnlyVariables y ReadWriteVariables
 Puede escribir listas delimitada por comas de variables existentes como los valores de estas propiedades para que las variables estén disponibles con acceso de solo lectura o de lectura y escritura dentro del código del componente de script. El acceso a las variables en el código se realiza a través de las propiedades <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> y <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> de la clase base generada automáticamente. Para más información, consulte [Using Variables in the Script Task](using-variables-in-the-script-component.md) (Uso de variables en la tarea Script).

> [!NOTE]
>  Los nombres de variables distinguen entre mayúsculas y minúsculas.

#### <a name="scriptlanguage"></a>Lenguaje de script
 Puede seleccionar [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# como el lenguaje de programación del componente Script.

#### <a name="edit-script-button"></a>Botón Editar script
 El botón **Editar script** abre el IDE de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) donde se escribe el script personalizado. Para obtener más información, consulte [Coding and Debugging the Script Component](coding-and-debugging-the-script-component.md) (Programar y depurar el componente de script).

### <a name="connection-managers-page-of-the-script-transformation-editor"></a>Página Editores de conexión del Editor de Script de transformación
 En la página **Administradores de conexión** del **Editor de transformación Script**, puede agregar y quitar los administradores de conexión quiera utilizar en el script personalizado. Normalmente debe hacer referencia a los administradores de conexión al crear un componente de origen o de destino.

 En el proyecto de código que se generará en función de estos metadatos, el elemento de proyecto `ComponentWrapper` contiene una clase de colección `Connections` que incluye una propiedad de descriptor de acceso con tipo para cada administrador de conexiones seleccionado. Cada propiedad de descriptor de acceso con tipo tiene el mismo nombre que el propio administrador de conexiones y devuelve una referencia al administrador de conexiones como una instancia de <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>. Por ejemplo, si ha agregado un administrador de conexiones denominado `MyADONETConnection` en la página **Administradores de conexión** del editor, puede obtener una referencia al administrador de conexiones en el script mediante el código siguiente:

```vb
Dim myADONETConnectionManager As IDTSConnectionManager100 = _
    Me.Connections.MyADONETConnection
```

 Para obtener más información, consulte [Conectarse a orígenes de datos del componente de script](connecting-to-data-sources-in-the-script-component.md)

![Integration Services icono (pequeño)](../../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.

## <a name="see-also"></a>Consulte también
 [Codificar y depurar el componente de script](coding-and-debugging-the-script-component.md)


