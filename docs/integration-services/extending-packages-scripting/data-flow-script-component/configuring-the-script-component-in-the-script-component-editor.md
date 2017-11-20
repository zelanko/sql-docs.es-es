---
title: Configurar el componente de Script en el Editor de componentes de Script | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8488fcc7d402430f66b9b9018b31956a5a1d8383
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>Configurar el componente de script en el editor de componentes de script
  Antes de escribir código personalizado en el componente de Script, debe seleccionar el tipo de componente de flujo de datos que desea crear: origen, transformación o destino y, a continuación, configurar los metadatos y propiedades en el componente la **Editor de transformación Script**.  
  
## <a name="selecting-the-type-of-component-to-create"></a>Seleccionar el tipo de componente que se va a crear  
 Al agregar un componente de Script al panel flujo de datos de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] diseñador, el **seleccionar el tipo de componente de Script** aparece el cuadro de diálogo. En él preconfigura el componente como un origen, transformación o destino. Después de realizar esta selección inicial, puede seguir configurando el componente en el **Editor de transformación Script**.  
  
 Para establecer el lenguaje de script predeterminado para el componente de Script, utilice la **lenguaje de Scripting** opción el **General** página de la **opciones** cuadro de diálogo. Para obtener más información, vea [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
## <a name="understanding-the-two-design-time-modes"></a>Descripción de los dos modos en tiempo de diseño  
 En el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)], el componente Script tiene dos modos: modo de diseño de metadatos y modo de diseño de código.  
  
 Cuando se abre la **Editor de transformación Script**, el componente entra en el modo de diseño de metadatos. En este modo, puede seleccionar columnas de entrada y agregar o configurar salidas y columnas de salida, pero no puede escribir código. Una vez configurados los metadatos del componente, puede cambiar al modo de diseño de código para escribir el script.  
  
 Al cambiar al modo de diseño de código haciendo clic en **editar Script**, el componente de Script bloquea los metadatos para evitar cambios adicionales y, a continuación, genera automáticamente código base de los metadatos de las entradas y salidas. Después de que finaliza el código generado automáticamente, puede escribir código personalizado. Este código utiliza las clases base generadas automáticamente para procesar las filas de entrada, para tener acceso a los búferes y columnas de los búferes y para recuperar administradores de conexión y variables del paquete, todos como objetos con establecimiento inflexible de tipos.  
  
 Después de escribir el código personalizado en modo de diseño de código, puede volver a cambiar al modo de diseño de metadatos. Esto no elimina el código que haya escrito; sin embargo, los cambios subsiguientes a los metadatos provocan que se vuelva a generar la clase base. Posteriormente el componente puede producir un error en la validación ya que es posible que los objetos a los que hace referencia el código personalizado no existan o se hayan modificado. En este caso, debe corregir manualmente el código para que se pueda compilar correctamente en la clase base regenerada.  
  
## <a name="configuring-the-component-in-metadata-design-mode"></a>Configurar el componente en modo de diseño de metadatos  
 En el modo de diseño de metadatos, puede seleccionar columnas de entrada y agregar y configurar salidas y columnas de salida, pero no puede escribir código. Una vez configurados los metadatos del componente, cambie al modo de diseño de código para escribir el script.  
  
 Las propiedades que debe configurar en el editor personalizado dependen del uso del componente de script. Este componente se puede configurar como origen, transformación o destino. Según la forma en que se usa el componente, admite una entrada o salidas, o ambas cosas. El código personalizado que escribirá procesa las filas y columnas de entrada y salida.  
  
### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>Página Columnas de entrada del Editor de Script de transformación  
 El **columnas de entrada** página de la **Editor de transformación Script** se muestra para las transformaciones y destinos, pero no para los orígenes. En esta página, selecciona las columnas de entrada disponibles que desea que estén disponibles en el script personalizado y especifica el acceso de solo lectura o de lectura y escritura a ellas.  
  
 En el proyecto de código que se generará en función de estos metadatos, el elemento de proyecto BufferWrapper contiene una clase para cada entrada, y esta clase contiene propiedades de descriptor de acceso con tipo para cada columna de entrada seleccionada. Por ejemplo, si selecciona un número entero **CustomerID** columna y una cadena **CustomerName** columna de una entrada con el nombre **CustomerInput**, el elemento de proyecto BufferWrapper contendrá una **CustomerInput** clase que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>y el **CustomerInput** clase expondrá una propiedad de entero denominada **CustomerID** y una propiedad de cadena denominada **CustomerName**. Esta convención hace posible escribir código con comprobación de tipos como el siguiente:  
  
```vb  
Dim currentCustomerID as Integer = CustomerInput.CustomerID  
Dim currentCustomerName as String = CustomerInput.CustomerName  
```  
  
 Para obtener más información sobre cómo configurar las columnas de entrada para un tipo específico de componente de flujo de datos, vea el ejemplo correspondiente en [desarrollar específico Types of Script Components](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>Página Entradas y salidas del Editor de Script de transformación  
 El **entradas y salidas** página de la **Editor de transformación Script** se muestra para los orígenes, transformaciones y destinos. En esta página, agrega, quita y configura entradas, salidas y columnas de salida que desea utilizar en el script personalizado, con las limitaciones siguientes:  
  
-   Si se usa como origen, el componente de script no tiene ninguna entrada y admite varias salidas.  
  
-   Si se usa como transformación, el componente de script admite una entrada y varias salidas.  
  
-   Si se usa como destino, el componente de script admite una entrada y no tiene ninguna salida.  
  
 En el proyecto de código que se generará en función de estos metadatos, el elemento de proyecto BufferWrapper contiene una clase para cada entrada y salida. Por ejemplo, si crea una salida llamada **CustomerOutput**, el elemento de proyecto BufferWrapper contendrá una **CustomerOutput** clase que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>y el **CustomerOutput** clase contendrá propiedades de descriptor de acceso con tipo para cada columna de salida creada.  
  
 Puede configurar las columnas de salida en el **entradas y salidas** página. Puede seleccionar columnas de entrada para las transformaciones y destinos en el **columnas de entrada** página. Las propiedades de descriptor de acceso con tipo creadas en el elemento de proyecto BufferWrapper serán de solo escritura para las columnas de salida. Las propiedades de descriptor de acceso para las columnas de entrada se sea de solo lectura o lectura/escritura según el tipo de uso que se haya seleccionado para cada columna en el **columnas de entrada** página.  
  
 Para obtener más información acerca de cómo configurar entradas y salidas para un tipo específico de datos de componente de flujo de vea el ejemplo correspondiente en [desarrollar específico Types of Script Components](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
> [!NOTE]  
>  Aunque no puede configurar directamente una salida como una salida de error en el componente de script para el control automático de filas del error, puede reproducir la funcionalidad de una salida de error mediante la creación de una salida adicional y la utilización de script para dirigir las filas a esta salida cuando corresponda. Para obtener más información, consulte [simular una salida de Error para el componente de Script](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>Propiedades ExclusionGroup y SynchronousInputID de las salidas  
 El **ExclusionGroup** propiedad tiene un valor distinto de cero solo en transformaciones con salidas sincrónicas, donde el código realiza el filtrado o bifurcación y dirige cada fila a una de las salidas que comparten el mismo distinto de cero **ExclusionGroup** valor. Por ejemplo, la transformación puede dirigir las filas a la salida predeterminada o a una salida de error. Al crear salidas adicionales para este escenario, asegúrese de establecer el valor de la **SynchronousInputID** propiedad en el entero que coincide con el **ID** de la entrada del componente.  
  
 El **SynchronousInputID** propiedad tiene un valor distinto de cero solo en transformaciones con salidas sincrónicas. Si el valor de esta propiedad es cero, significa que la salida es asincrónica. Para una salida sincrónica, donde filas se pasan a la salida o salidas seleccionadas sin agregar nuevas filas, esta propiedad debe contener el **ID** de la entrada del componente.  
  
> [!NOTE]  
>  Cuando el **Editor de transformación Script** crea la primera salida, el editor establece la **SynchronousInputID** propiedad de la salida en el **ID** de la entrada del componente. Sin embargo, cuando el editor crea las salidas subsiguientes, el editor establece la **SynchronousInputID** propiedades de estas salidas en cero.  
>   
>  Si está creando un componente con salidas sincrónicas, cada salida debe tener su **SynchronousInputID** propiedad establecida en el **ID** de la entrada del componente. Por lo tanto, cada salida que el editor crea después de la primera salida debe tener su **SynchronousInputID** cambia el valor de cero a la **ID** de la entrada del componente.  
>   
>  Si está creando un componente con salidas asincrónicas, cada salida debe tener su **SynchronousInputID** propiedad establecida en cero. Por lo tanto, debe tener la primera salida su **SynchronousInputID** cambió el valor de la **ID** de la entrada del componente a cero.  
  
 Para obtener un ejemplo de dirigir las filas a uno de dos salidas sincrónicas en el componente de Script, consulte [crear una transformación sincrónica con el componente de secuencia de comandos](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md).  
  
### <a name="object-names-in-generated-script"></a>Nombres de objeto en el script generado  
 El componente de script analiza los nombres de las entradas y salidas y analiza los nombres de las columnas en las entradas y salidas; basándose en estos nombres, genera clases y propiedades en el elemento de proyecto BufferWrapper. Si los nombres que se encuentran incluyen caracteres que no pertenecen a las categorías Unicode **UppercaseLetter**, **LowercaseLetter**, **TitlecaseLetter**, **ModifierLetter**, **OtherLetter**, o **DecimalDigitLetter**, se quitan los caracteres no válidos en los nombres generados. Por ejemplo, se quitan los espacios, por lo tanto, dos columnas que tienen los nombres de entrada **FirstName** y [**nombre**] se interpretan como que tiene el nombre de columna **FirstName**, con resultados imprevisibles. Para evitar esta situación, los nombres de entradas y salidas y de columnas de entrada y salida que utiliza el componente de script solamente deben contener caracteres de las categorías Unicode indicadas en esta sección.  
  
### <a name="script-page-of-the-script-transformation-editor"></a>Página Script del Editor de Script de transformación  
 En el **Script** página de la **Editor de la tarea de secuencia de comandos**, asigne un nombre único y una descripción para la tarea de secuencia de comandos. También puede asignar valores a las propiedades siguientes.  
  
> [!NOTE]  
>  En [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] y versiones posteriores, se recompilan todos los scripts. En versiones anteriores, especifica si se precompilaban los scripts estableciendo un **Precompile** propiedad para la tarea.  
  
#### <a name="validateexternalmetadata-property"></a>Propiedad ValidateExternalMetadata  
 El valor booleano de la **ValidateExternalMetadata** propiedad especifica si el componente debe realizar la validación en orígenes de datos externos en tiempo de diseño, o si debe posponer la validación hasta el tiempo de ejecución. De forma predeterminada, el valor de esta propiedad es **True**; es decir, los metadatos externos se validan en tiempo de diseño y en tiempo de ejecución. Puede que desee establecer el valor de esta propiedad en **False** cuando un origen de datos externo no está disponible en tiempo de diseño: por ejemplo, cuando el paquete de descarga el origen o el destino se crea en tiempo de ejecución.  
  
#### <a name="readonlyvariables-and-readwritevariables-properties"></a>Propiedades ReadOnlyVariables y ReadWriteVariables  
 Puede escribir listas delimitada por comas de variables existentes como los valores de estas propiedades para que las variables estén disponibles con acceso de solo lectura o de lectura y escritura dentro del código del componente de script. El acceso a las variables en el código se realiza a través de las propiedades <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> y <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> de la clase base generada automáticamente. Para obtener más información, consulte [usar Variables en el componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
> [!NOTE]  
>  Los nombres de variables distinguen entre mayúsculas y minúsculas.  
  
#### <a name="scriptlanguage"></a>Lenguaje de script  
 Puede seleccionar [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# como el lenguaje de programación del componente Script.  
  
#### <a name="edit-script-button"></a>Botón Editar script  
 El **editar Script** botón abre la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] herramientas IDE Applications (VSTA) en el que escribir un script personalizado. Para obtener más información, consulte [codificar y depurar el componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="connection-managers-page-of-the-script-transformation-editor"></a>Página Editores de conexión del Editor de Script de transformación  
 En el **administradores de conexión** página de la **Editor de transformación Script**, agregar y quitar administradores de conexión que desea usar en el script personalizado. Normalmente debe hacer referencia a los administradores de conexión al crear un componente de origen o de destino.  
  
 En el código de proyecto que se generará en función de estos metadatos, el **ComponentWrapper** elemento de proyecto contiene un **conexiones** clase de colección que tiene una propiedad de descriptor de acceso con tipo para cada administrador de conexiones seleccionado. Cada propiedad de descriptor de acceso con tipo tiene el mismo nombre que el propio administrador de conexiones y devuelve una referencia al administrador de conexiones como una instancia de <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>. Por ejemplo, si ha agregado un administrador de conexiones denominado `MyADONETConnection` en el **administradores de conexión** página del editor, puede obtener una referencia al administrador de conexiones en el script mediante el código siguiente:  
  
```vb  
Dim myADONETConnectionManager As IDTSConnectionManager100 = _  
    Me.Connections.MyADONETConnection  
```  
  
 Para obtener más información, consulte [conectarse a orígenes de datos en el componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
## <a name="see-also"></a>Vea también  
 [Codificar y depurar el componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  

